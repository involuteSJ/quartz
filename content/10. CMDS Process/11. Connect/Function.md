---
CMDS: Frontend
type:
  - note
tags:
  - "#JavaScript"
관련 문서:
  - "[[104 WEB]]"
---
## Function
Function literal
```javascript
function function_name(parameter_name, ...) {
	...
	return value;
}
```

- parameter
	- 전달받을 인자로 이름만 표시하며 local 변수 취급
	- 변수 선언 지시어 사용x
	- 파라미터 개수와 실제 내부에서 사용되는 변수의 개수가 다를 수 있음
		- 
- return
	- function의 종료
	- return 타입 명시 x

#### 함수의 정의
- function 선언을 이용한 정의 - hoisting의 대상
```javascript
function add(x, y) {
	return x+y;
};
```
- 리터럴을 이용한 표현식 -anonymous function
	- 바로 변수에 할당하거나 파라미터로 전달
```javascript
let minus = function(x, y) {
	return x-y;
};
```
- function 생성자 사용 - function도 객체로 취급
```javascript
let multi = new Function("x", "y", "return x*y");
console.log(multi(3,4));
```
- arrow function : 함수를 간략하게 표시 - lambda와 유사
```javascript
let arrowFunc = (p1, p2)=>{
	return p1 + p2;
};
```

#### 함수 호이스팅
- 변수 선언 시 **자신이 해당하는 scope의 최상단**으로 이동
	- **변수 선언 x** -> global 함수의 최상단
	- **var** -> 해당 변수가 포함된 함수의 최상단
	- let -> 이동 안함
- 함수도 마찬가지로 자신이 속한 함수의 최상단으로 이동
- **파싱** - 프로그램 전역 레벨에서의 파싱
	 - 어떤 함수에도 포함되지 않은 var변수를 undefined로 초기화
	 - 전역레벨 함수에 대해 함수명으로 변수 생성 후 함수에 대한 참조로 초기화
- **실행** - 실행문을 실행하다가 함수 호출을 만나면 함수 레벨의 파싱 반복

#### this
- js에서 this는 해당 객체를 실행하는 함수의 변수를 의미

- 함수의 인자로 함수 사용 가능
```javascript
function c() {
	console.log("function c");
}

var a = function(b) {
	b();
}

a(c);

function fa(arg) {
	arg();
	var r = function() {
		console.log("inner r function");
	}
	var r2 = function() {
		console.log("inner r2 function");
	}
	return {
		aa : r,
		bb : r2
	};
}

var res = fa(c);
res.aa();
res.bb();

function ff() {
	console.log("function ff");
	var b = function(f) {
		console.log("function b");
		f();
	}
	return b;
}

var bb() = function() {
	console.log("function bb");
}

var cc = ff();
cc(bb);
```

#### closure
- 함수가 끝나더라도 내부에 인스턴스가 남아있으면 함수 종료 후에도 지역변수가 사라지지 않음
```javascript
function make(a) {
	return function(b) {
		return a+b;
	}
}

var x = make(5);
var y = make(20);

//함수가 끝나면 지역변수가 없어져야 하는데 
console.log(x(6))
```

#### callback function
- **다른 함수에 인자로 전달**되어 **특정 조건에 호출**되는 function
- 배열에 sort 적용