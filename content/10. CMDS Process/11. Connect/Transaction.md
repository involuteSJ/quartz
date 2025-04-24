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
## Transaction
- 분할해서 실행할 수 없는 작업들의 모음
- 여러 SQL문을 하나의 작업 단위로 묶어 처리
- 모든 작업이 수행되면 COMMIT, 하나라도 실패하면 ROLLBACK
- 데이터의 무결성을 보장
- ex) 금융 거래, 재고 관리, 예약 시스템

#### 특징(ACID)
- **A**tomicity (원자성) - 하나라도 실패하면 전체 취소
- **C**onsistency (일관성) - 트랜잭션이 실행되기 전과 후의 DB 상태가 일관성을 유지
- **I**solation (고립성) - 하나의 트랜잭션이 완료될 때까지 다른 트랜잭션이 접근 못함
- **D**urability (지속성) - 성공적으로 완료되면 결과가 영구적으로 반영

>[!tips]
>잠금 : 동시성을 제어하기 위한 기능
>격리 수준 : 트랜잭션 간의 작업 내용을 어떻게 공유하고 차단할 것인가

#### 격리 수준
- READ UNCOMMITTED
	- 커밋되지 않은 데이터를 읽을 수 있음 -> *Dirty Read*
- READ COMMITTED
	- 커밋된 데이터만 읽을 수 있음 -> *Non-Repeatable Read*
- REPEATABLE READ
	- 트랜잭션 내 같은 데이터를 조회하면 항상 같은 데이터 조회 보장 -> *Phantom Read*
- SERIALIZABLE
	- 동시 실행을 막음 -> *성능 저하*

>[!TIPS]
>MYSQL 격리 수준 확인
>> SELECT @@TRANSACTION_ISOLATION
>
>MYSQL 격리 수준 명시적 변경
>>SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED

#### 성능 최적화
- 범위를 최소화하여 잠금 유지 시간을 줄임
- 적절한 격리 수준을 선택하여동시성 개선
- 인덱스를 활용하여 성능 향상

![[transaction1]]


## TCL

<center><i><b>T</b>ransaction <b>C</b>ontrol <b>L</b>anguage</i></center>

- START TRANSACTION
	- 명시적인 트랜잭션 시작
	- 암묵적 자동 커밋 해제
- COMMIT
	- 트랜잭션을 완료하고 변경 사항을 저장
- ROLLBACK \[TO SAVEPOINT명\]
	- 트랜잭션을 취소하고 변경 사항을 되돌림
- SAVEPOINT *SAVEPOINT명*
	- 특정 지점을 저장하여 부분 롤백을 가능하게 함

#### 잠금 읽기
- 읽기 허용 / 쓰기 금지
```SQL
START TRANSACTION;
SELECT ~ FOR SHARE;
```
- 읽기 / 쓰기 금지
```SQL
START TRANSACTION;
SELECT ~ FOR UPDATE;
```
