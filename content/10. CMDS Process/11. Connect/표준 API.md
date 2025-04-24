---
CMDS: Java
type:
  - note
tags:
  - "#Consumer"
  - "#Supplier"
  - "#Function"
  - "#Operator"
  - "#Predicate"
관련 문서:
  - "[[101.01 Object-Oriented Concepts]]"
  - "[[표준 API-문제]]"
category: content
---
## 표준 API - SCOFP
- #### Supplier 계열
	- prameter가 없고 return 만 존재
		- Supplier\<**T**\> - T타입 객체 리턴
		- PSupplier - p타입 값 리턴
- #### Consumer 계열
	- parameter는 있으며 return 이 없는 형태 - 파라미터를 받아서 소비
	- parameter 타입에 따라 다양한 consumer 존재
		- Consumer\<**T**\> - T타입 객체 t를 받아서 소비
		- BiConsumer\<**T**, **U**\> - T타입과 U타입 객체를 받아서 소비
		- PConsumer - p타입 값을 받아서 소비
		- ObjPConsumer\<**T**\> - 객체 타입 T와 p값을 받아서 소비
- #### Operator 계열
	- Function과 유사하게 parameter와 return 값이 있는 형태
	- Function과 달리 연산 수행 후 동일한 타입으로 리턴
- #### Function 계열
	- parameter와 return 값이 있는 형태
- #### Predicate 계열
	- parameter를 받고 boolean 타입을 리턴