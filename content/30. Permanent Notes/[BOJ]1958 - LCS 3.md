---
CMDS: CodingTest
creation date: 2025-04-09 17:43
modification date: 2025-04-09 17:43:30
Algorithm Site: BOJ
tags:
  - "#CodingTest"
관련 문서:
  - "[[103.02 Related Problems]]"
문제 링크:
  - https://www.acmicpc.net/problem/1958
category: coding_test
---

# \[BOJ]1958 - LCS 3

## 문제 분석

문자열과 놀기를 세상에서 제일 좋아하는 영식이는 오늘도 문자열 2개의 LCS(Longest Common Subsequence)를 구하고 있었다. 어느 날 영식이는 조교들이 문자열 3개의 LCS를 구하는 것을 보았다. 영식이도 도전해 보았지만 실패하고 말았다.

이제 우리가 할 일은 다음과 같다. 영식이를 도와서 문자열 3개의 LCS를 구하는 프로그램을 작성하라.

## 문제 해결 아이디어
3차원 LCS

## 코드
```java
import java.util.*;
import java.io.*;

public class Main {
	public static void main(String[] args) throws IOException{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		StringBuilder sb = new StringBuilder();
		
		String s1 = st.nextToken();
		st = new StringTokenizer(br.readLine());
		String s2 = st.nextToken();
		st = new StringTokenizer(br.readLine());
		String s3 = st.nextToken();
		
//		int[][] dp = new int[s1.length()+1][s2.length()+1];
//		
//		for(int i=1; i<s1.length()+1; i++) {
//			for(int j=1; j<s2.length()+1; j++) {
//				if(s1.charAt(i-1)==s2.charAt(j-1)) {
//					dp[i][j] = dp[i-1][j-1]+1;
//				} else {
//					dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
//				}
//			}
//		}
		
		int[][][] dp = new int[s1.length()+1][s2.length()+1][s3.length()+1];
		
		for(int i=1; i<s1.length()+1; i++) {
			for(int j=1; j<s2.length()+1; j++) {
				for(int k=1; k<s3.length()+1; k++) {
					if(s1.charAt(i-1)==s2.charAt(j-1) && s2.charAt(j-1) == s3.charAt(k-1)) {
						dp[i][j][k] = dp[i-1][j-1][k-1]+1;
					} else {
						dp[i][j][k] = Math.max(dp[i][j][k-1], Math.max(dp[i-1][j][k], dp[i][j-1][k]));
					}
				}
			}
		}
		
		
		
		System.out.println(dp[s1.length()][s2.length()][s3.length()]);
	}
}
```

## 시간 복잡도


## 느낀점