## 1-3. 스프링 어플리케이션 작성

### Controller

- 서버로 들어온 요청을 가져와서 처리한다. 
  - HandlerMapping 객체가 요청의 경로에 해당하는 컨트롤러를 호출한다. 
  - 요청 처리 이후 적절한 응답 혹은 응답을 야기할 수 있는 데이터 등을 반환한다. 

#### @Controller

- 클래스 앞에 위치하여, 현재 클래스가 컨트롤러임을 스프링 어플리케이션 컨텍스트에 알려준다. 
- 스프링 어플리케이션 컨텍스트는 이를 컴포넌트로 등록한다. 

#### @GetMapping(String path)

- 메서드 앞에 위치하여, *path*에 해당하는 HTTP GET 요청을 처리하는 로직임을 알려준다. 
- GetMapping, PostMapping, PutMapping, DeleteMapping - HTTP GET, POST, PUT, DELETE 메서드
- RequestMapping - HTTP 전반

---

### View Template

- 템플릿 엔진으로 Thymeleaf, JSP 등의 엔진을 사용할 수 있다. 
- 타임리프 엔진을 사용하는 경우, ".html" 확장자를 사용하기 때문에 어플리케이션 속성을 변경하지 않아도 무방하다. 
  - View를 반환할 때 폴더의 위치, 확장자는 "src/main/resources/templates/", ".html"을 기본으로 한다. 
  - ViewResolver 컴포넌트가 이를 처리한다. 
- JSP 엔진을 활용하는 경우, ".jsp" 확장자를 사용하기 때문에 어플리케이션 속성을 변경해야 한다. 
  - ViewResolver의 접두사(prefix)와 접미사(suffix)를 수정한다. 

---

### 테스트 코드 작성

- @WebMvcTest(xxxController.class)
  - 스프링 MVC 형태의 테스트를 수행한다. 
  - 컨트롤러를 스프링 MVC에 등록하기 때문에, 클라이언트의 요청에 대한 테스트를 진행할 수 있다. 
- org.springframework.test.web.servlet.MockMvc
  - 실제 서버를 동작시키는 것이 아닌, 스프링 MVC 모의 객체를 사용해 테스트한다. 
  - 메서드
    1. perform(RequestBuilder requestBuilder)
       - RequestBuilder를 통해 정의한 요청을 수행한다. 
       - MockMvcRequestBuilders 클래스의 static 메서드를 인자로써 활용할 수 있다. 
    2. andExpect(ResultMatcher resultMatcher)
       - ResultMatcher를 통해 정의된 응답과, perform()에서 수행된 요청의 응답을 비교한다. 
       - MockMvcResultMatchers 클래스의 static 메서드를 인자로써 활용할 수 있다. 

---

### 어플리케이션 빌드 및 실행

- STS 기준으로, 부트스트랩 클래스(@SpringBootApplication)에 들어가서 Ctrl + F11을 통해 실행할 수 있다. 
  - 어떤 어플리케이션으로 실행할 것이냐고 물어본다면, Spring Boot Application을 선택한다. 
- 혹은 Boot Dashboard를 활용하여, 선택한 어플리케이션을 실행할 수 있다. 

---

### Spring Boot DevTools

- 스프링 부트 어플리케이션을 개발할 때 유용하게 사용되는 도구를 제공하며, 다음과 같은 기능을 포함한다. 
  - 소스 코드가 변경될 때 자동으로 어플리케이션이 재시작된다. 
  - 리소스 변경 시 자동으로 브라우저를 새로고침한다. 
  - 템플릿 캐시 비활성화
  - H2 DB 사용 시, H2 콘솔 활성화
  - 위 기능들은 실제 운영 시에 모두 비활성화된다. 

#### 자동 어플리케이션 재시작

- DevTools를 사용하는 경우 JVM의 클래스로더를 두 개 사용한다. 
  - "src/main" 폴더 내 파일 로드
  - 나머지 파일 로드 (의존성 라이브러리, ...)
- pom.xml 파일을 수정한 경우, 어플리케이션을 수동으로 재시작해야 한다. 

#### 템플릿 캐싱

- Thymeleaf 템플릿 엔진은 캐싱 기법을 사용한다. 
  - 엔진이 파싱한 결과를 캐시에 저장하여, 추후 요청에 사용하여 성능 상 이점을 추구한다. 
  - 이를 개발 시점에서 사용하는 경우, 템플릿 파일을 변경하여도 브라우저 내에서 변동 사항을 확인할 수 없는 문제점이 생긴다. 
    - 어플리케이션을 수동으로 재시작해야 한다. 

---

### 참조

- 크레이그 월즈, *스프링 인 액션*. 제이펍, 2020