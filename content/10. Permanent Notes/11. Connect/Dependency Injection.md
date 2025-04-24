---
CMDS: "[[110 Frameworks]]"
creation date: 2025-04-17 11:25
modification date: 2025-04-17 11:25:24
type:
  - note
tags:
  - "#DI"
관련 문서:
  - "[[110.01 Spring]]"
category: content
---

# Dependency Injection
- Spring bean 과 di에 대해 설명해줘

 ### 스프링 빈(Spring Bean)과 의존성 주입(Dependency Injection)에 대해 설명

**1. 의존성 주입(Dependency Injection, DI)이란?**

의존성 주입은 소프트웨어 디자인 패턴 중 하나로, 객체 간의 의존 관계를 외부에서 주입(설정)해주는 방식을 말합니다. 이를 통해 객체 간의 결합도를 낮추고, 코드의 재사용성과 테스트 용이성을 향상시킬 수 있습니다.

- **전통적인 방식 (수동 주입):**
  객체가 자신의 의존성을 직접 생성하거나 조회합니다. 이 경우 객체 간의 결합도가 높아져 유지보수가 어려워집니다.

- **의존성 주입 방식:**
  객체가 필요한 의존성을 외부에서 주입받습니다. 이를 통해 객체는 자신의 의존성에 대해 알 필요가 없으며, 결합도가 낮아집니다.

**의존성 주입의 주요 방식:**
- **생성자 주입 (Constructor Injection):** 의존성을 생성자를 통해 주입받습니다.
- **세터 주입 (Setter Injection):** 의존성을 세터 메서드를 통해 주입받습니다.
- **필드 주입 (Field Injection):** 의존성을 필드에 직접 주입받습니다.

**2. 스프링 빈(Spring Bean)이란?**

스프링 빈은 스프링 IoC 컨테이너에 의해 생성되고 관리되는 객체를 말합니다. 스프링 애플리케이션에서의 모든 구성 요소는 스프링 빈으로 등록되어 관리됩니다.

- **스프링 빈의 특징:**
  - **싱글턴:** 기본적으로 스프링 빈은 싱글턴으로 관리되지만, 프로토타입 등 다양한 스코프로 설정할 수 있습니다.
  - **생명주기 관리:** 스프링은 빈의 생성, 초기화, 소멸 등의 생명주기를 관리합니다.
  - **의존성 관리:** 빈 간의 의존성을 설정하고 관리합니다.

**3. 스프링에서의 의존성 주입 구현**

스프링 프레임워크는 의존성 주입을 통해 객체 간의 의존 관계를 설정하고 관리합니다. 주요 방법은 다음과 같습니다.

- **어노테이션 기반 설정:**
  - `@Component`, `@Service`, `@Repository`, `@Controller`: 스프링 빈으로 등록할 클래스를 표시합니다.
  - `@Autowired`: 의존성을 주입할 필드, 생성자, 메서드에 사용됩니다.
  - `@Qualifier`: 동일 타입의 빈이 여러 개일 때 특정 빈을 지정할 때 사용됩니다.

- **XML 기반 설정:**
  과거에는 XML 파일을 통해 빈을 정의하고 의존성을 설정했으나, 최근에는 어노테이션 기반 설정이 더 많이 사용됩니다.

**예시: 생성자 주입을 이용한 스프링 빈 구성**

```java
// 서비스 인터페이스
public interface GreetingService {
    void greet();
}

// 인터페이스 구현 클래스
@Service
public class GreetingServiceImpl implements GreetingService {
    @Override
    public void greet() {
        System.out.println("안녕하세요!");
    }
}

// 컨트롤러 클래스
@Controller
public class GreetingController {
    private final GreetingService greetingService;

    // 생성자 주입
    @Autowired
    public GreetingController(GreetingService greetingService) {
        this.greetingService = greetingService;
    }

    public void doGreet() {
        greetingService.greet();
    }
}
```

위 예시에서 `GreetingController`는 `GreetingService`에 의존하고 있습니다. 스프링은 `@Autowired` 어노테이션이 붙은 생성자를 통해 `GreetingServiceImpl` 빈을 주입합니다. 이를 통해 `GreetingController`는 `GreetingService`의 구체적인 구현을 알 필요 없이, 인터페이스에 의존하게 됩니다. 이는 코드의 유연성과 테스트 용이성을 높여줍니다.

**4. 의존성 주입의 장점**

- **결합도 감소:** 객체 간의 직접적인 의존을 줄여 코드의 유연성을 높입니다.
- **테스트 용이성:** 의존성을 외부에서 주입받기 때문에 목(Mock) 객체을 사용한 단위 테스트가 용이합니다.
- **모듈화:** 각 컴포넌트가 독립적으로 개발되고 관리될 수 있습니다.
- **유지보수성 향상:** 의존 관계가 명확하게 설정되어 코드의 이해와 유지보수가 쉬워집니다.

**5. 결론**

스프링의 의존성 주입과 스프링 빈 관리는 현대적인 자바 애플리케이션 개발에서 중요한 요소입니다. 이를 통해 개발자는 더 깔끔하고 유지보수하기 쉬운 코드를 작성할 수 있으며, 애플리케이션의 확장성과 테스트 용이성을 크게 향상시킬 수 있습니다.

## 명시적 DI
- `@Configuration`을 통해 설정 정보 저장
- `@Bean`을 통해 bean 생성
- `getBean`을 통해 bean 가져오기
![[Pasted image 20250417113505.jpg|640x154]]

- 메타정보 작성
```java
@Configuration
public class WasherConfig {
	@Bean
	public SWasher sWasher() {
		return new SWasher();
	}

	@Bean
	public LWasher lWasher() {
		return new lWasher();
	}
	
	@Bean(name="myWasherUser")
	public WasherUser washerUser() {
		WasherUser washerUser = new WasherUser();
		washerUser.setWasher(sWasher());
		return washerUser;
	}
}
```
## 묵시적 DI
- `@Configuration`에서 `@Bean`을 사용하지 않음
- bean으로 사용할 클래스에 `@Component` 표시
- `@Autowired` : bean을 주입하기 위한 annotation
- `@ComponentScan` : 실제 빈을 만들지 않고 빈이 될 수 있다는 의미
- `@Qualifier` : 이름 기반으로 주입될 빈 한정
- `@Component` : 단순 빈의 대상임을 나타내는 annotation
	- ##### 스테레오 타입
	- `@Repository` : DAO 역할
	- `@Service` : service 역할
	- `@Controller` :  controller 역할
	- `@Configuration` : 메타정보 클래스에 사용
	- `@Component` : 다른 스테레오 타입 annotation에 해당되지 않을 경우

#### 빈 생성 및 설정
```java
//Bag.java
@Component
public class Bag {
	Hat hat;
	Watch watch;
	SmartWatch swatch;

	@Autowired
	public Bag(Hat hat,@Qualifier("watch") Watch watch) {}

	@Autowired
	public void setSmartWatch(SmartWatch swatch) {
		this.swatch = swatch;
	}
}

//Hat.java
public class Hat {}

//Watch.java
public class Watch {}

//SmartWatch.java
public class SmartWatch extends Watch {}

//BagConfig.java
@Configuration
@ComponentScan("com.ssafy.live.accessory")
public class BagConfig {}
```

- 테스트
```java
//Junit과 Spring 연결 - @Autowired 사용 가능
@ExtendWith(SpringExtension.class)
//설정 파일 등록
@ContextConfiguration(class = BagConfig.class)
public class BagTest {
	@Autowired
	Bag bag;

	@Test
	public void bagTest() {
		Assertions.assertNotNull(bag);
	}
}
```
#### 주입 방식에 따른 DI 방법
- 생성자 주입 (권장)
	- bean의 의존성이 필요하다는 것을 명시적으로 나타냄
	- 빈의 순환 의존성 문제를 생성 시점에 발견 가능
- setter 주입
	- 선택적인 의존성을 가진 빈의 주입
- field 주입 (비추)
	- Mock객체 주입의 어려움
	- 빈의 불변성을 보장하지 않음

![[Pasted image 20250417115400.jpg]]
