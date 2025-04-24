---
CMDS: Java
type:
  - note
tags:
  - "#XML"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
category: content
---
## 공공데이터
- 공공기관이 만들어내는 모든 공적인 정보
- 공공긱관이 보유한 데이터를 개방하여 누구나 활용 가능
- #### 데이터의 형태
	- csv - comma separated value
	- xml - 태그를 통해 데이터 정의
	- json - JavaScript Object Notation

## XML

<center><i>Extensible Markup Language</i></center>

- Markup Language
	- 태그를 활용하여 문서나 데이터 구조를 명기
- HTML과 달리
	- 태그를 확장해서 사용 가능
- #### 기본 문법
	- 문서의 시작은 \<?xml version="1.0" encoding="UTF-8"?\>
	- root element가 존재해야 함
	- 시작 태그와 종료 태그는 일치해야 함
	- 시작 태그는 key-value 구조의 속성을 가질 수 있음
	- 대소문자 구별
- #### Valid
	- 최초 작성자의 의도대로 작성되는지 확인 필요
	- DTD 또는 Schema를 이용해서 문서 규칙 작성