# RememberMeAuthenticationFilter

- 인증 정보를 세션 관리하는 경우, 쿠키를 이용해 로그인을 기억했다 자동으로 재로그인 시켜주는 기능입니다.

  - key : Hash 암/복호화에 사용할 키 값
  - token-validity-seconds : 토큰 유효 기간
  - authentication-success-handler-ref : 핸들러를 커스마이징 했다면 로그인 성공 후 수행할 로직
  - user-service-ref : UserDetailsService를 커스터마이징 했을 경우 주입

- 토큰 기반과 DB 기반으로 나눌 수 있습니다.
- PersistentTokenBasedRememberMeServices 테스트 하기

## RememberMe 테스트 하기

- 기존의 student 유저를 가지고 로그인 한 경우로 테스트 한다.
- remember-me 쿠키가 만들어지는 것을 확인한다.
- remember-me 쿠키가 있는 경우 RememberMeAuthenticationFilter 를 통해 로그인이 되는 것을 확인한다.
- remember-me 쿠키를 삭제하면 재로그인 하는 것을 확인한다.
- 로그 아웃하면 remember-me 쿠키가 삭제되는 것을 확인한다.

## 참고

- https://www.baeldung.com/spring-security-persistent-remember-me
- https://codevang.tistory.com/274
- https://codevang.tistory.com/277
- https://codevang.tistory.com/280
-
