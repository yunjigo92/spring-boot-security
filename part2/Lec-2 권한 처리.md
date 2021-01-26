# 권한 처리

## 필터에서 권한 체크하기

WebSecurityConfigurarAdapter 에서 설정합니다.

```java

  // HttpSecurity 에 설정

```

## 메쏘드에서 권한 체크 하기

- SecurityExpressionRoot 클래스에서 설정

| 표현식                                                               | 의미                                                                                                                                                     |
| -------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------- |
| hasRole(String role)                                                 | princial 이 해당 role을 가지고 있으면 true                                                                                                               |
| hasAnyRole(String... roles)                                          | principal 이 제시한 role 중에 한개라도 있으면 true.                                                                                                      |
| hasAuthority(String authority)                                       | principal 이 제시한 authority를 가지고 있으면 true                                                                                                       |
| principal                                                            | 인증서의 principal 객체에 바로 접근 가능                                                                                                                 |
| permitAll                                                            | 모두 허용                                                                                                                                                |
| denyAll                                                              | 모두 거부                                                                                                                                                |
| isAnonymous()                                                        | 익명사용자                                                                                                                                               |
| isRememberMe()                                                       | 자동 로그인 사용자                                                                                                                                       |
| isAuthenticated()                                                    | 익명사용자가 아니면 true                                                                                                                                 |
| isFullyAuthenticated()                                               | 익명사용자나 자동로그인한 사용자가 아니면 true                                                                                                           |
| hasPermission(Object target, Object permission)                      | Returns true if the user has access to the provided target for the given permission. For example, hasPermission(domainObject, 'read')                    |
| hasPermission(Object targetId, String targetType, Object permission) | Returns true if the user has access to the provided target for the given permission. For example, hasPermission(1, 'com.example.domain.Message', 'read') |

### WebExpressionVoter

- Bean 객체를 만들고 호출해서 사용할 수 있습니다.
  - @ 로 빈 이름을 사용
- URL 에 path variable 을 선언해서 체크할 수 있습니다.
  - # 으로 변수 이름에 접근
- WebSecurityExpressionRoot 를 사용합니다.

## AccessDecisionVoter

- 권한 심사 위원회에 참여하는 투표자
- 결정
  - ACCESS_GRANTED : 허가
  - ACCESS_DENIED : 불허
  - ACCESS_ABSTAIN : 보류

### 1. AuthenticatedVoter

인증(통행증)을 받았다면 그 인증의 종류가 어떤 종류인지를 판단합니다. 이제 막 인증을 받고 들어온 사용자와 RememberMe 토큰을 통해서 들어온 사용자와 익명 사용자를 구분하기 위해 쓰입니다. RememberMe 인증 사용자는 탈취된 토큰을 가지고 들어온 사용자일 수 있기 때문에 필요한 경우 한번 더 인증을 요구할 수 있습니다.

- fully authenticated
- remember me
- anonymous

### 2. RoleVoter

Role 기반의 권한은 리눅스부터 아파치, 톰켓등 IT 초기부터 전통적으로 구현해서 사용하던 가장 직관적인 권한 체계입니다. 하지만, Role 을 기반으로 권한을 판단하기엔, 상황이 너무 다양해졌죠. 그래서 Role 을 확장한 Authority 기반의 권한 체계를 사용하고 있습니다. 그렇지만, 기존의 Role 기반이 가지고 있는 직관적이고 계층적인 사용성을 그대로 사용할 수 있도록 해주기 위해 RoleVoter가 쓰입니다.

- ROLE_xxx : GrantedAuthority
- 권한 계층 선언 : RoleHierarchyVoter

### 3. WebExpressionVoter

- 필터에서 설정하는 voter (FilterInvocation)
- SpEL 로 표현한 권한식

### 4. PreInvocationAuthorizationAdviceVoter

### 5. AbstractACLVoter

---

## Granted Authority

- Role
  - Role\_ 로 시작하는 권한으로 변환해줌.
  - Role Hierarchy 장치를 사용할 수 있음.
- Authority
  - 다양한 권한을 설계할 수 있는 유연한 구조임.
