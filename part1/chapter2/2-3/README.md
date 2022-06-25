## 2-3. 폼 입력 유효성 검사

### 개요

- **폼 입력 유효성 검사**
  - `<form>` 태그의 하위 노드, `<input>` 태그의 `value` 속성의 값의 유효성(validation)을 검사(check)한다. 
- **방식**
  - 서버에서 데이터를 받아서 처리하는 로직에 유효성 검사 로직을 추가하는 방식
    - 다수의 if~else 문이 추가되어, 코드가 너저분해진다. 
    - 직접 모든 유효성 검사 로직을 추가하는 것은, 번거롭다. 
  - 빈 유효성 검사(Bean Validation) API - 하이버네이트(Hibernate) API 방식
    - `@Data` 객체에 유효성 규칙을 추가한다. 
    - `@Data` 객체를 처리하는 메서드에 유효성 검사를 해야함을 지정한다. 
    - `View`에서 유효성 검사 에러를 보여주도록 수정한다. 

---

### javax.validation

#### 개요

- 빈 유효성 검사(Bean Validation)을 진행할 때 사용할 수 있는 어노테이션을 지원한다. 
- 스프링 부트 2.3버전부터, `spring-boot-starter-validation` 의존성을 추가해야 사용할 수 있다. 
  - `spring-boot-starter-web`만 추가한 경우, `javax.validation` 패키지를 사용할 수 없다. 

#### 어노테이션

- **javax.validation.constraints.NotNull**
  - `@NotNull` - 해당 필드가 Null이 될 수 없음
- **javax.validation.constraints.Size**
  - `@Size(min, max)` - 해당 필드의 크기의 최소, 최대 값을 정의
- **javax.validation.constraints.NotBlank**
  - `@NotBlank` - `.trim()` 메서드의 결과 값 이후의 크기가 0보다 커야 함
- **javax.validation.constraints.Digits**
  - `@Digits(integer, fraction)` - 해당 필드의 숫자의 개수, 소숫점 이후 숫자의 개수를 정의
- **javax.validation.constraints.Pattern**
  - `@Pattern(regexp)` - 해당 필드가 만족해야하는 정규표현식(Regular Expression)을 정의

#### message

- 상기 어노테이션을 선언할 때, `message` 속성에 값을 대입할 수 있다. 
- 어노테이션이 선언된 필드의 유효성 검사에 실패하였을 때, `message`를 던진다. 

#### javax.validation.Valid

- 요청을 처리하는 함수 안에, 유효성 검사가 필요한 도메인 객체의 앞에 위치한다. 

  ```java
  ...
  
  @PostMapping
  public String processAny(@Valid DomainObj anyThing, Errors errors) {
      if (errors.hasErrors()) {
          return "anyError";
      }
      // anyThing 처리
      return "redirect:/anySuccessfuls";
  }
  ```

- `@Valid` 어노테이션 처리 흐름

  - `DomainObj` 객체에 데이터가 바인딩 된 이후

  - **객체 내에 정의한 유효성 검사를 진행**

    - 유효성 검사 실패 시, `Errors` 객체에 에러의 내용을 추가한다. 

  - `processAny` 메서드 호출

    :arrow_forward: 데이터 바인딩 - 유효성 검사 - 요청 처리 함수 호출

#### in Thymeleaf

- `<form>` 태그를 통해 전달한 요청이 유효성 검사에 실패한 경우

  - 사용자에게 에러 메시지를 보여주는 것이 적절하다. 

- **필요한 속성**

  - `th:if="${#fields.hasErrors('field')}"`
  - `th:errors="*{field}"`
    - 'field'에 해당하는 값이 유효성 검사에 실패한 경우, 현재 태그를 보여준다. 
    - 'field'에 해당하는 에러 메시지를 보여준다. 

- **HTML 5**

  ```html
  <!-- Thymeleaf 네임스페이스 선언, ... -->
  <form method="POST" th:object="${anyThing}">
      <input type="text" th:field="${anyField}" />
      <span th:if="${#fields.hasErrors('anyField')}"
            th:errors="*{anyField}">Any Field Error</span>
      <br />
      
      <button>
          submit
      </button>
  </form>
  ```

  - `anyThing`에 해당하는 도메인 모델(객체)을 서버에 전송한다. 
  - `anyField`에 해당하는 값을 `text`로 입력받는다. 
  - 만약 사용자가 `anyField`에 입력한 값이 유효성 검사에 실패한 경우
    - `th:errors` 속성으로 넘어온 메시지를 `<span>` 태그 안에 보여준다. 

---

### Reference

- 크레이그 월즈, *스프링 인 액션*. 제이펍, 2020
- https://docs.jboss.org/hibernate/stable/validator/reference/en-US/html_single/