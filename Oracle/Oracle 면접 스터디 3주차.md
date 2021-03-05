# Oracle 면접 스터디 3주차



## 1. 면접 질문 소개

### 셋째마당_13: 객체 종류

1. **DB에서 Index를 사용하는 이유는?**
2. **인덱스 생성시 고려할 사항**
3. **뷰에 대해 설명하시오.**
4. **Synonym (동의어)란?**



### 셋째마당_14: 제약조건

1. **기본키(Primary Key)와 유일키(Unique Key)의 차이점은 무엇입니까?**



## 각 면접 질문 영역 개념 설명

### 셋째마당_13: 객체 종류

 데이터 사전(data dictionary), 인덱스(index), 뷰(view), 시퀀스(sequence), 동의어(synonym) 등의 사용 빈도 높은 객체들을 알아봅니다.

1. **데이터 사전**
   데이터베이스를 구성하고 운영하는데 필요한 모든 정보를 저장하는 특수 테이블

   - 메모리, 성능, 사용자, 권한, 객체 등 오라클 데이터베이스 운영에 주요 데이터가 보관

   - 데이터 사전 뷰(data dictionary view)를 통해 SELECT 문으로 정보 열람 가능

     <img src="C:\Users\oh12s\Desktop\면접스터디\SKILL\Oracle\image\image-20210304232816471.png" alt="image-20210304232816471" style="zoom: 80%;" />

2. **인덱스**
   데이터 검색 성능의 향상을 위해 테이블 열에 사용하는 객체

   - 데이터 검색 방식은 인덱스 사용여부에 따라 Full Scan, Index Scan으로 구분한다.

     - Full Scan: 테이블 데이터를 처음부터 끝까지 검색
     - Index Scan: 인덱스를 통해 검색 

   - 인덱스 정보는 USER_INDEXES, USER_IND_COLUMNS 같은 데이터 사전에서 열람 가능

   - 열이 기본키(PK), 고유키(UK)일 경우 자동으로 인덱스 생성

   - 인덱스 생성

     ```SQL
     -- CREATE INDEX 인덱스 이름 ON 열 이름;
     CREATE INDEX IDX_EMP_SAL ON EMP(SAL);
     -- 생성된 인덱스 살펴보기
     SELECT * FROM USER_IND_COLUMNS;
     ```

   - 인덱스 삭제

     ```SQL
     --DROP INDEX 인덱스 이름
     DROP INDEX IDX_EMP_SAL;
     -- 없어졌는지 확인
     SELECT * FROM USER_IND_COLUMNS;
     ```

     

3. **뷰**
   하나 이상의 테이블을 조회하는 SELECT문을 저장한 객체. 가상테이블(virtual table)

   - 뷰의 사용 목적

     - 편리성: SELECT문은 A4용지 몇 장을 꽉 채울 정도의 길이를 가질 수 있다. 따라서, 여러 SQL문에서 자주 활용하는 SELECT문을 뷰로 저장하고 다른 SQL문에 활용함으로써 전체 SQL문의 복잡도를 완화하고 메인 쿼리에 집중할 수 있어 편리
     - 보안성: 어떤 테이블에는 아무에게나 노출하기에는 예민한 데이터가 존재. 따라서, 테이블의 일부 데이터 또는 조인이나 함수로 가공한 데이터만을 SELECT하는 뷰를 만들어 열람을 제공한다면 다른 불필요한 데이터에 대한 노출을 막을 수 있다.

   - 뷰 생성

     ```SQL
     -- 뷰 생성 권한은 SYSTEM에게 있다. SYSTEM 계정으로 접속
     SQLPLUS SYSTEM/oracle
     
     -- 권한 부여
     GRANT CREATE VIEW TO SCOTT;
     
     -- 뷰 생성
     CREATE VIEW VW_EMP20 AS (SELECT EMPNO, ENAME, JOB, DEPTNO FROM EMP WHERE DEPTNO = 20);
     -- 생성한 뷰 확인
     SELECT * FROM USER_VIEWS;
     ```

   - 뷰 삭제

     ```SQL
     DROP VIEW VW_EMP20;
     -- 뷰는 가상테이블이므로 삭제해도 실제 테이블 데이터는 삭제되지 않음
     ```

   ※ 인라인뷰를 사용한 TOP-N SQL문은 실무에서 중요하므로 교재에서 꼭 실습 바람!

4. **시퀀스**
   특정 규칙에 맞는 연속 숫자를 생성하는 객체

   - 게시판 번호, 상품 주문 번호 등등..

   - 지속적이고 효율적인 번호 생성이 가능

   - 시퀀스 생성

     ```SQL
     --CREATE SEQUENCE 시퀀스 이름
     --[INCREMENT BY n]	: 시퀀스에서 생성할 번호의 증가값 (기본값 1)
     --[START WITH n]	: 시퀀스에서 생성할 번호의 시작값 (기본값 1)
     --[MAXVALUE n | NOMAXVALUE]	: 최댓값 지정.
     --[MINVALUE n | NOMINVALUE]	: 최솟값 지정.
     --[CYCLE | NOCYCLE] : 시퀀스가 최대값에 도달했을 경우 다시 처음으로 | 번호 생성 중단
     --[CACHE n | NOCACHE] : 시퀀스가 생성할 번호를 메모리에 미리 할당해 놓은 수를 지정(기본값 20) | 미리 생성하지 않도록 설정
     
     CREATE SEQUENCE SEQ_DEPT_SEQUENCE
     INCREMENT BY 10
     START WITH 10
     MAXVALUE 90
     MINVALUE 0
     NOCYCLE
     CACHE 2;
     ```

   - 시퀀스 수정

     ```SQL
     --ALTER SEQUENCE 시퀀스 이름
     --[INCREMENT BY n]
     --[MAXVALUE n | NOMAXVALUE]
     --[MINVALUE n | NOMINVALUE]
     --[CYCLE | NOCYCLE]
     --[CACHE n | NOCACHE]
     
     ALTER SEQUENCE SEQ_DEPT_SEQUENCE
     INCREMENT BY 3
     MAXVALUE 99
     CYCLE;
     ```

   - 시퀀스 삭제

     ```SQL
     DROP SEQUENCE SEQ_DEPT_SEQUENCE;
     ```

5. **동의어**
   테이블, 뷰, 시퀀스 등 객체 이름 대신 사용할 수 있는 다른 이름을 부여하는 객체.

   - 동의어 생성

     ```SQL
     -- 동의어 생성도 SYSTEM이 권한을 갖고 있다.
     SQLPLUS SYSTEM/oracle
     -- 동의어에 대한 권한 주기
     GRANT CREATE SYNONYM TO SCOTT;
     -- PUBLIC 권한도 따로 줘야함
     GRANT CREATE PUBLIC SYNONYM TO SCOTT;
     
     
     --CREATE [PUBLIC] SYNONYM 동의어 이름 FOR [사용자.][객체 이름]
     -- PUBLIC: 이 별칭을 모든 사용자가 사용할 수 있도록 설정
     
     CREATE SYNONYM E FOR EMP;
     ```

   - 동의어 삭제

     ```SQL
     DROP SYNONYM E;
     ```



### 셋째마당_14: 제약조건

1. **제약조건**

<img src="C:\Users\oh12s\Desktop\면접스터디\SKILL\Oracle\image\image-20210304232746790.png" alt="image-20210304232746790" style="zoom:80%;" />



2. **데이터 무결성**

   데이터베이스에 저장되는 데이터의 정확성과 일관성을 보장한다는 의미로 항상 유지해야하는 기본 규칙을 갖는다.

   <img src="C:\Users\oh12s\Desktop\면접스터디\SKILL\Oracle\image\image-20210304233516046.png" alt="image-20210304233516046" style="zoom:80%;" />



## 3. 면접문제 풀이

### 셋째마당_13: 객체 종류

1. **DB에서 Index를 사용하는 이유는?**

- 인덱스(Index)는 데이터를 논리적으로 정렬하여 검색과 정렬 작업의 속도를 높이기 위해 사용된다.
- 예를 들면, 책에서 가장 빨리 내용을 찾는 방법은 책의 뒤편의 색인을 보는 것.
- 기본키에 대해서는 항상 DBMS가 내부적으로 정렬된 목록을 관리하기에 특정 행을 가져올 때 빠르게 처리된다. 하지만, 다른 열의 내용을 검색하거나 정렬시에는 하나하나 대조를 해보기 때문에 시간이 오래걸린다. (이를 인덱스로 정의해두면 검색속도가 향상된다.)
- 단점: 인덱스를 사용하면 데이터를 가져오는 작업의 성능은 향상시킬 수 있지만 데이터 삽입, 변경 등이 일어날 때 매번 인덱스가 변경되기 때문에 성능이 떨어질 수 있다.
- 사용대상 : 데이터 필터링과 정렬에 사용되므로, 데이터를 특정한 순서로 자주 정렬한다면 인덱스를 사용하기에 적합

2. **인덱스 생성시 고려할 사항**

- 테이블의 전체 데이터 중 적은 양을 조회할 때 사용한다.

- 테이블에 데이터가 적을수록 인덱스의 효율은 떨어진다.

- 데이터의 유일성이 높을수록, 데이터의 범위가 넓을수록 인덱스의 효율은 올라간다.

- NULL이 적은 컬럼이 인덱스 효율이 좋다.

- 결합 인덱스의 경우 자주 사용되는 컬럼을 앞쪽에 배치한다.

3. **뷰에 대해 설명하시오.**

사용자에게 접근이 허용된 자료만을 제한적으로 보여주기 위해 하나 이상의 기본테이블로부터 유도된 가상테이블

4. **Synonym (동의어)**

- 테이블에 대한 일종의 별명. Alias와 기능이 비슷함

- 다른 스키마에 있어 접근이 번거로울 때(DB인스턴스명을 테이블명에 붙여야한다던가 등) 사용하여 간편화함



### 셋째마당_14: 제약조건

1. **기본키(Primary Key)와 유일키(Unique Key)의 차이점은 무엇입니까?**

 기본키는 널을 허용하지 않지만 유일키는 모든 컬럼 중 유일하게 하나에 대한 NULL을 허용합니다. 그래서 unique키는 개체하나하나를 구분할 기본키가 될 수 없다.
