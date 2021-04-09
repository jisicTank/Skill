# Hadoop 기술면접 질문 모음

**1. Hadoop Framework에서 사용되는 개념은 무엇입니까?**

답변 : Hadoop Framework는 두 가지 핵심 개념에서 작동합니다.

**HDFS** : Hadoop Distributed File System의 약자로, 대규모 데이터 세트의 확장 가능하고 안정적인 저장을위한 Java 기반 파일 시스템입니다. HDFS 자체는 마스터 - 슬레이브 아키텍처에서 작동하며 모든 데이터를 블록 형태로 저장합니다.

**MapReduce** : 빅데이터를 처리하고 생성하기위한 프로그래밍 모델 및 관련 구현입니다. Hadoop 작업은 기본적으로 두 가지 다른 작업으로 나뉩니다. 맵 작업은 데이터 세트를 키 - 값 쌍 또는 튜플로 나눕니다. 그런 다음 reduce 작업은 맵 작업의 출력을 가져 와서 데이터 튜플을 더 작은 튜플 세트로 결합합니다.

**2. 하둡이란 무엇입니까? Hadoop 응용 프로그램의 주요 구성 요소 이름을 지정합니다.**

답변 : Hadoop은 "빅 데이터"문제에 대한 해결책으로 진화 한 것입니다. Hadoop은 Big Data를 저장하고 처리하기 위해 다양한 도구와 서비스를 제공하는 프레임 워크로 설명됩니다. 또한 기존의 방법을 사용하여 의사 결정을 내리기가 어려울 때 큰 데이터를 분석하고 비즈니스 의사 결정을 효율적으로 수행하는 데 중요한 역할을합니다.

Hadoop은 데이터를 매우 쉽게 저장하고 처리 할 수있는 방대한 도구 세트를 제공합니다. 다음은 Hadoop의 모든 주요 구성 요소입니다.

[![img](https://www.whizlabs.com/wp-content/uploads/2017/12/hadoop-ecosysterm.png)](https://m.blog.naver.com/PostView.nhn?blogId=sunny_86_&logNo=221503974389&proxyReferer=https:%2F%2Fwww.google.com%2F#)

하둡 일반

HDFS

Hadoop MapReduce

방사

PIG 및 HIVE - 데이터 액세스 구성 요소.

HBase - 데이터 저장 용

Apache Flume, Sqoop, Chukwa - 데이터 통합 구성 요소

Ambari, Oozie 및 ZooKeeper - 데이터 관리 및 모니터링 구성 요소

Thrift 및 Avro - 데이터 직렬화 구성 요소

Apache Mahout 및 Drill - 데이터 인텔리전스 구성 요소

**3. Hadoop에는 몇 가지 입력 형식이 있습니까? 설명.**

답변 : Hadoop에는 다음 세 가지 입력 형식이 있습니다.

텍스트 입력 형식 : 텍스트 입력은 Hadoop의 기본 입력 형식입니다.

순서 파일 입력 형식 :이 입력 형식은 파일을 순서대로 읽는 데 사용됩니다.

키 값 입력 형식 :이 입력 형식은 일반 텍스트 파일에 사용됩니다.

**4. 얀에 대해 뭘 알고 있니?**

답변 : YARN은 Yet Another Resource Negotiator의 약자로 Hadoop 프로세싱 프레임 워크입니다. YARN은 자원을 관리하고 프로세스의 실행 환경을 설정해야합니다.

**5. Hadoop 클러스터에서 노드가 자주 제거되고 추가되는 이유는 무엇입니까?**

답변 : Hadoop 프레임 워크의 다음 기능을 사용하면 Hadoop 관리자가 Hadoop 클러스터에서 데이터 노드를 추가 (커미션) 및 제거 (폐기) 할 수 있습니다.

Hadoop 프레임 워크는 상용 하드웨어를 사용하며 Hadoop 프레임 워크의 중요한 기능 중 하나입니다. Hadoop 클러스터에서 DataNode 충돌이 자주 발생합니다.

데이터 볼륨의 급속한 증가에 따라 수행되는 Hadoop 프레임 워크의 또 다른 중요한 기능은 규모의 용이함입니다.

**6. "Rack Awareness"란 무엇을 알고 있습니까?**

답변 : Hadoop에서 Rack Awareness는 NameNode가 블록과 해당 복제본을 Hadoop 클러스터에 저장하는 방법을 결정하는 알고리즘으로 정의됩니다. 이는 동일한 랙 내의 DataNode 간 트래픽을 최소화하는 랙 정의를 통해 수행됩니다. 예를 들어 봅시다 - 복제 계수의 기본값은 3입니다. "Replica Placement Policy"에 따르면 모든 데이터 블록에 대한 복제본 두 개가 단일 랙에 저장되는 반면 세 번째 복사본은 다른 랙에 저장됩니다 고문.

**7. 투기 적 실행에 대해 무엇을 압니까?**

답변 : Hadoop에서, 추측 실행은 노드에서 작업을 더 느리게 실행하는 동안 발생하는 프로세스입니다. 이 프로세스에서 마스터 노드는 다른 노드에서 동일한 작업의 다른 인스턴스 실행을 시작합니다. 그리고 처음에 완료된 작업은 받아 들여지고 다른 작업의 실행은 그 작업을 중단하여 중단됩니다.

**8. Hadoop의 중요한 기능 중 일부를 설명하십시오.**

답변 : Hadoop의 중요한 기능은 다음과 같습니다.

Hadoop 프레임 워크는 Google Big Data File System을 기반으로하는 Google MapReduce에서 설계되었습니다.

하둡 프레임 워크는 빅 데이터 분석을 위해 많은 질문을 효율적으로 해결할 수 있습니다.

**9. Hadoop을 사용하는 몇몇 회사를 알고 있습니까?**

답변 : 예, Hadoop을 사용하는 인기있는 이름을 알고 있습니다.

Yahoo - Hadoop 사용

Facebook - 분석을 위해 Hive를 개발했습니다.

Amazon, Adobe, Spotify, Netflix, eBay 및 Twitter는 Hadoop을 사용하는 잘 알려진 기존 회사 중 일부입니다.

**10. RDBMS와 Hadoop을 어떻게 구별 할 수 있습니까?**

답변 : RDBMS와 Hadoop을 차별화하는 핵심 포인트는 다음과 같습니다.

RDBMS는 구조화 된 데이터를 저장하도록 만들어졌지만 Hadoop은 구조화되지 않은, 구조화 된 또는 반 구조화 된 모든 종류의 데이터를 저장할 수 있습니다.

Hadoop은 "Schema on Read"정책을 기반으로하는 반면 RDBMS는 "Schema on Write"정책을 따르고 있습니다.

데이터 스키마는 RDBMS에서 이미 알려져있어 읽기가 빠르지 만 HDFS에서는 HDFS 쓰기 중에 스키마 유효성 검사가 수행되지 않으므로 쓰기가 빠릅니다.

RDBMS는 라이센스가 부여 된 소프트웨어이므로 Hadoop은 오픈 소스 소프트웨어이므로 비용을 지불해야하므로 비용이 들지 않습니다.

RDBMS는 OLTP (온라인 트랜잭션 처리) 시스템에 사용되는 반면 Hadoop은 데이터 분석, 데이터 검색 및 OLAP 시스템에도 사용됩니다.

**하둡 아키텍처 인터뷰 질문**

다음으로 Hadoop 아키텍처를 기반으로 한 Hadoop 인터뷰 질문이 있습니다. Hadoop 아키텍처를 알고 이해하면 Hadoop 전문가가 모든 Hadoop 인터뷰 질문에 올바르게 대답 할 수 있습니다.

**11. Hadoop 1과 Hadoop 2의 차이점은 무엇입니까?**

답변 : 다음 두 가지 사항은 Hadoop 1과 Hadoop 2의 차이점을 설명합니다.

Hadoop 1.X에는 단일 실패 지점 인 단일 NameNode가 있지만 Hadoop 2.x에는 Active 및 Passive NameNodes가 있습니다. 활성 NameNode가 실패하면 수동 NameNode가 활성 NameNode를 대체하고 요금을 청구합니다. 결과적으로 Hadoop 2.x에는 고 가용성이 존재합니다.

Hadoop 2.x에서 YARN은 Hadoop에서 여러 애플리케이션을 실행하기위한 공통 리소스를 공유하는 중앙 리소스 관리자를 제공하는 반면 Hadoop 1.x에서는 데이터 처리가 문제가됩니다.

**12. 활성 및 수동 NameNodes에 대해 무엇을 알고 있습니까?**

답변 : 고 가용성 Hadoop 아키텍처에는 두 개의 NameNode가 있습니다.

**Active NameNode -** Hadoop 클러스터에서 실행되는 NameNode는 Active NameNode입니다.

**Passive NameNode -** Active NameNode와 동일한 데이터를 저장하는 대기 NameNode는 Passive NameNode입니다.

활성 NameNode의 실패시 수동 NameNode가이를 대체하고 요금을 청구합니다. 이런 식으로 항상 클러스터에 실행중인 NameNode가 있으므로 결코 실패하지 않습니다.

**13. Apache HBase의 구성 요소는 무엇입니까?**

답변 : Apache HBase 다음 주요 구성 요소로 구성됩니다.

**지역 서버** : 표는 여러 지역으로 나눌 수 있습니다. 이러한 지역 그룹은 지역 서버에 의해 클라이언트에 제공됩니다.

**HMaster** : 지역 서버를 조정하고 관리합니다.

**ZooKeeper** : HBase 분산 환경에서 코디네이터 역할을합니다. 세션에서 통신을 통해 클러스터 내부의 서버 상태를 유지 관리합니다.

**14. NameNode가 DataNode 실패를 어떻게 처리합니까?**

Answer : NameNode는 DataNode의 적절한 기능을 지정하는 Hadoop 클러스터에있는 모든 DataNode로부터 지속적으로 신호를받습니다. DataNode에있는 모든 블록 목록은 블록 보고서에 저장됩니다. DataNode가 NameNode로 신호를 보내는데 실패하면, 특정 시간 후에 Dead로 표시됩니다. 그런 다음 NameNode는 이전에 생성 된 복제본이있는 다른 DataNode로 사용 불능 노드의 블록을 복제 / 복사합니다.

**15. NameNode 복구 프로세스를 설명하십시오.**

답 : NameNode 복구 프로세스는 Hadoop 클러스터를 계속 실행하는 데 도움이되며 다음 단계에 따라 설명 할 수 있습니다.

1 단계 : 새 NameNode를 시작하려면 파일 시스템 메타 데이터 복제본 (FsImage)을 사용합니다.

2 단계 : 새 NameNode를 확인하도록 클라이언트와 DataNode를 구성합니다.

3 단계 : 새 Name이 마지막 체크 포인트 FsImage의로드를 완료하고 DataNode에서 블록 보고서를 수신하면 새 NameNode가 클라이언트를 제공하기 시작합니다.

**16. Hadoop에서 사용할 수있는 다른 스케줄러는 무엇입니까?**

답변 : Hadoop에서 사용 가능한 여러 가지 스케줄러는 다음과 같습니다.

COSHH - 클러스터, 작업 부하를 고려하고 이질성을 사용하여 의사 결정을 예약합니다.

FIFO 스케줄러 - 이질성을 사용하지 않고 대기열에 도착 시간을 기준으로 작업을 주문합니다.

공정한 공유 - 여러 맵을 포함하고 자원의 슬롯을 줄이는 각 사용자에 대한 풀을 정의합니다. 각 사용자는 작업 실행을 위해 자체 풀을 사용할 수 있습니다.

**17. DataNode와 NameNode는 필수 하드웨어 일 수 있습니까?**

답변 : DataNode는 랩톱이나 개인용 컴퓨터와 같은 데이터를 저장할 수있는 상용 하드웨어입니다. 많은 수의 데이터 노드가 필요합니다. 대신 NameNode는 마스터 노드입니다. HDFS에 저장된 모든 블록에 대한 메타 데이터를 저장합니다. 높은 메모리 공간이 필요하므로 훌륭한 메모리 공간을 갖춘 고급 컴퓨터로 작동합니다.

**18. Hadoop 대몬이란 무엇입니까? 그들의 역할을 설명하십시오.**

답변 : Hadoop 데몬은 NameNode, Secondary NameNode, DataNode, NodeManager, ResourceManager, JobHistoryServer입니다. 다른 Hadoop 데몬의 역할은 다음과 같습니다.

**NameNode -** 모든 디렉토리와 파일에 대한 메타 데이터 저장을 담당하는 마스터 노드를 NameNode라고합니다. 또한 파일의 각 블록과 Hadoop 클러스터에서의 할당에 대한 메타 데이터 정보를 포함합니다.

**Secondary NameNode -** 이 데몬은 수정 된 파일 시스템 이미지를 병합하여 영구 저장 장치에 저장합니다. NameNode가 실패 할 경우에 사용됩니다.

**DataNode -** 실제 데이터를 포함하는 슬레이브 노드는 DataNode입니다.

**NodeManager -** 노예 머신에서 실행되는 NodeManager는 애플리케이션 컨테이너의 실행을 처리하고 리소스 사용을 모니터링하며 ResourceManager와 동일하게보고합니다.

**ResourceManager - 리소스** 관리 및 YARN 상단에서 실행되는 응용 프로그램 예약을 담당하는 주요 기관입니다.

**JobHistoryServer -** 응용 프로그램 마스터가 작동을 멈추거나 (종료 될 때) MapReduce 작업에 대한 모든 정보를 유지 관리합니다.

**19. "검사 점"을 정의하십시오. 그것의 이득은 무엇입니까?**

답변 : 체크 포인트는 FsImage와 편집 로그를 새로운 FsImage로 압축하는 절차입니다. 이런 식으로 NameNode는 편집 로그를 재생하는 대신 FsImage에서 최종 메모리 내 상태를 직접로드합니다. 보조 NameNode는 검사 점 프로세스를 수행합니다.

**Hadoop 관리자 인터뷰 질문**

Hadoop 관리자는 Hadoop 클러스터가 원활하게 실행되는 것을 처리 할 책임이 있습니다. Hadoop Administrator 취업 면접을 해독하려면 Hadoop 환경, 클러스터 등과 관련된 Hadoop 면접 질문을 수행해야합니다. Hadoop Administrator에 대한 일반적인 Hadoop 면접 질문은 다음과 같습니다.

**20. 프로덕션 환경에서 Hadoop을 배포 할 때 중요한 하드웨어 고려 사항은 무엇입니까?**

답변 : **메모리 시스템의 메모리 요구 사항** : 이는 작업자 서비스와 응용 프로그램을 기반으로하는 관리 서비스에 따라 다릅니다.

**운영 체제 :** 64 비트 OS는 작업자 노드에서 사용할 수있는 메모리 양에 대한 이러한 제한을 피하기 때문에 선호됩니다.

**스토리지** : Hadoop 플랫폼은 컴퓨팅 활동을 데이터로 이동시켜 확장 성 및 고성능을 달성함으로써 설계되어야합니다.

**용량** : 대형 폼 팩터 디스크는 비용이 적게 들고 더 많은 저장 공간을 허용합니다.

**네트워크 :** 랙 당 2 개의 TOR 스위치는 중복성을 피하는 데 이상적입니다.

**21. 2 차 NameNode를 배치하는 동안 고려해야 할 사항은 무엇입니까?**

답변 : 보조 NameNode는 항상 별도의 독립 실행 형 시스템에 배포해야합니다. 이렇게하면 기본 노드의 작업을 방해하지 않습니다.

**22. Hadoop 코드를 실행할 수있는 모드의 이름을 지정하십시오.**

답변 : Hadoop 코드를 실행하는 데는 여러 가지 모드가 있습니다.

완전 분산 모드

의사 분산 모드

독립 실행 형 모드

**23. Hadoop 배치가 지원하는 운영체제의 이름을 지정하십시오.**

답변 : Linux는 Hadoop에 사용되는 주요 운영 체제입니다. 그러나 일부 추가 소프트웨어를 사용하여 Windows 운영 체제에 배포 할 수도 있습니다.

**24. HDFS가 여러 개의 작은 파일이 아닌 대용량 데이터 세트가있는 응용 프로그램에 사용되는 이유는 무엇입니까?**

답변 : HDFS는 여러 파일에 저장된 작은 데이터 덩어리에 비해 단일 파일로 유지되는 많은 수의 데이터 세트에 대해 더 효율적입니다. NameNode는 RAM의 파일 시스템에 대한 메타 데이터 저장을 수행하기 때문에 메모리 양은 HDFS 파일 시스템의 파일 수를 제한합니다. 간단히 말해서, 더 많은 파일이 더 많은 메타 데이터를 생성하고, 차례로 더 많은 메모리 (RAM)를 필요로합니다. 블록, 파일 또는 디렉토리의 메타 데이터는 150 바이트를 차지하는 것이 좋습니다.

**25. hdfs-site.xml의 중요한 특성은 무엇입니까?**

답변 : hdfs-site.xml에는 다음과 같은 세 가지 중요한 속성이 있습니다.

data.dr - 데이터 저장 위치를 식별합니다.

name.dr - 메타 데이터 저장 위치를 식별하고 DFS가 디스크에 있는지 또는 원격 위치에 있는지 여부를 지정합니다.

checkpoint.dir - 보조 NameNode에 사용됩니다.

**26. Big Data의 성능을 향상시키는 필수 Hadoop 도구는 무엇입니까?**

답변 : 빅 데이터의 성능을 향상시키는 필수 Hadoop 도구 중 일부는 다음과 같습니다.

하이브, HDFS, HBase, Avro, SQL, NoSQL, Oozie, Clouds, Flume, SolrSee / Lucene 및 ZooKeeper

**SequenceFile에 대해 무엇을 알고 있습니까?**

답 : SequenceFile은 바이너리 키 또는 값 쌍을 포함하는 플랫 파일로 정의됩니다. 주로 MapReduce의 입력 / 출력 형식에서 사용됩니다. 맵 출력은 SequenceFile로 내부적으로 저장됩니다.

SequenceFile의 다른 형식은 다음과 같습니다.

**레코드 압축 키 / 값 레코드 -** 이 형식에서는 값이 압축됩니다.

**압축 된 키 / 값 레코드 차단 -** 이 형식에서 값과 키는 별도로 블록에 저장되고 압축됩니다.

**압축되지 않은 키 / 값 레코드 -** 이 형식에서는 값이나 키가 압축되지 않습니다.

**28. Job Tracker의 기능을 설명하십시오.**

답변 : Hadoop에서 Job Tracker는 다음과 같은 다양한 기능을 수행합니다.

리소스를 관리하고 리소스 가용성을 추적하며 작업의 수명주기를 관리합니다.

NameNode와 통신하여 데이터 위치를 식별합니다.

최적의 작업 추적 노드를 찾아 주어진 노드에서 작업을 실행합니다.

Job Tracker는 모든 작업 추적기를 개별적으로 모니터링 한 다음 전체 작업을 클라이언트에 제출합니다.

로컬에서 슬레이브 노드로 MapReduce 워크로드 실행을 추적합니다.

**Hadoop HDFS 인터뷰 질문**

Hadoop 분산 파일 시스템 (HDFS)은 Hadoop에서 사용되는 주요 스토리지 시스템입니다. Hadoop 전문가에게는 HDFS, HDFS 구성 요소 및 HDFS에 대한 지식이 있어야합니다. Hadoop 인터뷰를 진행하는 데 도움이되는 몇 가지 HDFS 기반 Hadoop 인터뷰 질문이 있습니다. 이 HDFS 관련 Hadoop 인터뷰 질문을하기 전에 기본 Hadoop 인터뷰 질문을 먼저 읽어보고 더 나은 이해를 얻는 것이 좋습니다.

**29. HDFS는 NAS와 어떻게 다른가요?**

답변 : 다음 사항은 HDFS와 NAS의 차이점입니다.

Hadoop 분산 파일 시스템 (HDFS)은 범용 하드웨어를 사용하여 데이터를 저장하는 분산 파일 시스템입니다. NAS (Network Attached Storage)는 컴퓨터 네트워크에 연결된 데이터 저장소의 파일 서버입니다.

HDFS는 데이터 블록을 클러스터에있는 모든 시스템에 분산 방식으로 저장하지만 NAS는 전용 하드웨어에 데이터를 저장합니다.

HDFS는 비용 효율적인 비용으로 상용 하드웨어를 사용하여 데이터를 저장하며, NAS는 높은 비용을 포함하는 고급 장치에 데이터를 저장합니다.

HDFS는 MapReduce 패러다임과 함께 작동하지만 NAS는 MapReduce와 함께 작동하지 않으며 데이터와 계산이 별도로 저장됩니다.

**30. HDFS 내결함성이 있습니까? 그렇다면 어떻게?**

답변 : 예, HDFS는 내결함성이 뛰어납니다. 일부 데이터가 HDFS에 저장 될 때마다 NameNode는 해당 데이터를 여러 DataNode에 복제 (복사)합니다. 기본 복제 요소의 값은 요구 사항에 따라 변경할 수있는 3입니다. DataNode가 다운 된 경우 NameNode는 복제본의 데이터를 가져 와서 다른 노드로 복사하므로 데이터를 자동으로 사용할 수 있습니다. 이러한 방식으로 HDFS는 내결함성 기능을 갖추고 있으며 내결함성으로 알려져 있습니다.

**31. HDFS 블록과 입력 분할을 구별하십시오.**

답변 : HDFS 블록과 입력 분할의 가장 큰 차이점은 HDFS 블록은 데이터의 물리적 구분으로 알려져 있고 입력 분할은 데이터의 논리적 구분으로 간주된다는 것입니다. 처리를 위해 HDFS는 먼저 데이터를 블록으로 나눈 다음 모든 블록을 함께 저장합니다. MapReduce는 먼저 데이터를 입력 분할로 나눈 다음이 입력 분할을 매퍼 함수에 할당합니다.

**32. 두 클라이언트가 HDFS에서 동일한 파일에 액세스하려고하면 어떻게됩니까?**

답변 : HDFS는 단독 쓰기 (한 번에 한 파일에 대해 하나의 쓰기 요청 만 처리) 만 지원하는 것으로 알려져 있습니다.

첫 번째 클라이언트가 NameNode에 연결하여 쓰기 파일을 열면 NameNode는 클라이언트에 임대를 제공하여이 파일을 만듭니다. 두 번째 클라이언트가 동일한 파일을 열어 쓰기 요청을 보내면 NameNode는 해당 파일에 대한 임대가 이미 다른 클라이언트에 주어 졌으므로 두 번째 클라이언트의 요청을 거부합니다.

**33. HDFS의 블록은 무엇입니까?**

답변 : 데이터를 저장할 수있는 하드 드라이브상의 가장 작은 사이트 또는 위치를 블록이라고합니다. HDFS의 데이터는 블록으로 저장되고 Hadoop 클러스터를 통해 배포됩니다. 전체 파일은 먼저 작은 블록으로 분할 된 다음 별도의 단위로 저장됩니다.

**Hadoop 개발자 인터뷰 질문**

Hadoop 개발자는 큰 데이터 영역에서 작업하면서 Hadoop 응용 프로그램 개발을 담당합니다. Big Data Hadoop 인터뷰 질문은 단순히 Hadoop 생태계와 그 구성 요소에 대한 이해를 기반으로합니다. 하둡 개발자 인터뷰에 도움이 될 Hadoop 인터뷰 질문이 있습니다.

**34. Apache Yarn이란 무엇입니까?**

답변 : YARN은 Yet Another Resource Negotiator를 의미합니다. Hadoop Cluster 자원 관리 시스템입니다. MapReduce를 돕기 위해 Hadoop 2에 도입되었으며 Hadoop의 차세대 계산 및 리소스 관리 프레임 워크입니다. Hadoop을 사용하면보다 다양한 처리 방식과 다양한 애플리케이션을 지원할 수 있습니다.

**35. 노드 관리자 란 무엇입니까?**

답변 : 노드 관리자는 Tasktracker와 동일한 YARN입니다. ResourceManager로부터 지시를 받고 단일 노드에서 사용 가능한 자원을 관리합니다. 컨테이너에 대한 책임이 있으며 ResourceManager에 대한 리소스 사용을 모니터링 및보고합니다. 종속 노드에서 실행되는 모든 단일 컨테이너 프로세스는 해당 종속 노드에 해당하는 노드 관리자 데몬에 의해 초기에 프로비저닝, 모니터링 및 추적됩니다.

**36. Hadoop의 RecordReader는 무엇을 위해 사용 되었습니까?**

Hadoop에서 RecordReader는 분할 된 데이터를 단일 레코드로 읽는 데 사용됩니다. Hadoop이 데이터를 다양한 블록으로 분할 할 때 데이터를 결합하는 것이 중요합니다. 예를 들어 입력 데이터가 -

행 1 :에 오신 것을 환영합니다.

2 행 : 하둡 세계

RecordReader를 사용하면 "Hadoop에 오신 것을 환영합니다"로 읽힐 것입니다.

**37. 감속기 출력에 영향을주지 않고 매퍼 출력을 압축하는 절차는 무엇입니까?**

감속기 출력에 영향을 미치지 않고 맵퍼 출력을 압축하려면 다음을 설정하십시오.

Conf.set ( "mapreduce.map.output.compress", true)

Conf.set ( "mapreduce.output.fileoutputformat.compress", false)

**38. 감속기의 여러 가지 방법을 설명하십시오.**

감속기의 다른 방법은 다음과 같습니다.

Setup () - 입력 데이터 크기와 같은 다른 매개 변수를 구성하는 데 사용됩니다.

구문 : public void setup (context)

정리 () - 작업이 끝날 때 모든 임시 파일을 정리하는 데 사용됩니다.

구문 : public void cleanup (context)

Reduce () -이 방법은 감속기의 핵심으로 알려져 있습니다. 연관된 감소 작업과 함께 키마다 한 번씩 정기적으로 사용됩니다.

구문 : public void reduce (키, 값, 컨텍스트)

**39. HDFS에서 복제 요소를 어떻게 구성 할 수 있습니까?**

HDFS의 설정은 hdfs-site.xml 파일이 사용됩니다. HDFS에 저장된 모든 파일에 대한 복제 계수의 기본값을 변경하기 위해 다음 속성이 hdfs-site.xml에서 변경되었습니다

dfs.replication

**40. "jps"명령의 사용은 무엇입니까?**

"jps"명령은 Hadoop 데몬이 실행 중 상태인지 여부를 확인하는 데 사용됩니다. 이 명령은 시스템에서 실행중인 모든 Hadoop 데몬, 즉 namenode, nodemanager, resourcemanager, datanode 등을 나열합니다.

**41. Hadoop에서 "NameNode"또는 다른 모든 데몬을 재시작하는 절차는 무엇입니까?**

Hadoop에서 NameNode 및 다른 모든 데몬을 다시 시작하는 데는 여러 가지 방법이 있습니다.

**NameNode를 다시 시작하는 방법 :** 먼저 /sbin/hadoop-daemon.sh stop namenode 명령을 사용하여 NameNode를 중지 한 다음 /sbin/hadoop-daemon.sh start namenode 명령을 사용하여 NameNode를 다시 시작합니다.

**모든 데몬을 다시 시작하는 방법 :** /sbin/stop-all.sh 명령을 사용하여 한 번에 모든 데몬을 중지 한 다음 /sbin/start-all.sh 명령을 사용하여 동시에 중지 된 데몬을 모두 시작하십시오.

**42. 하이브에서 HDFS로 데이터를 전송하는 쿼리는 무엇입니까?**

Hive에서 HDFS로 데이터를 전송하는 쿼리는 다음과 같습니다.

hive> 디렉토리 덮어 쓰기 '/'select * from emp;

이 쿼리의 출력은 지정된 HDFS 경로의 파트 파일에 저장됩니다.

**43. 복사 작업에 사용되는 일반적인 Hadoop 쉘 명령은 무엇입니까?**

복사 작업을위한 일반적인 Hadoop 쉘 명령은 -

fs -copyToLocal

fs -put

fs -copyFromLocal

**시나리오 기반 하둡 인터뷰 질문**

종종 특정 시나리오에 대한 까다로운 빅 데이터 인터뷰 질문 및 처리 방법을 묻는 메시지가 나타납니다. 그러한 Hadoop 인터뷰 질문을하는 이유는 Hadoop 기술을 확인하는 것입니다. 이 Hadoop 인터뷰 질문은 주어진 큰 데이터 문제를 해결하기 위해 Hadoop 지식과 접근 방식을 구현하는 방법을 지정합니다. 시나리오 기반 Hadoop 인터뷰 질문을 통해 아이디어를 얻을 수 있습니다.

**44. Hadoop123Training.txt, _Spark123Training.txt, # DataScience123Training.txt, .Salesforce123Training.txt 파일이있는 XYZ 디렉터리가 있습니다. XYZ 디렉토리를 Hadoop MapReduce 작업에 전달하면 얼마나 많은 파일이 처리 될 수 있습니까?**

답변 : Hadoop123Training.txt 및 # DataScience123Training.txt는 MapReduce 작업에 의해 처리되는 유일한 파일입니다. 이는 FileInputFormat을 사용하여 Hadoop에서 파일을 처리하는 동안 "_"또는 "."과 같은 숨겨진 파일 접두어가없는 파일이 있는지 확인해야하기 때문에 발생합니다. MapReduce FileInputFormat은 기본적으로 HiddenFileFilter 클래스를 사용하여 이러한 모든 파일을 무시합니다. 그러나 이러한 기준을 없애기 위해 맞춤 필터를 만들 수 있습니다.

**45. 우리는 국가가 파티션 컬럼 인 하이브 파티셔닝 된 테이블을 가지고 있습니다. 우리는 10 개의 파티션을 가지고 있으며 한 국가에서만 데이터를 사용할 수 있습니다. 다른 9 개의 파티션에 대한 데이터를 복사하려면 명령 또는 수동으로 반영됩니까?**

대답 : 위의 경우 데이터는 수동으로 복사하는 대신 명령을 통해 데이터를 입력 할 때 다른 모든 파티션에 대해서만 사용할 수 있습니다.

**46. -put, -copyToLocal 및 -copyFromLocal 명령의 차이점은 무엇입니까?**

이 세 명령은 사용 된 내용에 따라 차별화 될 수 있습니다.

-put :이 명령은 원본에서 대상으로 파일을 복사하는 데 사용됩니다.

-copyToLocal :이 명령은 Hadoop 시스템에서 로컬 파일 시스템으로 파일을 복사하는 데 사용됩니다.

-copyFromLocal :이 명령은 로컬 파일 시스템에서 Hadoop 시스템으로 파일을 복사하는 데 사용됩니다.

**47. Left Semi Join과 Inner Join의 차이점은 무엇입니까?**

Left Semi Join은 왼쪽 테이블에서만 튜플을 반환하지만 Inner Join은 주어진 조건에 따라 두 테이블 (즉, 왼손 및 오른 테이블)에서 공통 튜플을 반환합니다.

**48. Hadoop 1과 Hadoop 2의 기본 블록 크기 값은 무엇입니까? 블록 크기를 변경할 수 있습니까?**

답변 : Hadoop 1의 블록 크기 기본값은 64MB입니다.

Hadoop 2의 블록 크기 기본값은 128MB입니다.

예, 블록 크기를 기본값에서 변경할 수 있습니다. 다음 매개 변수는 hdfs-site.xml 파일을 사용하여 Hadoop에서 블록 크기를 변경하고 설정합니다.

dfs.block.size

**49. NameNode가 jps 명령을 사용하여 올바르게 작동하는지 어떻게 확인합니까?**

답변 : 다음 상태는 NameNode가 jps 명령을 사용하여 작동하는지 확인하는 데 사용할 수 있습니다.

/etc/init.d/hadoop-0.20-namenode

**50. MapReduce 작업이 다시 시작되기 전에 제대로 작동하는 동안 최근 재시작 된 클러스터에서 MapReduce 작업이 실패합니다. 이 실패의 원인은 무엇입니까?**

데이터 크기에 따라 데이터 복제에는 다소 시간이 걸립니다. Hadoop 클러스터는 모든 데이터를 복사 / 복제해야합니다. 따라서 작업 실패의 분명한 이유는 큰 데이터 크기이므로 복제 프로세스가 지연되고 있습니다. 일자리가 제대로 작동하려면 몇 시간에서 몇 시간 정도 걸릴 수 있습니다.



----

### **1. 관계형 데이터베이스와 HDFS의 기본적인 차이점은 무엇입니까?**

HDFS와 관계형 데이터베이스의 주요 차이점은 다음과 같습니다.

|                                  | **RDBMS**                                                    | **하둡**                                                     |
| -------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **데이터 유형**                  | RDBMS는 구조화 된 데이터에 의존하며 데이터의 스키마는 항상 알려져 있습니다. | 구조화, 비 구조화 또는 반 구조화 등 모든 종류의 데이터를 Hadoop에 저장할 수 있습니다. |
| **가공**                         | RDBMS는 제한된 처리 기능을 제공하거나 제공하지 않습니다.     | Hadoop을 사용하면 클러스터 전체에 분산 된 데이터를 병렬 방식으로 처리 할 수 있습니다. |
| **읽기 대** **스키마.** **쓰다** | RDBMS는 데이터를로드하기 전에 스키마 유효성 검사가 수행되는 '쓰기시 스키마'를 기반으로합니다. | 반대로 Hadoop은 읽기 정책에 대한 스키마를 따릅니다.          |
| **읽기 / 쓰기 속도**             | RDBMS에서는 데이터 스키마가 이미 알려져 있기 때문에 읽기가 빠릅니다. | HDFS 쓰기 중에 스키마 유효성 검사가 발생하지 않기 때문에 HDFS에서 쓰기가 빠릅니다. |
| **비용**                         | 따라서 라이센스가 부여 된 소프트웨어는 소프트웨어 비용을 지불해야합니다. | Hadoop은 오픈 소스 프레임 워크입니다. 따라서 소프트웨어 비용을 지불 할 필요가 없습니다. |
| **최적의 사용 사례**             | RDBMS는 OLTP (Online Trasanctional Processing) 시스템에 사용됩니다. | Hadoop은 데이터 검색, 데이터 분석 또는 OLAP 시스템에 사용됩니다. |

### 

### **2. "빅 데이터"를 설명하고 빅 데이터의 5 가지 V는 무엇입니까?**

"빅 데이터"는 관계형 데이터베이스 관리 도구 또는 기존 데이터 처리 응용 프로그램을 사용하여 처리하기 어렵게 만드는 크고 복잡한 데이터 세트 모음을 가리키는 용어입니다. 빅 데이터를 캡처, 큐레이팅, 저장, 검색, 공유, 전송, 분석 및 시각화하는 것은 어렵습니다. 빅 데이터는 기업의 기회로 떠 올랐습니다. 이제 그들은 데이터에서 성공적으로 가치를 도출 할 수 있으며 향상된 비즈니스 의사 결정 기능을 통해 경쟁사보다 뚜렷한 이점을 갖게됩니다.

*♣ Tip : 구체적으로 물어 보든 말든, 그런 질문에서 5V에 대해 이야기하는 것이 좋습니다!*

- **볼륨** : 볼륨은 기하 급수적으로 증가하는 데이터의 양을 나타냅니다 (예 : 페타 바이트 및 엑사 바이트). 
- **Velocity** : Velocity는 데이터가 증가하는 속도를 말하며 매우 빠른 속도입니다. 오늘날 어제의 데이터는 오래된 데이터로 간주됩니다. 오늘날 소셜 미디어는 데이터 증가 속도의 주요 원인입니다.
- **다양성** : 다양성은 데이터 유형의 이질성을 나타냅니다. 즉, 수집되는 데이터는 비디오, 오디오, csv 등과 같은 다양한 형식을 가지고 있습니다. 따라서 이러한 다양한 형식은 다양한 데이터를 나타냅니다.
- **Veracity** : Veracity는 데이터 불일치 및 불완전 성으로 인해 사용 가능한 데이터의 불확실성 또는 불확실성을 의미합니다. 사용 가능한 데이터는 때때로 지저분 해지고 신뢰하기 어려울 수 있습니다. 다양한 형태의 빅 데이터로 인해 품질과 정확성을 제어하기가 어렵습니다. 데이터의 품질과 정확성이 부족한 이유는 볼륨 때문입니다.
- **가치** : 빅 데이터에 접근하는 것은 좋은 일이지만 가치로 바꿀 수 없다면 쓸모가 없습니다. 그것을 가치로 바꾸는 것은 조직의 혜택을 더하는 것입니까? 빅 데이터를 작업하는 조직이 높은 ROI (투자 수익률)를 달성하고 있습니까? 빅 데이터로 작업하여 이익을 더하지 않는 한 쓸모가 없습니다.

우리가 알고 있듯이 빅 데이터가 빠른 속도로 증가하고 있으므로 이와 관련된 요인도 진화하고 있습니다. 자세히 살펴보고 자세히 이해하려면 [***BigData Tutorial\***](https://www.edureka.co/blog/big-data-tutorial) 블로그 를 살펴 보는 것이 좋습니다 .

### **3. Hadoop과 그 구성 요소는 무엇입니까?** 

"빅 데이터"가 문제로 등장했을 때 Apache Hadoop은 이에 대한 해결책으로 진화했습니다. Apache Hadoop은 빅 데이터를 저장하고 처리하기위한 다양한 서비스 또는 도구를 제공하는 프레임 워크입니다. 기존 시스템을 사용하여 효율적이고 효과적으로 수행 할 수없는 빅 데이터를 분석하고 비즈니스 결정을 내리는 데 도움이됩니다.

*♣ 팁 : 이제 Hadoop을 설명하면서 Hadoop의 주요 구성 요소에 대해서도 설명해야합니다* .

- ***저장 장치\*** – HDFS (NameNode, DataNode)
- ***처리 프레임 워크\*** – YARN (ResourceManager, NodeManager)

### **4. HDFS와 YARN은 무엇입니까?**

**HDFS** (Hadoop Distributed File System)는 Hadoop의 저장 장치입니다. 분산 환경에서 다양한 종류의 데이터를 블록으로 저장하는 역할을합니다. 마스터 및 슬레이브 토폴로지를 따릅니다.

*♣ 팁 : HDFS 구성 요소도 설명하는 것이 좋습니다.*

- ***NameNode\*** **:** NameNode는 분산 환경의 마스터 노드이며 블록 위치, 복제 인자 등 HDFS에 저장된 데이터 블록에 대한 메타 데이터 정보를 유지합니다.
- ***DataNode\*** **:** DataNode는 HDFS에 데이터를 저장하는 역할을하는 슬레이브 노드입니다. NameNode는 모든 DataNode를 관리합니다.

**YARN** (Yet Another Resource Negotiator)은 리소스를 관리하고 프로세스에 실행 환경을 제공하는 Hadoop의 처리 프레임 워크입니다.

*♣ 팁 : 마찬가지로 HDFS에서했던 것처럼 YARN의 두 가지 구성 요소도 설명해야합니다.*  

- ***ResourceManager\*** **:** 처리 요청을 수신 한 다음 요청의 일부를 이에 따라 해당 NodeManager에 전달하여 실제 처리가 수행됩니다. 필요에 따라 애플리케이션에 리소스를 할당합니다.
- ***NodeManager\*** **:** NodeManager는 모든 DataNode에 설치되며 모든 단일 DataNode에서 작업 실행을 담당합니다.

HDFS 및 YARN에 대해 자세히 알아 보려면 [***Hadoop Tutorial\***](https://www.edureka.co/blog/hadoop-tutorial/) 블로그를 참조하십시오.

### **5. 다양한 Hadoop 데몬과 Hadoop 클러스터에서의 역할에 대해 알려주십시오.**

일반적으로 HDFS 데몬 인 NameNode, DataNode 및 Secondary NameNode를 먼저 설명한 다음 YARN 데몬 인 ResorceManager 및 NodeManager로 이동하고 마지막으로 JobHistoryServer를 설명하여이 질문에 접근합니다.

- **NameNode :** 모든 파일과 디렉토리의 메타 데이터를 저장하는 마스터 노드입니다. 블록에 대한 정보, 파일을 만드는 정보 및 해당 블록이 클러스터의 위치에 있습니다.
- **데이터 노드 :** 실제 데이터를 포함하는 슬레이브 노드입니다.
- **Secondary NameNode :** 주기적으로 변경 사항 (편집 로그)을 NameNode에있는 FsImage (파일 시스템 이미지)와 병합합니다. 수정 된 FsImage를 영구 저장소에 저장하여 NameNode 장애시 사용할 수 있습니다.
- **ResourceManager : 리소스** 를 관리하고 YARN에서 실행되는 애플리케이션을 예약하는 중앙 기관입니다.
- **NodeManager :** 슬레이브 머신에서 실행되며 애플리케이션의 컨테이너 (애플리케이션이 해당 부분을 실행하는 위치)를 시작하고 리소스 사용량 (CPU, 메모리, 디스크, 네트워크)을 모니터링하고이를 ResourceManager에보고합니다.
- **JobHistoryServer :** Application Master가 종료 된 후 MapReduce 작업에 대한 정보를 유지합니다.



## **Hadoop HDFS 인터뷰 질문**

### **6. HDFS와 NAS (Network Attached Storage)를 비교합니다.**

이 질문에서 먼저 NAS와 HDFS에 대해 설명하고 다음과 같이 기능을 비교하십시오.

- NAS (Network-Attached Storage)는 이기종 클라이언트 그룹에 데이터 액세스를 제공하는 컴퓨터 네트워크에 연결된 파일 수준 컴퓨터 데이터 스토리지 서버입니다. NAS는 파일 저장 및 액세스를위한 서비스를 제공하는 하드웨어 또는 소프트웨어 일 수 있습니다. 반면 Hadoop 분산 파일 시스템 (HDFS)은 상용 하드웨어를 사용하여 데이터를 저장하는 분산 파일 시스템입니다.
- HDFS에서 데이터 블록은 클러스터의 모든 시스템에 분산됩니다. 반면 NAS 데이터는 전용 하드웨어에 저장됩니다.
- HDFS는 계산이 데이터로 이동하는 MapReduce 패러다임과 함께 작동하도록 설계되었습니다. NAS는 데이터가 계산과 별도로 저장되기 때문에 MapReduce에 적합하지 않습니다.
- HDFS는 비용 효율적인 상용 하드웨어를 사용하는 반면 NAS는 높은 비용을 포함하는 고급 스토리지 장치입니다.

### **7. Hadoop 1과 Hadoop 2의 차이점을 나열하십시오.**

이것은 중요한 질문이며이 질문에 답하는 동안 우리는 주로 Passive NameNode와 YARN 아키텍처라는 두 가지 점에 초점을 맞춰야합니다.

- Hadoop 1.x에서 "NameNode"는 단일 장애 지점입니다. Hadoop 2.x에는 액티브 및 패시브“NameNodes”가 있습니다. 활성 "NameNode"가 실패하면 수동 "NameNode"가 담당합니다. 이로 인해 Hadoop 2.x에서 고 가용성을 달성 할 수 있습니다.
- 또한 Hadoop 2.x에서 YARN은 중앙 리소스 관리자를 제공합니다. YARN을 사용하면 이제 Hadoop에서 여러 애플리케이션을 실행할 수 있으며 모두 공통 리소스를 공유합니다. MRV2는 YARN 위에서 MapReduce 프레임 워크를 실행하는 특정 유형의 분산 애플리케이션입니다. 다른 도구도 YARN을 통해 데이터 처리를 수행 할 수 있는데, 이는 Hadoop 1.x에서 문제였습니다.

|                          | **Hadoop 1.x**                    | **하둡 2.x**                                 |
| ------------------------ | --------------------------------- | -------------------------------------------- |
| **패시브 N** **ameNode** | NameNode는 단일 실패 지점입니다.  | 액티브 및 패시브 네임 노드                   |
| **가공**                 | MRV1 (작업 추적기 및 작업 추적기) | MRV2 / YARN (ResourceManager 및 NodeManager) |

### 

### **8. 능동 및 수동“NameNodes”는 무엇입니까?** 

HA (고 가용성) 아키텍처에는 두 개의 NameNode (활성 "NameNode"및 수동 "NameNode")가 있습니다.

- 활성 "NameNode"는 클러스터에서 작동하고 실행되는 "NameNode"입니다.
- 패시브 "NameNode"는 활성 "NameNode"와 유사한 데이터를 가진 대기 "NameNode"입니다.

활성 "NameNode"가 실패하면 수동 "NameNode"가 클러스터의 활성 "NameNode"를 대체합니다. 따라서 클러스터에는 "NameNode"가 없어서 실패하지 않습니다.

### **9. Hadoop 클러스터에서 노드를 자주 제거하거나 추가하는 이유는 무엇입니까?**

Hadoop 프레임 워크의 가장 매력적인 기능 중 하나는 *상용 하드웨어* 의 *활용입니다* . 그러나 이로 인해 Hadoop 클러스터에서 빈번한 "DataNode"충돌이 발생합니다. Hadoop Framework의 또 다른 놀라운 기능은 데이터 볼륨의 급격한 증가에 따른 *확장 용이성입니다* . 이러한 두 가지 이유 때문에 Hadoop 관리자의 가장 일반적인 작업 중 하나는 Hadoop 클러스터에서 "데이터 노드"를 시운전 (추가) 및 해제 (제거)하는 것입니다.

이 블로그를 읽고 Hadoop 클러스터의 ***[노드 커미셔닝 및 디 커미셔닝에](https://www.edureka.co/blog/commissioning-and-decommissioning-nodes-in-a-hadoop-cluster/)*** 대해 자세히 알아보십시오 .

### **10. 두 클라이언트가 HDFS에서 동일한 파일에 액세스하려고하면 어떻게됩니까?**

HDFS는 단독 쓰기 만 지원합니다.

첫 번째 클라이언트가 "NameNode"에 접속하여 쓰기 위해 파일을 열면 "NameNode"는 클라이언트에게이 파일을 만들 수있는 임대 권한을 부여합니다. 두 번째 클라이언트가 쓰기 위해 동일한 파일을 열려고 할 때 "NameNode"는 파일에 대한 임대가 이미 다른 클라이언트에 부여되었음을 인식하고 두 번째 클라이언트에 대한 열기 요청을 거부합니다.

### **11. 네임 노드는 데이터 노드 장애를 어떻게 해결합니까?**

NameNode는 클러스터의 각 DataNode에서 주기적으로 Heartbeat (신호)를 수신합니다. 이는 DataNode가 제대로 작동하고 있음을 의미합니다.

[![코스 커리큘럼](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/themes/edu-new/img/course-curriculum.png)BigData Hadoop 인증 교육강사 주도 세션실제 사례 연구평가평생 액세스커리큘럼 살펴보기](https://www.edureka.co/big-data-hadoop-training-certification)

블록 보고서에는 DataNode의 모든 블록 목록이 포함됩니다. DataNode가 하트 비트 메시지 전송에 실패하면 특정 시간이 지나면 Dead로 표시됩니다.

네임 노드는 이전에 생성 된 복제본을 사용하여 죽은 노드의 블록을 다른 데이터 노드로 복제합니다.

### **12. NameNode가 다운되면 어떻게 하시겠습니까?**

NameNode 복구 프로세스에는 Hadoop 클러스터를 시작하고 실행하기위한 다음 단계가 포함됩니다.

1. 파일 시스템 메타 데이터 복제본 (FsImage)을 사용하여 새 NameNode를 시작합니다. 
2. 그런 다음 시작된이 새 NameNode를 인식 할 수 있도록 DataNode 및 클라이언트를 구성하십시오.
3. 이제 새 NameNode는 마지막 체크 포인트 FsImage (메타 데이터 정보 용)로드를 완료하고 DataNode에서 충분한 블록 보고서를 수신 한 후 클라이언트 서비스를 시작합니다. 

반면 대규모 Hadoop 클러스터에서이 NameNode 복구 프로세스는 많은 시간을 소비 할 수 있으며 일상적인 유지 관리의 경우 훨씬 더 큰 문제가됩니다. 따라서 ***[HA 아키텍처](https://www.edureka.co/blog/how-to-set-up-hadoop-cluster-with-hdfs-high-availability/)*** 블로그 에서 다루는 HDFS 고 가용성 아키텍처가 있습니다.

### **13. 체크 포인트 란 무엇입니까?**

간단히 말해서 "체크 포인트"는 FsImage를 가져 와서 로그를 편집하고 새 FsImage로 압축하는 프로세스입니다. 따라서 편집 로그를 재생하는 대신 NameNode는 FsImage에서 직접 최종 메모리 내 상태를로드 할 수 있습니다. 이것은 훨씬 더 효율적인 작업이며 NameNode 시작 시간을 줄입니다. 검사 점은 Secondary NameNode에 의해 수행됩니다. 

### **14. HDFS는 어떻게 내결함성이 있습니까?** 

데이터가 HDFS를 통해 저장되면 NameNode는 데이터를 여러 DataNode에 복제합니다. 기본 복제 요소는 3입니다. 필요에 따라 구성 요소를 변경할 수 있습니다. DataNode가 다운되면 NameNode는 자동으로 데이터를 복제본에서 다른 노드로 복사하고 데이터를 사용할 수 있도록합니다. 이것은 HDFS에서 내결함성을 제공합니다.

### **15. NameNode와 DataNode가 상용 하드웨어가 될 수 있습니까?** 

이 질문에 대한 현명한 대답은 데이터 노드가 데이터를 저장하고 많은 수가 필요하기 때문에 개인용 컴퓨터 및 랩톱과 같은 상용 하드웨어입니다. 그러나 경험으로 볼 때 NameNode는 마스터 노드이며 HDFS에 저장된 모든 블록에 대한 메타 데이터를 저장합니다. 높은 메모리 (RAM) 공간이 필요하므로 NameNode는 좋은 메모리 공간을 갖춘 고급 시스템이어야합니다.

### **16. 작은 파일이 많을 때가 아니라 대용량 데이터 세트가있는 응용 프로그램에 HDFS를 사용하는 이유는 무엇입니까?** 

HDFS는 여러 파일에 분산 된 소량의 데이터에 비해 단일 파일의 대량 데이터 세트에 더 적합합니다. 아시다시피 NameNode는 파일 시스템에 관한 메타 데이터 정보를 RAM에 저장합니다. 따라서 메모리 양으로 인해 HDFS 파일 시스템의 파일 수가 제한됩니다. 즉, 파일이 너무 많으면 메타 데이터가 너무 많이 생성됩니다. 그리고 이러한 메타 데이터를 RAM에 저장하는 것은 어려울 것입니다. 일반적으로 파일, 블록 또는 디렉터리의 메타 데이터는 150 바이트를 차지합니다. 



### **17. HDFS에서 "블록"을 어떻게 정의합니까? Hadoop 1 및 Hadoop 2의 기본 블록 크기는 얼마입니까? 변경할 수 있습니까?** 

블록은 데이터가 저장되는 하드 드라이브에서 가장 작은 연속 위치 일뿐입니다. HDFS는 각각을 블록으로 저장하고 Hadoop 클러스터에 배포합니다. HDFS의 파일은 독립적 인 단위로 저장되는 블록 크기의 청크로 분할됩니다.

- Hadoop 1 기본 블록 크기 : 64MB
- Hadoop 2 기본 블록 크기 : 128MB

예, 블록을 구성 할 수 있습니다. dfs.block.size 매개 변수는 hdfs-site.xml 파일에서 사용하여 Hadoop 환경에서 블록의 크기를 설정할 수 있습니다.

### **18. 'jps'명령의 기능은 무엇입니까?** 

'jps'명령은 Hadoop 데몬이 실행 중인지 여부를 확인하는 데 도움이됩니다. 시스템에서 실행중인 모든 Hadoop 데몬, 즉 namenode, datanode, resourcemanager, nodemanager 등을 보여줍니다.

### **19. Hadoop에서 "랙 인식"을 어떻게 정의합니까?**

**Rack Awareness** 는 "NameNode"가 동일한 랙 내의 "DataNode"간의 네트워크 트래픽을 최소화하기 위해 랙 정의를 기반으로 블록 및 해당 복제본을 배치하는 방법을 결정하는 알고리즘입니다. 복제 요소 3 (기본값)을 고려한다고 가정 해 보겠습니다. 정책은 "모든 데이터 블록에 대해 두 개의 복사본이 한 랙에 존재하고 세 번째 복사본은 다른 랙에 존재합니다."라는 것입니다. 이 규칙을 "복제 배치 정책"이라고합니다.

랙 인식에 대한 자세한 내용은 ***[HDFS 아키텍처](https://www.edureka.co/blog/apache-hadoop-hdfs-architecture/)*** 블로그를 참조하십시오 . 

### **20. Hadoop에서 "예상 실행"이란 무엇입니까?** 

노드가 작업을 더 느리게 실행하는 것처럼 보이면 마스터 노드는 다른 노드에서 동일한 작업의 다른 인스턴스를 중복 실행할 수 있습니다. 그런 다음 먼저 완료된 작업이 수락되고 다른 작업은 종료됩니다. 이 프로세스를 "예상 실행"이라고합니다.

### **21. "NameNode"또는 Hadoop의 모든 데몬을 다시 시작하려면 어떻게해야합니까?** 

이 질문에는 두 가지 답이있을 수 있습니다. 두 가지 답을 모두 논의하겠습니다. 다음 방법으로 NameNode를 다시 시작할 수 있습니다.

1. 를 사용하여 NameNode를 개별적으로 중지 할 수 있습니다 ***.\*** ***/ sbin /hadoop-daemon.sh stop namenode\*** 명령을 사용하여 NameNode를 시작합니다 *.* ***/sbin/hadoop-daemon.sh start namenode\*** 명령.
2. 모든 데몬을 중지하고 시작하려면을 사용하십시오 **.** ***/ sbin / stop-all.\*** ***sh\*** 를 사용하고. ***/sbin/start-all.sh\*** 명령은 먼저 모든 데몬을 중지 한 다음 모든 데몬을 시작합니다.

이러한 스크립트 파일은 Hadoop 디렉토리 내의 sbin 디렉토리에 있습니다.

### **22. "HDFS 블록"과 "입력 분할"의 차이점은 무엇입니까?**

"HDFS 블록"은 데이터의 물리적 분할이고 "입력 분할"은 데이터의 논리적 분할입니다. HDFS는 블록을 함께 저장하기 위해 데이터를 블록으로 분할하는 반면, 처리를 위해 MapReduce는 데이터를 입력 분할로 분할하여 매퍼 기능에 할당합니다.

### **23. Hadoop을 실행할 수있는 세 가지 모드의 이름을 지정하십시오.**

Hadoop을 실행할 수있는 세 가지 모드는 다음과 같습니다.

1. ***독립형 (로컬) 모드*** : 아무것도 구성하지 않은 경우 기본 모드입니다. 이 모드에서는 NameNode, DataNode, ResourceManager 및 NodeManager와 같은 Hadoop의 모든 구성 요소가 단일 Java 프로세스로 실행됩니다. 이것은 로컬 파일 시스템을 사용합니다.
2. ***의사 분산 모드*** : 단일 노드 Hadoop 배포는 의사 분산 모드에서 Hadoop 시스템을 실행하는 것으로 간주됩니다. 이 모드에서는 마스터 및 슬레이브 서비스를 포함한 모든 Hadoop 서비스가 단일 컴퓨팅 노드에서 실행되었습니다.
3. ***완전 분산 모드*** : Hadoop 마스터 및 슬레이브 서비스가 별도의 노드에서 실행되는 Hadoop 배포는 완전 분산 모드로 표시됩니다.



![img](https://ssl.gstatic.com/ui/v1/icons/mail/images/cleardot.gif)

## **Hadoop MapReduce 인터뷰 질문**

### **24. "MapReduce"란 무엇입니까? "MapReduce"프로그램을 실행하는 구문은 무엇입니까?** 

병렬 프로그래밍을 사용하여 컴퓨터 클러스터에서 대용량 데이터 세트를 처리하는 데 사용되는 프레임 워크 / 프로그래밍 모델입니다. MapReduce 프로그램을 실행하는 구문은 **hadoop_jar_file.jar / input_path / output_path** 입니다.

MapReduce에 대한 의문이 있거나 개념을 수정하려는 경우이 ***[MapReduce 자습서를](https://www.edureka.co/blog/mapreduce-tutorial/)*** 참조 할 수 있습니다 .

### **25. "MapReduce"프로그램의 주요 구성 매개 변수는 무엇입니까?**

사용자가 "MapReduce"프레임 워크에서 지정해야하는 주요 구성 매개 변수는 다음과 같습니다.

- 분산 파일 시스템에서 작업의 입력 위치
- 분산 파일 시스템에서 작업의 출력 위치
- 데이터 입력 형식
- 데이터의 출력 형식
- 지도 함수를 포함하는 클래스
- reduce 함수를 포함하는 클래스
- 매퍼, 감속기 및 드라이버 클래스가 포함 된 JAR 파일

### **26. 매퍼에서 "집계"(추가)를 수행 할 수없는 이유를 설명하십시오. 이를 위해 "감속기"가 필요한 이유는 무엇입니까?**

이 답변에는 많은 점이 포함되어 있으므로 순차적으로 살펴 보겠습니다.

- "매퍼"기능에서 정렬이 발생하지 않기 때문에 매퍼에서 "집계"(추가)를 수행 할 수 없습니다. 정렬은 감속기 측에서만 발생하며 정렬없이 집계 할 수 없습니다.
- "집계"중에 매퍼가 데이터 블록이 저장된 다른 머신에서 실행될 수 있으므로지도 단계에서 수집 할 수없는 모든 매퍼 함수의 출력이 필요합니다.
- 마지막으로 매퍼에서 데이터를 집계하려면 다른 컴퓨터에서 실행될 수있는 모든 매퍼 기능 간의 통신이 필요합니다. 따라서 높은 네트워크 대역폭을 소비하고 네트워크 병목 현상을 일으킬 수 있습니다.

### **27. Hadoop에서 "RecordReader"의 목적은 무엇입니까?**

"InputSplit"은 작업 조각을 정의하지만 액세스 방법은 설명하지 않습니다. "RecordReader"클래스는 소스에서 데이터를로드하고 "Mapper"작업에서 읽기에 적합한 (키, 값) 쌍으로 변환합니다. "RecordReader"인스턴스는 "입력 형식"으로 정의됩니다.

### **28. "MapReduce 프레임 워크"에서 "분산 캐시"를 설명합니다.**

분산 캐시는 애플리케이션에 필요한 파일을 캐시하기 위해 MapReduce 프레임 워크에서 제공하는 기능으로 설명 할 수 있습니다. 작업을 위해 파일을 캐시하면 Hadoop 프레임 워크가 작업을 매핑 / 축소하는 각 데이터 노드에서 해당 파일을 사용할 수 있도록합니다. 그런 다음 Mapper 또는 Reducer 작업에서 캐시 파일에 로컬 파일로 액세스 할 수 있습니다.

### **29.“감소 자들”은 어떻게 서로 소통합니까?** 

이것은 까다로운 질문입니다. “MapReduce”프로그래밍 모델은“reducer”가 서로 통신하는 것을 허용하지 않습니다. "Reducers"는 격리되어 실행됩니다.

**30. "MapReduce Partitioner"는 무엇을합니까?**

"MapReduce Partitioner"는 단일 키의 모든 값이 동일한 "reducer"로 이동하도록하여 "reducer"를 통해 맵 출력을 균일하게 배포 할 수 있도록합니다. 특정 키를 담당하는 "reducer"를 결정하여 "mapper"출력을 "reducer"로 리디렉션합니다.

### **31. 사용자 지정 파티 셔 너를 어떻게 작성합니까?**

Hadoop 작업을위한 사용자 지정 파티 셔 너는 아래 단계에 따라 쉽게 작성할 수 있습니다.

- Partitioner 클래스를 확장하는 새 클래스 만들기
- Override 메서드 – MapReduce에서 실행되는 래퍼의 getPartition.
- 방법 set Partitioner를 사용하여 작업에 사용자 지정 파티 셔 너를 추가하거나 사용자 지정 파티 셔 너를 구성 파일로 작업에 추가합니다.

### **32. "결합 자"란 무엇입니까?** 

"Combiner"는 로컬 "reduce"작업을 수행하는 미니 "reducer"입니다. 특정 "노드"의 "매퍼"에서 입력을 수신하고 출력을 "감소 기"로 보냅니다. "Combiners"는 "reducers"로 전송되는 데 필요한 데이터의 양을 줄여 "MapReduce"의 효율성을 높이는 데 도움이됩니다.

### 빅 데이터 교육

[BIGDATA HADOOP 인증 교육BigData Hadoop 인증 교육*리뷰*5 (162844)](https://www.edureka.co/big-data-hadoop-training-certification)

[PYSPARK를 사용한 PYTHON SPARK 인증 교육PySpark를 사용한 Python Spark 인증 교육*리뷰*5 (6157)](https://www.edureka.co/pyspark-certification-training)

[SPLUNK 교육 및 인증-고급 사용자 및 관리자Splunk 교육 및 인증-고급 사용자 및 관리자*리뷰*5 (7857)](https://www.edureka.co/splunk-certification-training)

[APACHE SPARK 및 SCALA 인증 교육Apache Spark 및 Scala 인증 교육*리뷰*5 (27359)](https://www.edureka.co/apache-spark-scala-certification-training)

[APACHE KAFKA 인증 교육Apache Kafka 인증 교육*리뷰*5 (6524)](https://www.edureka.co/kafka-certification-training)

[ELK 스택 교육 및 인증ELK 스택 교육 및 인증*리뷰*5 (1605)](https://www.edureka.co/elk-stack-training-sp)

[HADOOP 관리 인증 교육Hadoop 관리 인증 교육*리뷰*5 (25224)](https://www.edureka.co/hadoop-administration-training-certification)

[APACHE STORM 인증 교육Apache Storm 인증 교육*리뷰*5 (5550)](https://www.edureka.co/apache-storm-certification-training)

[포괄적 인 HIVE 인증 교육포괄적 인 Hive 인증 교육*리뷰*5 (2295)](https://www.edureka.co/comprehensive-hive)

다음

### **33. "SequenceFileInputFormat"에 대해 무엇을 알고 있습니까?**

"SequenceFileInputFormat"은 시퀀스 파일 내에서 읽기위한 입력 형식입니다. 하나의 "MapReduce"작업의 출력간에 다른 "MapReduce"작업의 입력으로 데이터를 전달하는 데 최적화 된 특정 압축 이진 파일 형식입니다.

시퀀스 파일은 다른 MapReduce 작업의 출력으로 생성 될 수 있으며 하나의 MapReduce 작업에서 다른 작업으로 전달되는 데이터에 대한 효율적인 중간 표현입니다.

![img](https://ssl.gstatic.com/ui/v1/icons/mail/images/cleardot.gif)

## **Apache Pig 인터뷰 질문**

### **34. MapReduce에 비해 Apache Pig의 이점은 무엇입니까?** 

Apache Pig는 Yahoo에서 개발 한 데이터 흐름으로이를 나타내는 대규모 데이터 세트를 분석하는 데 사용되는 플랫폼입니다. MapReduce를 추상화하여 MapReduce 프로그램 작성의 복잡성을 줄 이도록 설계되었습니다.

- Pig Latin은 고수준 데이터 흐름 언어 인 반면 MapReduce는 저수준 데이터 처리 패러다임입니다.
- MapReduce에서 복잡한 Java 구현을 작성하지 않고도 프로그래머는 Pig Latin을 사용하여 동일한 구현을 매우 쉽게 수행 할 수 있습니다.
- Apache Pig는 코드 길이를 약 20 배 줄입니다 (Yahoo에 따르면). 따라서 개발 기간이 거의 16 배 단축됩니다.
- Pig는 조인, 필터, 순서 지정, 정렬 등과 같은 데이터 작업을 지원하기 위해 많은 기본 제공 연산자를 제공합니다. 반면 MapReduce에서 동일한 기능을 수행하는 것은 엄청난 작업입니다.
- Apache Pig에서 조인 작업을 수행하는 것은 간단합니다. MapReduce에서는 작업을 수행하기 위해 여러 MapReduce 작업을 순차적으로 실행해야하므로 데이터 세트간에 조인 작업을 수행하기가 어렵습니다.
- 또한 pig는 MapReduce에서 누락 된 튜플, 백 및 맵과 같은 중첩 데이터 유형도 제공합니다.

### **35. Pig Latin의 다른 데이터 유형은 무엇입니까?**

Pig Latin은 int, float, long, double 등과 같은 원자 데이터 유형과 tuple, bag 및 map과 같은 복잡한 데이터 유형을 모두 처리 할 수 있습니다.

원자 데이터 유형 : 원자 또는 스칼라 데이터 유형은 string, int, float, long, double, char [], byte []와 같은 모든 언어에서 사용되는 기본 데이터 유형입니다.

복합 데이터 유형 : 복합 데이터 유형은 Tuple, Map 및 Bag입니다.

이러한 데이터 유형에 대해 자세히 알아 보려면 ***[Pig 자습서](https://www.edureka.co/blog/pig-tutorial/)*** 블로그를 참조하십시오.

### **36. "Pig Latin"에서 작업 한 다른 관계 연산은 무엇입니까?**

다른 관계 연산자는 다음과 같습니다.

1. 각각
2. 주문
3. 필터
4. 그룹
5. 뚜렷한
6. 어울리다
7. 한도



### **37. UDF 란 무엇입니까?**

내장 연산자에서 일부 함수를 사용할 수없는 경우 프로그래밍 방식으로 UDF (사용자 정의 함수)를 생성하여 Java, Python, Ruby 등과 같은 다른 언어를 사용하여 해당 기능을 가져와 스크립트 파일에 포함 할 수 있습니다.



## ![img](https://ssl.gstatic.com/ui/v1/icons/mail/images/cleardot.gif)**Apache Hive 인터뷰 질문**

### **38. "Hive"에서 "SerDe"는 무엇입니까?**

Apache Hive는 Hadoop을 기반으로 구축 된 데이터웨어 하우스 시스템으로 Facebook에서 개발 한 정형 및 반 정형 데이터를 분석하는 데 사용됩니다. Hive는 Hadoop MapReduce의 복잡성을 추상화합니다.

"SerDe"인터페이스를 사용하면 레코드 처리 방법에 대해 "Hive"에 지시 할 수 있습니다. "SerDe"는 "시리얼 라이저"와 "디시리얼라이저"의 조합입니다. "Hive"는 "SerDe"(및 "FileFormat")를 사용하여 테이블의 행을 읽고 씁니다.

Apache Hive에 대해 자세히 알아 보려면이 ***[Hive 자습서](https://www.edureka.co/blog/hive-tutorial/)*** 블로그를 참조하십시오.

### **39. 여러 사용자 (프로세스)가 동시에 기본 "Hive Metastore"를 사용할 수 있습니까?**

"Derby 데이터베이스"는 기본 "Hive Metastore"입니다. 여러 사용자 (프로세스)가 동시에 액세스 할 수 없습니다. 주로 단위 테스트를 수행하는 데 사용됩니다.

### **40. "Hive"가 테이블 데이터를 저장하는 기본 위치는 무엇입니까?**

Hive가 테이블 데이터를 저장하는 기본 위치는 / user / hive / warehouse의 HDFS 내부입니다.





## **Apache HBase 인터뷰 질문**

### **41. Apache HBase 란 무엇입니까?**

HBase는 오픈 소스, 다차원, 분산, 확장 가능 및 Java로 작성된 NoSQL 데이터베이스입니다. HBase는 HDFS (Hadoop 분산 파일 시스템)에서 실행되며 BigTable (Google)과 같은 기능을 Hadoop에 제공합니다. 스파 스 데이터 세트의 대규모 콜렉션을 저장하는 내결함성 방법을 제공하도록 설계되었습니다. HBase는 방대한 데이터 세트에 대해 더 빠른 읽기 / 쓰기 액세스를 제공하여 높은 처리량과 짧은 지연 시간을 달성합니다.

HBase에 대한 자세한 내용은 ***[HBase 튜토리얼](https://www.edureka.co/blog/hbase-tutorial)*** 블로그를 참조하십시오.

### **42. Apache HBase의 구성 요소는 무엇입니까?**

HBase에는 HMaster Server, HBase RegionServer 및 Zookeeper의 세 가지 주요 구성 요소가 있습니다.

- ***지역 서버\*** : 테이블을 여러 지역으로 나눌 수 있습니다. 리젼 서버는 리젼 그룹을 클라이언트에 제공합니다.
- ***HMaster\*** : Region Server를 조정하고 관리합니다 (NameNode가 HDFS에서 DataNode를 관리하는 것과 유사).
- ***ZooKeeper\*** : Zookeeper는 HBase 분산 환경 내에서 조정자 역할을합니다. 세션을 통해 통신하여 클러스터 내부의 서버 상태를 유지하는 데 도움이됩니다.

자세한 내용은이 ***[HBase 아키텍처](https://www.edureka.co/blog/hbase-architecture/)*** 블로그를 참조하십시오.

### **43. 리젼 서버의 구성 요소는 무엇입니까?**

리젼 서버의 구성 요소는 다음과 같습니다.

- ***WAL\*** : Write Ahead Log (WAL)는 분산 환경 내의 모든 리젼 서버에 첨부 된 파일입니다. WAL은 영구 저장소에 저장되거나 커밋되지 않은 새 데이터를 저장합니다.
- ***블록 캐시\*** : 블록 캐시는 리젼 서버 상단에 있습니다. 자주 읽은 데이터를 메모리에 저장합니다.
- ***MemStore\*** : 쓰기 캐시입니다. 들어오는 모든 데이터를 디스크 또는 영구 메모리에 커밋하기 전에 저장합니다. 지역의 각 column family에 대해 하나의 MemStore가 있습니다.
- ***HFile\*** : HFile은 HDFS에 저장됩니다. 디스크에 실제 셀을 저장합니다.

### **44. HBase에서 "WAL"을 설명 하시겠습니까?**

WAL (Write Ahead Log)은 분산 환경 내의 모든 리젼 서버에 첨부 된 파일입니다. WAL은 영구 저장소에 저장되거나 커밋되지 않은 새 데이터를 저장합니다. 데이터 세트를 복구하지 못한 경우에 사용됩니다.

### **45. "HBase"와 "관계형 데이터베이스"의 차이점을 언급하십니까?**

HBase는 오픈 소스, 다차원, 분산, 확장 가능 및 Java로 작성된 *NoSQL 데이터베이스* 입니다. HBase는 HDFS 위에서 실행되며 Hadoop에 BigTable과 같은 기능을 제공합니다. HBase와 관계형 데이터베이스의 차이점을 살펴 보겠습니다.

|                     HBase                     |                     관계형 데이터베이스                     |
| :-------------------------------------------: | :---------------------------------------------------------: |
|                  스키마리스                   |               스키마 기반 데이터베이스입니다.               |
|         열 지향 데이터 저장소입니다.          |                행 지향 데이터 저장소입니다.                 |
| 비정규 화 된 데이터를 저장하는 데 사용됩니다. |         정규화 된 데이터를 저장하는 데 사용됩니다.          |
|      드물게 채워진 테이블을 포함합니다.       |              얇은 테이블이 포함되어 있습니다.               |
|         자동 파티셔닝은 HBase입니다.          | 파티셔닝에 대한 그러한 제공 또는 기본 제공 지원이 없습니다. |





## **Apache Spark 인터뷰 질문**

### **46. Apache Spark 란 무엇입니까?**

이 질문에 대한 대답은 Apache Spark가 분산 컴퓨팅 환경에서 실시간 데이터 분석을위한 프레임 워크라는 것입니다. 데이터 처리 속도를 높이기 위해 메모리 내 계산을 실행합니다.

인 메모리 계산 및 기타 최적화를 활용하여 대규모 데이터 처리를 위해 MapReduce보다 100 배 빠릅니다.

### **47. 특정 Hadoop 버전으로 "Spark"를 구축 할 수 있습니까?**

예, 특정 Hadoop 버전에 대한 "Spark"를 구축 할 수 있습니다. ***[Spark에서 YARN 및 HIVE를 구축](https://www.edureka.co/blog/yarn-hive-get-electrified-by-spark/)*** 하는 방법에 대해 자세히 알아 보려면이 블로그를 확인하십시오 . 

### **48. RDD를 정의합니다.**



[![코스 커리큘럼](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/themes/edu-new/img/batch-schedule.png)BigData Hadoop 인증 교육평일 / 주말 배치배치 세부 정보보기](https://www.edureka.co/big-data-hadoop-training-certification)

RDD는 Resilient Distribution Datasets (병렬 실행되는 운영 요소의 내결함성 모음)의 약어입니다. RDD의 분할 된 데이터는 변경 불가능하고 분산되어 Apache Spark의 핵심 구성 요소입니다.



## **Oozie & ZooKeeper 인터뷰 질문**

### **49. Apache ZooKeeper 및 Apache Oozie 란 무엇입니까?**

Apache ZooKeeper는 분산 환경에서 다양한 서비스와 조정됩니다. 동기화, 구성 유지 관리, 그룹화 및 이름 지정을 수행하여 많은 시간을 절약합니다.

Apache Oozie는 Hadoop 작업을 예약하고이를 하나의 논리적 작업으로 결합하는 스케줄러입니다. Oozie 작업에는 두 가지 종류가 있습니다.

- ***Oozie Workflow\*** : 실행될 일련의 작업입니다. 릴레이 경주로 가정 할 수 있습니다. 각 선수가 마지막 선수가 자신의 부분을 완료하기를 기다리는 곳.
- ***Oozie Coordinator\*** : 데이터를 사용할 수있을 때 트리거되는 Oozie 작업입니다. 이것을 우리 몸의 반응 자극 시스템이라고 생각하십시오. 같은 방식으로 우리가 외부 자극에 반응 할 때 Oozie 코디네이터는 데이터의 가용성에 반응하고 그렇지 않으면 휴식을 취합니다.

### **50. Hadoop에서 "Oozie"작업을 어떻게 구성합니까?**

"Oozie"는 "Java MapReduce", "Streaming MapReduce", "Pig", "Hive"및 "Sqoop"과 같은 여러 유형의 Hadoop 작업을 지원하는 나머지 Hadoop 스택과 통합됩니다.

"Oozie"를 자세히 이해하고 "Oozie"작업을 구성하는 방법을 배우려면 ***[Apache Oozie](https://www.edureka.co/blog/brief-introduction-to-oozie/)*** 블로그 소개를 확인하십시오 .

---

### Reference

- https://m.blog.naver.com/PostView.nhn?blogId=sunny_86_&logNo=221503974389&proxyReferer=https:%2F%2Fwww.google.com%2F
- https://shelling203.tistory.com/34