---
CMDS: DataBase
type:
  - note
tags:
  - "#DataBase"
관련 문서:
  - "[[105.01 Basic Concept]]"
category: content
---
## DBMS

<center><i><b>D</b>ata<b>B</b>ase <b>M</b>anagement <b>S</b>ystem</i></center>

- 응용 프로그램과 데이터베이스의 중개자

#### RDBMS
- 관계형 모델을 지원하는 DBMS
- 다양한 정보를 효율적으로 저장하고 처리
- ##### 구성 요소
	- **개체** -> Table
		- 현실 세계에서의 유/무형의 실체
		- 서로 독립적으로 존재하면서 분별 가능
	- **관계** -> Foreign Key
		- 2개 이상의 개체 간의 상호 작용이나 연결
		- 1:1 , 1:N, N:M
	- **속성** -> Column
		- 개체가 포함하고 있는 성질
		- 개체를 설명하는 세부 항목이나 특성

## Query Plan
- DBMS가 SQL 쿼리를 어떻게 처리하겠다고 짜는 계획 -> 옵티마이저가 처리
- #### 옵티마이저
	- 가장 효율적인 방법으로 SQL을 수행할 최적의 경로를 생성
	- ##### 규칙 기반 최적화
		- 옵티마이저에 내장된 우선 순위를 기준으로 실행 계획을 수립
		- 같은 쿼리는 같은 실행 계획
		- 테이블 레코드 수나 컬럼 값의 분포도를 고려하지 않음
	- ##### 비용 기반 최적화
		- 실행 가능한 여러 방법을 만들고, 각 작업의 비용 정보와 통계 정보를 이용해 비용 산출
			- 통계 정보
				- 선택도 - 특정 조건에 의해 선택될 것으로 예상되는 레코드 비율
				- 카디널리티 - row 수 \* 선택도
				- 히스토그램 - 미리 저장된 히스토그램 정보를 사용해 더 정확한 카디널리티를 구함
				- 비용 - 쿼리를 수행하는데 소요되는 일량 또는 시간
		- 이후 최소 비용의 실행 계획을 선택

## SQL

<center><i><b>S</b>tructed <b>Q</b>uery <b>L</b>anguage</i></center>

- RDBMS의 데이터를 관리하기 위해 설계한 프로그래밍 언어

#### 데이터 구문의 종류
- ##### DML - Data Manipulation Language
	- INSERT - 레코드 삽입
	- UPDATE - 레코드 수정
	- DELETE - 레코드 삭제
	- SELECT - 레코드 조회, DQL
- ##### DDL - Data Definition Language
	- CREATE - DB 객체 생성
	- ALTER - DB 객체 수정
	- DROP - DB 객체 삭제
	- RENAME - DB 객체 이름 수정
- ##### TCL - Transaction Control Language
	- COMMIT - 변화된 내용이 있으면 적용 후 트랜잭션 종료
	- ROLLBACK - 변화된 내용이 있어도 적용 않아며 트랜잭션 종료
	- SAVEPOINT - 롤백 가능한 저장점 생성
- ##### DCL - Data Control Language
	- GRANT - 권한 부여
	- REVOKE - 권한 회수

- #### 함수
	- 단일 행 함수 - 연산 결과가 행 개수만큼 나오는 함수
	- 다중 행 함수 - 연산 결과가 하나로 나오는 함수(집계함수)
		- **count** - 레코드의 컬럼이 null이 아닌 레코드의 수
		- **max** - 레코드의 컬럼 중 최대값
		- **min** - 레코드 컬럼 중 최소값
		- **sum** - 레코드 컬럼 값의 합
		- **avg** - 레코드 컬럼 값의 평균
	- 단일 행 함수 (단일 행 함수) - 가능
	- 단일 행 함수 (다중 행 함수) - 가능
	- 다중 행 함수 (다중 행 함수) - 불가능
	- WHERE절에 함수를 적용할 경우 테이블 전체 스캔 -> 속도가 느려짐
- #### 데이터 타입에 따른 함수
	- ##### 숫자
		- round
		- cell
		- floor
	- ##### 문자
		- upper
		- lower
		- incap
		- substr
		- concat
	- ##### 날짜
		- date_add(날짜, INTERVAL n UNIT)
			- UNIT - YEAR, MONTH, DAY ...
		- year(), month(), day() ...
		- extract(year / month / day from 날짜)
	- ##### null
		- 비교 불가
- #### 데이터 타입
	- 숫자
		- ![[Pasted image 20250313111557.jpg]]
	- 문자
		- ![[Pasted image 20250313111638.jpg]]
		- ![[Pasted image 20250313111718.jpg]]
	- 날짜
		- ![[Pasted image 20250313111847.jpg]]