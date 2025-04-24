---
CMDS: B형 특강
상위 문서: "[[B형 특강]]"
category: content
---
## 다른 언어에서 어떤 문법과 매칭되는가

|                |         **C++**          |                               **JAVA**                                |               **Python**               |
| :------------: | :----------------------: | :-------------------------------------------------------------------: | :------------------------------------: |
|   ArrayList    |          Vector          |                               ArrayList                               |                  List                  |
|     Deque      |          deque           |                    import java.util.Deque<br>deque                    | from collections import deque<br>deque |
|      List      |          직접 구현           |                                   <                                   |                   <                    |
|      set       |         std::set         |                  import java.util.TreeSet<br>TreeSet                  |                   X                    |
|    HashSet     |    std::unordered_set    |                  import java.util.HashSet<br>HashSet                  |                  set                   |
|     Stack      | std::stack<br>std::queue | import java.util.Queue<br>import java.util.LinkedList<br>stack, queue |     stack : \[\]<br>queue : deque      |
| Priority Queue |   std::priority_queue    |                    import java.util.PriorityQueue                     |              import heapq              |

## vector 구현
- 동적할당
- 배열에서 Random Access[^1]를 하기 위해서는 연속적으로 존재해야 함
- #### 분할상환기법
	- 기존 배열에서 추가 용량이 필요할 경우 필요 용량만큼 추가해서 재할당
		- 사용자가 계속 추가할 경우 계속 재할당 해줘야 하는 불필요한 작업 필요
		- 이를 해결하기 위해 기존 용량의 1.5(java) 만큼 크게 만들어서 할당
	- 81번의 append가 일어나는 동안 총 연산 수
		- 1 \* 81 == N
		- 1 + 20 + 40 < N
		- 80 < N
	- N번 append하는 경우 총 연산 수 : O(N)
	- N번 append의 총 연산 : O(N)
	- 한번이 O(1)처럼 작동
	- append의 시간 복잡도 : amortized O(1)
	- n번 작업 총량을 하나하나에 나눠봤을 때 시간복잡도 : amortized O(??) 


[^1]: 특정 레코드를 찾을 때 다른 레코드를 순차적으로 읽지 않고 원하는 레코드만을 집접 엑세스 하는 방법