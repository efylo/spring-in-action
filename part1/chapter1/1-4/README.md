## 1.4 스프링 살펴보기

### 스프링 프레임워크

#### 스프링 IoC 컨테이너

- 스프링 빈(Bean)의 생명 주기를 관리하며, 의존성 주입을 진행한다. 
- IoC는 제어의 역전, Inversion of Control의 약어이다. 
  - 객체가 직접 의존성들을 생성하던 제어 흐름에서 역전되어 타 객체(IoC 컨테이너)가 의존성의 생성과 주입을 관리하는 것을 의미한다고 한다. 

#### 스프링 웹 MVC

- 웹 요청을 MVC(Model-View-Controller) 패턴을 기반으로 하여 처리하는 프레임을 제공한다. 
- 스프링의 웹 MVC 프레임워크의 처리 흐름
  - DispatcherServlet - 요청의 전반적인 처리를 제어한다. 
  - HandlerMapping - 요청 경로에 적합한 컨트롤러를 가리킨다. 
  - Controller - 요청에 적합한 처리를 진행하여, 적절한 View를 반환한다. 
  - ViewResolver - Controller에서 넘어온 View를 적절히 해석한다. 

#### 기타

- IoC 컨테이너, 웹 MVC 외에도 다수의 기능을 지원한다. 
  - 관점 지향 프로그래밍 (AOP)
  - JDBC
  - 리액티브 프로그래밍 (WebFlux)
  - 웹 소켓 (WebSocket)
  - 이메일
  - 스케줄링
  - 테스팅
  - 외 다수

---

### 스프링 부트

- 스타터 의존성 관리
  - "spring-boot-starter-..." 등과 같이 의존성을 자체적으로 관리한다. 
    - 버전 관리가 따로 필요 없다. 
    - 필요한 경우 해당 의존성이 필요로 하는 다른 의존성을 자체적으로 가져와서 사용한다. 
- 자동-구성 (Auto-Configuration)
  - 별도의 설정 파일 없이, 어플리케이션 구성을 자동으로 진행한다. 
  - 필요한 경우, 자바 방식의 구성(Configuration)을 추가하여 사용할 수 있다. 
- 기타
  - 액추에이터(Actuator)를 통해 런타임 시 어플리케이션의 내부 작동을 확인할 수 있다. 
  - 환경 속성의 명세
  - 테스트 지원

---

### 스프링 데이터

- 데이터 퍼시스턴스 지원
  - 기본적인 지원 외에도, 편리함을 위해 많은 기능을 제공한다. 
  - 여러 종류의 DB 엔진 지원
    - 관계형, 문서형, 그래프형 DB 모두 지원

---

### 스프링 시큐리티

- 어플리케이션 보안 프레임워크 지원
  - 인증(authentication), 허가(authorization), API 보안 등의 보안 요구를 다룬다. 
- 어려움
  - 기본적으로 알아야 하는 내용이 많다. 
  - 필터가 다수 존재하여 동작 방식을 이해하기 어렵다. 

---

### 기타

- 아직 감이 안 잡히는 내용들
  - **스프링 통합(Integration)**과 **배치(Batch)**
  - **스프링 클라우드(Cloud)**

---

### 참조

- https://docs.spring.io/spring-framework/docs/current/reference/html/index.html
- 크레이그 월즈, *스프링 인 액션*. 제이펍, 2020