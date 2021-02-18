# AfterInvocationManager

사전 체크 말고도 리턴된 객체에 대한 사후 체크를 합니다.

<img src="../images/fig-24-access-decision-manager.png" width="600" style="max-width:600px;width:100%;" />

## Method Security Meta Annotations

코드의 가독성을 향상시키기 위해 meta annotation을 쓸수도 있다. 반복되는 복잡한 표현식이 있다면 특별히 유용하다. 예를들면 이렇다

@PreAuthorize("#contact.name == authentication.name")
을

@Retention(RetentionPolicy.RUNTIME)
@PreAuthorize("#contact.name == authentication.name")
public @interface ContactPermission {}
위와같이 할수있다. 단, JSR-250 스펙은 지원되지 않음
