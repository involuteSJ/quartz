---
CMDS: Algorithm
관련 문서:
  - "[[Algorithm Concepts]]"
tags:
  - "#BFS"
  - "#Algorithm"
category: content
---

## BFS

<center><i><b>B</b>readth <b>F</b>irst <b>S</b>earch</i></center>

- 너비 우선 탐색
- 자식 노드와 그 노드의 형제 노드부터 탐색하는 방식

#### 동작 방식
```
// 트리
BFS()
	큐 생성
	루트 v를 큐에 삽입
	while(큐가 비어있지 않으면) {
		t <- 큐 첫번째 원소 반환
		t 방문
		for(t와 연결된 모든 간선에 대해) {
			u <- t의 자식노드
			u를 큐에 삽
		}
	}
end BFS()

//그래프
BFS(v) // v : 탐색 시작 정점
	큐 생성
	방문관리 배열 생성
	시작 정점 v를 큐에 삽입
	정점 v를 방문한 것으로 표시
	while(큐가 비어있지 않으면) {
		t <- 큐 첫번째 원소 반환
		for(t와 연결된 모든 간선에 대해) {
			u <- t의 인접 정점
			u가 방문되지 않은 곳이면
			u를 큐에 넣고 방문 표시
		}
	}
end BFS()
```
#### 구현
```java
import java.util.*;
import java.io.*;

//완전 이진 트리
public class CompleteBinaryTree<T> {
	private Object[] nodes;
	private final int MAX_SIZE;
	private int lastIndex;
	public CompleteBinaryTree(int size) {
		this.MAX_SIZE = size;
		nodes = new Object[size+1];
	}

	public boolean isEmpty() {
		return lastIndex==0;
	}

	public boolean isFull() {
		return lastIndex == MAX_SIZE;
	}

	public void add(T e) {
		if(isFull()) throw new RuntimeException("트리 포화 상태");
		nodes[++lastIndex] = e;
	}

	public void bfs() {
		if(isEmpty()) throw new RuntimeException("빈 트리 상태입니다.");
		Queue<Integer> queue = new ArrayDeque<>();
		queue.offer(1);
		
		while(!queue.isEmpty()) {
			int current = queue.poll();
			System.out.println(nodes[current]);

			if(current*2<=lastIndex) queue.offer(current*2);
			if(current*2+1<=lastIndex) queue.offer(current*2+1);
		}
	}

	public static void main(String[] args) {
		int[] num = [1,2,3,4,5,6];
		int size = num.length;
		CompleteBinaryTree<Integer> tree = new CompleteBinaryTree<>(size);

		for(int num:nums) {
			tree.add(name);
		}	

		tree.bfs();
	}
}
```