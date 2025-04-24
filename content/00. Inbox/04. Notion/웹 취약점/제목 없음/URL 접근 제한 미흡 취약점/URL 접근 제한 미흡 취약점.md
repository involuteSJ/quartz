---
CMDS: Security
관련 문서:
  - "[[109 Security]]"
tags:
  - "#URL_접근_제한_미흡_취약점"
---
> [!important] Failure to Restrict URL Access Vulnerability
> 
> 인증된 사용자가 접속 가능한 페이지에 대해 인증되지 않은 사용자가 접근 가능한 취약점

  

인증 vs 인가

- Authentication 인증 : 인증된 사용자인지 확인하는 과정
    
    ex) 로그인 유 / 무
    

- Authorization 인가 : 특정 사용자가 해당 작업의 권한이 존재하는지 확인
    
    ex) 일반 사용자의 관리자 페이지 접근 거부
    
      
    

공격 원리

특별히 공격 방법이 없고, 공격자가 접근 제한된 페이지를 유추해서 들어감

ex) admin, adm, rhksflwk, robots.txt …

웹 서비스의 네이밍 패턴으로 유추

ex) boardList → board ( Write, Create, Insert ) …

  

대응 방안

![[90. Settings/92. Attachments/Untitled 20.png|Untitled 20.png]]