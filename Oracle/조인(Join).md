## 조인(Join)

1. **조인(Join)**

   - **두 개 이상의 테이블을 연결하여 하나의 테이블처럼 출력할 때 사용하는 방식**

   - FROM절에 두 개 이상의 열을 넣게 되면 데카르트 곱으로 조인되고, 모든 경우의 결과값이 출력됨. 이 경우, 데이터와 데이터가 정확하게 맞아떨어지지 않는 경우도 함께 출력됨.
     조인을 사용한 데이터 출력에서 조합한 데이터 중 정확한 데이터만을 뽑아내기위해 **WHERE절**과 **테이블.열**을 사용함.

   - FROM절에서 `FROM 테이블 별칭`과 같이 테이블 이름과 별칭을 한 칸 띄워 입력하면 별칭이 지정된다.
		```SQL
     SELECT *
     FROM EMP E, DEPT D
     WHERE E.DEPTNO = D.DEPTNO		# 조인조건
     ORDER BY EMPNO;
		```

<br>
<br>

2. **조인(Join) 종류**

   2-1. 등가조인(Equal Join)

   - 테이블을 연결한 후에 각 테이블의 특정 열 값이 일치한 데이터를 기준으로 출력 결과를 사용하는 방식.

   - 내부조인(Inner Join), 단순 조인(simple Join)이라고도 함

   - '조인을 사용한다'라는 것은 대부분은 등가 조인.
   	```SQL
   	SELECT E.EMPNO, E.ENAME, E.SAL, D.DEPTNO, D.DNAME, D.LOC
   	FROM EMP E, DEPT D
   	WHERE E.DEPTNO = D.DEPTNO		# 조인조건
   	AND SAL >= 3000;
   	```
   - 조인 테이블 수와 조건식 개수의 관계: **`조건식의 최소 개수 = 조인 테이블 수 -1`**
     (테이블이 2개면, 이어주는 WHERE절이 무조건 하나 필요)

   <br>

   2-2. 비등가 조인(Non-equal Join)

   - 등가 조인 방식 외의 방식

   - 이 경우, 조인조건이 없기 때문에 데카르트 곱이 발생(데카르트 곱으로 이루어진 조인을 크로스 조인 또는 교차 조인이라고 함.)
   	```sql
   	SELECT *
   	FROM EMP E, SALGRADE S
   	WHERE E.SAL BETWEEN S.LOSAL AND S.HISAL;
   	```

    <br>
    2-3. 자체 조인(Self join)

   - 하나의 테이블을 여러 개의 테이블처럼 활용하여 조인하는 방식

   - FROM절에 같은 테이블을 여러 번 명시하되 테이블의 명칭만 다르게 지정한다.
   	```sql
   	SELECT E1.EMPNO, E1.ENAME, E1.MGR,
     E2.EMPNO AS MGR_EMPNO, E2.ENAME AS MGR_ENAME
     FROM EMP E1, EMP E2
     WHERE E1.MGR = E2.EMPNO;
   	```
   	<br>
   
	2-4. 외부 조인(Outer join)
   
   - 두 테이블간 조인 수행에서 조인 기준 열의 어느 한쪽이 NULL이어도 강제로 출력하는 방식

	- 조인 기준 열의 NULL을 처리할 때 자주 사용한다.
	
	- 외부 조인은 좌우로 나누어 지정할 수 있다. WHERE절에 조인 기준 열 중 한쪽에 `(+)`기호를 붙여준다.
| 왼쪽 외부 조인(Left Outer Join)        | WHERE TABLE1.COL1 = TABLE2.COL1(+)     |
| -------------------------------------- | -------------------------------------- |
| **오른쪽 외부 조인(Right Outer Join)** | **WHERE TABLE1.COL1(+) = TALBE2.COL1** |

<img src="C:\Users\oh12s\Desktop\마크다운 이미지\image-20210219103321303.png" alt="image-20210219103321303" style="zoom: 80%;" />

<br>
	**2-5. NL조인**

<img src="https://t1.daumcdn.net/cfile/tistory/994377375B75B82205" alt="img"/>

<br>

  - 프로그래밍 언어에서 사용하는 중첩된 반복문과 유사한 방식으로 조인을 수행 

  - Inner Table에서 Join 컬럼이 인덱스에 걸려있지 않으면 비효율이발생
    -> for 문을 돌릴때마다 전부 full scan
    
  - 따라서 Inner Table의 인덱스 구성 전략이 매우 중요한 요소

  - for문으로 반복하여 Join을 하기 때문에 대량의 테이블을 Join하는 방식으로는 적절하지 않음. 보통 OLTP성 환경의 쿼리에 적절

  - 두 테이블 중 소량의 데이터를 가진 테이블이 Outer Table로 설정되는 것이 유리

  - Random Access 위주의 조인 방식

  - NL Join 기법은 성공하면 바로 결과를 사용자에게 보여주므로 온라인 프로그램에 적당한 조인 기법이다.

  <br>
**2-6. Sort Merge Join**

  ![img](https://t1.daumcdn.net/cfile/tistory/99F16B4E5BC6F1CA16)
<br>

  - Join 컬럼을 기준으로 sorting을 시키고 Join을 시키는 방법

  - Inner Table 쪽에 적절한 인덱스가 없어서 NL Join을 쓰기 비효율적일 때 사용

  - 등가 조인이 아니라 범위로 Join을 하는 경우에도 적절함

  - Table Random Access가 일어나지 않고 sorting 작업이 PGA영역에서 수행되기 때문에 경합이 발성하지 않아 성능에 유리함

  <br>

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

---

### 면접질문

1. **RDB에서 Join이 무엇인지에 대한 설명과 간단한 샘플 쿼리문을 작성해보아라.**
   <br>
2. **Join의 종류에 대해 아시는대로 말씀해주세요**.
   <br>
3. **NL 조인과 HASH 조인의 차이점과 어떤 부분에 유리한지 말씀해주세요.**

<br>

<br>

<br>

<br>

<br>

<br>

<br>

<br>

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
     - 가장 많이 쓰이는 Join은 Inner Join.

   <br>

2. **Join의 종류에 대해 아시는대로 말씀해주세요**
   Equal Join = Inner Join,Self Join Outer Join, Cross Join, NL Join, Sort Merge Join, Hash Join
   <br>

3. **NL 조인과 HASH 조인의 차이점과 어떤 부분에 유리한지 말씀해주세요.**

   - NL은 Random Access의 부하를 받고 대용량 테이블을 Join하는데 비효율적이지만, Hash는 Random Access의 부하를 받지 않아 대용량 테이블을 Join하는데 비효율적이다.
   - NL은 OLTP성 환경의 쿼리에 적절, Hash는 PGA환경에 적절
   - NL Join 기법은 성공하면 바로 결과를 사용자에게 보여주므로 온라인 프로그램에 적당한 조인 기법이다.

---

### Reference

- join 수행원리: https://www.youtube.com/watch?v=SVD5ldwVYpo
- NL, Sort Merge, Hash: https://mozi.tistory.com/168