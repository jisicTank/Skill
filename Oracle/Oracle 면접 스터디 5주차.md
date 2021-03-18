# Oracle 면접 스터디 4주차

### 셋째마당_15: 사용자, 권한, 롤 관리

1. **롤(Role)**

### 넷째마당_19: 저장 서브프로그램

1. **트리거란?**
2. **프로시저란?**
3. **트리거 vs 프로시저**



### 셋째마당_15: 사용자, 권한, 롤 관리

1. 사용자
   데이터베이스에 접속하여 데이터를 관리하는 계정

   - SCOTT 계정은 대부분 비밀번호까지 알고 있는 계정이기 때문에 주요 데이터를 보관하고 관리하기에는 보완 위험이 있다.
   - 즉, 사용자는 SCOTT계정 외에 오라클 데이터베이스에 접속할 수 있는 새로운 계정 또는 개체.
   - 데이터를 활용한 서비스 규모가 크거나, 작은 규모의 여러 서비스를 통합한 방식 등 실무에서 사용하는 여러 종류의 서비스는 한 사용자가 관리하기에는 데이터 분량이 너무 방대하고 구조가 복잡하다. 따라서 업무 분할과 효율, 보안을 고려하여 업무에 따라 여러 사용자들을 나눈다. 

2. 데이터베이스 스키마
   데이터 간 관계, 데이터 구조, 제약 조건 등 데이터를 저장 및 관리하기 위해 정의한 데이터베이스 구조의 범위를 스키마(schema)를 통해 그룹으로 분류. 즉 DB에 접속한 사용자와 연결된 객체를 의미.

   - SCOTT -> 사용자
   - SCOTT이 사용한 테이블, 뷰, 제약조건, 인덱스, 시퀀스, 동의어, ... -> SCOTT의 스키마
   
3. 사용자 실습

   ```SQL
   -- 사용자 생성 (SYSTEM 계정에서 가능)
   CREATE USER ORCLSTUDY IDENTIFIED BY oracle; -- 패스워드 대문자 조심!!!
   
   -- 사용자 권한 부여
   GRANT CREATE SESSION TO ORCLSTUDY;
   
   -- 사용자 정보(패스워드) 변경하기 (패스워드 대문자 조심!!!)
   ALTER USER ORCLSTUDY IDENTIFIED BY orcl;
   
   -- 사용자 정보 조회
   SELECT * FROM ALL_USERS;
   SELECT * FROM DBA_USERS;
   SELECT * FROM DBA_OBJECTS;
   
   -- 사용자 삭제
   DROP USER ORCLSTUDY;
   -- 사용자와 객체 모두 삭제
   DROP USER ORCLSTUDY CASCADE;
   ```

   

4. 시스템 권한(System privilege)
   시스템 권한은 사용자 생성과 정보 수정 및 삭제, 데이터베이스 접근, 오라클 데이터베이스의 여러 자원과 객체 생성 및 관리 등의 권한을 포함함.

   <img src="https://user-images.githubusercontent.com/71415474/111593668-873ff480-880d-11eb-9e60-1f8c77bd46cf.jpg" alt="KakaoTalk_20210318_171413303" style="zoom: 50%;" />

   5. 권한 실습

      ```sql
      -- 사용자 생성(SYSTEM 계정으로 가능)
      CREATE USER ORCLSTUDY IDENTIFIED BY oracle;
      
      --CONNECT, RESOURCE, UNLIMITED TABLESPACE 권한을 ORCLSTUDY에게 부여
      GRANT RESOURCE, CREATE SESSION, CREATE TABLE TO ORCLSTUDY;
      
      -- 권한 취소
      REVOKE RESOURCE, CREATE TABLE FROM ORCLSTUDY;
      
      -------------------------------------------------------------------------------
      --SCOTT 계정이 ORCLSTUDY 사용자에게 TEMP 테이블 권한 부여하기
      --CONN SCOTT/tiger
      CREATE TABLE TEMP(
          COL1 VARCHAR(20),
          COL2 VARCHAR(20)
      );
      
      GRANT SELECT ON TEMP TO ORCLSTUDY;
      GRANT INSERT ON TEMP TO ORCLSTUDY;
      
      -- 여러 권한 부여
      GRANT SELECT, INSERT ON TEMP TO ORCLSTUDY;
      
      --ORCLSTUDY 계정에 가서 SELECT, INSERT 테스트
      -- 권한을 받았다면 실행될 것이고, 안 받았거나 취소되었다면 에러문
      --CONN ORCLSTUDY/oracle
      SELECT * FROM SCOTT.TEMP;
      INSERT INTO SCOTT.TEMP VALUES('TEXT', 'FROM ORCLSTUDY');
      SELECT * FROM SCOTT.TEMP;
      
      -- ORCLSTUDY에 부여된 TEMP 테이블 사용 권한 취소
      --: SCOTT계정이 ORCLSTUDY계정에게 권한을 부여했으니 취소도 SCOTT계정해서 함
      REVOKE SELECT, INSERT ON TEMP FROM ORCLSTUDY;
      
      ```

      

   6. 롤(Role)
      여러 종류의 권한을 묶어 놓은 그룹. 롤을 사용하면 여러 권한을 한 번에 부여하고 해제할 수 있어 권한 관리 효율을 높일 수 있다.

      (1) 사전 정의된 롤

      - CONNECT 롤: 10g 버전부터 CREATE SESSION 밖에 없음
      - RESOURCE 롤: CREATE TRIGGER, CREATE SEQUENCE, CREATE TYPE, CREATE PROCEDURE, CREATE CLUSTER, CREATE OPERATOR, CREATE INDEXTYPE, CREATE TABLE

      ** CONNECT 롤에서 CREATE VIEW, CREATE SYNONYM 권한이 제외되었기 때문에 따로 권한 부여를 해주어야함

      - DBA 롤: 데이터베이스를 관리하는 시스템 권한 대부분을 가지고 있다.

      (2) 사용자 정의 롤: 필요에 의해 직접 권한을 포함 시킨 롤.

      ```SQL
      --SYSTEM 계정으로 ROLESTUDY 롤 생성 및 권한 부여하기
      -- CONN SYSTEM/ORACLE
      CREATE ROLE ROLESTUDY;
      
      GRANT CONNECT, RESOURCE, CREATE VIEW, CREATE SYNONYM TO ROLESTUDY;
      
      GRANT ROLESTUDY TO ORCLSTUDY;
      
      --ORCLSTUDY에 부여된 롤과 권한 확인하기
      --CONN ORCLSTUDY/ORACLE
      SELECT * FROM USER_SYS_PRIVS;
      SELECT * FROM USER_ROLE_PRIVS;
      
      -- 부여된 롤 취소
      -- CONN SYSTEM/ORACLE
      REVOKE ROLESTUDY FROM ORCLSTUDY;
      
      -- 롤 삭제
      DROP ROLE ROLESTUDY;
      ```

   

### 넷째마당_19: 저장 서브프로그램

1. 저장 서브프로그램
   여러번 사용할 목적으로 이름을 지정하여 오라클에 저장해두는 PL/SQL프로그램

   - PL/SQL ?
     SQL만으로는 구현이 어렵거나 구현 불가능한 작업을 수행하기 위해 오라클에서 제공하는 프로그래밍 언어

     - PL/SQL 프로그램의 기본단위를 블록(block)이라 하며 기본형식은 다음과 같다.

       ```sql
       DECLARE
       	[실행에 필요한 여러 요소 선언]
       BEGIN
       	[작업을 위해 실제 실행하는 명령어]
       EXCEPTION
       	[PL/SQL수행 도중 발생하는 오류 처리]
       END;
       ```

     - 예시

       ```SQL
       -- 기본 출력
       SET SERVEROUTPUT ON;
       BEGIN
       DBMS_OUTPUT.PUT_LINE('Hello, PL/SQL!');
       END;
       /
       --변수와 상수
       DECLARE
       V_EMPNO NUMBER(4) := 7788;
       V_ENAME VARCHAR2(10);
       BEGIN
       V_ENAME := 'SCOTT';
       DBMS_OUTPUT.PUT_LINE('V_EMPNO: ' || V_EMPNO);
       DBMS_OUTPUT.PUT_LINE('V_ENAME: ' || V_ENAME);
       END;
       /
       -- 상수 정의하기
       DECLARE
       V_TAX CONSTANT NUMBER(1) :=3;
       BEGIN
       DBMS_OUTPUT.PUT_LINE('V_TAX: ' || V_TAX);
       END;
       /
       -- 변수의 기본값 지정하기
       DECLARE
       V_DEPTNO NUMBER(2) DEFAULT 10;
       BEGIN
       DBMS_OUTPUT.PUT_LINE('V_DEPTNO : ' || V_DEPTNO);
       END;
/
       -- 변수에 NULL 값 저장 막기
    DECLARE
       V_DEPTNO NUMBER(2) NOT NULL := 10;
       BEGIN
       DBMS_OUTPUT.PUT_LINE('V_DEPTNO: ' || V_DEPTNO);
       END;
       /
       -- 변수에 NOT NULL 및 기본값을 설정하고 출력
       DECLARE
       V_DEPTNO NUMBER(2) NOT NULL DEFAULT 10;
       BEGIN
       DBMS_OUTPUT.PUT_LINE('V_DEPTNO: ' || V_DEPTNO);
       END;
       /
       -- 참조형
       SELECT * FROM DEPT;
       SET SERVEROUTPUT ON;
       DECLARE
       V_DEPTNO DEPT.DEPTNO%TYPE := 50;
       BEGIN
       DBMS_OUTPUT.PUT_LINE('V_DEPTNO: ' || V_DEPTNO);
       END;
       /
       select * from dept;
       
       ```
       
       
   
2. 프로시저
   특정 처리 작업을 수행하는데 사용하는 저장프로그램

   - 자주 사용하는 SQL을 프로시저로 만든 뒤 필요할 때마다 호출하고 사용. 작업효율 증가

   - 프로시저 실습

     ```SQL
     -- 프로시저 생성하기
     CREATE OR REPLACE PROCEDURE pro_noparam
     IS
         V_EMPNO NUMBER(4) := 7788;
         V_ENAME VARCHAR2(10);
     BEGIN
         V_ENAME := 'SCOTT';
         DBMS_OUTPUT.PUT_LINE('V_EMPNO: ' || V_EMPNO);
         DBMS_OUTPUT.PUT_LINE('V_ENAME: ' || V_ENAME);
     END;
     /
     
     -- 실행방법 1: 생성한 프로시저 실행하기
     SET SERVEROUTPUT ON;
     EXECUTE pro_noparam;
     
  -- 실행방법 2: 익명 블록에서 프로시저 실행
     BEGIN
      pro_noparam;
     END;
     /
     
     -- USER_SOURCE를 통해 프로시저 확인
     SELECT * FROM USER_SOURCE WHERE NAME = 'PRO_NOPARAM';
     
     -- 프로시저 삭제
     DROP PROCEDURE PRO_NOPARAM;
     
     -- IN 모드 파라미터
     CREATE OR REPLACE PROCEDURE pro_param_in
     (
         param1 IN NUMBER,
         param2 NUMBER,
         param3 NUMBER := 3,
         param4 NUMBER DEFAULT 4
     )
     IS
     BEGIN
         DBMS_OUTPUT.PUT_LINE('param1 : ' || param1);
         DBMS_OUTPUT.PUT_LINE('param2 : ' || param2);
         DBMS_OUTPUT.PUT_LINE('param3 : ' || param3);
         DBMS_OUTPUT.PUT_LINE('param4 : ' || param4);
     END;
     /
     
     EXECUTE pro_param_in(1,2,9,8);
     EXECUTE pro_param_in(1,2);
     EXECUTE pro_param_in(1);
     EXECUTE pro_param_in(param1 => 10, param2 => 20);
     
     -- OUT 모드 
     --파라미터 정의
     CREATE OR REPLACE PROCEDURE pro_param_out
     (
         in_empno IN EMP.EMPNO%TYPE,
         out_ename OUT EMP.ENAME%TYPE,
         out_sal OUT EMP.SAL%TYPE
     )
     IS
     
     BEGIN
         SELECT ENAME, SAL INTO out_ename, out_sal
             FROM EMP
             WHERE EMPNO = in_empno;
         END pro_param_out;
     /
     
     -- 파라미터 사용
     DECLARE
         v_ename EMP.ENAME%TYPE;
         v_sal EMP.SAL%TYPE;
     BEGIN
         pro_param_out(7788, v_ename, v_sal);
         DBMS_OUTPUT.PUT_LINE('ENAME : ' || v_ename);
         DBMS_OUTPUT.PUT_LINE('SAL : ' || v_sal);
     END;
     /
     
     -- IN OUT 모드 파라미터
     -- 파라미터 정의
     CREATE OR REPLACE PROCEDURE pro_param_inout
     (
         inout_no IN OUT NUMBER
     )
     IS
     BEGIN
         inout_no := inout_no * 2;
     END pro_param_inout;
     /
     -- 파라미터 사용
     DECLARE
         no NUMBER;
     BEGIN
         no := 5;
         pro_param_inout(no);
         DBMS_OUTPUT.PUT_LINE('no : ' || no);
     END;
     /
     
     -- 에러 확인
     SHOW ERRORS;    -- 가장 최근에 생성되거나 변경된 서브프로그램의 오류정보를 출력
     ```
   

3. 트리거
   데이터베이스 안의 특정 상황이나 동작, 즉 이벤트가 발생할 경우에 자동으로 실행되는 기능을 정의하는 서브프로그램

   - 트리거 연관 데이터 작업
     - 어떤 테이블의 데이터를 특정 사용자가 변경하려 할 때 해당 데이터나 사용자 기록을 확인한다든지 상황에 따라 데이터를 변경하지 못하게 막는 것이 가능
     - 오라클 데이터베이스가 가동하거나 종료할 때 데이터베이스 관리자 등 관련 업무자에게 메일을 보내는 기능도 구현
   - 데이터와 관련된 여러 작업을 수행함에 있어 여러 PL/SQL문 또는 서브프로그램을 일일이 실행해야하는 번거로움을 줄임
   - 제약조건만으로 구현이 어렵거나 불가능한 좀 더 복잡한, 수준 높은 데이터 정의가 가능
   - 데이터 변경과 관련된 일련의 정보를 기록. 여러 사용자가 공유하는 데이터 보안성과 안정성 그리고 문제가 발생했을 때 대처 능력을 높일 수 있음
   - 무분별하게 사용하면 데이터베이스 성능을 떨어뜨리는 원인이 되므로 주의
   - 트리거의 종류

   ![20210318_184225](https://user-images.githubusercontent.com/71415474/111605557-beb49e00-8819-11eb-9fef-dac382e1e8cc.png)

4. DML 트리거
   가장 사용 빈도가 높은 트리거. INSERT, UPDATE, DELETE와 같은 명령어를 기점으로 동작.

   ```SQL
   --EMP_TRG 테이블 생성
   CREATE TABLE EMP_TRG AS SELECT * FROM EMP;
   
   -- DML 실행 전에 수행할 트리거 생성
   CREATE OR REPLACE TRIGGER trg_emp_nodml_weekend
   BEFORE
   INSERT OR UPDATE OR DELETE ON EMP_TRG
   BEGIN
      IF TO_CHAR(sysdate, 'DY') IN ('토', '일') THEN
         IF INSERTING THEN
            raise_application_error(-20000, '주말 사원정보 추가 불가');
         ELSIF UPDATING THEN
            raise_application_error(-20001, '주말 사원정보 수정 불가');
         ELSIF DELETING THEN
            raise_application_error(-20002, '주말 사원정보 삭제 불가');
         ELSE
            raise_application_error(-20003, '주말 사원정보 변경 불가');
         END IF;
      END IF;
   END;
   /
   
   -- 평일 날짜로 EMP_TRG 테이블 UPDATE하기
   UPDATE emp_trg SET sal = 3500 WHERE empno = 7788;
   
   -- EMP_TRG_LOG 테이블 생성
   CREATE TABLE EMP_TRG_LOG(
      TABLENAME VARCHAR2(10), -- DML이 수행된 테이블 이름
      DML_TYPE VARCHAR2(10),  -- DML 명령어의 종류
      EMPNO NUMBER(4),        -- DML 대상이 된 사원 번호
      USER_NAME VARCHAR2(30), -- DML을 수행한 USER 이름
      CHANGE_DATE DATE        -- DML이 수행된 날짜
   );
   
   -- DML 실행 후 수행할 트리거 생성
   CREATE OR REPLACE TRIGGER trg_emp_log
   AFTER
   INSERT OR UPDATE OR DELETE ON EMP_TRG
   FOR EACH ROW
   
   BEGIN
   
      IF INSERTING THEN
         INSERT INTO emp_trg_log
         VALUES ('EMP_TRG', 'INSERT', :new.empno,
                  SYS_CONTEXT('USERENV', 'SESSION_USER'), sysdate);
   
      ELSIF UPDATING THEN
         INSERT INTO emp_trg_log
         VALUES ('EMP_TRG', 'UPDATE', :old.empno,
                  SYS_CONTEXT('USERENV', 'SESSION_USER'), sysdate);
   
      ELSIF DELETING THEN
         INSERT INTO emp_trg_log
         VALUES ('EMP_TRG', 'DELETE', :old.empno,
                  SYS_CONTEXT('USERENV', 'SESSION_USER'), sysdate);
      END IF;
   END;
   /
   
   -- EMP_TRG 테이블에 INSERT 실행하기
   INSERT INTO EMP_TRG
   VALUES(9999, 'TestEmp', 'CLERK', 7788,
          TO_DATE('2018-03-03', 'YYYY-MM-DD'), 1200, null, 20);
          
   -- EMP_TRG 테이블에 INSERT 실행(COMMIT하기)
   COMMIT;
   
   -- EMP_TRG 테이블의 INSERT 확인
   SELECT * FROM EMP_TRG;
   
   -- EMP_TRG_LOG 테이블의 INSERT 기록 확인
   SELECT * FROM EMP_TRG_LOG;
   
   -- EMP_TRG 테이블에 UPDATE 실행
   UPDATE EMP_TRG SET SAL = 1300 WHERE MGR = 7788;
   -- UPDATE 실행(COMMIT하기)
   COMMIT;
   
   -- USER_TRIGGERS로 트리거 정보 조회
   SELECT TRIGGER_NAME, TRIGGER_TYPE, TRIGGERING_EVENT, TABLE_NAME, STATUS
     FROM USER_TRIGGERS;
     
   -- 트리거 변경
   ALTER TRIGGER trg_emp_log ENABLE;
   ALTER TRIGGER trg_emp_log DISABLE;
   
   -- 특정 테이블과 관련된 모든 트리거의 상태 활성화
   ALTER TABLE EMP_TRG ENABLE ALL TRIGGERS;
   -- 특정 테이블과 관련된 모든 트리거의 상태 비활성화
   ALTER TABLE EMP_TRG DISABLE ALL TRIGGERS;
   
   --트리거 삭제
   DROP TRIGGER trg_emp_log;
   ```

---

### 셋째마당_15: 사용자, 권한, 롤 관리

1. **롤(Role)**

- 객체에 대해 권한을 생성

- 그룹 및 사용자에 대해 권한을 생성하여 보안과 관리에 용이하게 함

- 롤 관리자는 DBA이다.

### 넷째마당_19: 저장 서브프로그램

1. **트리거란?**

- 생성 후 자동으로 실행
- 트리거 내부에 commit, rollback 불가능

- 작업대상 : 테이블, 뷰, 데이터베이스 작업

- 트리거란 방아쇠로써, 방아쇠를 당기면 총알이 나가는 것과 같은 의미

- 테이블에 트리거를 생성하여 어떠한 이벤트가 발생할 시 그에 대한 작업을 실행

- 작업테이블에 트리거를 생성하여 이벤트 발생시 이력테이블 혹은 통계테이블에 데이터가 저장 및 수정, 삭제가 되도록 만들어 관리할 수 있다.

- 이력테이블, 합계 잔액 등 통계테이블, 동기화 및 테이블 복제 가능

2. **프로시저란?**

- execute 명령어로 실행
- 프로시저 내부에 commit, rollback 가능

- 비절차적 언어인 SQL을 보완하기 위해 제공하는 절차적 언어

- 연속적인 실행 혹은 조건에 따른 분기처리를 통해 특정 기능을 수행할 수 있도록 작성 가능

- 변수 및 상수 선언 가능, IF문 및 LOOP문 등 사용 가능

- 보안(데이터 엑세스에 대해 제한), 생산성 향상, 무결성 일관성 향상

3. **트리거 vs 프로시저**

- 프로시저는 사용자, 애플리케이션, 트리거 등에 의해 명시적으로 실행

- 트리거는 이벤트 발생(DML문 수행)시 DBMS에 의해 암시적으로 실행