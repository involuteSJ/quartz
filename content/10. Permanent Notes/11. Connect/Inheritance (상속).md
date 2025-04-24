---
CMDS: "[[101 Java]]"
creation date: 2025-04-06 16:30
modification date: 2025-04-04 16:52:39
tags:
  - "#Overriding"
  - "#Overloading"
상위 문서: "[[객체 지향]]"
category: content
---
# Inheritance (상속)

>[!정의]
> 하위클래스가 상위클래스의 모든것을 물려받는것

- extends 선언을 통해 사용
- 모든 클래스는 Object 클래스를 extends를 해서 사용하고 있음
- 단일 상속만 지원 -> 다중 상속의 경우 Interface에서 사용
- 두개 이상의 특성을 가져올 때 하나는 상속, 하나는 멤버 변수로 처리
- Java에서 동적바인딩만 지원
- 기능 확장, 재정의, reference 데이터의 형변환을 할때 사용

#### Overriding
>
>   조상 클래스에서 정의된 메서드를 자식 클래스에서 적합하게 수정
>
- *상위 클래스 메서드 재정의*

##### 조건
1. 메서드 이름이 같아야 함
2. 매개 변수의 개수, 타입, 순서가 같아야 함
3. 리턴 타입이 동일해야함
4. 접근 제한자는 부모보다 범위가 넓거나 같아야 함
5. 조상보다 더 큰 예외는 던질 수 없음

#### Overloading
>
>  부모 클래스의 메서드 매개변수 유형과 개수만 다른 메서드
>
- *이름이 같지만 매개변수가 다른 여러 메서드를 정의*

```java
class parent{
	void phone(String name) {
		System.out.println(name + "의 휴대폰을 가지고 있음");
	}
}

class son extends parent {
	// 메서드 오버라이딩
	void phone(String name) {
		System.out.println(name + " 휴대폰을 아빠가 사줌");
	}
	//메서드 오버로딩
	void phone(String name, int year) {
		System.out.println(year + "년 동안 사용해야하는 "+name+" 휴대폰을 아빠가 사줌");
	}
}
```
