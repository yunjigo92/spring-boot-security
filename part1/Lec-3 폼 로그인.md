# 폼 로그인

## DefaultLoginPageGeneratingFilter

- GET /login 을 처리한다.
- 별도의 로그인 페이지 설정을 하지 않으면 제공되는 필터이다.
- 기본 로그인 폼을 제공한다.
- OAuth2 소설 로그인과도 같이 사용할 수 있다.
-

## UsernamePasswordAuthenticationFilter

- POST /login 을 처리한다. processingUrl 을 변경하면 주소를 바꿀 수 있다.
- form 인증을 처리해주는 필터로 스프링 시큐리티에서 가장 일반적으로 쓰인다.
- 주요 설정 정보

  - filterProcessingUrl : 로그인을 처리해 줄 URL (POST)
  - username parameter : POST에 username에 대한 값을 넘겨줄 인자의 이름
  - password parameter : POST에 password에 대한 값을 넘겨줄 인자의 이름
  - 로그인 성공시 처리 방법
    - defaultSuccessUrl : alwaysUse 옵션 설정이 중요
    - successHandler
  - 로그인 실패시 처리 방법
    - failureUrl
    - failureHandler
  - authenticationDetailSource : Authentication 객체의 details 에 들어갈 정보를 직접 만들어 줌.

## DefaultLogoutPageGeneratingFilter

- GET /logout 을 처리한다.
- POST /logout 을 요청할 수 있는 UI 를 제공한다.
- csrf

## LogoutFilter

- POST /logout 을 처리한다. processiongUrl 을 변경하면 바꿀 수 있다.
- 로그 아웃을 처리한다.
  - session 삭제
  - Authentication 삭제
  - 쿠키 삭제
  - (기본) 로그인 페이지로 redirect
  ```java
  private void doFilter(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
  		throws IOException, ServletException {
  	if (requiresLogout(request, response)) {
  		Authentication auth = SecurityContextHolder.getContext().getAuthentication();
  		if (this.logger.isDebugEnabled()) {
  			this.logger.debug(LogMessage.format("Logging out [%s]", auth));
  		}
  		this.handler.logout(request, response, auth);
  		this.logoutSuccessHandler.onLogoutSuccess(request, response, auth);
  		return;
  	}
  	chain.doFilter(request, response);
  }
  ```
