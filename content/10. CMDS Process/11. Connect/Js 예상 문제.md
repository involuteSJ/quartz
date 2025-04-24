---
CMDS: Frontend
type:
  - note
tags:
  - "#JavaScript"
관련 문서:
  - "[[104.03 JavaScript]]"
category: problem
---
## 문제
**1번**
아래 스크립트 실행 시 출력되는 결과로 옳은 것은?
```javascript
for(var i=0; i<3; i++) {
	setTimeout(()=>{
		console.log(i);
	}, 1000);
}
```
1. 1 2 3
2. 0 1 2
3. 2 3 4
4. 3 3 3

---
**2번**
아래 스크립트 실행 시 출력되는 결과로 옳은 것은?
```javascript
console.log(name);
var name = "Alice";
```
1. Alice
2. undefined
3. null
4. ReferenceError

---
**3번**
아래 스크립트 실행 시 출력되는 결과로 옳은 것은?
```javascript
for(let i=0; i<3; i++) {
	var message = 0+i;
	var message = 3+i;
}

console.log(message);
```
1. 5
2. 2
3. SyntaxError
4. ReferenceError

---
**4번**
아래 스크립트 실행 시 출력되는 결과로 옳은 것은?
```javascript
const name="gildong";
name = "rename";

console.log(name);
```
1. gildong
2. rename
3. SyntaxError
4. ReferenceError

---
**5번**
자바스크립트의 자료형 중 기본형에 해당하는 것이 아닌 것은?
1. number
2. string
3. boolean
4. undefined
5. null
6. 전부 해당

---
**6번**
아래 연산의 결과로 올바르게 짝지어진 것은?
(console.log(new Date(2001, 1, 1) =>Thu Feb 01 2001 00:00:00 GMT+0900 (한국 표준시) )
```javascript
console.log(1+"10");
console.log(1-"10");
console.log(1-"a");
console.log(1+true);
console.log(new Date(2001, 1, 1)+1);
```
1. 110, NaN, NaN, NaN, Thu Feb 01 2001 00:00:00 GMT+0900 (한국 표준시)1
2. 110, -9, NaN, 2, NaN
3. 110, -9, NaN, 2, Thu Feb 01 2001 00:00:00 GMT+0900 (한국 표준시)1
4. SyntaxError

---
**7번**
아래 스크립트 실행 시 출력되는 결과로 옳은 것은?
```javascript
console.log(4||undefined);
console.log(1==true);
console.log(1===true);
```
1. undefined, true, true
2. undefined, true, false
3. true, false, false
4. 4, true,true
5. 4, true, false

---
**8번**
자바스크립트에서 for loop, for-of, for-in의 차이점은?

---
**9번**
아래 스크립트 실행 시 출력되는 결과로 옳은 것은?
```javascript
let element = ["1", "2", "3"]
let x = element.push(5);

console.log(x);
```
1. 5
2. 4
3. 1
4. 3

---
**10번**
다음 중 일급함수의 특징으로 작성된 함수가 아닌 것은?
```javascript
//1번
const greet = function() {
	return "Hello";
}
//2번
function callFunction(fn) {
	console.log(fn());
}
//3번
function printHello() {
	console.log("Hello");
}
//4번
function greetFunction() {
	return function() {
		return "Hi";
	}
}
//5번
const functions=[
	function() {return "A";},
	function() {return "B";}
]
```

---
**11번**
JSON 에서 키를 작성할때 키 값 따옴표가 항상 필요할까?


---
**12번**
아래 스크립트 실행 시 출력되는 결과로 옳은 것은?
```javascript
//a
console.log(greet("Alice"));

const greet = function(name) {
	return `Hello, ${name}`;
}
//b
console.log(add(2, 3));

const add = (a, b) => a + b;
//c
console.log(multiply(2, 3));

var multiply = function(a, b) {
    return a * b;
};

```
1. a : Alice / b : 5 / c : 6
2. a : ReferenceError / b : TypeError / c : ReferenceError
3. a : ReferenceError / b : ReferenceError / c : ReferenceError
4. a : ReferenceError / b : ReferenceError / c : TypeError

---
**13번**
eval과 parse의 차이점을 설명하시오


## 답
1. 4번
	- var로 선언된 i는 블록 스코프를 따르지 않기 때문에 루프가 끝나도 살아있고, setTimeout이 실행될 때 i=3이 되어버림
2. 2번
	- var로 name을 선언 할 경우 호이스팅 때문에 에러가 아닌 undefined 출력
	- ReferenceError : 정의되지 않은 변수나 객체 참조
		- 존재하지 않는 변수 참조
		- 변수 선언 전 접근
		- 함수 내부에서 선언되지 않은 변수 사용
		- 전역 객체 잘못 참조
3. 1번
	- SyntaxError : 문법이 잘못된 경우 발생
		- 잘못된 변수 선언
		- 괄호 누락
		- const 값 재할당
		- json 형식 오류
		- await의 잘못된 위치 사용
4. 3번
5. 6번
	- undefined
		- 변수 선언만 하고 값 할당을 하지 않은 경우
		- 객체의 미 정의된 속성을 참조하는 경우
		- void 를 반환하는 함수를 출력하는 경우
	- null
		- 객체가 없음을 나타내기 위해 할당
		- GC의 대상임을 알림
6. 3번
7. 5번
8. 답
	- for loop
		- 일반적인 for문
	- for-of
		- of 뒤에 오는 배열에서 값을 하나씩 꺼내 of 앞에있는 변수에 대입
		- 배열의 값이 없을 때까지 진행
	- for-in
		- for-of 와 유사하지만, for-in에서는 배열 대신 객체 사용
9. 2번
	- 배열의 push 메서드 사용 시 배열의 길리 return
10. 3번
	- 일급함수의 특징
		- 함수를 변수에 할당
		- 함수를 다른 함수의 인자로 전달
		- 함수를 다른 함수의 반환값으로 사용
		- 함수를 배열이나 객체에 저장
11. 필요함 - js 객체를 사용할 때는 키 값 따옴표가 항상 필요하진 않음
12. 4번
	- var는 호이스팅되어 자료형이 undefined로 설정
	- TypeError - 자료형 타입이 예상과 다를 때 발생하는 오류
		- undefined 혹은 null 값을 함수처럼 호출할 때
		- 숫자, 문자열을 함수처럼 호출할 때
		- 객체의 undefined 속성에 접근하려 할 때
		- 객체에 존재하지 않는 메서드를 호출할 때
		- 읽을 수 없는 프로퍼티를 설정하려 할 때
13. 답
	- eval
		- 문자열로 된  js 코드를 실행하는 함수
		- 문자열 -> 코드로 변환해서 실행
		- 외부 입력시 악성 코드가 동작할 위험이 있음
		- js 엔진이 eval 함수를 최적화하지 못함
	- parse
		- 문자열을 특정 형식으로 변환