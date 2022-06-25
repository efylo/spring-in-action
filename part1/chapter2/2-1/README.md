## 2.1 정보 보여주기

### 개요

- 웹 어플리케이션의 **흐름**
  1. 웹 브라우저(클라이언트)에서 서버에 데이터를 요청
     - 정적인 컨텐츠 (HTML, 이미지, 자바스크립트, CSS, ...)
     - 상태 정보 (자원 + 동작)
  2. 웹 서버에서 요청에 적합한 응답 생성
     - 컨트롤러 호출 (요청 데이터 처리 및 응답 생성)
       - DB 접근 / 입력 검사 / 응답 생성 / 에러 반환 / ...
  3. 뷰에서 응답 처리
     - 컨트롤러에서 반환한 응답에 맞는 처리를 진행

---

###  도메인

#### 도메인이란?

- 사전적 의미로는 분야, 영역, 범위, 영토를 뜻한다. 
  - 인터넷 주소의 도메인을 떠올릴 수 있다. (.kr / .com / .net / ...)
- 어플리케이션의 도메인은 해당 어플리케이션이 포함하는 영역을 전반적으로 나타내는 표현으로 보인다. 

#### 도메인 객체

- 현재 어플리케이션의 영역에 존재하는 객체
  - 모델, DTO 등과 비슷한 의미로 생각해볼 수 있다. 
  - lombok을 활용하여, 도메인 객체의 소스 코드 분량을 줄일 수 있다. 

#### lombok

- 도메인 객체(모델, DTO)에 반복적으로 사용되는 소스 코드를 줄여주는 라이브러리

  - 실제로 Getter, Setter, equals, Constructor 등의 코드가 반복적으로 작성된다. 

- 도메인 객체에 필요한 Getter, Setter, 등을 어노테이션을 통해 지정한다. 

  | Annotation | Description                                                  |
  | ---------- | ------------------------------------------------------------ |
  | @Data      | @ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor 모두 포함 |
  | @NonNull   | 메서드 매개변수의 null 체크                                  |
  | @Value     | Immutable(불변) 특성을 갖는 클래스 지정                      |
  | @Slf4j     | 로깅을 위한 객체를 클래스 내부에 생성                        |

  - 외에 다수의 어노테이션을 지원한다. 

- STS

  - 어노테이션을 통해 생성한 메서드는, STS 내에서 바로 확인할 수 없다. 
    - lombok이 메서드, 초기화 블럭 등을 런타임 시에 생성하기 때문
  - `SpringTookSuite4.ini`를 수정하거나, `java -jar lombok.jar` 실행
    - lombok이 런타임 시 생성하는 코드를 STS 내에서 확인 가능하다. 

---

### enum

- 어떤 변수가 사전에 정의된 상수의 집합 내에서 값을 가져야 하는 경우, enum 사용을 고려해볼 수 있다. 

  - 해당 변수는 집합 내에 존재함이 보장되며, 사람이 이해하기 쉬운 단어로 구성할 수 있는 장점이 존재한다. 

- **in Java**

  ```java
  public enum Day {
      SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
  }
  ```

  - 요일, 성별 등의 예시를 생각해볼 수 있다. 

  - 클래스 내에 static enum을 지정하여 사용하기도 한다. 

    ```java
    public class Car {
        private Type type;
        
        public static enum Type {
            SUV, SEDAN, SUPER_CAR
        }
    }
    ```

---

### Thymeleaf 엔진

#### 개요

- Java 진영의 서버-사이드 템플릿 엔진
  - 서버-사이드 렌더링을 진행한다. 
  - 이에 반하는 개념으로, 클라이언트-사이드 렌더링이 존재한다. 

#### 적용

- **스프링 부트**
  - 프로젝트 구성 파일 내에 `spring-boot-starter-thymeleaf`에 대한 의존성을 추가
  - 스프링 부트가 런타임에 Thymeleaf를 찾아서 빈으로 등록
- **HTML 템플릿**
  - `xmlns:th="http://www.thymeleaf.org"`를 통해 thymeleaf 네임스페이스를 사용함을 지정한다. 
  - HTML 페이지 내 `th:prop` 속성은, 상기 네임스페이스에 정의된 `prop` 속성을 사용할 것임을 지정한다. 
    - JSP 페이지 내에서 JSTL 태그 라이브러리를 사용하는 것과 비슷하다. 
    - 기존 HTML에 존재하지 않는 `th:if`, `th:each`, `th:object` 등의 문법을 사용할 수 있다. 
    - 페이지 내에서 사용하는 모델(데이터)에 대해 변수를 사용할 수 있다. 
- **표현식 (Expression)**
  - `#{msg}`, `${var}`, `@{link}`, `*{sel}`, `#expr` 등의 표현식을 사용할 수 있다. 

---

### Reference

- 크레이그 월즈, *스프링 인 액션*. 제이펍, 2020
- https://projectlombok.org/features/all
- https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html
- https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html

