---
CMDS: Frontend
type:
  - note
tags:
  - "#JavaScript"
  - "#AJAX"
  - "#Promise"
관련 문서:
  - "[[104.03 JavaScript]]"
---
# AJAX

<center><i><b>A</b>synchronous <b>J</b>avascript <b>A</b>nd <b>X</b>ML</i></center>

- 비동기 처리
	- 다중 작업 수행
	- 이전 작업 여부와 상관없이 다음 작업 진행
	- 병렬 실행
	- 콜백함수나 프로미스 등을 통한 실행
	- 네트워크 요청이나 대용량 파일 처리에 사용
- 주 사용처
	- 화면 갱신 없이 클라이언트-서버 간 XML, JSON, HTML 정보 교환

## Promise

비동기 작업이 종료된 이후에 결과값과 실패 사유를 처리
=> callback hell을 탈출하기 위해 나온 API

- 상태
	- pending - fulfilled, rejected 일때 실행할 함수 바인딩
	- fulfilled(성공)
	- rejected(실패)

- promise 객체의 생성과 호출
	- 작업을 정의하는 producing code
	- 결과를 활용하는 consuming code

- #### Producing code
	- promise 생성자의 파라미터인 executor 함수 작성
		- executor에는 콜백 함수로 onfulfilled와 onrejected 두개의 콜백을 받음
		- 작업 성공 시 onfulfilled
		- 작업 실패 시 onrejected
```javascript
const promise = new Promise((onfulfilled, onrejected) => {
	setTimeout(()=>{
		if(pcheck.checked) {
			// 성공 시 반환
			onfulfilled(pcheck.checked);
		} else {
			// 실패 시 반환
			onrejected(pcheck.checked);
		}
	}, 2*1000);
})
```

- #### Consuming code
	- 비동기 작업의 결과를 활용하는 코드
	- .then으로 성공했을 때 handler 처리
	- .catch로 실패했을 때 handler 처리
	- .finally로 언제나 호출
```javascript
promise
.then((message)=>{
	console.log("성공!", message);
})
.catch((error)=>{
	console.log("실패..", error);
})
.finally(()=>{
	console.log("무조건 실행");
})
```

- #### Promise Chaining
	- then, catch, finally 함수가 Promise를 리턴
	- 지속적인 chaining 가능

## Async, Await

Promise가 then hell을 유발

### async
- 비동기 함수를 동기 함수로 만들 때 사용
- async 함수는 자동 promise
### await
- 비동기 코드를 호출할 때 사용
- async 함수 내에서만 사용

try-catch-finally 구문 사용

## 비동기 동작 원리

- JavaScript 는 Single Thread Model
- 한번에 하나의 동작만 가능
- eventLoop와 taskQueue 동작으로 비동기 작업 처리
- ![[Pasted image 20250218150903.png]]

## fetch API

JavaScript에서 네트워크 요청을 수행하기 위해 사용하는 API

- promise 기반 비동기 요청 처리

- #### fetch API 요청
	- input: 정보를 가져올 대상의 URL
	- init: 요청시 추가 전달 내용
		- method - GET / POST
		- headers - 요청 header에 대한 속성
		- body - string, object literal, FormData 등 전달할 내용
```javascript
function fetch(input: RequestInfo | URL, init?: RequestInit): Promise<Response>
```

- #### fetch API 응답 처리
	1. Response 객체 수산
		- 네트워크 장애 및 요청 실패 - rejected
		- 반응하면 fulfilled
	2. Response에서 본문 내용 추출
		- body 타입에 따라 response.json(), .text(), .blob()
		- chaining 가능

SOP 정리
CORS 정리