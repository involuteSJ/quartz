---
CMDS: "[[108 Engineer Information Security]]"
creation date: 2025-04-08 16:21
modification date: 2025-04-08 16:21:20
type:
  - note
tags:
  - "#AES"
관련 문서:
  - "[[대칭키 암호]]"
category: content
---

# AES

<center><i><b>A</b>dvanced <b>E</b>ncryption <b>S</b>tandard</i></center>

- 128비트 평문을 128비트 암호문으로 출력
- 10, 12, 14라운드 사용
- 128, 192, 256비트 키 사용
- DES 라운드 함수이 Feistel 과 달리 SPN 구조 사용
- ###### 각 라운드에서 수행되는 연산
	- SubBytes()
		- s-box를 적용하여 byte 단위로 치환
	- ShiftRows()
		- 행 단위로 순환 시프트를 수행
	- MixColumns()
		- 열 단위로 혼합
	- AddRoundKey()
		- 라운드 키와 state를 xor연산
- 마지막 라운드에서는 MinColumns 연산을 수행하지 않음
![[Pasted image 20250408162711.jpg]]