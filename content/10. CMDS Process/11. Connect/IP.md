---
CMDS: DataBase
type:
  - note
tags:
  - "#HTTP"
  - "#IP"
관련 문서:
  - "[[107.01 HTTP]]"
category: content
---
## IP

<center><i><b>I</b>nternet <b>P</b>rotocol</i></center>

- 패킷 단위로 데이터 전송
- 용량이 많을 경우 잘라서 보냄 -> 순서대로 도착 보장 X
- #### 한계
	- 비연결성
		- 받을 대상이 없어도(대상 서비스 불능) 패킷 전송
	- 비신뢰성
		- 중간에 사라지면?
		- 순서대로 안오면?
		- 중간에 사라지면?

=> IP의 한계를 해결하기 위해 TCP / UDP 프로토콜이 나옴
#### 인터넷 프로토콜 4계층
- 애플리케이션 - HTTP, FTP
- 전송 계층 - TCP, UDP
- 인터넷 계층 - IP
- 네트워크 인터페이스 계층
![[패킷]]

## TCP

<center><i><b>T</b>ransmission <b>C</b>ontrol <b>P</b>rotocol</i></center>

- 전송 제어 프로토콜
- 연결 지향
	- TCP 3 way handshake
- 데이터 전달 보증
	- 데이터 전송 후 서버의 연락으로 서버가 데이터를 잘 받았는지 알 수 있음
- 순서 보장
	- 잘못된 순서로 도착 시 데이터를 전부 버리고 다시 요청
- <font color="#ff0000">시간이 오래 걸림</font>
=> **신뢰 가능**

#### TCP 3 way handshake
![[tcp3way]]

## UDP

<center><i><b>U</b>ser <b>D</b>atagram <b>P</b>rotocol</i></center>

- 사용자 데이터그램 프로토콜
- 연결 지향 X -> TCP 3 way handshake X
- 데이터 전달 보증 X
- 순서 보장 X
- 데이터 전달과 순서가 보장되지 않지만 단순하고 빠름
	- IP와 거의 유사. port + checksum 기능 추가 정도
	- 애플리케이션 추가 작업 필요