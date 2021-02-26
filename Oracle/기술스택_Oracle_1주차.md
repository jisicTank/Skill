# Oracle 면접 스터디 1주차

## 강의 순서

1. 면접 질문 소개
2. 각 면접 질문 영역 개념 설명
3. 면접질문 풀기



## 1. 면접 질문 소개

### 둘째마당_04: SELECT문의 기본 형식

1. **SELECT문은 무엇입니까?**
2. **전체 이름이 아닌 이름의 일부로 값을 비교할 수 있는 방법은 무엇입니까?**
3. **테이블에서 어떻게 중복이 없는(별개) 항목을 얻을 수 있습니까?(distinct)**
4. **어떤 순서로 정렬된 결과를 얻는 방법은 무엇입니까?(order by)**

### 둘째마당_07: 다중행 함수와 데이터 그룹화

1. **테이블의 전체 레코드 수를 어떻게 얻을 수 있습니까?**
2. **GROUP BY는 무엇입니까?**
3. **Group by절을 사용시 일반적으로 사용되는 그룹 함수를 나열하시오.**
4. **HAVING 절에 대해 설명하시오.**
5. **Where 절과 Having절의 다른 점은 무엇입니까?**
6. **쿼리 순서 (ORDER BY, FROM, WHERE, SELECT, GROUP BY)**

### 둘째마당_08: 여러 테이블을 하나의 테이블처럼 사용하는 조인

1. **RDB에서 Join이 무엇인지에 대한 설명과 간단한 샘플 쿼리문을 작성해보아라.**

2.  **Join의 종류에 대해 아시는대로 말씀해주세요**

3.  **NL 조인과 HASH 조인의 차이점과 어떤 부분에 유리한지 말씀해주세요.**





## 각 면접 질문 영역 개념 설명

### 둘째마당_04: SELECT문의 기본 형식

1. **데이터의 조회방법 3가지**
   - 셀렉션:  행 단위로 원하는 데이터를 조회
   - 프로젝션: 열 단위로 원하는 데이터를 조회
   - 조인: 두 개 이상의 테이블을 양 옆에 연결하여 마치 하나의 테이블인 것처럼 데이터를 조회.
     - 실무에서 2개 이상의 데이터를 조인하는 경우를 흔히 볼 수 있음
     - 행과 열로 구성된 다른 '요소'를 활용하거나 같은 테이블을 여러 번 사용하여 SELECT문의 조인에 활용

2. **SELECT**
- DB에 보관되어 있는 데이터를 조회하는 데 사용
   - `SELCET 열 FROM 테이블;` 구성으로 사용
   - `SELECT 열들 FROM 테이블;`처럼 부분 열을 프로젝션할 수 있다.
   
3. **DISTINCT**
- SELECT 문으로 데이터를 조회한 후에 **중복을 제거**한다.
   
- `SELECT DISTINCT 열 FROM 테이블;`
   
- 반대의 개념으로 `ALL`이 있음. **중복을 제거하지 않고 그대로 출력**
     `SELECT ALL 열 FROM 테이블;`
   
4. **AS**
- **별칭 지정**. 테이블에 연산식을 추가할 때 길어지는 열 이름을 짧고 간단하게 함
   - 예시: `SAL*12+COMM AS ANNSAL`. 원래는 표현방법이 3개 더 있으나 이게 보편적.
   
5. **ORDER BY**
- SELECT문을 사용하여 데이터를 조회할 때 **데이터를 정렬해서 출력.**
   - 시간이나 이름 순서 또는 어떤 다른 기준으로 데이터를 정렬해서 출력해야하는 경우 사용
   - `SELECT 열 FROM 테이블 ORDER BY 열 정렬옵션;`
   - 정렬옵션에는 오름차순과 내림차순이 있다. **오름차순이 디폴트이며, 내림차순은
     `SELECT 열 FROM 테이블 ORDER BY 열 DESC;`**
   
- 꼭 필요한 경우가 아니면 사용하지 않는다. **데이터를 특정 기준으로 순서를 맞추는 것은 많은 자원(특히 시간)과 비용을 소모하기 때문.**
      SQL문의 효율이 낮아지는 것은 서비스 응답 시간이 느려진다는 것을 의미.



### 둘째마당_07: 다중행 함수와 데이터 그룹화

1. **다중행 함수**

   |함수|설명|
   |-----|:--|
   |SUM|지정한 데이터의 합 반환|
   |COUNT|지정한 데이터의 개수 반환|
   |MAX|지정한 데이터의 최댓값 반환|
   |MIN|지정한 데이터의 최솟값 반환|
   |AVG|지정한 데이터의 평균관 반환|
   
   - DISTINCT, ALL 과 같이 쓸 수 있다.
     `AVG(DISTINCT SAL)`, ` MAX(ALL SAL)`


2. **GROUP BY**

   - 하나 이상의 열을 기준으로 그룹화하여 결과를 출력한다.
   - `SELECT 다중행함수(열), 열2 FROM 테이블 WHERE 조건식 GROUP BY 열2 ORDER BY 열3`
   - **다중행 함수를 사용하지 않은 일반 열을 GROUP BY절에 명시하지 않으면 SELCET절에서 사용할 수 없다.**
   - GROUP BY 절에는 별칭이 인식되지 않는다.

3. **HAVING**

   - **SELECT문에 GROUP BY절이 존재해야만 사용가능.**

   - **GROUP BY절을 통해 그룹화된 결과 값의 범위를 제한하는데 사용.**

   - `SELECT 다중행함수(열), 열2 FROM 테이블 WHERE 조건식 GROUP BY 열2 HAVING 조건식 ORDER BY 열3`

   - **WHERE vs HAVING**

     - WHERE: 1. 출력 대상 행을 제한

     - HAVING: 그룹화된 대상을 출력에서 제한

     - 따라서 만약 출력 결과를 제한하기 위해 HAVING이 아닌 WHERE를 쓴다면 오류가 발생

       ```SQL
       SELECT DEPTNO, JOB, AVG(SAL)
       FROM EMP
       WHERE AVG(SAL) >= 2000			# 여기가 틀림
       GROUP BY DEPTNO, JOB
       ORDER BY DEPTNO, JOB;
       ```

     - **WHERE절이 GROUP BY, HAVING보다 먼저 실행되어 출력 행을 제한한다. 따라서 WHERE절을 실행한 데이터를 바탕으로 GROUP BY, HAVING절이 실행되어 그륩화된 결과를 출력한다.**

### 둘째마당_08: 여러 테이블을 하나의 테이블처럼 사용하는 조인

1. **조인(Join)**

   - **두 개 이상의 테이블을 연결하여 하나의 테이블처럼 출력할 때 사용하는 방식**

   - FROM절에 두 개 이상의 열을 넣게 되면 데카르트 곱으로 조인되고, 모든 경우의 결과값이 출력됨. 이 경우, 데이터와 데이터가 정확하게 맞아떨어지지 않는 경우도 함께 출력됨.
      조인을 사용한 데이터 출력에서 조합한 데이터 중 정확한 데이터만을 뽑아내기위해 **WHERE절**과 **테이블.열**을 사용함.

   - FROM절에서 `FROM 테이블 별칭`과 같이 테이블 이름과 별칭을 한 칸 띄워 입력하면 별칭이 지정된다.

   - ```SQL
     SELECT *
     FROM EMP E, DEPT D
     WHERE E.DEPTNO = D.DEPTNO		# 조인조건
     ORDER BY EMPNO;
     ```

     

2.  **조인(Join) 종류**

   2-1. 등가조인(Equal Join)

   - 테이블을 연결한 후에 각 테이블의 특정 열 값이 일치한 데이터를 기준으로 출력 결과를 사용하는 방식.

   - 내부조인(Inner Join), 단순 조인(simple Join)이라고도 함

   - '조인을 사용한다'라는 것은 대부분은 등가 조인.
   
   - ```SQL
     SELECT E.EMPNO, E.ENAME, E.SAL, D.DEPTNO, D.DNAME, D.LOC
     FROM EMP E, DEPT D
     WHERE E.DEPTNO = D.DEPTNO		# 조인조건
    AND SAL >= 3000;
     ```
   
- 조인 테이블 수와 조건식 개수의 관계: **`조건식의 최소 개수 = 조인 테이블 수 -1`**
     (테이블이 2개면, 이어주는 WHERE절이 무조건 하나 필요)

   

   2-2. 비등가 조인(Non-equal Join)

   - 등가 조인 방식 외의 방식
   
   - 이 경우, 조인조건이 없기 때문에 데카르트 곱이 발생(데카르트 곱으로 이루어진 조인을 크로스 조인 또는 교차 조인이라고 함.)
   
   - ```sql
    SELECT *
     FROM EMP E, SALGRADE S
    WHERE E.SAL BETWEEN S.LOSAL AND S.HISAL;
     ```
  
     

#####    2-3. 자체 조인(Self join)

   - 하나의 테이블을 여러 개의 테이블처럼 활용하여 조인하는 방식
   
   - FROM절에 같은 테이블을 여러 번 명시하되 테이블의 명칭만 다르게 지정한다.
   
- ```sql
     SELECT E1.EMPNO, E1.ENAME, E1.MGR,
    		E2.EMPNO AS MGR_EMPNO, E2.ENAME AS MGR_ENAME
     		FROM EMP E1, EMP E2
    		WHERE E1.MGR = E2.EMPNO;
    ```

   2-4. 외부 조인(Outer join)
   
   - 두 테이블간 조인 수행에서 조인 기준 열의 어느 한쪽이 NULL이어도 강제로 출력하는 방식
   
   - 조인 기준 열의 NULL을 처리할 때 자주 사용한다.

   - 외부 조인은 좌우로 나누어 지정할 수 있다. WHERE절에 조인 기준 열 중 한쪽에 `(+)`기호를 붙여준다.
   
   
   |왼쪽 외부 조인(Left Outer Join)|WHERE TABLE1.COL1 = TABLE2.COL1(+)|
   |------|---|
   |**오른쪽 외부 조인(Right Outer Join)**|**WHERE TABLE1.COL1(+) = TALBE2.COL1**|
   
     <img src="C:\Users\oh12s\Desktop\TIL\Coding Test\md-image\image-20210219103321303.png" alt="image-20210219103321303" style="zoom: 200%;" />
   
     
   
   **2-5. NL조인**
   
   <img src="https://t1.daumcdn.net/cfile/tistory/994377375B75B82205" alt="img" style="zoom: 150%;" />
   
   - 프로그래밍 언어에서 사용하는 중첩된 반복문과 유사한 방식으로 조인을 수행 
   
   - Inner Table에서 Join 컬럼이 인덱스에 걸려있지 않으면 비효율이발생
     -> for 문을 돌릴때마다 전부 full scan
   - 따라서 Inner Table의 인덱스 구성 전략이 매우 중요한 요소
   - for문으로 반복하여 Join을 하기 때문에 대량의 테이블을 Join하는 방식으로는 적절하지 않음. 보통 OLTP성 환경의 쿼리에 적절
   - 두 테이블 중 소량의 데이터를 가진 테이블이 Outer Table로 설정되는 것이 유리
   - Random Access 위주의 조인 방식
   - NL Join 기법은 성공하면 바로 결과를 사용자에게 보여주므로 온라인 프로그램에 적당한 조인 기법이다.
   
   
   
   **2-6. Sort Merge Join**
   
   ![img](https://t1.daumcdn.net/cfile/tistory/99F16B4E5BC6F1CA16)
   
   - Join 컬럼을 기준으로 sorting을 시키고 Join을 시키는 방법
   - Inner Table 쪽에 적절한 인덱스가 없어서 NL Join을 쓰기 비효율적일 때 사용
   - 등가 조인이 아니라 범위로 Join을 하는 경우에도 적절함
   - Table Random Access가 일어나지 않고 sorting 작업이 PGA영역에서 수행되기 때문에 경합이 발성하지 않아 성능에 유리함
   
   
   
   **2-7. Hash Join**
   
   ![img](https://t1.daumcdn.net/cfile/tistory/994012345B75BA3A07)
   
   - 배치에서 쓰면 좋고 대용량 테이블을 Join할 때 사용하면 좋다.
   - Inner Table이 대용량 테이블일 때, Outer Table을 Build Input으로 삼아서 Hash영역에 저장한다. Outer Table이 해쉬영역에 올라가고 Inner Table이 읽히면서 Join이 됨
   - PGA영역에 있기 때문에 처리 속도가 빠르다.
   - Hash 영역으로 올라갈 때 Join 컬럼을 기준으로 Hash Fuction이 적용되기 때문에, Join 컬럼에 중복값이 없을수록 성능에 유리하다.
   - Equal 조인만 가능하다.
   - Sort Merge Join처럼 Random Access 부하가 없다.
   - Hash 영역에 들어가는 테이블의 크기가 충분히 작아야지 성능에 유리하다. Hash영역의 용량이 정해져있는데 이를 초과하고 벗어나버리면 디스크 영역을 사용하게 되기 때문에 성능에 매우 불리하게 된다.
   - 수행빈도가 높은 OLTP환경에서 Hash Join으로 풀리게 되면 오히려 CPU나 메모리의 사용량이 늘어서 성능이 안좋아진다. 
   
   

## 면접 질문 풀기

### 둘째마당_04: SELECT문의 기본 형식

1. **SELECT문은 무엇입니까?**
    Select문은 사용자들이 데이터베이스 내 테이블에서 값들을 선택할 수 있도록 합니다. 데이터베이스 테이블에서 어떤 값들을 선택하는 가는 SQL질의 내 다양한 조건에 달려있습니다.
2. **전체 이름이 아닌 이름의 일부로 값을 비교할 수 있는 방법은 무엇입니까?**
   like절. 예를 들어 `SELECT * FROM people WHERE name LIKE ‘%na%’;` 이렇게 하면 `name`에 문자열 `na`를 포함하는 `name`레코드들을 가진 레코드셋을 반환합니다.
3. **테이블에서 어떻게 중복이 없는(별개) 항목을 얻을 수 있습니까?(distinct)**
   DISTINCT에 대해서 설명을 하자면 중복된 결과를 제거하고 하나만 원하고자 할 때 쓰이는 문법이다. 데이터베이스 테이블에 특정 값에 a,a,b,c가 있으면 a,b,c만 나오게 할 수 있다.
4. **어떤 순서로 정렬된 결과를 얻는 방법은 무엇입니까?(order by)**
   프로그램에서 ORDER BY 키워드를 사용하여 정렬하고 정렬된 결과를 반환하여 정렬을 수행하는 수고를 덜 수 있습니다. 키워드는 ORDER BY 렬에 사용됩니다. ORDER BY를 이용함으로써 오름차순으로 정렬되고 ‘DESC’값을 주게 되면 내림차순이 된다.



### 둘째마당_07: 다중행 함수와 데이터 그룹화

1. **테이블의 전체 레코드 수를 어떻게 얻을 수 있습니까?**
   COUNT 함수를 사용. 예를 들어 SELECT COUNT(*) FROM employees WHERE age > 40 에서 처럼 count키워드를 사용하게 되면 카운트(수)를 얻을 수 있습니다.
2. **GROUP BY는 무엇입니까?**
   GROUP BY 키워드는 집계함수(SUM같은)가 호출되 때마다 모든 컬럼 값들의 합계를 반환하기 때문에 SQL에 추가되었습니다. GROUP BY기능 없이 컬럼 값들의 개별 그룹마다 합계를 구하는 것은 불가능합니다.
3. **Group by절을 사용시 일반적으로 사용되는 그룹 함수를 나열하시오.**
   COUNT, MAX, MIN, SUM, AVG
4. **HAVING 절에 대해 설명하시오.**
   GROUP BY절에 의해 생성된 결과 값 중 원하는 조건에 부합하는 자료만 보고자할 때 사용
5. **Where 절과 Having절의 다른 점은 무엇입니까?**
   Having절은 그룹함수의 그룹의 조건으로 사용되고, where 절은 select할 데이터에 조건을 주는 역할입니다.
6. **쿼리 순서 (ORDER BY, FROM, WHERE, SELECT, GROUP BY)**
   SELECT -> FROM -> WHERE -> GROUP BY -> ORDER BY



### 둘째마당_08: 여러 테이블을 하나의 테이블처럼 사용하는 조인

1. **RDB에서 Join이 무엇인지에 대한 설명과 간단한 샘플 쿼리문을 작성해보아라.**

   - - Join이란 2개 이상의 테이블에서 조건에 맞는 데이터를 추출하기 위하여 사용
     - \* Inner Join : 2개 이상의 테이블에서 교집합만을 추출
     - \* Left Join : 2개 이상의 테이블에서 from에 해당하는 부분을 추출
     - \* Right Join : 2개 이상의 테이블에서 from과 join하는 테이블에 해당하는 부분을 추출
     - \* Outer Join : 아웃터 조인 또는 풀 조인이라고 불림, 2개 이상의 테이블에서 모든 테이블에 해당하는 부분을 추출
     - Inner) SELECT user.name, course.name FROM user INNER JOIN course ON user.course=course.id;
     - Left) SELECT user.name, course.name FROM user LEFT JOIN course ON user.course=course.id;
     - Right) SELECT user.name, course.name FROM user RIGHT JOIN course ON user.course=course.id;
     - Outer) SELECT user.name, course.name FROM user OUTER JOIN course ON user.course=course.id;
     - \* 가장 많이 쓰이는 Join은 Inner Join.
2. **Join의 종류에 대해 아시는대로 말씀해주세요**
   Equal Join = Inner Join,Self Join Outer Join, Cross Join, NL Join, Sort Merge Join, Hash Join
3. **NL 조인과 HASH 조인의 차이점과 어떤 부분에 유리한지 말씀해주세요.**
   - NL은 Random Access의 부하를 받고 대용량 테이블을 Join하는데 비효율적이지만, Hash는 Random Access의 부하를 받지 않아 대용량 테이블을 Join하는데 비효율적이다.
   - NL은 OLTP성 환경의 쿼리에 적절, Hash는 PGA환경에 적절
   - NL Join 기법은 성공하면 바로 결과를 사용자에게 보여주므로 온라인 프로그램에 적당한 조인 기법이다.

---

### Reference

- 면접 질문 출처 사이트1: https://sas-study.tistory.com/56

- Youtube-Join, 수행원리: https://www.youtube.com/watch?v=SVD5ldwVYpo
- NL, Sort Merge, Hash: https://mozi.tistory.com/168

