---
CMDS: DataBase
type:
  - note
tags:
  - "#DataBase"
  - "#SubQuery"
  - "#집합연산"
관련 문서:
  - "[[105.01 Basic Concept]]"
category: content
---
## Sub Query
- 두개 이상의 SQL 문을 하나의 SQL 문으로 처리하는 방법
- 다른 SQL문에 포함된 서브 쿼리는 메인 SQL 문에 사옹될 값을 반환
- #### 주의 사항
	- 괄호로 감싸서 표현
	- 쿼리 끝에 세미클론 X
	- ORDER BY 사용 불가

#### 단일 행 Sub Query
- 하나의 행만 조회하여 메인 SQL문에 반환
- 비교 조건 -> 단일 행 비교 연산자(=, >, <, !=)만 사용 가능
```SQL
SELECT ENAME, DEPTNO
FROM EMP
WHERE DEPTNO = (
	SELECT DEPTNO
	FROM EMP
	WHERE ENAME = 'SMITH'
);

SELECT ENAME, HIREDATE
FROM EMP
WHERE HIREDATE > (
	SELECT HIREDATE
	FROM EMP
	WHERE ENAME = 'SMITH'
);
```
#### 다중 행 Sub Query
- 여러 행을 검색하여 메인 SQL 문에 반환
- 비교 조건 -> 비교 연산자(IN, ANY, ALL, EXIST) 사용
- ##### 비교 연산자
	- **IN** - 하나라도 만족하면 참
	- **ANY** - IN의 기능 + 비교 연산자
		- = ANY, > ANY, < ANY ...
	- **ALL** - 모든 값이 만족하면 참
		- = ALL, > ALL, < ALL ...
	- **EXISTS** - 실행 결과가 존재하면 참
```SQL
-- IN
SELECT EMPNO, ENAME
FROM EMP
WHERE EMPNO IN (
	SELECT MGR
	FROM EMP
);

-- ANY
SELECT ENAME, SAL
FROM EMP
WHERE SAL > ANY (
	SELECT SAL
	FROM EMP
	WHERE JOB = 'SALESMAN'
);

-- ALL
SELECT ENAME, SAL
FROM EMP
WHERE SAL > ALL (
	SELECT SAL
	FROM EMP
	WHERE JOB = 'SALESMAN'
);

-- EXISTS
SELECT M.EMPNO, M.ENAME
FROM EMP M
WHERE EXISTS (
	SELECT 1
	FROM EMP E
	WHERE M.EMPNO = E.MGR
)
```

#### Sub Query 유형
- *서브쿼리를 실행하는 방식과 최적화 방식이 다름*
- ##### 상호 연관 Sub Query
	- *특정 행 단위로 조건을 검사할 때 유용*
	- 독립 실행이 불가능한 서브 쿼리
	- 서브 쿼리의 결과를 메인 쿼리에서 참조
- ##### 다중 열 Sub Query
	- *다중 값 비교*
	- 여러 열을 조회하는 서브 쿼리
	- ###### PAIRWISE
		- 컬럼을 쌍으로 묶어서 비교
	- ###### UNPAIRWISE
		- 컬럼별로 나눠서 비교한 후 AND 연산
- ##### 스칼라 Sub Query
	- *단일 값을 가져와 연산에 활용*
	- 하나의 값만 조회
	- 단일 행 단일 열 서브 쿼리
- ##### 인라인 뷰
	- *복잡한 쿼리를 정리하고 중간 결과를 활용*
	- FROM절, JOIN절 뒤에 오는 서브 쿼리
	- 서브 쿼리의 실행 결과를 테이블처럼 사용
		- 가공된 결과를 이용하고자 할 때
		- 가독성을 높이기 위해
	- **별칭** 반드시 사용

## 집합 연산
- 쿼리 실행 결과를 하나의 집합으로 보고 집합 간 연산 수행
- 두 쿼리의 컬럼 개수가 같아야 함

#### 집합 연산의 종류
- **UNION ALL** - 합집합 (중복 포함)
- **UNION** - 합집합
- **INTERSECT** - 교집합
- **EXCEPT** - 차집합