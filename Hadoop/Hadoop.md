# Hadoop

### 1. 개요: 구글 검색 알고리즘

1. 검색엔진에서 중요한 것
   - 매칭: 내가 검색한 검색어에 맞는 정보들이 검색되는것 
   - 랭킹: 검색결과에 대해 내가 원하는 정보와 가장 밀접한 정보를 우선순위로 두어 가장 상위로 올려줌
   
   <br>
2. 검색의 한계

![hadoop_1](https://user-images.githubusercontent.com/71415474/113334195-5fe53d80-935e-11eb-87f1-0bbb6218f69f.PNG)

<br>

3. 구글은 400억개 이상의 웹을 검색하는 방법은? = **인덱스(Index)**

![hadoop_2](https://user-images.githubusercontent.com/71415474/113334381-9a4eda80-935e-11eb-972d-8ea5a1483dc3.PNG)

- Google (2020년 기준)
  - 일일 처리량: 100PB
  - index 페이지 수: 60조
  - 현재 스토리지: 15EB
  - 웹페이지를 읽는데 약 3개월 소요
  - 1000개의 드라이브에 저장하고 사용
  - 평균 디스크 읽기 성능 = 약 120MB/sec
- **시사점**
  - 빠른 데이터 처리에 비해 매우 느린 I/O(Read/Write) 작업
  - 대용량 데이터를 위한 컴퓨팅은 이전과는 근본적으로 다른 접근 방법이 필요
  - **해결책 => 데이터 중심의 병렬 reads 시스템**

<br>

---

### Hadoop

1. Hadoop
   대용량 데이터를 분산 처리할 수 있는 자바 기반의 오픈소스 프레임워크. 구글이 논문으로 발표한 GFS(Google File System)와 맵리듀스(MapReduce)를 2005년에 구현한 결과물. 2008년에 아파치 최상위 프로젝트로 승격.
   
<img src="https://user-images.githubusercontent.com/71415474/113336171-f0bd1880-9360-11eb-88d4-4920499fa75a.PNG" alt="hadoop_3" style="zoom:67%;" />
   
2. RDBMS vs Hadoop
   
<img src="https://user-images.githubusercontent.com/71415474/113336334-38dc3b00-9361-11eb-9d0d-48bfda33b5f5.PNG" alt="hadoop_4" style="zoom:67%;" />
   
   > Scale Up: 처리하기 위한 CPU나 메모리나 디스크의 자원이 갑자기 사용량이 많아짐에 따라 부족하게 되었을때, 실제 그 서버의 CPU나 메모리 등을 교체하는 것. 수직 스케일
   >
   > Scale Out: 접속된 서버의 대수를 늘려서 처리 능력을 향상 시키는 것. 수평스케일
   >
   > 파레토 법칙: 전체 결과의 80%가 전체 원인의 20%에서 일어나는 현상
   >
> 롱테일 법칙: 사소해보이는 80%가 소수의 핵심보다도 뛰어난 가치를 창출
   
- 추가 차이점
   
  - RDBMS는 온라인 트랜잭션 처리에 사용 가능. Hadoop의 경우 이에 부적절함
   
  - Hadoop은 "Schema on Read"정책을 기반으로하는 반면 RDBMS는 "Schema on Write"정책을 따르고 있습니다.
   
       > Schema on Read: 데이터를 저장할 때 스키마와 상관없이 저장 가능. 데이터를 읽을 때 읽은 데이터를 기준으로 스키마가 정의
       >
    > Schema on Write: 데이터를 저장할 때 스키마를 먼저 정의하고 데이터를 저장.
       
       <br>
   
3. Hadoop1 & Hadoop2

   - Hadoop1
     : HDFS + MapReduce(v1) 의 구성으로 되어있다. 

     - HDFS = NameNode(M) + DataNode(S) 
       : "데이터를 어디에 저장할 것인가?"를 다루며, Namenode는 데이터의 위치를 저장하는 메타데이터 역할, DataNode는 데이터 저장소이다.
     - MapReduce(v1) = JobTracker(M) + TaskTracker(S) 
       : "데이터를 어떻게 처리할 것인가?"를 다루며, 주어진 Job을 JobTracker에서 받아 Task를 TaskTracker에게 분배. TaskTracker는 Task들을 실행

     > M: Master, S: Slave

     분산 어플리케이션의 역할뿐만 아니라, 자원관리의 역할도 같이 포함하고 있다.

     ![hadoop_5](https://user-images.githubusercontent.com/71415474/113340486-edc52680-9366-11eb-91c7-9c84c0b46d5b.PNG)

   <br>
   
- Hadoop2
     : HDFS + YARN(v2) 로 구성되어있다.
   
     - HDFS 는 Hadoop1과 역할 동일
  - YARN(v2) = Resource Manager(M) + Node Manager
       : YARN은 Yet Another Resource Negotiator 자원 협상을 말한다. 1.0의 Jobtracker의 resource management를 2.0의 YARN에게 넘긴 셈. 전체 자원 사용을 관리하는 Resource Manager를 Master로 Node Manager가 클러스터의 컴퓨터에서 컴퓨터 컨테이너를 시작하고 감시한다.

     ![hadoop_6](https://user-images.githubusercontent.com/71415474/113340495-f0278080-9366-11eb-991c-02bc1ad0eb6d.PNG)

   <br>

   - Hadoop1과 Hadoop2 차이

     ![img](https://mblogthumb-phinf.pstatic.net/MjAxOTEyMTNfMTEz/MDAxNTc2MjI4MjQ4NDU1.5la4QgT8j84D_03yIHEHK9Ampx5DRGiStDK0kmSg-TAg.cfuVxA7Cvo1479JfR9c7NvhmYyYu__JM32NRJBQIQxsg.PNG.hse05105/image.png?type=w800)
   
     
  
     - Hadoop1
       - 네임노드, 데이터 노드가 처리
       - 병렬처리(MapReduce): 잡트래커, 태스트 트래커가 처리
    - 클러스터당 최대 4000개의 노드를 등록
       - 작업 처리를 슬롯(slot) 단위로 처리
       - 맵, 리듀스 슬롯을 구분하여 처리
     - Hadoop2
       - 클러스터 관리: 리소스 매니저, 노드 매니저
       - 작업 관리: 애플리케이션 마스터, 컨테이너
       - MR외 Spark, Hive, Pig 등 다른 분산 처리 모델도 수행 가능
       - 클러스터당 1만개 이상의 노드 등록 가능
       - 작업 처리를 컨테이너(container) 단위로 처리
   
   

---

### Reference

- Hadoop 강의: https://www.youtube.com/watch?v=Ep9QiRjpifc&t=4532s
- 강의 안에 참조: https://www.internetlivestats.com/google-search-statistics/#trend