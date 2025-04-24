---
CMDS: Java
type:
  - note
tags:
  - "#Sort"
  - "#Comparable"
  - "#Comparator"
  - "#Algorithm"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Java Sort-문제]]"
category: content
---
## Sort
- 요소를 **특정 기준**에 대해 내림차순, 오름차순으로 배치하는 것
- 크기를 비교할 수 있는 요소를 가지는 Collection들만 정렬 가능
- **특정 기준**을 정하는 방법
```java
public class SmartPhone implements Comparable<SmartPhone>{
	...
	/*
	* 양수 : 자리 바꿈
	* 음수 : 자리 유지
	* 0 : 동일 위치
	*/
	@Override
	public int compareTo(SmartPhone o) {
		return this.number.compareTo(o.number);
	} 
}
```
- #### Comparable interface
	- *문자열은 사전순, 숫자는 크기순 처럼 자연스러운 순서를 정의*
	- 정렬 대상 클래스의 내부에서 Comparable 인터페이스를 구현
	- compareTo(T o) 를 오버라이드하여 자기자신과 다른 객체 비교
	- 사전에 비교 가능한 기준이 있으면 그것들을 재사용하기
```java
public class SmartPhone implements Comparable<SmartPhone>{
	String number;
	...
	@Override
	public int compareTo(SmartPhone o) {
		return this.number.compareTo(o.number);
	}
}
```
- #### comparator 의 활용
	- *사용자 정의 정렬, 다중 정렬 기준 지원*
		- Employee -> salary 혹은 name 정렬
	- 별도의 클래스나 익명 클래스로 구현 -> 기존 클래스 수정 없음
	- compare(T o1, T o2) 를 오버라이드하여 객체 비교
	- 객체가 Comparable을 구현하고 있지 않거나 사용자 정의 알고리즘으로 정렬하려는 경우
```java
public class StringLengthComparator implements Comparator<String> {
	@Override
	public int compare(String o1, String o2) {
		int len1 = o1.length();
		int len2 = o2.length();
		return Integer.compare(len1, len2);
	}
}
```