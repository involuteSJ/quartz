---
CMDS: DataBase
type:
  - note
tags:
  - "#DataBase"
  - "#SELECT"
관련 문서:
  - "[[105.01 Basic Concept]]"
category: content
---
## SELECT
>[!Define]
>테이블에 저장되어 있는 데이터 조회

#### SELECT 기본 구문
```sql
-- DB에서 쿼리를 해석하는 순서
-- 1. FROM 에서 테이블을 살펴봄
-- 2. WHERE 절 조건에 따라 가져올 row 선택
-- 3. SELECT 절 조건에 따라 가져올 column 선택

SELECT [projection]
FROM Table
WHERE column = condition
	[and] / [or]
```

- **SELECT절** - 조회하려는 컬럼 명 / 표현식 나열
	- distinct - 중복 행 제거
- **FROM절** - 조회하려는 데이터가 저장된 테이블 명시
	- as - 별칭
- **WHERE절** - 결과를 필터링
	- 비교 연산
	- ![[Pasted image 20250310130630.jpg]]
	- CASE 연산자
		- 값의 동등 비교
		- 조건식 분기
- **GROUP BY절** - 결과 집합의 하위 데이터 그룹
	- 각 그룹별 집계 함수가 적용
	- WHERE절에는 집계 함수를 사용할 수 없음
	- SELECT절에 기술된 컬럼 중, 집계 함수에 사용되지 않은 컬럼은 GROUP BY절에 기술되어야 함
- **HAVING절** - 집계 관련 조건절
	- GROUP BY절에 의해 생성된 그룹을 대상으로 조건을 적용하여 그룹을 필터링
	- with rollup - 그룹 항목 총계 혹은 각 그룹별 소계
- **ORDER BY절** - 정렬
	- select 구문의 실행 결과를 특정 컬럼 값 기준으로 정렬
	- 여러 정렬 기준 사용 시 기술 순서대로 사용
	- ASC - 오름차순 / DESC - 내림차순
- **LIMIT절** - 행 결과 제한
	- LIMIT n, OFFSET m
	- 결과를 m+1 행 부터 m+1+n행까지만 출력
	- OFFSET 생략 시 기본값 0

not => !=, <>, ^=
