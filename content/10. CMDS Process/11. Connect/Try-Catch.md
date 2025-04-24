---
CMDS: Java
type:
  - note
tags:
  - "#Try_Catch"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Try-Catch-문제]]"
category: content
---
## Try-Catch
<center><i>try 구문에 예외가 발생할 수 있는 코드를 넣고<br>
catch에 예외가 발생할 경우 처리하는 코드 작성</i></center>

- #### Throwable의 주요 메서드
	- public String getMessage()
		- 구체적인 메세지 반환
	- public Throwable getCause()
		- 예외의 원인이 되는 Throwable 혹은 Null 반환
	- public void printStackTrace()
		- 예외 메서드가 호출되기까지의 메서드 호출 스택 출력
- #### 흐름
	- 예외가 발생하면
		- JVM이 Exception 클래스 객체 생성 후 던짐
		- 던져진 exception을 catch 블록에서 받은 후 처리
		- 이후 다음 문장 진행
	- 발생하지 않으면
		- catch를 거치지 않고 다음 문장 진행
- #### Checked Exception
	- 처리하지 않으면 컴파일 불가
	- 예외 발생 시 어떻게 할 것인가
- #### 다중 exception handling
	- try 블록에서 여러 종류의 예외가 발생할 경우
		- try블록에 여러 catch구문 추가 가능
		- 상위 타입의 예외가 먼저 선언되면 뒤 catch블록은 동작 안함
```java
try {
	//exception 발생
} catch(XXException e) {
	//XXException 발생 시 처리
} catch(YYException e) {
	//YYException 발생 시 처리
} catch(Exception e) {
	//Exception 발생 시 처리
}
// 아래의 경우 Exception 만 처리 후 종료
try {
	//exception 발생
} catch(Exception e) {
	//Exception 발생 시 처리
} catch(YYException e) {
	//YYException 발생 시 처리
} catch(XXException e) {
	//XXException 발생 시 처리
}
```
- #### 다중 예외 처리를 이용한 Checked Exception 처리
	- 예외들을 하나로 처리
	- 심각하지 않은 예외는 묶어서 처리
```java
try {
	//실행
} catch(ClassNotFoundException | FileNotFoundException e){
	//'|'를 이용해 상속관계가 없는 여러 예외처리
}
```