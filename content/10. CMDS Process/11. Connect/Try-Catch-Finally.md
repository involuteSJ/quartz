---
CMDS: Java
type:
  - note
tags:
  - "#Try_Catch_Finally"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Try-Catch-Finally-문제]]"
category: content
---
## Try-Catch-Finally
*finally는 예외 발생 여부와 상관 없이 언제나 실행*
- 중간에 return을 만나는 경우도 finally 블록을 먼저 수행 후 리턴 실행
- #### Finally 블록을 사용하는 이유
	- try 블록에서 사용한 리소스 반납
	- finally 구문에서 close를 통한 자원 반납
- #### 단점
	- close 메서드 자체가 IOException 유발 가능
	- finally 구문 내에 다른 try-catch문이 들어가게 됨
- #### try-with-resources
	- 리소스의 자동 close처리
	- try로 선언된 객체들에 대해 자동 close 호출
	- final 변수로 간주되기 때문에 재할당 불가
	- 하나 이상의 catch, finally가 필요
	- rollback이 필요한 경우 사용하면 안됨
```java
public void useStreamNewStyle() {
	try(FileInputStream fileInput = new FileInputStream("abc.txt")) {
		System.out.println("파일 생성")
		fileInput.read();
	} catch(IOException e) {
		System.out.println("파일 처리 실패");
	}
}
```
