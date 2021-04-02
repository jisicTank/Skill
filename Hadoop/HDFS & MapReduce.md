# HDFS & MapReduce

> 큰 데이터를 어디에 저장? -> HDFS
>
> 큰 데이터를 어떻게 처리? -> MapReduce

<br>

### 1. HDFS(Hadoop Distributed File System)

분산 파일 시스템. 블록 크기, 복제 수를 제어하여 데이터를 어디에, 어떻게 처리할 것인지를 결정.

<img src="https://user-images.githubusercontent.com/71415474/113380191-8636c780-93b6-11eb-96d7-170d0e8e4c2d.PNG" alt="hadoop_16" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/71415474/113380204-8b941200-93b6-11eb-8912-5710c92a6458.PNG" alt="hadoop_18" style="zoom:67%;" />

<img src="https://user-images.githubusercontent.com/71415474/113379763-5804b800-93b5-11eb-9e4f-49b94a90435c.PNG" alt="hadoop_14" style="zoom:67%;" />



<br>

- Hadoop은 많은 수의 작은 파일보다. 적은 수의 큰 파일을 다루는데 더 적합

  <img src="https://user-images.githubusercontent.com/71415474/113379765-59ce7b80-93b5-11eb-811a-48685c8de7f2.PNG" alt="hadoop_15" style="zoom:50%;" />

  <br>

- 장점

  - 분산 프로세싱 지원 - 전체 파일이 아닌 블록
  - 고장 제어 - 블록 복제
  - 확장성(Scale Out)
  - 비용 효율 (일반적인 하드웨어)

  <br>

- 한번 쓰고, 여러번 읽음

  <img src="https://user-images.githubusercontent.com/71415474/113379341-2fc88980-93b4-11eb-88ec-84244e1ce7ae.PNG" alt="hadoop_8" style="zoom: 67%;" />

  <img src="https://user-images.githubusercontent.com/71415474/113379344-32c37a00-93b4-11eb-85d0-b35adf5a9fe8.PNG" alt="hadoop_9" style="zoom: 67%;" />

  <br>

- HDFS Block Size

  <img src="https://user-images.githubusercontent.com/71415474/113379431-669e9f80-93b4-11eb-8c6a-dc56904fc530.PNG" alt="hadoop_11" style="zoom:67%;" />

  - 파일 시스템에서 읽고 쓰는 데이터의 최소 크기
  - Replication 및 Fault tolerance를 위한 단위
  - 기본 Disk는 512byte, HDFS는 기본이 64MB
    - Block Size가 큰 이유? => Seek Time 최소화
      - Seek Time = 10ms
      - 전송률 100MB/s  => Seek Time이 1% 차지 (전송률의 1%)
  - 많은 설치본이 128MB를 사용
  - 블록 사이즈가 크면 병렬처리가 줄어들고, 블록 사이즈가 작으면 오버헤드가 증가한다.

  <br>

- 복제 계수(=Replication Factor)

  - 설정 파일 : hdfs-site.xml
    ex. dfs.replication = 3


  <img src="https://user-images.githubusercontent.com/71415474/113379483-9e0d4c00-93b4-11eb-8e2b-784a105228bd.PNG" alt="hadoop_12" style="zoom:67%;" />

  <br>

- 복제 위치 선택

  - Rack Awareness
    :  서로 다른 Rack에 뭔가를 쓰기 위해서는 네트워크의 대역폭을 이용할 수 밖에 없다. Rack Awareness란 어떻게 Rack에 블록들을 복제하여 배치할 것
    - 다른 Rack을 사용하면 쓰기 대역폭이 증가한다.
    - 동일 Rack을 사용하면 중복이 감소한다. 대신 장애 복구가 어렵다.

  <img src="https://user-images.githubusercontent.com/71415474/113379582-dad94300-93b4-11eb-8b0a-3e4ae05b9f2d.PNG" alt="hadoop_13" style="zoom:67%;" />

  <br>

- 백업 위치 설정

  - 설정 파일: hdfs-site.xml
    - dfs.namenode.name.dir
      - $PATH_1, $PATH_2, $PATH_3 : 원격 드라이브에 백업 위치 추가 설정.
        -> 문제가 발생하면 살릴 수 없는 Namenode(단일 고장 장애 지점)의 데이터를 여러 디렉토리에 저장하여 문제를 보완

  <br>

- 보조 네임노드(Secondary Namenode)

  - fsimage와 edits 편집로그를 병합하는 것은 컴퓨팅이 심한 작업임

    > fsimage: RDBMS에서 초기 데이터베이스 역할
    >
    > edits: RDBMS에서 트랜잭션 로그 역할. 읽거나 쓰거나 할 때 로그가 쌓임
    >
    > 하둡 유지보수를 위해 시스템을 다시 내렸다 올리면 기존의 edits 로그를 커밋하여 올리게 됨. edits 메모리의 크기가 크다면 컴퓨팅이 심하다는 뜻

    <br>

  - 보조 네임노드를 두어 체크 포인팅 작업을 진행하게 함

    - 설정 파일: hdfs-site.xml
      - dfs.namenode.checkpoint.period: 각 체크포인트 사이의 시간(초)
      - dfs.namenode.checkpoint.check.period: 점검되지 않은 트랜잭션에 대한 폴링 기간
      - dfs.namenode.checkpoint.txns: 체크포인팅 이전의 트랜잭션 수(edits 편집로그 수)

  <br>

- 정리 

  - HDFS는 이렇게 설계되었다.
    - 큰 파일을 다루기 위해 (수 백 MB, TB 그 이상)
    - 데이터 액세스 (한번 쓰고 여러번 읽는다.)
    - 일반적인 하드웨어

  <br>

  - HDFS는 이렇게 설계되지 않았따.
    - 짧은 지연시간을 가진 데이터 액세스
    - 작은파일 (많은 작은 파일들은 네임 노드의 메모리를 증가시킴)
    - 임의적인 파일 수정 (추가만 지원)

