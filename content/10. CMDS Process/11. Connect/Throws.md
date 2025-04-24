---
CMDS: Java
type:
  - note
tags:
  - "#Throws"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Throws-문제]]"
category: content
---
## Throws
- #### throws 키워드를 통한 처리 위임
	- 메서드에서 처리해야 할 예외를 호출한곳으로 전달
- #### checked exception과 throws
	- checked exception은 반드시 try-catch 또는 throws 필요
	- 필요한 곳에서 try-catch 처리
- #### runtime exception 과 throws
	- runtime exception은 throws 하지 않아도 전달
	- 마지막에는 try-catch 처리 필요
- #### printStackTrace를 통해 확인해야 할 정보
	- 예외 종류
	- 예외 원인
	- 디버깅 출발점
- #### 목적
	- API가 제공하는 메서드들은 예외가 발생할 수 있다고 명시하고 프로그래머가 이에 대처 하도록 강요
- #### 메서드 재정의와 throws
	- 메서드 재정의 시 부모가 던지는 예외보다 더 큰 예외는 던질 수 없음
- #### 예외 변환
	- 하위 계층에서 발생한 예외는 상위 계층에 맞는 예외로 던져야 함