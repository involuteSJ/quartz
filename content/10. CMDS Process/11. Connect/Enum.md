---
CMDS: Java
type:
  - note
tags:
  - "#Enum"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Enum-문제]]"
category: content
---
## Enum
>[!tips]
>열거형 데이터 타입
>>*값 뿐만 아니라 타입 체크 가능 -> 논리적 오류 방지*

- 데이터가 몇 가지 한정된 값만을 갖는 형태로 구성되는 경우
- java.lang.Enum을 내부적으로 상속 받는 형태의 특별한 클래스
- 클래스와 동일하게 선언하며 할당될 수 있는 값은 enum상수, null로 한정

#### Enum의 주요 메서드
- public final String name()
	- enum 상수의 이름을 문자열 리턴
- public final int ordinal()
	- enum 상수의 순서로 0부터 시작함
- public final int compareTo()
	- enum 상수의 ordinal 차이 리턴
- public static T \[ \] values()
	- Enum 타입에 선언된 enum 상수를 배열로 리턴
- public static T valueOf(String name)
	- 문자열에 매핑 된 enum 상수 객체 리턴