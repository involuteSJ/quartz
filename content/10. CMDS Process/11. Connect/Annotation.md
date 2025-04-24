---
CMDS: Java
type:
  - note
tags:
  - "#Annotation"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Annotation-문제]]"
category: content
---
## Annotation
>[!tips]
>컴파일러, JVM, 프레임워크 등이 보는 주석으로 소스코드에 메타 데이터를 삽입하는 형태

- @Deprecated
	- 컴파일러에게 해당 메서드가 deprecated 되었다고 알려줌
- @Override
	- 컴파일러에게 해당 메서드가 override한 메서드 임을 알려줌
- @SuppressWarning
	- 사소한 오류는 신경쓰지 말라고 알려줌

#### Annotation 분석
- 선언
	- interface 선언과 유사하게 @interface 사용
- 구성
	- @Target, @Retention 등 메타 에너테이션

#### 메타 에너테이션
> 에너테이션 설정을 위한 에너테이션
- @Document : JavaDoc을 만들 때 이 에너테이션이 문서에 포함되어야 함
- @Inherited: 에너테이션이 하위 클래스에 상속
- @Repeatable: 해당 에너테이션이 반복해서 적용될 수 있는지 표시
- @Retention: 얼마나 오래 에너테이션 정보를 유지할 것인가?
	- SOURCE: 클래스 파일 안에는 포함되지 않음
	- CLASS: 클래스 안에 포함, 리플렉션시 정보를 얻을 수 없음
	- RUNTIME: 컴파일 시 포함되고 리플렉션 시 정보를 얻을 수 있음
- @Target: 에너테이션을 어디에 사용할 수 있는가?
	- TYPE
	- FIELD
	- METHOD
	- PARAMETER
	- CONSTRUCTOR
	- LOCAL_VARIABLE
	- ANNOTATION_TYPE
	- PACKAGE

#### 속성
- 추상 메서드처럼 쓰고 일반 속성처럼 키=값 으로 사용
- 설정하는 속성이 value 하나인 경우 생략 가능
- 배열은 {}를 사용하는데 길이기 1이면 생략 가능
- 속성은 default 값을 가질 수 있으며 이 경우 속성을 설정 생략 가능