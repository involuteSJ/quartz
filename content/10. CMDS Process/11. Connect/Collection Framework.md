---
CMDS: Java
type:
  - note
tags:
  - "#Collection"
  - "#List"
  - "#Set"
  - "#Map"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Collection Framework-문제]]"
category: content
---
## Collection Framework
>[!define]
>컴퓨터 과학에서 효율적인 접근 및 수정을 가능케 하는 자료의 조직, 관리, 저장을 의미한다.
- java.util 패키지 - 다수의 데이터를 쉽게 처리하는 방법 제공
- 핵심 Interface
	- list
		- 입력 순서가 있는 데이터의 집합
		- 중복 허락
	- set
		- 입력 순서를 유지하지 않는 데이터의 집합
		- 중복 불가 
	- map
		- key와 value의 쌍으로 데이터를 관리하는 집합
### List
- #### LinkedList
	- 각 요소를 Node로 정의하고 Node는 다음 요소의 참조 값과 데이터로 구성됨
	- 연속적으로 구성될 필요 없음
	- 동적인 데이터 추가, 삭제가 많을 경우 사용
- #### ArrayList
	- 접근 속도가 빠름
	- 순차적 데이터 추가, 삭제가 빠름
	- 비 순차적 데이터 추가, 삭제에 많은 시간 소요
	- 정적인 데이터 활용, 데이터 조회가 많을 경우 사용
- *요소를 제거하는 경우 size가 줄어들기 때문에 반복문 실행시 주의*
### Set
- 입력 순서를 관리하지 않고 데이터를 넣는 형태
- 중복 제거
- 객체의 동일한 데이터 기준
	- equals() 가 true
	- hashCode() 값이 같을 것
- *이를 해결하기 위해 객체의 equals() 와 hashCode() 를 재정의*
```java
@Override
public boolean equals(Object obj) {
	if(obj instanceof SmartPhone s) {
		return this.number.equals(s.number);
	}
	return false;
}

public int hashCode() {
	return this.number.hashCode();
}
```
### Map
- Key와 Value를 하나의 Entry로 묶어서 데이터 관리
	- Key - Object로 중복 불가
	- Value - Object로 중복 허용cc d
- Entry 활용
```java
//Value값으로 Key값을 가져오는 방법
Map<String, String> keys = HashMap<>();
Set<Entry<String, String>> eset = hMap.entrySet();
for(Entry<String, String> e: eset) {
	if(e.getValue().equals("4567")) {
		System.out.println(e.getKey());
		break;
	}
}
```