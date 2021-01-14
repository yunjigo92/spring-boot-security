# 세션 관리

## ConcurrentAuthenticationFilter

- 동시 세션의 개수를 제한할 수 있다. 만약 세션의 개수를 초과하는 경우

  - 이전 사용자 세션 만료
  - 추가 로그인 하려는 사용자의 세션 만료

- 세션 정책
  - Always : 항상 세션을 생성함
  - If_Required : 필요시 생성
  - Never : 생성하지 않음. 존재하면 사용함.
  - Stateless : 생성하지 않음. 존재해도 사용하지 않음.

## 실습을 통해 확인할 내용

-
