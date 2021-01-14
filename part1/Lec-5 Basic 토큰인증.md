# BasicTokenAuthenticationFilter

- 기본적으로 로그인 페이지를 사용할 수 없는 상황에서 사용한다.

  - SPA 페이지
  - 모바일 (기본적으로는 JWT 토큰 방식을 써야 한다.)

- SecurityContext 에 인증된 토큰이 없다면 아래와 같은 포멧의 토큰을 받아서 인증처리를 하고 간다.

  ```
  Authorization: Basic token
  token = username:password 가 Base64로 인코딩된 상태
  Authorization: Basic Y2hvaTox
  ```

- http 에서는 header 에 username:password 값이 묻어서 가기 때문에 보안에 매우 취약하다. 그래서, 반드시 https 프로토콜에서 사용할 것을 권장하고 있다.
- 최초 로그인시에만 인증을 처리하고, 이후에는 session에 의존한다.
- 에러가 나면 401 (UnAuthorized) 에러를 내려보내야 한다.

## SecurityContextPersistenceFilter

- SecurityContext 를 저장하고 있는 저장소에서 만료되지 않은 인증이 있으면 SecurityContextHolder 에 넣어준다. 이전에는 HttpSessionContextIntegrationFilter 이란 필터가 있었는데, 저장소가 반드시 세션일 필요는 없기 때문에 추상화된 객체로 발전된 필터라고 볼 수 있다.

- HttpSessionSecurityContextRepository : 서버 세션에 SecurityContext 를 저장하는 기본 저장소이다.
