# MethodSecurityInterceptor

권한 체크는 필터에서 1차로 체크가 되고, 2차 이후는 메소드에서 AOP 를 이용해 체크가 됩니다. MethodSecurityInterceptor 는 2차 이후의 메소드 체크에 관여합니다. 이를 설정하는 곳이 GlobalMethodSecurityConfiguration 입니다.
이 곳에서 secured 를 설정하면 @Secured 로 설정된 권한을 체크합니다. prePostEnabled=true 로 설정하면 @PreAuthorize, @PreFilter, @PostAuthorize, @PostFilter 로 설정된 권한을 체크합니다.

MethodSecurityInterceptor 에서 중요한 멤버는 아래 세가지 입니다.

- AccessDecisionManager : @Secured 나 @PreAuthorize, @PreFilter 를 처리합니다.
- AfterInvocationManager : @PostAuthorize, @PostFilter 를 처리합니다.
- RunAsManager : 임시권한 부여

<img src="../images/fig-24-access-decision-manager.png" width="600" style="max-width:600px;width:100%;" />

## AfterInvocationManager

Authentication 통행증만 가지고는 권한 체크를 충분히 했다고 볼 수가 없습니다. 보통, 어떤 객체의 값을 변경해야 하는 경우에는 메소드에 들어오기 전에, 값을 조회하려고 하는 경우에는 값을 가져온 이후에 각각 접근 권한을 체크해줘야 합니다.

체크해야 할 대상이 한개라면 Pre/PostAuthorized 로 체크를 하면 되지만, 대상이 복수개라면 보통은 리스트로 묶이기 때문에 대상을 filtering을 해서 들어가거나 넘겨야 합니다.

물론, 메소드를 처리하는 중간에 권한을 검사해야 하는 경우도 있습니다. 이 경우는 Proxy 빈의 특징을 잘 파악해서 메서드 간에 권한 검사가 충분히 이루어지도록 annotation을 설계해서 처리할 수 있습니다.

### 시험지 테스트

- tutor1이 시험지 ...

## Method Security Meta Annotations

코드의 가독성을 향상시키기 위해 meta annotation을 쓸수도 있다. 반복되는 복잡한 표현식이 있다면 특별히 유용하다. 예를들면 이렇다

@PreAuthorize("#contact.name == authentication.name")
을

@Retention(RetentionPolicy.RUNTIME)
@PreAuthorize("#contact.name == authentication.name")
public @interface ContactPermission {}
위와같이 할수있다. 단, JSR-250 스펙은 지원되지 않음
