---
CMDS: CodingTest
creation date: 2025-04-18 16:30
modification date: 2025-04-18 16:30:18
Algorithm Site: BOJ
tags:
  - "#CodingTest"
관련 문서:
  - "[[103.02 Related Problems]]"
문제 링크:
  - https://www.acmicpc.net/problem/1005
category: coding_test
---

# \[BOJ]1005 - ACM Craft

## 문제 분석

서기 2012년! 드디어 2년간 수많은 국민들을 기다리게 한 게임 ACM Craft (Association of Construction Manager Craft)가 발매되었다.

이 게임은 지금까지 나온 게임들과는 다르게 ACM크래프트는 다이나믹한 게임 진행을 위해 건물을 짓는 순서가 정해져 있지 않다. 즉, 첫 번째 게임과 두 번째 게임이 건물을 짓는 순서가 다를 수도 있다. 매 게임시작 시 건물을 짓는 순서가 주어진다. 또한 모든 건물은 각각 건설을 시작하여 완성이 될 때까지 Delay가 존재한다.

![](https://www.acmicpc.net/upload/201003/star.JPG)

위의 예시를 보자.

이번 게임에서는 다음과 같이 건설 순서 규칙이 주어졌다. 1번 건물의 건설이 완료된다면 2번과 3번의 건설을 시작할수 있다. (동시에 진행이 가능하다) 그리고 4번 건물을 짓기 위해서는 2번과 3번 건물이 모두 건설 완료되어야지만 4번건물의 건설을 시작할수 있다.

따라서 4번건물의 건설을 완료하기 위해서는 우선 처음 1번 건물을 건설하는데 10초가 소요된다. 그리고 2번 건물과 3번 건물을 동시에 건설하기 시작하면 2번은 1초뒤에 건설이 완료되지만 아직 3번 건물이 완료되지 않았으므로 4번 건물을 건설할 수 없다. 3번 건물이 완성되고 나면 그때 4번 건물을 지을수 있으므로 4번 건물이 완성되기까지는 총 120초가 소요된다.

프로게이머 최백준은 애인과의 데이트 비용을 마련하기 위해 서강대학교배 ACM크래프트 대회에 참가했다! 최백준은 화려한 컨트롤 실력을 가지고 있기 때문에 모든 경기에서 특정 건물만 짓는다면 무조건 게임에서 이길 수 있다. 그러나 매 게임마다 특정건물을 짓기 위한 순서가 달라지므로 최백준은 좌절하고 있었다. 백준이를 위해 특정건물을 가장 빨리 지을 때까지 걸리는 최소시간을 알아내는 프로그램을 작성해주자.

## 문제 해결 아이디어
- 위상 정렬을 이용하여 이전 건물과 현재 건물을 더한 값과 기존 값중 큰 값을 저장

## 코드
```java
import java.util.*;
import java.io.*;

class Build {
	ArrayList<Integer> n;
	int time;
	Build(int time) {
		this.time = time;
		n = new ArrayList<>();
	}
}

public class Main {
	static Build[] b;
	static int N;
	static int[] cnt;
	static int[] ans;
	static int target;
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		StringBuilder sb = new StringBuilder();
		
		int T = Integer.parseInt(st.nextToken());
		for(int t=0; t<T; t++) {
			st = new StringTokenizer(br.readLine());
			N = Integer.parseInt(st.nextToken());
			int K = Integer.parseInt(st.nextToken());
			
			b = new Build[N+1];
			cnt = new int[N+1];
			ans = new int[N+1];
			st = new StringTokenizer(br.readLine());
			for(int i=1; i<N+1; i++) {
				int tmp = Integer.parseInt(st.nextToken());
				b[i] = new Build(tmp);
				ans[i] = tmp;
			}
			
			for(int i=0; i<K; i++) {
				st = new StringTokenizer(br.readLine());
				int sn = Integer.parseInt(st.nextToken());
				int en = Integer.parseInt(st.nextToken());
				
				cnt[en]++;
				b[sn].n.add(en);
			}
			st = new StringTokenizer(br.readLine());
			target = Integer.parseInt(st.nextToken());
			
			topology();
			sb.append(ans[target]);
			sb.append("\n");
		}
		System.out.println(sb);
	}
	
	public static void topology() {
		Queue<Integer> q = new ArrayDeque<>();
		while(true) {
			if(cnt[target]==-1)
				break;
			for(int i=1; i<N+1; i++) {
				if(cnt[i]==0) {
					q.add(i);
					cnt[i]=-1;
				}
			}
			
			while(!q.isEmpty()) {
				int tmp = q.poll();
				for(int i=0; i<b[tmp].n.size(); i++) {
					int t = b[tmp].n.get(i);
					cnt[t]--;
					ans[t] = Math.max(ans[t], ans[tmp]+b[t].time);
				}
			}
		}
	}
}

```

## 시간 복잡도


## 느낀점