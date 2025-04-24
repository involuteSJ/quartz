---
CMDS: "[[101 Java]]"
creation date: 2025-04-06 16:30
modification date: 2025-04-06 22:02:17
tags:
  - "#추상클래스"
  - "#인터페이스"
  - "#다중상속"
상위 문서: "[[객체 지향]]"
category: content
---
# Abstraction (추상화)

## 추상 클래스
>[!정의]
>abstract - 상속 전용 클래스
- 구현부가 없는 메소드가 있으므로 객체 생성 불가
- 자식 참조는 가능
- 자식 클래스의 구현 강제를 통해 프로그램의 안전성 향상
- #### 특징
	- 실체가 없는 객체는 추상클래스로 생성
## Interface
- 인터페이스의 일반 메스드는 전부 **abstract class**
- 모든 멤버변수는 **public static final**
- 모든 메서드는 **public abstract**
- Interface는 클래스가 아니기 때문에 Object를 상속받지 않음
- implements를 통해 Interface 상속
	- *Interface의 경우 extends로 다른 인터페이스 상속 가능*
	- *이때 여러 인터페이스로부터 상속 가능*
- 구현하지 않을 경우 abstract 표기
- *default 키워드를 통해 인터페이스에서 여러 메소드 구현 가능*
- *@FunctionalInterface 키워드가 붙을 경우 미구현 메소드는 무조건 하나*
#### 상속
- 다중상속 가능
- class에서 implement 키워드를 통해 상속

#### 필요성
- 구현의 강제로 표준화 처리
- 손쉬운 모듈 교체
- 다형성 확장
- 독립적 프로그래밍 가능

|      Default Method       |    Static Method     |           Private Method            |
| :-----------------------: | :------------------: | :---------------------------------: |
| 인터페이스에 선언된 구현부가 있는 일반 메소드 |      객체가 필요 없음       | 외부 공개가 필요 없는 메서드 지정을 위해 private  추가 |
|  기존 인터페이스에 추가 기능이 필요한 경우  | interface에서 바로 사용 가능 |                                     |

##### Default 메서드의 경우 구현부가 있기 때문에 추가 기능이 필요한 경우 모든 구현체들이 구현해야 하는 현상이 발생
###### => 이를 방지하기 위해 Default 메서드는 반드시 구현할 필요 없음

#### 다중 상속으로 인한 충돌
- Super Class Method 우선 상속
- interface간의 충돌이 발생한 경우 서브클래스는 반드시 해당 메서드에 대한 재정의 필요