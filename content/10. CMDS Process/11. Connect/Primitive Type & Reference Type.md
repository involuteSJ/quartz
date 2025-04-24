---
CMDS: Algorithm
tags:
  - "#epsilon"
  - "#배열"
  - "#리스트"
  - "#해시맵"
  - "#문자열"
  - StringBuilder
  - StringBuffer
  - Method
date modified: 
관련 문서:
  - "[[103.01 Basic Concepts]]"
category: content
---
## Primitive Type & Reference Type

|        Primitive Type         |        Reference Type         |
|:-----------------------------:|:-----------------------------:|
|           `int i=0`           |         `Integer I=0`         |
| `long[] longs = new long[10]` | `Long[] Longs = new Long[10]` |
|       `float f = 10.5f`       |       `Float F = 10.5f`       |
|      `double d = 10/3.0`      |      `Double D = 10/3.0`      |

#### Epsilon
>[!tip]
>부동소수형 데이터를 이진법으로 표현할 때 생기는 오류

```java
double epsilon = 1E-5;
double a = 0.1 + 0.2;
double b = 0.3;

if(Math.abs(a-b) < epsilon) {
	System.out.println("a, b는 같은 값");
}
```

## Collection Framework
#### Array
- 길이 고정
- 배열 접근, 변경의 시간복잡도 O(1)

```java
// stack 영역에 저장
int[] array;

// heap 영역에 저장
// 0으로 자동 초기화
array = new int[5];

// 출력
System.out.println(Arrays.toString(array));
```

#### ArrayList
- 가변 크기로 되어 있어 새 데이터를 중간에 삽입 가능
- 데이터를 맨 뒤에 삽입할 경우 시간복잡도 O(1)
- 데이터를 중간에 삽입할 경우 시간복잡도 O(N)

```java
ArrayList<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);

// 출력 : [1, 2]
System.out.println(list)
```

#### HashMap
- 키와 값을 저장하는 해시 테이블


```java
HashMap<String, Integer> map = new HashMap<>();

// 삽입(수정)과 출력
map.put("apple", 1);
map.put("banana", 2);
map.put("Orange", 3);

// 검색
if(map.containsKey("apple")) {
	int value = map.get("apple");
	System.out.println(key + ": " + value);
}

// 삭제
map.remove("Orange");
```

#### String
- Immutable 객체 -> 값 변경 불가능
- 문자열을 + 연산을 할 경우 기존 주소를 끊기 새로운 주소로 변경

#### StringBuilder & StringBuffer
- String의 단점을 보완하기 위해 StringBuilder 혹은 StringBuffer 사용
- 이 둘의 차이는 멀티쓰레드 환경에서 Thread-Safe 여부로 갈림

```java
StringBuilder sb = new StringBuilder();

sb.append(10);
ab.append("ABC");

// 10ABC
System.out.println(sb);
sb.deleteCharAt(3);
// 10AC
System.out.println(sb);
sb.insert(1,2);
//120AC
System.out.println(sb);
```

## Method
>[!tips]
>클래스 내에서 정의된 함수

- 람다식

```java
private static class Node {
	int dest, cost;
	
	public Node(int dest, int cost) {
		this.dest = dest;
		this.cost = cost;
	}
}

public static void main(String[] args) {
	Node[] nodes = new Node[5];
	node[0] = new Node(1, 10);
	node[1] = new Node(2, 20);
	node[2] = new Node(3, 15);
	node[3] = new Node(4, 5);
	node[4] = new Node(1, 25);
	// lamda
	Arrays.sort(nodes, (o1, o2) -> Integer.compare(o1.cost, o2.cost));
	
	Arrays.sort(nodes, new Comparator<Node>() {
		@Override
		public int compare(Node o1, Node o2) {
			return Integer.compare(o1.cost, o2.cost);
		}
	})
}
```