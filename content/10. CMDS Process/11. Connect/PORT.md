---
CMDS: DataBase
type:
  - note
tags:
  - "#HTTP"
  - "#PORT"
관련 문서:
  - "[[107.01 HTTP]]"
category: content
---
## PORT
- 애플리케이션의 상호 구분을 위해 사용하는 번호
- 사용자가 여러 서버와 연결하기 위해 사용 -> IP + PORT
- ![[Pasted image 20250326101417.png]]

- 0~65535 까지 사용 가능. 0~1023까지는 잘 알려진 포트로 사용하지 않는 것 추천
	- FTP - 20, 21
	- TELNET - 23
	- HTTP - 80
	- HTTPS - 443

## DNS

<center><i><b>D</b>omain <b>N</b>ame <b>S</b>ystem</i></center>

- IP가 계속 변경될 수 있음
- IP는 기억하기 어려움
=> IP 주소를 도메인 명으로 변환
![[Pasted image 20250326102223.png]]

- ### URI (Uniform Resource Identifier)
	- 리소스를 구분하는데 필요한 정보
	- ![[Pasted image 20250326102314.png]]
- #### URL (Uniform Resource Locator)
	- 리소스 위치를 지정
	- scheme://\[userinfo@\]host\[:port\]\[/path\]\[?query\]\[#fragment\]
	- 프로토콜://\[사용자 정보\]호스트명\[포트번호]\[/패스]\[?쿼리]\[파라미터]
		- 프로토콜(http / https) - 어떤 방식으로 자원에 접근할 것인가
		- 사용자 정보 - 거의 사용 안함
		- 호스트명 - 도메인명 또는 ip 정보
		- 포트 번호(생략 가능) - 접속 포트
		- 패스 - 리소스 경로
		- 쿼리 파라미터 - 웹 서버에서 제공하는 파라미터
		- 파라미터 - html 내부 북마크로 사용. 서버 전송 X
- #### URN (Uniform Resource Name)
	- 리소스 이름을 부여

## 웹 브라우저 요청 흐름
1. 웹 브라우저가 HTTP 메세지 생성
	- ex) GET /search?q=hello&hi=ko HTTP/1.1
	-       HOST:www.google.com
2. Socket 라이브러리를 통해 서버로 전달
	1. TCP/IP 연결
	2. 데이터 전달
3. 서버에서 패킷 정보를 읽고 응답 메세지 생성
	- TCP/IP 패킷 생성, HTTP 메세지 포함

#### 패킷 예시
```
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
	<body> ... </body>
</html>
```