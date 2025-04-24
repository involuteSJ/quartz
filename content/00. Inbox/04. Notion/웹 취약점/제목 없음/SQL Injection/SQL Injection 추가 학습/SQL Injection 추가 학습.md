---
CMDS: Security
관련 문서:
  - "[[SQL Injection]]"
tags:
  - "#SQL_Injection"
---
### SQL 인젝션이란

> [!important] 구조화된 질의 언어를 주입하는 공격

⇒ 사용자 입력 값으로 주입

  

웹에 종속적인 공격인가?

→ 주요 경로가 웹일뿐, 웹에 종속적인 공격은 아님.

  

사고사례

여기어때

1. SQL 인젝션 공격을 통한 관리자 세션 탈취
2. 관리자 세션을 통한 서비스 관리 서비스 접속

  

공격 대상

사용자 입력이 가능한 모든 곳이 공격의 대상이며 사용자 입력 값을 받는 모든 기능들은 잠재적인 SQL 인젝션 위협에 노출되어 있음

  

SQL 관점에서 본 공격 포인트

1. CRUD 관점
    - INSERT
    - SELECT
    - UPDATE
    - DELETE

1. SQL 구문 관점
    
    SELECT idx, title, date FROM Board Where tb_name=’notice’ ORDER BY idx desc
    
    ⇒ 어디든 공격 포인트가 될 수 있음
    

  

SQL 인젝션 공격 종류

- 인증 우회 공격
    - 로그인, PIN, ID, PW …
- 데이터 조회 공격
    - DB를 조회해서 정보를 알아내는 방법
- 시스템 명령어 실행 공격
    - DB 서버에 직접 공격

  

취약점 분석 방법론

1. 취약점 분석
    
    1. 에러 유/무 확인
        
        에러가 발생할 경우 공격할 여지가 있음
        
    2. 취약점 유/무 확인
        
        1. 데이터 타입이 문자형인 경우
            
            문자 사이에 ‘||’ 를 넣어서 조회할 때 조회가 되고, ‘a’ 를 넣었을 때 오류가 나오면 취약하다고 판단
            
            |   |   |   |   |
            |---|---|---|---|
            |DBMS|연산자|표현식|예시|
            |ORACLE|\||피연산자1 \| 피연산자2|‘te’ \| ‘st’|
            |MSSQL|+|피연산자1 + 피연산자2|‘te’ + ‘st’|
            |MYSQL|공백|피연산자1 피연산자2|‘te’ ‘st’|
            
        2. 데이터가 숫자형인 경우
            
            idx=192 인 경우 idx=193-1을 입력해서 같은 결과가 출력되는지 확인
            
        3. 파라미터가 테이블로 들어가는 경우
            
            where 1=1을 넣어 정상적으로 조회되는지 확인
            
            +파라미터가 테이블인 경우 대부분 tb 혹은 table이 들어감
            
        4. 컬럼 형태로 삽입
            
            ![[46003a91-1ba8-47ad-9aa5-2901cfa99e56.png]]
            
            ![[fbf8df82-90c8-42d4-ad4e-d9d91f4a22c1.png]]
            
            사용자 입력 값을 1부터 차례대로 증가시켰을 때 정상출력되다가 오류가 날 경우 컬럼이 없다는 뜻이므로 컬럼의 개수 파악 가능
            
            ![[fefa13f1-79a8-441e-8466-369efa2aed16.png]]
            
        
          
        
        SQL 인젝션 구문 종류
        
        ![[5c735e6a-472f-482b-9d8a-e2e7f02ad82c.png]]
        
    3. 조건 구문 완성
        
        1. 데이터 타입이 문자형인 경우
            
            ![[5aa206ae-ab49-4360-a113-c234dcd6fa43.png]]
            
        2. 데이터 타입이 숫자형인 경우
            
            ![[9a12c84b-72e5-4c1d-ab91-302acb7165e6.png]]
            
        
          
        
        CASE WHEN 구문의 활용
        
        ```SQL
        case when [condition] then [true] else [false] end
        ```
        
        ![[43854dd5-10ef-47ed-9985-f3b0f981b6f8.png]]
        
    
      
    
    검색 기능 동작 원리 분석을 통한 올바른 분석 방법
    
    ![[1ed7d0b5-ad74-4042-987b-4c9bbb294d49.png]]
    
    ![[e7f1d091-6348-4b1f-a5de-d10091ad56d8.png]]
    
      
    
    검색 기능 컬럼 파라미터에 대한 올바른 취약점 점검 방법
    
    ```SQL
    -- 정상 SQL
    select * from board where title like '%test%'
    -- 비정상 SQL
    select * from board where 'test' like '%test%'
    -- 버프스위트를 이용하여 title 대신 'test' 삽입
    ```
    
    mssql에서 +연산자를 사용할 때 반드시 URL 인코딩 진행
    
    ‘te’+’st’ ⇒ ‘te’%2b’st’
    
      
    
    참과 거짓을 구분할 수 있는 구문 완성
    
    ```SQL
    -- 구문(1)
    select * from board where 1=1 and title like '%test%' --TRUE
    select * from board where 1=2 and title like '%test%' --FALSE
    
    -- 구문(2)
    select * from board where (case when 1=1 then 'test'else 'ha' end) like '%test%' --TRUE
    select * from board where (case when 1=2 then 'test'else 'ha' end) like '%test%' --FALSE
    ```
    

테이블 파라미터에 대한 올바른 취약점 점검 방법

Oracle의 경우 파라미터값으로 all_tables를 전달했을 때 테이블 목록이 출력된다면 SQL 인젝션에 취약한 상태

테이블 파라미터는 FROM절에 들어가기 때문에 뒤에 들어갈 내용 유추할 필요가 있음

```SQL
select * from ex_member-- where id=?
-- 오류 발생!
```

위와 같은 prepared statement 환경에서는 뒤에 들어갈 예약어를 주석 처리할 경우 오류가 발생

⇒뒤에 들어갈 내용을 예측할 경우에는 정상 출력 가능

```SQL
select * from ex_member where id=?--where id=?
```

하지만 뒤에 들어갈 예약어가 여러개가 들어갈 경우 예측하기 힘듦

⇒ 서브쿼리를 이용하여 해결

```SQL
select * from (select * from ex_member where 1=1) where id=?
```

  

## 인증 우회 공격 기법

인증 우회 공격이란

![[29302e85-916f-463e-b0f0-334b78267f9e.png]]

  

인증 기능에 대한 이해

![[afbee9c0-701b-4e39-822f-8976bd293d8e.png]]