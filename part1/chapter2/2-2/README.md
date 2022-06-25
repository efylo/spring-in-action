## 2-2. 폼 제출 처리하기

### 개요

- **HTML** - `<form>` 태그
  - `action` 속성에 데이터를 전송할 서버의 URL을 지정한다. 
    - 지정하지 않을 경우 현재 페이지의 URL을 기본 값으로 사용한다. 
  - `method` 속성을 통해 HTTP의 메서드를 지정한다. (GET, POST)
  - `submit` 동작이 수행되는 경우 서버에 데이터를 제출한다. 
    - 웹 페이지 버튼 클릭 시 제출: `<button>`, `<input type="submit">`
    - JavaScript: `document.getElementById("form-id").submit();`
- **컨트롤러**
  - `<form>` 태그의 URL에 해당하는 컨트롤러의 로직이 필요하다. 
  - `<input>` 태그 내의 `value` 속성의 값을 URL에 전송한다. 
    - GET - 쿼리 스트링 방식 `http://...?field1=value1&field2=value2`
    - POST - 본문(body)에 동일한 데이터를 전송한다. 
- **데이터 파싱**
  - 서버는 폼 제출을 통해 넘어온 데이터를 해석하여 적절하게 처리한다. 
  - *고려해야 하는 부분*
    - 데이터를 담는 위치 (URL, body, header, cookie)
      - URL에 담아 전송하는 경우, URL 인코딩 여부
    - 데이터 형식 (key=value, json, ...)
      - 클라이언트는 형식에 맞게 전송하고, 서버는 형식에 맞게 해석한다. 
    - 문자열 인코딩 타입 (UTF-8, EUC-KR, ...)

---

### Reference

- 크레이그 월즈, *스프링 인 액션*. 제이펍, 2020