# Oracle면접 스터디 4주차

- Oracle DB 관리자 계정
- SCOTT 계정 생성

---

### Oracle DB 관리자 계정

**1. SYS**

- Oracle DB 관리자, Super User.

- data dictionary를 갖고 있음.

- default password : change_on_install ( 8i 이전 ver. )

- **DB 생성 및 삭제 가능**

**2. SYSTEM**

- 권한은 SYS와 동일하지만 **DB를 생성할 권한이 없음**.

- default password : manager ( 8i 이전 ver. )

**3. SCOTT**

- Oracle에서 제공하는 샘플 사용자 계정

- default password : tiger

**4. HR**

- Oracle에서 제공하는 샘플 사용자 계정



### SCOTT 계정 생성

 명령 프롬프트(cmd)를 실행하고 다음을 입력

```sql
-- SQLPLUS 접속
> sqlplus
Enter user-name: system
Enter password: 설치할 때 지정한 sys와 system 비밀번호
-- 연결됨
Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production
SQL>
```

```sql
-- SCOTT 계정 생성 파일을 실행
SQL> @C:\oraclexe\app\oracle\product\11.2.0\server\rdbms\admin\scott.sql
-- 에러없이 커서가 떨어지면 실행 성공
SQL> 
```

```sql
--접속 사용자 확인
SQL> show user
USER is "SCOTT"
SQL>
```

```sql
-- 비밀번호 변경
SQL> alter user scott identified by tiger;
User altered.
SQL>
```



### SQL Developer에 사용자 생성

1. sys 사용자 생성
   sys 사용자에게 db 생성권한이 있으므로 sys 사용자를 생성하고 다른 사용자를 만들어 권한을 부여한다.
   ![a](https://user-images.githubusercontent.com/71415474/110724380-030fcf00-8259-11eb-9344-5eb1b5fd7ff2.PNG)

2. 사용자 생성 및 권한 부여
   SQL developer나 SQLPLUS에서 아래 작업 수행

   ```SQL
   -- 사용자 생성
   CREATE USER OSHUSER IDENTIFIED BY 111111;
   -- 사용자에게 CONNECT, RESOURCE 롤 부여
   GRANT CONNECT, RESOURCE TO OSHUSER;
   -- 사용자에게 뷰 생성 권한 부여
   GRANT CREATE VIEW TO OSHUSER; 
   ```

3. 사용자 생성
   생성한 사용자의 이름과 비밀번호를 입력하고 롤을 기본값으로 하여 사용자를 생성
   ![b](https://user-images.githubusercontent.com/71415474/110728117-cf847300-825f-11eb-9d81-26e3cfa488a1.PNG)

   ※ 비밀번호 찾기
   SQLPLUS에서 SYS나 SYSTEM, 다른 사용자들의 비밀번호를 변경하는 방법이다. 비밀번호를 찾는 방법은 없고, SYS사용자로 들어가 비밀번호를 변경시킨다.

   ```sql
   -- sqlplus 접속
   > sqlplus
   Enter user-name: sys as sysdba
   Enter password: 그냥 엔터
   -- 접속 완료
   Connected to:
   Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production
   
   -- 비밀번호 변경
   SQL> ALTER USER SYS IDENTIFIED BY 111111;
   User altered. 
   ```

   <img src="https://user-images.githubusercontent.com/71415474/110728751-ebd4df80-8260-11eb-91da-2255927c2ed7.PNG" alt="c" style="zoom: 67%;" />



---

### Reference

- Oracle DB 관리자 계정: https://rwen.tistory.com/entry/Oracle-DB-%EA%B4%80%EB%A6%AC%EC%9E%90-%EA%B3%84%EC%A0%95-sys-system%EC%9D%98-%EC%B0%A8%EC%9D%B4