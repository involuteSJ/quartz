---
CMDS: Java
type:
  - note
tags:
  - "#FileIO"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
category: content
---
## Thread
- Thread 내부에 public void run() 이라는 메서드 존재
- run 메서드에 기능을 작성하고 start 메서드에서 스레드 실행
- runnable 인터페이스를 통해 스레드에게 넘겨줄 수 있음
- thread를 실행시키면 runnable room에 스레드가 들어감
- running room에서 하나의 스레드만 실행시킬 수 있음
- runngin room에서 스레드가 가지고 있는 메서드를 끝까지 실행하는게 아닌 context mark 까지만 실행후 다시 runnable room으로 이동
- 각 스레드에는 priority를 가지고 있음
	- max
	- normal
	- min - GC
- GC는 runnable room 에 항상 존재
- memory가 가득 차면 GC의 priority가 max로 변경
- 순서를 맞추기 위해 Synchronize
- 한 스레드가 객체를 이용할 때 다른 객체가 이용하지못하도록 하는 방식 - 동시에 이용할 경우 객체를 정상적인 이용이 안됨
- -> thread deadlock

#### Thread의 종료
- 모든 메서드를 돌려서종료하는 경우
- stop()을 통해 running room에서 스레드를 빼옴 - **deprecated**
- sleep()메서드 실행 시 스레드를 sleep room으로 이동
- => sleep 메서드 실행 시 스레드가 running room에 존재할 경우 runnable room 까지 기다려야 하기 때문에 실제 시간과 정확히 일치하지 않음
- suspend를 통해 스레드를 sleep room으로 이동시키고 resume을 통해 sleep room -> runnable room으로 이동 - **deprecated**
- thread deadlock 때문에 stop, suspend, resume이 deprecated
- => 객체의 사용 여부에 따라 스레드의 상태를 제어하는 방법으로 변경 - wait, notify