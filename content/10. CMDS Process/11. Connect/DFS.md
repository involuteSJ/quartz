---
CMDS: Algorithm
관련 문서:
  - "[[Algorithm Concepts]]"
tags:
  - "#DFS"
  - "#Algorithm"
category: content
---
## DFS

<center><i><b>D</b>epth <b>F</b>irst <b>S</b>earch</i></center>

- 깊이 우선 탐색
- 자식 노드의 자식 노드를 먼저 탐색하는 방법
- Stack 활용 - 재귀

DFS(v)
	v 방문;
	for(v의 모든 자식 노드 w) {
		DFS(w)
	}
end DFS() 