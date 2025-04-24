---
CMDS: DataBase
type:
  - note
tags:
  - "#DataBase"
  - "#View"
관련 문서:
  - "[[105.01 Basic Concept]]"
category: content
---
## View
- 테이블이나 또 다른 뷰를 기반으로 한 가상 테이블
- 복잡한 쿼리 -> 심플하게 만들 수 있음
- db 구조를 감출 수 있다

#### VIEW의 유형
- 단순 뷰
	- 하나의 테이블에서만 조회
	- 데이터 가공 X
- 복합 뷰
	- 두개 이상의 테이블에서 조회
	- 데이터 가공 O
- 데이터 조작
	- 가공 되지 않은 경우에만 데이터 조작 가능

```sql
-- VIEW 생성
CREATE VIEW 뷰명
AS SUBQUERY;

-- VIEW 삭제
DROP VIEW 뷰명;

-- VIEW 수정
ALTER VIEW 뷰명
AS SUBQUERY;

-- 이름, 급여, 부서, 부서별급여합을 구하세요
CREATE VIEW EMPDEPT
AS
SELECT ENAME, SAL, DNAME, DSAL
FROM EMP JOIN DEPT USING(DEPTNO)
		JOIN (SELECT DEPTNO, SUM(SAL) AS DSAL FROM EMP GROUP BY DEPTNO) C 
		ON (EMP.DEPTNO = C.DEPTNO);

SELECT * FROM EMPDEPT;
```