---
CMDS: Frontend
type:
  - note
tags:
  - "#JavaScript"
관련 문서:
  - "[[104.03 JavaScript]]"
---
## Storage

<center><i>브라우저에서 페이지를 새로고침하거나 다른 페이지로 이동하면 JavaScript의 변수, 데이터는 초기화</i></center>

- key, value 쌍으로 데이터 관리
- 모두 문자열
- same origin 별로 구분되어 저장

- #### Storage 종류
	- window 객체의 속성
	- localStorage, sessionStorage로 구분

| 구분      | localStorage                           | sessionStorage         |
| ------- | -------------------------------------- | ---------------------- |
| 데이터 지속성 | 브라우저를 닫아도 유지                           | 브라우저 / 탭을 닫으면 삭제       |
| 유효 범위   | 동일 출처의 모든 탭 / 창                        | 탭 /창 별로 독립적            |
| 만료 시점   | 직접 삭제 전까지                              | 세션 종료 시                |
| 사용 사례   | 사용자 설정/ 테마/ 로그인 정보                     | 임시 폼 데이터 / 단일 페이지 앱 상태 |
| 데이터 접근  | JavaScript로만 가능                        | <                      |
| 저장 용량   | 일반적으로 5-10MB                           | <                      |
| API 메서드 | setItem / getItem / removeItem / clear | <                      |
| 이벤트 지원  | storage 이벤트 지원                         | <                      |
- #### Storage API
	- ![[Pasted image 20250214110405.png]]
- #### 객체 저장
	- storage는 value로 문자열만 사용 -> 묵시적 형 변환 후 저장
	- toString()을 재정의하지 않은 객체의 문자열은 \[object Object\]
- #### 객체의 직렬화 / 역직렬화
	- JSON.stringify() - 객체를 JSON 문자열로 변환
	- JSON.parse() - JSON 문자열을 JavaScript 객체로 변환