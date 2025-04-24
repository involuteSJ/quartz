---
CMDS: Java
type:
  - note
tags:
  - "#Generic"
상위 문서: "[[101.01 Object-Oriented Concepts]]"
---
## Generics
>[!tips]
> 타입에 대한 안전성을 유지하기 위해 사용

- 클래스, 인터페이스 선언 시 <> 에 타입 파라미터 표시
- 형인자 : 임의의 참조형 타입을 말하며 성격에 따라 선언
	- *T : reference Type*
	- *E : Element*
	- *K : Key*
	- *V : Value*
- 변수 쪽과 생성 쪽의 타입은 반드시 같아야 함 (상속 관계 X)

##### 주의사항
- 타입 파라미터는 인스턴스 레벨에서 결정
	- static 멤버에서는 사용할 수 없음
- Generic은 컴파일 타입에 지정한 타입으로 존재
	- 런타임에는 타입 정보 소거
	- runtime에게 타입 파리미터를 알려주지 않고 요소의 추가 제거가 자유로움
	- runtime에 동작하는 new, instanceof 키워드 사용 불가
- Generic을 이용한 배열 생성 불가

#### Generic Method
- 파라미터와 리턴타입으로 type parameter를 갖는 메서드
	- 메서드 리턴 타입 앞에 타입 파라미터 변수 선언
```java
public class TypeParameterMethodTest<T> {
	T some;
	public TypeParameterMethodTest(T some) {
		this.some = some;
	}
	public <P> void mehtod1(P p) {
		System.out.printf("클래스 레벨의 T: %s%n", some.getClass().getSimpleName());
		System.out.printf("파라미터 레벨의 P: %s%n", p.getClass().getSimpleName());
	}
}
```

#### 한정된 형인자
- 필요에 따라 구체적인 타입 제한 필요
	- `class NumberBox<T extends Number>`

#### 와일드 카드(?) 자료형
- 실제 type parameter가 무엇인지 모르거나 신경 쓰고싶지 않을 경우
	- Generic type - \<?\>
		- set - 불가
		- get - Object 형으로 받을 수 있음
	- Generic type - \<? extends Person\>
		- set - 불가
		- get - Person 형으로 받을 수 있음
	- Generic type - \<? super Person\>
		- set - Person 자식은 저장 가능
		- get - 불가
- PECS
	- Producer Extends: 제네릭 타입이 데이터를 생산하여 외부로 제공하는 역할
	- Consumer Super : 제네릭 타입이 데이터를 쓰는 역할(추가, 수정)
```java
void useWildCardType2(GenericBox<? extends Person> boxExtendsPerson) {

}

void useWildCardType3(GenericBox<? super person> boxSuperPerson) {

}

public class Collections {
	public static <T> void copy(List<? super T> dest, List<? extends T> src) {
}
}
```