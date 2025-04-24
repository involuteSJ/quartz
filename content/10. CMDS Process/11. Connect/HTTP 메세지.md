---
CMDS: DataBase
type:
  - note
tags:
  - "#HTTP"
관련 문서:
  - "[[107.01 HTTP]]"
category: content
---
## HTTP Mesage
![[http message]]
### HTTP 메세지 구조
- **start-line**
- **header**
- **empty line**
	- header와 body를 구분해주는 공백 줄
-  **message body**

#### 요청 메세지
![[req message]]
- ##### start-line = request-line
	- SP - 공백
	- CRLF - 엔터
	- request-line = method SP request-target SP HTTP-version CRLF
		- ###### method - 서버가 수행해야 할 동작 지정
			- GET : 리소스 조회
			- POST : 요청 내역 처리
			- PUT
			- DELETE
		- ###### request-target: 요청 대상
			- absolute-path\[?query]
			- 절대 경로 = "/"로 시작하는 경로
		- ###### HTTP-version
- ##### header
	- OWS - 공백 허용
	- header-field = field-name ":" OWS field-value OWS
		- ###### field-name - 대소문자 구분 없음
		- ###### field-value
- ##### body
	- 실제 전송할 데이터
	- HTML문서, 이미지, 영상, JSON 등등
#### 응답 메세지
![[res message]]
- ##### start-line = status-line
	- SP - 공백
	- CRLF - 엔터
	- status-line = HTTP-version SP status-code SP reason-phrase CRLF
		- ###### HTTP-version
		- ###### status-code: 상태 코드
			- 200 : 성공
			- 400 : 클라이언트 요청 오류
			- 500 : 서버 내부 오류
		- ###### reason-phrase
			- 사람이 이해할 수 있는 짧은 상태 코드 설명
- ##### header
	- OWS - 공백 허용
	- header-field = field-name ":" OWS field-value OWS
		- ###### field-name - 대소문자 구분 없음
		- ###### field-value
- ##### body
	- 실제 전송할 데이터
	- HTML문서, 이미지, 영상, JSON 등등