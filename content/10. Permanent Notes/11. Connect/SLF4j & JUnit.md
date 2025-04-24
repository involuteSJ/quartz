---
CMDS: "[[110 Frameworks]]"
creation date: 2025-04-16 12:40
modification date: 2025-04-16 12:40:54
type:
  - note
tags:
  - "#SLF4j"
  - "#JUnit"
관련 문서:
  - "[[110.01 Spring]]"
category: content
---

# SLF4j

<center><i><b>S</b>imple <b>L</b>ogging <b>F</b>acade <b>for</b> <b>J</b>ava</i></center>

- java에서 로깅을 위한 facade
- 구현체는 <i>log4j</i> 와 logback
	- log4j는 보안 이슈 때문에 log4j2로 대체

#### 특징
- 심각도에 따라 다섯 단계로 구분 (trace, debug, info, warn, error)
- **사용자 설정**에 따라 확인할 로그 레벨 결정
	- 개발 과정 - trace
	- 운영 과정 - info

# JUnit
- 단위 테스트 자동화를 위한 프레임워크
- assertion을 이용한 단정문 사용

#### FIRST 원칙
- ##### Fast
	- 빠르게 동작해야 함
	- 외부 환경과 무관하게 작성
- ##### Independent
	- 이전 테스트에 의존하면 안됨
	- 순서와 상관없이 언제나 성공해야 함
- ##### Repeatable
	- 여러번 반복해도 동일하게 동작해야 함
- ##### Self-Validating
	- 테스트 자체로 검증이 완료되어야 함
- ##### Timely
	- TDD를 하면 테스트는 production code 개발 전에 진행해야 함