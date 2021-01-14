# ExceptionTranslationFilter

## 401 에러와 403 에러

- 401 : 인증 실패

  - AuthenticationException
  -

- 403 : 권한 없음

  - AccessDeniedException
  -

## AuthenticationEntryPoint

- Authentication 이 실패하면 AuthenticationException 이 발생되고
- void commence(HttpServletRequest request, HttpServletResponse response, AuthenticationException authException) throws IOException, ServletException;

##
