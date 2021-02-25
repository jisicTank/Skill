# Oracle 면접 스터디 2주차

## 강의순서

1. 면접 질문 소개
2. 각 면접 질문 영역 개념 설명
3. 면접질문 풀기



## 1. 면접 질문 소개

### 둘째마당_09: SQL문 속 또 다른 SQL문, 서브쿼리

1. **인라인뷰, 서브쿼리, 스칼라서브쿼리 이런게 뭔지 아시나요?**
2. **아신다면 각각의 차이점에 대해서 말씀해 주세요.**

### 둘째마당_10: 데이터를 추가, 수정, 삭제하는 데이터 조작어

1. **Insert문은 무엇입니까?**

2. **데이터베이스에서 레코드는 어떻게 삭제합니까?**

3. **다음 테이블을 참고하여 질문에 해당하는 SQL문을 작성하라.**

   | 이름(name) | 학번(num) | 폰번호(pnum)  | 주소(address) | 이메일(email) | 성별(sex) |
   | ---------- | --------- | ------------- | ------------- | ------------- | --------- |
   | 홍길동     | 10        | 010-1111-1111 | 서울시        | hong@com      | 남        |
   | 민수       | 11        | 010-2222-2222 | 경기도        | m@com         | 남        |
   | 유관순     | 12        | 010-3333-3333 | 경상도        | yu@com        | 여        |

   

   **3-1. 테이블 생성 - 테이블 명은 'student'로 할 것**

   **3-2. 테이블 수정 - 대학교(university)를 추가하고 null 값을 허용해라**

   

   **3-3. 데이터 삽입 - 임의의 데이터 2개를 추가하라.**

   **3-4. 데이터 수정 - 홍길동의 핸드폰 번호를 010-5555-5555로 변경**

   **3-5. 데이터 검색**

   - - 전체 자료 조회 : 
     - 학번이 3번보다 이상인 사람들의 이름과 학번을 조회 : 
     - 김자로 시작하는 학생의 이름을 조회 : 

   **3-6. 데이터 삭제**

   - - 모든 자료(행) :
     - 특정 자료(행) :

### 둘째마당_11

1. **DB Transaction(트랜잭션) 이란?**
2. **DB에서의 Commit과 Rollback이란?**
### 둘째마당_12

1. **테이블을 드롭(DROP)하는 것과 자르는 것(Truncate), 그리고 테이블 내 모든 레코드를 삭제(Delete)하는 것의 차이점은 무엇입니까?**



## 2. 각 면접 질문 영역 개념 설명

### 둘째마당_09: SQL문 속 또 다른 SQL문, 서브쿼리

1. 서브쿼리란?
   SQL문을 실행하는 데 필요한 데이터를 추가로 조회하기 위해 SQL문 내부에서 사용하는 SELECT문.

   ```SQL
   -- 사원이름이 JONES인 사원의 급여
   SELECT SAL FROM EMP WHERE ENAME = 'JONES';
   -- 급여가 2900보다 높은 사원
   SELECT * FROM EMP WHERE SAL > 2900;
   -- JONES의 급여보다 높은 급여를 받는 사원
   SELECT * FROM EMP WHERE SAL > (SELECT SAL FROM EMP WHERE ENAME = 'JONES');
   ```

2.  서브쿼리의 특징

   - 대부분의 서브쿼리에서는 ORDER BY절을 사용할 수 없다.
   - 서브쿼리의 SELECT절에 명시한 열은 메인쿼리의 비교 대상과 같은 자료형과 같은 개수로 지정해야한다.

   

3. 단일행 서브쿼리
   실행 결과가 단 하나의 행으로 나오는 서브쿼리. 단일행 연산자를 사용하여 비교

   ```SQL
   SELECT E.EMPNO, E.ENAME, E.JOB, E.SAL, D.DEPTNO, D.DNAME, D.LOC
   FROM EMP E, DEPT D
   WHERE E.DEPTNO = D.DEPTNO
   AND E.DEPTNO = 20
   AND E.SAL > (SELECT AVG(SAL) FROM EMP);
   ```

   ![image-20210226020639670](C:\Users\oh12s\Desktop\TIL\Coding Test\md-image\image-20210226020639670.png)

5. 다중행 서브쿼리
   실행 결과 행이 여러 개로 나오는 서브쿼리

   ```SQL
   SELECT * FROM EMP WHERE SAL IN (SELECT MAX(SAL) FROM EMP GROUP BY DEPTNO);
   SELECT * FROM EMP WHERE SAL = ANY(SELECT MAX(SAL) FROM EMP GROUP BY DEPTNO);
   SELECT * FROM EMP WHERE SAL < ALL(SELECT SAL FROM EMP WHERE DEPTNO =30);
   SELECT * FROM EMP WHERE EXISTS (SELECT DNAME FROM DEPT WHERE DEPTNO = 10);
   ```

   ![image-20210226020319096](C:\Users\oh12s\Desktop\TIL\Coding Test\md-image\image-20210226020319096.png)

6. 인라인 뷰(Inline view)
   FROM절에서 사용하는 서브쿼리. 일부 데이터를 먼저 추출해 온 후 별칭을 주고 테이블로 하여 사용한다.

   ```SQL
   SELECT E10.EMPNO, E10.ENAME, E10.DEPTNO, D.DNAME, D.LOC
   FROM (SELECT * FROM EMP WHERE DEPTNO = 10) E10,
   	(SELECT * FROM DEPT) D
   WHERE E10.DEPTNO = D.DEPTNO;
   ```

   - 테이블 내 데이터 규모가 너무 크거나 현재 작업에 불필요한 열이 너무 많아 일부 행과 열만 사용하고자 할 때 유용. 

   - 인라인 뷰를 너무 많이 지정하면 가독성이나 성능이 떨어질 수 있음
     -> WITH절을 이용. WITH절은 메인쿼리가 될 SELECT문 안에서 사용할 서브쿼리와 별칭을 먼저 지정한 후 메인쿼리에서 실행

     ```SQL
     WITH
     E10 AS (SELECT * FROM EMP WHERE DEPTNO = 10),
     D AS (SELECT * FROM DEPT)
     SELECT E10.EMPNO, E10.ENAME, E10.DEPTNO, D.DNAME, D.LOC
     FROM E10, D
     WHERE E10.DEPTNO = D.DEPTNO;
     ```

     

7. 스칼라 서브쿼리(scalar subquery)
   SELECT절에서 사용하는 서브쿼리. SELECT절에 하나의 열 영역으로서 결과를 출력

   ```SQL
   SELECT EMPNO, ENAME, JOB, SAL,
   (SELECT GRADE FROM SALGRADE WHERE E.SAL BETWEEN LOSAL AND HISAL) AS SALGRADE,
   DEPTNO,
   (SELECT DNAME FROM DEPT WHERE E.DEPTNO = DEPT.DEPTNO) AS DNAME
   FROM EMP E;
   ```

   - SELECT절에 명시하는 서브쿼리는 반드시 하나의 결과만 반환하도록 작성

   

### 둘째마당_10: 데이터를 추가, 수정, 삭제하는 데이터 조작어

SELECT문으로 조회한 테이블에 데이터를 추가, 변경, 삭제할 때 사용하는 명령어

1. INSERT
   데이터를 새로 추가.

   ```SQL
   CREATE TABLE DEPT_TEMP AS SELECT * FROM DEPT;
   INSERT INTO DEPT_TEMP (DEPTNO, DNAME, LOC) VALUES (50, 'DATABASE', 'SEOUL');
   SELECT * FROM DEPT_TEMP;
   ```

   - INSERT문에 오류가 발생했을 때

     - 데이터 수가 불일치
     - 자료형이 불일치
     - 열길이를 초과하는 데이터를 지정

   - 서브쿼리를 사용하여 여러 데이터 추가

     ```SQL
     CREATE TABLE EMP_TEMP AS SELECT * FROM EMP;
     
     INSERT INTO EMP_TEMP(EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
     SELECT E.EMPNO, E.ENAME, E.JOB, E.MGR, E.HIREDATE, E.SAL, E.COMM, E.DEPTNO
     FROM EMP E, SALGRADE S
     WHERE E.SAL BETWEEN S.LOSAL AND S.HISAL
     AND S.GRADE = 1;
     
     SELECT * FROM EMP_TEMP;
     ```

     - VALUES절은 사용하지 않음
     - 데이터가 추가되는 테이블의 열 개수와 서브쿼리의 열 개수가 일치
     - 데이터가 추가되는 테이블의 자료형과 서브쿼리의 자료형이 일치

2. UPDATE
   테이블에 저장된 데이터를 수정 또는 변경

   ```SQL
   CREATE TABLE DEPT_TEMP2 AS SELECT * FROM DEPT;
   UPDATE DEPT_TEMP2 SET LOC = 'SEOUL';
   SELECT * FROM DEPT_TEMP2;
   ```

   - 수정한 내용을 되돌리고 싶을때는?

     ```SQL
     ROLLBACK;
     ```

3. DELETE
   테이블에 있는 데이터 삭제

   ```SQL
   CREATE TABLE EMP_TEMP2 AS SELECT * FROM EMP;
   DELETE FROM EMP_TEMP2 WHERE JOB = 'MANAGER';
   SELECT * FROM EMP_TEMP2;
   ```

   

### 둘째마당_11: 트랜잭션 제어와 세션

1. 트랜잭션(Transaction)
   더 이상 분할할 수 없는 최소 수행 단위. 
   - 한 개 이상의 DML로 작업을 수행
   - 여러 명령어를 한 번에 수행하여 작업을 완료하거나 모두 수행하지 않는다(모든 작업을 취소).
   - 트랜잭션을 제어하기 위해 TCL(Transaction Control Language)을 사용
2. TCL(Transaction Control Language)
   - ROLLBACK: 모든 작업의 수행을 취소. 트랜잭션에 포함된 DML의 수행을 모두 취소
   - COMMIT: 지금까지 수행한 트랜잭션 명령어를 데이터베이스에 영구히 반영. COMMIT하면 ROLLBACK 불가능.

### 둘째마당_12: 데이터정의어

데이터베이스 데이터를 보관하고 관리하기 위해 제공되는 여러 객체(object)의 생성, 변경, 삭제 관련 기능을 수행

- DDL을 실행하면 자동으로 COMMIT됨. 즉, ROLLBACK을 통한 실행 취소가 불가 (실무에서 주의!)

1. CREATE
   테이블을 생성한다.

   ```SQL
   CREATE TABLE EMP_DDL(
   EMPNO NUMBER(4),
   ENAME VARCHAR2(10),
   JOB VARCHAR2(9),
   MGR NUMBER(4),
   HIREDATE DATE,
   SAL NUMBER(7,2),
   COMM NUMBER(7,2),
   DEPTNO NUMBER(2)
   );
   
   -- 기존 테이블을 복사하여 새 테이블 생성
   CREATE TABLE DEPT_DDL AS SELECT * FROM DEPT;
   
   -- 열 구조만 복사하여 새 테이블 생성
   CREATE TABLE EMPDEPT_DDL
   AS SELECT E.EMPNO, E.ENAME, E.JOB, E.MGR, E.HIREDATE, E.SAL, E.COMM, D.DEPTNO, D.DNAME, D.LOC
   FROM EMP E, DEPT D
   WHERE 1 <> 1;
   ```

   - 테이블 이름/열 이름 생성 규칙
     - 문자로 시작. 한글도 가능
     - 테이블 이름/열 이름은 30byte 이하 (영어 30자, 한글 15자)
     - 테이블 이름/열 이름은 중복 불가
     - 영문자(한글 가능), 숫자 0~9, 특수문자 `$`, `#`,` _` 사용 가능
     - "SELECT"나 "FROM" 같은 SQL 키워드는 테이블 이름/열 이름 불가

2. ALTER
   이미 생성된 오라클 데이터베이스 객체를 변경할 때 사용

   ```SQL
   CREATE TABLE EMP_ALTER AS SELECT * FROM EMP;
   --ADD
   ALTER TABLE EMP_ALTER ADD HP VARCHAR2(20);
   --RENAME
   ALTER TABLE EMP_ALTER RENAME COLUMN HP TO TEL;
   --MODIFY
   ALTER TABLE EMP_ALTER MODIFY EMPNO NUMBER(5);
   --DROP
   ALTER TABLE EMP_ALTER DROP COLUMN TEL;
   ```

3. RENAME
   테이블 이름을 변경

   ```SQL
   RENAME EMP_ALTER TO EMP_RENAME;
   ```

4. TRUNCATE
   특정 테이블의 모든 데이터를 삭제

   ```SQL
   TRUNCATE TABLE EMP_RENAME;
   ```

   - 유의점
     DML에서 WHERE절을 쓰지 않은 DELETE문으로도 수행가능한 작업이다. 그러나, TRUNCATE는 DDL이기 때문에, 실행하면 바로 COMMIT이 된다. ROLLBACK이 되지 않는다는 점에서 이 둘은 차이점을 갖는다.

5. DROP
   데이터베이스 객체를 삭제

   ```sql
   DROP TABLE EMP_RENAME;
   ```



## 면접질문 풀기

### 둘째마당_09: SQL문 속 또 다른 SQL문, 서브쿼리

1. **인라인뷰, 서브쿼리, 스칼라서브쿼리 이런게 뭔지 아시나요? 아신다면 각각의 차이점에 대해서 말씀해 주세요.**
   - 서브쿼리: WHERE절에 사용하는 SELECT문. 하나의 변수(상수)처럼 사용
   - 인라인뷰: FROM절에 사용하는 SELECT문. 하나의 테이블처럼 사용
   - 스칼라서브쿼리: SELECT절에 사용하는 SELECT문. 하나의 컬럼처럼 사용

### 둘째마당_10: 데이터를 추가, 수정, 삭제하는 데이터 조작어

1. **Insert문은 무엇입니까?**

   데이터베이스에 정보를 삽입하는 문입니다.

2. **데이터베이스에서 레코드는 어떻게 삭제합니까?**
   DELETE문은 데이터베이스에서 레코드 또는 특정 컬럼의 값을 삭제합니다.

3. **다음 테이블을 참고하여 질문에 해당하는 SQL문을 작성하라.**

   | 이름(name) | 학번(num) | 폰번호(pnum)  | 주소(address) | 이메일(email) | 성별(sex) |
   | ---------- | --------- | ------------- | ------------- | ------------- | --------- |
   | 홍길동     | 10        | 010-1111-1111 | 서울시        | hong@com      | 남        |
   | 민수       | 11        | 010-2222-2222 | 경기도        | m@com         | 남        |
   | 유관순     | 12        | 010-3333-3333 | 경상도        | yu@com        | 여        |

   

   **3-1. 테이블 생성 - 테이블 명은 'student'로 할 것**

   create table student ( name varchar(10) not null, num int not null, pnum int not null, address varchar(10) not null, email varchar(10) not null, sex varchar(2) not null, primary key(num) );

   **3-2. 테이블 수정 - 대학교(university)를 추가하고 null 값을 허용해라**

   alter table student add university varchar(10) null;

   **3-3. 데이터 삽입 - 임의의 데이터 2개를 추가하라.**

   - insert into student(name, num, pnum, address, email, sex) value('김사또', 11, 01022222222, '경기도', 'kim@com', '남');
   - insert into student(name, num, pnum, address, email, sex) value('강민수', 13, 01077777777, '서울', 'kang@com', '남');

   **3-4. 데이터 수정 - 홍길동의 핸드폰 번호를 010-5555-5555로 변경**

   update student set pnum = 010-5555-5555 where name = '홍길동';

   **3-5. 데이터 검색**

   - - 전체 자료 조회 : select * from student;
     - 학번이 3번보다 이상인 사람들의 이름과 학번을 조회 : select name, num from student where = num >= 3 order by num desc;
     - 김자로 시작하는 학생의 이름을 조회 : select name from student where name like '김%'; 

   **3-6. 데이터 삭제**

   - - 모든 자료(행) : delete from student;
     - 특정 자료(행) : delete from student where name = '홍길동';

### 둘째마당_11

1. **DB Transaction(트랜잭션) 이란?**

- 데이터의 무결성으로 인하여 데이터 작업시에 문제가 생기면, 데이터 작업을 하기 이전 시점으로 모든 데이터를 원상 복구 하는 것을 말한다.
- 즉, 모두 실행되거나 모두 실행되지 않거나를 뜻한다.

2. **DB에서의 Commit과 Rollback이란?**

- Commit : 작성한 쿼리문에서 Update, Delete, Insert를 수행했을 때, 그 쿼리문 수행결과에 대해 확정을 짓겠다는 뜻이다.
- Rollback : 쿼리문 수행결과에 대해 번복을 함. 즉, 쿼리문 수행 이전으로 원상복귀 하겠다는 뜻이다 (Commit 하기 전에 사용 됨).

### 둘째마당_12

1. **테이블을 드롭(DROP)하는 것과 자르는 것(Truncate), 그리고 테이블 내 모든 레코드를 삭제(Delete)하는 것의 차이점은 무엇입니까?**

- DELETE TABLE은 로그되는 작업이기 때문에 삭제되는 각 행은 트랜잭션 로그에 기록되고 이것은 작업을 느리게 합니다. TRUCATE TABLE 역시 테이블 내 행들을 삭제하지만 삭제되는 각 행을 기록하지 않고 대신 테이블의 데이터베이스 할당 해제를 기록하여 작업이 빠릅니다. TRUNCATE TABLE는 롤백할 수 없습니다.

- DELETE 명령어는 데이터는 지워지지만 테이블 용량은 줄어들지 않는다. 원하는 데이터만 지울 수 있다. 삭제 후 RollBack 가능하다.

- TRUNCATE 명령어는 용량이 줄어들고, 인덱스 등도 모두 삭제된다. 테이블은 삭제하지는 않고 데이터만 삭제한다. 한꺼번에 다 지워야 한다. 삭제후 절대 되돌릴 수 없다.

- DROP 명령어는 테이블 전체를 삭제,공간, 객체를 삭제한다. 삭제 후 절대 되돌릴 수 없다