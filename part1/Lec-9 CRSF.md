# CORS

- 해더 필터에 xssProtection 을 설정해 주어야 한다. 다른 사이트에서 요청하는 것을 무작정 막는다. 옳지 않은 요청이다.
  ``java
  protected void configure(HttpSecurity http) throws Exception {
  http
  .headers((headers) ->
  headers
  .contentTypeOptions(withDefaults())
  .xssProtection(withDefaults())
  .cacheControl(withDefaults())
  .httpStrictTransportSecurity(withDefaults())
  .frameOptions(withDefaults()
  );
  }

  ```


  ```

# CSRF

- CsrfTokenRepository 가 HttpSession 에 저장됩니다.
- 보통 CsrfTokenRepository의 구현체는 HttpSessionCsrfTokenRepository 를 사용하는데, \_csrf 값이 Model에 항상 들어 있습니다. 개발자들이 REST 에 충실하게 개발했다는 가정하에, GET, HEAD, TRACE, OPTIONS 요청은 허용하고, POST, PUT, DELETE 등 서버 리소스에 변경을 가하는 요청을 보내는 경우에만 \_csrf 값을 체크합니다. 반드시 같이 보내야 서버에서 인정을 해줍니다.
- 혹은 X-CSRF-TOKEN 이라는 해더에 값을 넣어서 보내도 됩니다.
- csrf 토큰의 파라미터 이름과 해더 이름은 설정에서 변경해서 사용할 수 있습니다.
- 보통 CSRF 토큰은 UUID 형태로 생성됩니다.

- CSRFToken 은 아래와 같은 방식으로 존재합니다.
  ```
  headerName: X-CSRF-TOKEN
  parameterName: _csrf
  token: aa0daaed-e300-4c3d-a76f-a7768901199b
  ```
-
