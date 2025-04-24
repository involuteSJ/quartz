---
CMDS: Frontend
type:
  - note
tags:
  - "#JavaScript"
관련 문서:
  - "[[104.03 JavaScript]]"
category: content
---
## DOM

문서를 구성하고 있는 요송들에 대한 function과 property를 갖는 문서 객체

![[Pasted image 20250214101423.png]]
- event - html 페이지에서 발생하는 모든 클라이언트의 행동
	- inline - 요소의 속성에 해당 이벤트 발생 시 실행할 코드 작성
	- listener - 이벤트 발생 시 호출할 callback 함수 등록
- event 객체를 통해 현재 발생한 이벤트를 처리
```javascript
document.getElementById("btn2").addEventListener("click", ()=>{
	console.log(event)
	console.log("event source:", event.currentTarget);
})
```
- #### document를 통한 조회
	- getElementById(id) - id 요소 반환
	- getElementsByClassName(class) - 클래스 요소를 **유사배열**로 반환
	- getElementsByTagName(tag) - 태그 요소를 **유사배열**로 반환
	- getElementsByName(name) - name 요소를 **유사배열**로 반환
	- querySelector(selector) - css 선택자와 일치하는 **첫번째 요소** 반환
	- querySelectorAll(selector) - css 선택자와 일치하는 요소를 **배열**로 반환
- #### Node의 조회
	- 조회된 노드와의 관계를 이용한 노드 탐색
	- ![[Pasted image 20250214102049.png]]
- #### Node의 생성
	- ![[Pasted image 20250214102335.png]]
	- 삽입 위치 결정
	- ![[Pasted image 20250214102403.png]]
	- 문자열 활용
		- innerHTML - 요소 내부의 콘텐츠를 가져오거나 설정(파싱)
		- innerText - 요소 내부의 컨텐츠를 가져오거나 설정(파싱x)
- #### Node의 삭제
	- removeChild() - 자식노드 제거 후 반환
	- remove() - DOM 트리에서 제거
- #### Node의 속성 관리
	- DOM 트리에 등록된 Node 속성 관리
		- setAttribute() - 속성 값 설정
		- getAttribute() - 속성 값 조회
		- removeAttribute() - 속성 제거
	- attribute에서 조회되는 style은 **inline style만 조회** 가능

| 구분    | Attribute                      | Property                                                  |
| ----- | ------------------------------ | --------------------------------------------------------- |
| 정의    | Node 의 초기 상태                   | 현재 DOM의 상태                                                |
| 값 타입  | 문자열만 가능                        | 모든 JavaScript 타입 가능                                       |
| 값 변경  | property까지 변경                  | value, checked 등 폼 관련 속성은 대부분 동기화 되지 않음<br>ID, Class는 동기화 |
| 접근 방법 | getAttribute(), setAttribute() | 직접 속성 접근 (element.property)                               |
| 사용 사례 | 초기값이나 markup관련 작업              | 실시간 상태 관리                                                 |
- #### data-\*
	- data-\* 을 이용해 사용자 정의 attribute를 일관된 방식으로 관리
	- property로 가져올 때는 dataset 사용
- #### class 관리
	- 클래스를 추가하거나 삭제할 때 사용
	- ![[Pasted image 20250214105417.png]]