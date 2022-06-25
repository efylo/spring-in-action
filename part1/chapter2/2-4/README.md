## 뷰 컨트롤러 (View Controller)

### 개요

- 클라이언트의 요청을 처리할 때, 어떠한 데이터도 처리하지 않고 단순히 View를 넘겨주는 경우가 존재한다. 

  ```java
  // ...
  @GetMapping("/")
  public String home() {
      return "home";
  }
  ```

  - `"/"`의 URL에 해당하는 요청이 들어왔을 때, `src/main/resources/templates/home.html` 페이지를 반환한다. 
  - 위와 같은 코드를, `@Controller` 내에서 작성하지 않는 방법이 스프링에서 존재한다. 

---

### WebMvcConfigurer

- **스프링 웹 MVC**와 관련된 구성(Configuration)을 자바 코드에서 작성하기 위한 인터페이스
  - `WebMvcConfigurer` 인터페이스를 구현한다고 해서, 메서드 전체를 재정의(Override)하지 않아도 된다. 
    - 인터페이스의 메서드가 모두 `default` 메서드이다. 
- **메서드**
  - public void addViewControllers(ViewControllerRegistry registry)
    - 레지스트리에 뷰 컨트롤러를 등록한다. 
    - `registry.addViewController(String url).setViewName(String view)`를 통해 등록 가능하다. 
      - `url`에 해당하는 요청에 대하여 `src/main/resources/templates/{view}.html` 페이지를 반환한다. 
- **관례**
  - 저자는, 구성(Configuration) 파일을 그 목적에 따라서 따로 관리하는 것을 선호한다고 한다. 
    - 그 목적에는 웹 MVC, 데이터, 보안, 등이 포함될 수 있다. 

---

### Reference

- 크레이그 월즈, *스프링 인 액션*. 제이펍, 2020