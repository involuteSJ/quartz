---
CMDS: DataBase
type:
  - note
tags:
  - "#DataBase"
  - "#DML"
관련 문서:
  - "[[105.01 Basic Concept]]"
category: content
---
## DML

<center><i><b>D</b>ata <b>M</b>anipulation <b>L</b>anguage</i></center>
<center><i>테이블의 데이터를 조작하기 위한 명령어</i></center>

#### INSERT
- 새로운 행 삽입
- 레코드 수 증가
- 단일 행 삽입
```sql
INSERT INTO 테이블명(컬럼명|생략)
VALUES (값|SubQuery);

-- 새로운 사원 등록
INSERT INTO emp
VALUES (9997, '홍길동', 'MANAGER', NULL, DEFAULT,
	(SELECT MAX(HISAL) FROM SALGRADE), 1000, 10);

-- 새로운 사원 등록(사원번호, 사원이름, 월급여) - 다중행
INSERT INTO emp(EMPNO, ENAME, SAL)
VALUES (9996, '둘리', 2000),
		(9995, '또치', 3000),
		(9994, '마이콜', 4000),
```

#### UPDATE
- 기존 데이터 수정
- 레코드 수 변화 없음
- 단일 행 서브 쿼리만 가능
- **WHERE절 생략 시 전체 레코드 수정**
```SQL
UPDATE 테이블명 A
[JOIN 테이블명 B ON (JOIN조건)]
SET 컬럼명='값|SubQuery'
[WHERE 조건];

-- 사번이 9996인 사원의 부서번호를 30, 연봉을 3000으로 변경
UPDATE emp
SET DEPTNO=30, SAL=3000
WHERE EMPNO=9996;

-- 사번이 9995인 사원의 부서번호를 7934번 사원과 같게 수정
UPDATE emp
SET DEPTNO=(SELECT DEPTNO FROM (SELECT DEPTNO FROM emp WHERE EMPNO=7934) E),
	JOB=(SELECT JOB FROM (SELECT JOB FROM emp WHERE EMPNO=7934) E)
WHERE EMPNO=9995;

UPDATE emp e1
CROSS JOIN (SELECT DEPTNO, JOB FROM emp WHERE EMPNO=7934) e2
SET e1.DEPTNO=e2.DEPTNO,
	e1.JOB=e2.JOB
WHERE e1.EMPNO=9995;
```

#### INSERT OR UPDATE
- 기존 데이터가 있으면 수정, 없으면 삽입
```SQL
INSERT INTO 테이블명(컬럼명|생략)
VALUES (값);
ON DUPLICATE KEY UPDATE 컬럼명=값;

INSERT INTO emp(EMPNO, ENAME, SAL)
VALUES (8003, 'MICKY', 3500)
ON DUPLICATE KEY UPDATE JOB='CLERK', DEPTNO=30;
```

#### DELETE
- 기존 데이터 삭제
- 레코드 수 감소
- **WHERE절 생략 시 전체 레코드 삭제**
```SQL
DELETE FROM 테이블명
[WHERE 조건];

DELETE FROM EMP
WHERE EMPNO>=8000;
```