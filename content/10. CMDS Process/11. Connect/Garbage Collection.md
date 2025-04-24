---
CMDS: Java
type:
  - note
tags:
  - "#GC"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
category: content
---
## Garbage Collection
- Java에서 thread로 관리
- application이 작동 중일때 GC가 작동하게 되면 끊김 현상 발생
- java에서 새로운 객체를 만들면 eden 영역에 저장
- eden의 용량이 크지 않기 때문에 GC가 eden의 용량이 다 차면 정리
- eden 영역에 객체의 reference count가 남아 있는 객체만 s1 영역으로 이동 후 eden 영역의 객체 제거
- s1이 가득 차면 s2로 사용중인 객체만 이동
- s2가 가득 차면 사용중인 객체만 old로 이동
- old 영역은 GC가 정리하는데 오래 걸리기 때문에 markup compact 와 같은 기법을 사용해서 효과적으로객체 정리
---
## Garbage Collection

<center><i>불필요한 메모리인 Garbage를 자동으로 정리시켜주는 작업</i></center>

Java - JVM을 통해 자동으로 정리
C - free() 함수를 통해 직접 메모리 해제

#### Stop-The-World
- GC를 수행하기 위해 JVM이 프로그램 실행을 멈추는 현상
- GC 관련 쓰레드를 제외한 모든 쓰레드가 멈춤

#### Heap
JVM의 Heap 영역은 두 공간으로 이루어져 있음
- Young 영역 (Minor GC)
	- Eden - 공간이 가장 작음
	- S0 (Survivor 0)
	- S1 (Survivor 1)
- Old 영역 (Major GC / Full GC)
![[garbageCollection]]

#### GC의 동작 방식
- Mark & Sweep 알고리즘
	- Mark
		- Stack, JNI, Method Area를 스캔하면서 Heap에 할당된 객체가 있는지 찾음
		- 사용되고 있는 데이터는 **Reachable**
		- 사용되지 않는 데이터는 **Unreachable**
	- Sweep
		- Unreachable로 구분된 객체들을 메모리에서 해제
	- Compact
		- Sweep 후에 분산된 객체를 모아주는 작업
##### Minor GC 과정
1. 처음 Eden 영역이 가득 찼을 때
	1. 처음 생성된 객체는 Eden 영역에 위치
	2. **Eden 영역**이 가득 차게 되면 Reachable 객체 탐색
	3. 살아남은 객체는 S0 영역으로 이동 후 **age 값 1 증가**
	4. Unreachable 객체 제거 -> **Eden이 비어있음**
2. 2번째 Eden 영역이 가득 찼을 때
	1. **Eden 영역과 S0 영역** Reachable 객체 탐색
	2. 살아남은 객체는 S1 영역으로 이동 후 **age 값 1 증가**
	3. Unreachable 객체 제거 -> **Eden + S0 가 비어있음**
3. 3번째 Eden 영역이 가득 찼을 때
	1. **Eden 영역과 S1 영역** Reachable 객체 탐색
	2. 살아남은 객체는 S0 영역으로 이동 후 age 값 1 증가
	3. Unreachable 객체 제거 -> Eden + S1 가 비어있음
4. 2-3 계속 반복
	- 이때 age가 MaxTenuringThreshold 값 이상이 넘어가면 Old 영역으로 이동
		- -> Promotion
	- S 영역에 공간이 가득 찬 경우 age가 많은 순서로 일부 객체 Old 영역으로 이동
		- -> Permature Promotion

##### Major GC 과정
- Minor GC에서 발생한 Promotion과 Permature Promotion 작업이 계속 발생하여 Old 영역이 가득 차면 발생
- Major GC의 경우 모든 객체를 검사하여 참조하지 않는 객체를 한꺼번에 삭제
- Major GC의 작업이 Minor GC의 작업보다 10배 이상 오래걸림
	- -> 멈추거나 버벅거리는 현상 발생

#### GC의 종류
- ##### Serial GC
	- GC를 처리하는 쓰레드가 1개
	- Minor GC 에는 Mark-Sweep 사용
	- Major GC 에는 Mark-Sweep-Compact 사용
- ##### Parallel GC
	- Java 8 디폴트 GC
	- Minor GC -> Serial GC + 멀티쓰레드
	- Major GC -> Serial GC
	- Serial GC보다 Stop-The-World 시간 감소
- ##### Parallel Old GC
	- parallel GC 개편 버전
	- Minor GC -> 이전과 그대로
	- Major GC -> Mark-Summary-Compact 방식 사용
		- Summary -> 객체의 이동 위치를 미리리계산하여 최적화
		- Compact -> 