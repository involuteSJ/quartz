---
CMDS: CodingTest
creation date: 2025-04-09 17:41
modification date: 2025-04-09 17:41:47
Algorithm Site: BOJ
tags:
  - "#CodingTest"
관련 문서:
  - "[[103.02 Related Problems]]"
문제 링크:
  - https://www.acmicpc.net/problem/13023
category: coding_test
---

# \[BOJ]13023 - ABCDE

## 문제 분석

BOJ 알고리즘 캠프에는 총 N명이 참가하고 있다. 사람들은 0번부터 N-1번으로 번호가 매겨져 있고, 일부 사람들은 친구이다.

오늘은 다음과 같은 친구 관계를 가진 사람 A, B, C, D, E가 존재하는지 구해보려고 한다.

- A는 B와 친구다.
- B는 C와 친구다.
- C는 D와 친구다.
- D는 E와 친구다.

위와 같은 친구 관계가 존재하는지 안하는지 구하는 프로그램을 작성하시오.

## 문제 해결 아이디어
depth == 5 조건을 만족하면 1 출력후 프로그램 종료
dfs + 백트래킹 사용

## 코드
```java
import java.util.*;
import java.io.*;

public class Main {
	static ArrayList<Integer>[] f;
	static int[] cnt;
	static boolean[] v;
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());

		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		
		f = new ArrayList[N];
		
		for(int i=0; i<N; i++) {
			f[i] = new ArrayList<>();
		}
		for(int i=0; i<M; i++) {
			st = new StringTokenizer(br.readLine());
			int sn = Integer.parseInt(st.nextToken());
			int en = Integer.parseInt(st.nextToken());
			
			f[sn].add(en);
			f[en].add(sn);
		}
		
		for(int i=0; i<N; i++) {
			cnt = new int[N];
			v = new boolean[N];
			v[i] = true;
			dfs(i,0);
		}
		
		System.out.println(0);
	}
	
	static void dfs(int n, int idx) {
		if(idx>=4) {
			System.out.println(1);
			System.exit(0);
		}
		
		for(int i=0; i<f[n].size(); i++) {
			int tmp = f[n].get(i);
			if(!v[tmp]) {
				v[tmp] = true;
				dfs(tmp, idx+1);
				v[tmp] = false;
			}
		}
	}
}
```

## 시간 복잡도


## 느낀점
메모이제이션 사용하면 탐색을 안하는 구간이 생기기 때문에 dp로 해결 불가