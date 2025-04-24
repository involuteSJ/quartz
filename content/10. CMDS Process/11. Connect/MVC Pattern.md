---
CMDS: Java
type:
  - note
tags:
  - "#MVC"
관련 문서:
  - "[[101.02 Design Patterns]]"
  - "[[106 BackEnd]]"
category: content
---
## MVC

<center><i><b>M</b>odel <b>V</b>iew <b>C</b>ontroller</i></center>

- 애플리케이션을 역할에 따라 Model, View, Controller로 모듈화 하는 패턴
	- **Controller** : 요청을 받고 Model과 View간의 상호 작용으르 조정하는 모듈
	- **Model** : 비즈니스 로직(업무)를 담당하는 모듈, 필요시 DB 연동(DAO)
	- **View** : 사용자와 상호작용을 위한 UI

##### 장점
- 독립적 개발 및 유지보수가 용이
- 코드 가독성, 재사용성 향상
![[mvc]]

#### Model 1
- JSP가 Controller를 맡아 View 로직과 함께 수행
- ##### 장점
	- 단순성 - 구조가 간단
	- 빠른 개발 - 개발 속도가 빠름
	- 직관성 - 학습 곡선이 완만
- ##### 단점
	- 유지보수의 어려움 - 코드가 복잡, 재사용성 저하
	- 확장성 제한 - 애플리케이션이 커질수록 구조가 복잡
![[Pasted image 20250320091514.jpg]]

#### Model 2
- MVC 패턴을 따르며 Servlet이 Controller를 맡아 클라이언트 요청 접수
- ##### 장점
	- 명확한 구조 : 각 구성 요소가 명확히 분리되어 가독성 향상
	- 유지보수 용이 : 비즈니스 로직과 프레젠테이션 로직이 분리
	- 확장성 : 규모가 커져도 구조가 명확
- ##### 단점
	- 복잡성 : 초기 설정과 개발이 어려움
	- 개발 속도 : Model 1에 비해 초기 개발 속도가 느림
	- 학습 곡선 - 학습 곡선이 가파름
![[Pasted image 20250320091559.jpg]]

#### Model 2 Deep Dive
![[Pasted image 20250320091709.jpg]]

#### 웹 컴포넌트 호출
- 서블릿, JSP는 Container가 호출
- ##### RequestDispatcher#forward
	- forward 방식 호출
	- controller가 받은 req, resp를 JSP에 전달 - req에 저장한 정보를 JSP에서 확인 가능
	- ![[Pasted image 20250320092217.jpg]]
- ##### HttpServletResponse#sendRedirect
	- redirect 방식 호출
	- 현재 실행중인 페이지 실행을 중단하고 다른 웹 자원이 대신 호출하게 함
	- 외부 리소스 사용 가능
	- 응답 2는 요청 1과 무관
	- ![[Pasted image 20250320092559.jpg]]
- ![[Pasted image 20250320092700.jpg]]