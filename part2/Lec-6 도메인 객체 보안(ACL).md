# AOP 를 활용한 동적 권한 설계

권한 체크가 단순한 권한(Authority)만으로 어려운 복잡한 경우가 있을 수 있습니다.

아래는 Spring Security 스펙에서 ACL이 필요한 경우를 설명하기 위해 만든 권한 체크의 3요소 입니다.

- 누가 (Authentication)
- 어떤 메소드에서 (MethodInvocation)
- 어떤 객체에 접근할 수 있는지 (DomainObject) => ACL

이를 위해, spring-security-acl 모듈이 간단한 접근권한과 관련해 표준 DB 모델을 만들어서 제공 하고 있습니다.

아래는 spring-security-acl이 제공하는 것으로 접근 정보를 DB화 하고 있습니다.

## ACL

<img src="../images/fig-28-acl-diagram.png" width="600" style="max-width:600px;width:100%;" />

- ACL_CLASS : 도메인 객체의 종류. 보통은 class 로 매핑되는 id 값을 조회 합니다.
- ACL_OBJECT_IDENTITY : 보안의 대상이 되는 정보 객체. 트리 구조로 되어 있습니다.
  - Id : ACL_CLASS 의 id 값
  -
- ACL_SID : principal. 권한의 주체가 되는 사용자 정보
- ACL_ENTRY :
