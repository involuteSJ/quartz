---
CMDS: Java
type:
  - note
tags:
  - "#Enum"
상위 문서: "[[Enum]]"
---

## Enum 관련 문제

1. Enum의 객체는 어떤 클래스에서 상속되나요?
	1. A) java.lang.Object
	2. B) java.lang.Enum
	3. C) java.lang.Class
	4. D) java.lang.String

2. Enum의 상수를 정의할 때 일반적으로 사용하는 구문은 무엇인가?
	1. A) enum constant;
	2. B) enum { constant1, constant2 };
	3. C) const enum { constant1, constant2 };
	4. D) enum constant1, constant2;

3. 다음 코드의 출력 결과는 무엇일까요?
   ```java
   enum Size {
       SMALL, MEDIUM, LARGE
   }
   System.out.println(Size.MEDIUM.ordinal());
   ```
	1. A) 0
	2. B) 1
	3. C) 2
	4. D) 오류가 발생한다

## 정답
1. B) java.lang.Enum  
2. B) enum { constant1, constant2 };  
3. B) 1  
