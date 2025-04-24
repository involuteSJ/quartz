---
CMDS: Algorithm
상위 문서: "[[Algorithm Concepts]]"
---
- #### 버블 정렬 \[O($n^2$)\]
	- 인접한 데이터의 크기를 비교해 정렬하는 방법
	- 속도가 느린 편
		![[bubbleSort]]
- #### 선택 정렬 \[O($n^2$)\]
	- 최대, 최솟값을 선택하여 나열하는 방법
	- ![[selectSort]]
- #### 삽입 정렬 \[O($n^2$)\]
	- 선택 데이터를 현재 정렬된 범위 내에서 적절한 위치에 삽입
	- 삽입 위치 탐색 시 이진탐색을 사용하면 시간복잡도 감소
	- ![[insertSort]]
- #### 퀵 정렬 \[평균 O($nlogn$)\]\[최악 O($n^2$)\]
	- pivot을 설정하여 해당 값보다 큰 데이터와 작은 데이터로 분류
	- ##### 과정
		1. start < pivot
			- start 오른쪽 1칸 이동
		2. end > pivot
			- end 왼쪽 1칸 이동
		3. start > pivot && end < pivot
			- start와 end 값 교환
		4. start = end일 때까지 진행
		5. start, end 사이에 pivot 삽입