---
CMDS: Java
type:
  - note
tags:
  - "#Stream"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[Stream API-문제]]"
category: content
---
## Stream API
>[!tips]
>배열 및 Collection의 요소를 하나씩 참조해서 처리하는 목적

- #### Stream API의 역할 및 특징
	- 컬렉션, 배열 등 데이터 소스에 대한 공통된 접근 방식 제공
	- 손쉬운 병렬 처리
		- set.stream().forEach\( System.out :: println \); - 순차처리
		- set.parallelStream().forEach\(System.out::println\); - 병렬처리
- #### 맵/ 리듀스 모델 지원
	- 맵 : 데이터를 작은 단위로 나누어 지정된 함수를 적용 처리
	- 리듀스 : 결과를 모아서 최종 결과를 생성
	- 중간 처리와 최종 처리를 조합
		- 중간 처리 : 매핑, 필터링, 정렬 등 가공처리
		- 최종 처리 : 반복, 카운팅, 평균, 총합 등의 집계 처리
	- 각각의 중간 처리는 새로운 스트림을 리턴하여 builder 패턴 적용
	- 최종 처리는 최종적으로 원하는 값을 반환
- #### Stream의 자료 처리
	- ![[stream]]
	- 중간 처리
		- 필터링
			- distinct() - 중복 제거 스트림 리턴
			- filter() - predicate의 test() 가 true인 값들만 리턴
		- 자르기
			- limit() - 중복 제거 스트림 리턴
			- skip() - predicate의 test() 가 true인 값들만 리턴
		- 정렬
			- sorted() - 정렬된 스트림 리턴
		- 매핑 - 스트림의 요소를 다른 요소로 대체
			- map() - 원본과 변환이 1:1 매칭
			- mapToP()
			- flatMap() - 원본과 변환이 1:n 매칭
			- flatMapToP()
		- 조회 - 중간 처리 과정에서 현재 요소의 상태를 확인
			- peek() - T와 1:1로 대응되는 새로운 스트림 리턴
	- 최종 처리
		- 반복
			- forEach() - 각 요소에 대해 action 수행
		- 집계
			- count - stream내 요소 개수 리턴
			- p sum()
			- 요소들의 총 합 리턴
```java
words.stream()
	.limit(5)
	.forEach(System.out::println);
//1. words에서 단어의 길이가 5이상인 단어의 개수는?
words.stream()
	.filter(item->item.length()>=5)
	.count();
//2. '오'가 들어가는 단어 중 처음 4개를 생략하고 2개를 출력
words.stream()
	.filter(item->item.contains("오"))
	.skip(4)
	.limit(2)
	.forEach(System.out::println);
//3. 0~100 까지의 정수에서 짝수의 합
IntStream
	.rangeClosed(0, 100)
	.filter(item->item%2==0)
	.sum();
```

## 예시
#### Array Stream
```java
Stream<String> stream = Arrays.stream(new String[] {"A", "B", "C"});
stream.foreach(System.out::println);

IntStream intStream = Arrays.stream(new int[] {1, 2, 3});
intStream.forEach(System.out::println);

LongStream longStream = Arrays.stream(new long[] {1, 2, 3});
longStream.forEach(System.out::println);

DoubleStream doubleStream = Arrays.stream(new double[] {1, 2, 3});
doubleStream.forEach(System.out::println);
```

#### Stream
```java
Stream<String> stream = Stream.of(new String[] {"A", "B", "C"});
stream.forEach(v->System.out.println(v));

IntStream intStream = IntStream.of(new int[] {1, 2, 3});
intStream.forEach(v->System.out.println(v));

LongStream longStream = LongStream.of(new long[] {1, 2, 3});
longStream.forEach(v->System.out.println(v));

DoubleStream doubleStream = DoubleStream.of(new double[] {1, 2, 3});
doubleStream.forEach(v->System.out.println(v));
```

#### Collection
```java
List<String> list1 = Arrays.asList("A", "B", "C");
Stream<String> stream1 = list1.stream();
stream1.forEach(System.out::println);

List<Integer> list2 = Arrays.asList(1, 2, 3);
Stream<Integer> stream2 = list1.stream();
stream1.forEach(System.out::println);
```

#### ETC
```java
Stream<Integer> stream = Stream.generate(() -> new Random().nextInt(10)).limit(5);
stream.forEach(System.out::println);

IntStream stream = IntStream.generate(() -> new Random().nextInt(10)).limit(5);
stream.forEach(System.out::println);

Stream<String> stream = Stream.iterate("a", s -> s + 1).limit(5);
stream.forEach(System.out::println);

IntStream stream = IntStream.iterate(1, s -> s + 2).limit(5);
stream.forEach(System.out::println);

IntStream stream = IntStream.range(1, 10);
stream.forEach(System.out::println);

IntStream stream = IntStream.rangeClosed(1, 10);
stream.forEach(System.out::println);
```
