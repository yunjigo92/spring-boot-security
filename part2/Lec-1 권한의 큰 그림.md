AccessDecisionVoter 를 만들어서 테스트 한다.

## AccessDecisionManager : 권한 위원회

- SecurityFilerChain 당 한개의 AccessDecisionManager 를 둘 수 있습니다.
- AffirmativeBased : 한개라도 허가하면 허가됨.
- ConsensusBased : 다수결
- UnanimouseBased : 만장일치

## AuthenticatedVoter

- fully authenticated
- remember me
- anonymous

## RoleVoter

- ROLE_xxx : GrantedAuthority

## WebExpressionVoter

- SpEL 로 표현한 권한식

## PreInvocationAuthorizationVoter

## AccessDecisionVoter

- 권한 심사 위원회에 참여하는 투표자
- 결정
  - ACCESS_GRANTED : 허가
  - ACCESS_DENIED : 불허
  - ACCESS_ABSTAIN : 보류

### 참고 자료

- https://www.baeldung.com/spring-security-custom-voter
