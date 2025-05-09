---
CMDS: Frontend
type:
  - note
tags:
  - "#JavaScript"
관련 문서:
  - "[[104.03 JavaScript]]"
---
## JavaScript

<center><i>동적 타이핑, 객체 지향, 함수형 프로그래밍을 지원하는 스크립트 언어</i></center>

- **객체지향적 특징**
	- Abstraction - 추상화
	- Inheritance & Polymorphism - prototype 개념
	- Encapsulation - closure
- **스크립트 언어**
	- 인터프리터 방식으로 동작하며 just-in-time 컴파일러 사용
	- 호스트 환경에 종속적
	- 일반적으로 독립적 실행파일을 만들지 않음

- #### Javascript 사용 선언
	- HTML 파일 내에  \<script\>태그 사용
	- 외부 파일 링크
		- \<script src="경로"\>\</script\>
	- inline 방식
- #### 변수의 선언 지시어
	- 동적 타입 언어 - 값을 할당할 때 타입 결정 -> **변수 선언 시 지시어 사용**
	- 지시어 생략 가능 - <font color="#ff0000">사용 x</font>
	- 변수의 life-cycle : function 기준으로 돌아감
	- var - <font color="#ff0000">사용 x</font>
		- 변수의 중복 선언, 변수 hoisting, 일반적이지 않은 scope
		- 함수 내에서 사용 가능 - block을 벗어나도 같은 함수면 ok
	- *let* - 주로 사용
		- 중복 선언 x, hoisting x, 일반적인 scope
		- block 단위의 scope
	- *const* - 상수 선언 지시어
		- 선언 시 반드시 초기화
		- block 단위의 scope
- #### 변수의 타입
	- ##### 기본형
		- **number** - 정수 / 실수
			- Infinity - 무한대
			- NaN(Not a Number) - 어떤 산술 연산을 해도 NaN
		- **string** - 문자
			- 템플릿 문자열 : \` 로 문자열을 감쌈. 안에 변수 삽입 가능
		- **boolean** - true / false
			- falsy - 0, "", undefined, NaN
			- truthy
		- **undefined** - 아무것도 할당하지 않음
			- 변수의 타입이 결정되지 않았을 때
			- 객체의 미 정의된 속성을 참조하려 할 때
			- void를 반환하는데 출력하는 경우
		- **null** - null 값 할당
			- 객체가 없음을 명시적으로 나타내기 위해 할당
		- typeof - 변수의 종류를 알기 위해 사용하는 연산자
	- ##### 참조형
		- Number
			- number의 wrapper
		- String
		- Boolean
- #### JS의 객체
	- key, value로 구성된 property의 집합
	- JS 객체의 분류
- #### 배열
	- Array 클래스의 생성자 함수 사용
		- `let nums = new Array(1,2,3,4,5);`
	- 배열 리터럴 \[ \] 활용
		- `let coffees = [1,2,3,4,5];`
	- 배열의 특징
		- 객체기반으로 index는 객체의 property
		- 필요에 따라 크기가 동적으로 조절
		- 연속적인 메모리 공간을 갖지 않을 수 있음
- #### 객체의 속성 관리
	- 조회 및 활용
		- . 이나 \[ \]로 접근
		- in 연산자를 통해 객체가 속성을 가지고 있는지 확인
	- 추가 / 수정
		- property의 키 값은 유일
		- 키가 존재하지 않을 시 추가
	- 삭제
		- delete 연산자를 통해 속성 제거
- #### 연산자
	- **산술연산**
		- 참조형의 + 연산
			- toString() 결과와 결합 연산
		- 참조형의 -, /, \*, \%, \*\* 연산
			- valueOf() 결과와 연산
	- **비교연산**
		- 동등 비교 연산자 \=\=, !\=
		- 일치 타입 연산자 \=\=\=, !\=\=
			- 값과 타입 모두 동일한지 비교
		- 형 변환
			- 피연산자의 크기를 비교해서 논리값 반환
			- 타입이 다른 경우 숫자로 변환하여 비교 -> 변경 불가시 NaN
	- **short-circuit 논리 연산자**
		- &&, ||
		- 비교와 할당이 동시에 발생
			- `console.log(4 || undefined); -> 4`
			- `console.log(4 && undefined); -> undefined`
- #### 반복문
	- for loop
	- for-of
	- for-in
		- 객체의 속성 순회를 위해 사용
- #### 예외 처리
	- 프로그램의 작성 오류, 파라미터 오류에 대한 대처
	- 유형
		- Error 객체 - 예외에 대한 정보를 담고 있는 객체의 최상위 객체
		- 사용자 정의 예외 - 숫자 값부터 객체까지 모든 것을 예외로 사용