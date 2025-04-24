---
CMDS: Java
creation date: 2025-04-06 16:30
modification date: 2025-04-04 16:53:09
상위 문서: "[[Class]]"
category: content
---
# Class 코딩 과정

1. 처음 객체를 생성할 때 Dynamic Loading을 불러옴
2. 이후 Verify 작업 진행
3. Static 과 관련된 변수 처리
4. Object 처리

>[!tip]
>Class를 불러오는 3가지 방법
>>객체 생성
>>Static을 통한 생성
>>Class 클래스에서 호출

![[makeClass]]

객체 변수는 초기화되지만, 지역 변수는 초기화되지 않음
java에는 전역함수, 전역변수 대신 인스턴스 변수, 메소드만 존재
#인스턴스변수 #메서드