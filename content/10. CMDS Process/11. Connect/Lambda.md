---
CMDS: Java
type:
  - note
tags:
  - "#Lambda"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Lambda-문제]]"
category: content
---
## Lambda
>[!tips]
>함수적 프로그래밍의 형태로 재사용 가능한 코드 블록

- 기존의 anonymous inner class를 이용한 처리 방식을 간결하게 처리
- 필요없는 부분을 줄이기 위해 만들어진 표현 방식

- #### 타겟 타입
	- Lambda 식이 할당되는 인터페이스를 Lambda 식의 타겟 타입이라 함
	- 타겟 타입은 abstract 메서드가 반드시 하나만 존재해야 함
- #### @FunctionalInterface
	- 컴파일러가 재정의해야 하는 abstract method가 하나만 있음
	- abstract method가 2개 이상 존재하는 경우 익명의 inner class 사용
- #### @FunctionalInterface 구현체 작성법
	- (type variable_name\[...\]) -> {실행문}
	- 선언된 변수를 이용해서 실행문을 실행
	- 매개변수 부분은 실행문 블록에서 사용하기 위한 값 제공
	- 매개변수 타입은 런타임 시 자동 인식되므로 생략 가능
	- 매개변수 및 실행문이 하나일 때는 괄호 생략 가능
	- return 이 필요한 경우 사용
	- 리턴문만 있을 경우 중괄호와 return 생략 가능

```java
interface Printer {
	void print(String str);
}
public class Lambda01 {
	// 대충 printer 구현한 내용
	...
	p = (String s)->{
		System.out.println(s);
	}
	p = (String s)->System.out.println(s);
	p = (s)->System.out.println(s);
	p = s->System.out.println(s);
}
```
- #### 실행 블록에서의 변수 참조
	- Lambda 식 내부에서의 this는 외부 클래스의 instance
	- 외부 클래스의 member 변수 - 접근제한자 제약 없이 사용 가능
	- 외부 메서드의 local 변수 - final  키워드가 추가된 것으로 동작 ->read only
- ##### 객체지향 프로그래밍
	- 클래스, 메서드 이름, 구조가 중요
- ##### 함수형 프로그래밍
	- 함수의 형태는 구조적이며 이름이 불필요