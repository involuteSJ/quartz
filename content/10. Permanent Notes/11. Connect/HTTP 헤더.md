---
CMDS: "[[107 Computer Science]]"
creation date: 2025-04-07 14:17
modification date: 2025-04-07 14:17:11
type:
  - note
tags:
  - "#HTTP_Header"
관련 문서:
  - "[[107.01 HTTP]]"
category: content
---

# HTTP 헤더
#### HTTP Body
- 메시지 본문에 표현 데이터 전달
- 표현은 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공

#### 표현
- Content-Type : 표현 데이터의 형식
- Content-Encoding: 표현 데이터의 압축 방식
- Content-Language : 표현 데이터의 자연 언어
- Content-Length L 표현 데이터의 길이
- 전송, 응답 둘 다 사용

##### Content-Type
- 표현 데이터의 형식 설명
- 미디어 타입, 인코딩 형식
##### Content-Encoding
- 표현 데이터를 압축하기 위해 사용
- 압축 후 인코딩 헤더 추가
- 데이터를 읽을 때 인코딩 헤더 정보로 압축 해제
##### Content-Language
- 표현 데이터의 자연 언어
##### Content-Length
- 바이트 단위
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

#### 협상 (콘텐츠 네고시에이션)
- 클라이언트가 선호하는 표현 요청
- Accept: 클라이언트가 원하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어
- 요청시에만 사용 

##### 우선순위
- Quality Values(q) 사용
- 0~1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7

#### 전송 방식
- 단순 전송
	- 일반적으로 보내는 방식
- 압축 전송
	- body 내용을 전송
	- Content-Encoding 필요
- 분할 전송 (Transfer-Encoding)
	- body 내용을 분할해서 전송
	- ![[Pasted image 20250407144037.png]]
- 범위 전송
	- 범위를 지정해서 보내는 방식

#### 일반 정보
- From - 유저 에이전트의 이메일 정보
- Referer
	- 이전 웹 페이지 주소
	- 유입 경로 분석 가능
	- 요청에서 사용
	- referrer의 오타
- User-Agent
	- 클라이언트의 애플리케이션 정보
	- 통계 정보
	- 어떤 브라우저에서 장애가 발생하는지 파악 가능
	- 요청에서 사용
- Server
	- 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
	- 응답에서 사용
- Date
	- 메시지가 발생한 날짜와 시간
	- 응답에서 사용

#### 특별한 정보
- Host
	- 요청한 호스트 정보
	- 필수
	- 하나의 서버가 여러 도메인을 처리해야 할 때
- Location
	- 페이지 리다이렉션
	- 300번대 응답 코드가 있으면 리다이렉션 실행
- Allow
	- 허용 가능한 HTTP 메서드
	- 405에서 응답에 포함해야 함
- Retry-After
	- 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
	- 503 코드에서 서비스가 언제까지 불능인지 알려줌

#### 인증
- WWW-Authenticate
	- 리소스 접근시 필요한 인증 방법 정의
	- 401 Unauthorized와 함께 사용
	- WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \\"apps\\"", Basic realm="simple"

#### 쿠키
- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달
- 서버는 클라이언트의 쿠키에 데이터를 저장
- 클라이언트는 서버에 모든 쿠키를 전달
- 민감한 데이터는 저장하지 않도록 주의
- 최소한의 정보만 사용
- ##### 생명주기
	- Set-Cookie: 서버에서 클라이언트로 쿠키 전달
		- expires=만료일
			- 만료일이 지나면 쿠키 삭제
		- max-age=초
			- 양수면 해당 초가 지난 후 쿠키 삭제
			- 0이면 즉시 쿠키 삭제
	- 세션 쿠키 : 만료 날짜를 생략하면 브라우저 종료시 까지 유지
	- 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지
- ##### 도메인
	- 명시 : domain=example.org
		- 명시한 문서 기준 도메인 + 서브 도메인 포함
	- 생략
		- 현재 문서 기준 도메인만 적용
- ##### 경로
	- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
	- 일반적으로 path=/
- ##### 보안
	- Secure를 적용하면 https인 경우에만 전송
	- HttpOnly
		- XSS 공격 방지
		- js에서 접근 불가
		- HTTP 전송에만 사용
	- SameSite
		- XSRF 공격 방지
		- 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송