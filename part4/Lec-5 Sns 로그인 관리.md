# OAuth2 와 스프링

OAuth2 인증서버는 Resource 서버와 Client 서버, Scope 에대한 관리와 토큰 인증 관리를 해야 한다. 이것 들을 관리하려면 매우 많은 구현이 필요하다.

여기서는 간단히 OAuth2 인증 구조를 설명하고, OAuth2 인증서버로 오픈 소스인 Keycloak 서버를 사용해 개념을 검증하기로 하자. 그리고 이어서 OAuth2 인증서버로 구글, 페이스북, 네이버, 카카오 등을 연동하는 방법에 대해서도 알아보자.

## 인증 서버

스프링에서 공식적으로 OAuth 의 인증서버에 대한 지원이 deprecated 되었기 때문에 앞으로 인증서버를 스프링 라이브러리를 이용해 구현하기를 기대하기는 어려울 것이다. 구지 스프링을 이용해 인증서버를 구현할 필요는 없을 것이라 생각한다.

- Keycloak 서버 다운로드 : https://www.keycloak.org/downloads

마이크로 서비스 아키텍처(MSA)를 사용해서 서비스 해야 하는 상황들이 늘어나고 있어서, 인증서버와 리소스 서버를 분리해서 운영해야 할 상황들이 빈번해지고 있다.
마이크로서비스의 가장 큰 특징은 모듈별로 관심사를 분리하던 것을 서버별로 관심사를 분리하는 작업이라고 볼 수 있다.
그런 관점에서 인증도 하나의 관심사 이기 때문에 인증서버를 분리해서 운영하려는 움직임은 당연하다고 볼 수 있다.
그런에 인증 서버가 반드시 OAuth2 를 구현해야 하는 건 아니다.

- 도커에 keycloak 설치하기

```
> docker network create keycloak-network
> docker run -d --name postgres --net keycloak-network -e POSTGRES_DB=keycloak -e POSTGRES_USER=jongwon -e POSTGRES_PASSWORD=keycloak postgres
> docker run -p 9040:8080 --name keycloak --net keycloak-network -e DB_USER=jongwon -e DB_PASSWORD=keycloak -e DB_ADDR=postgres jboss/keycloak
> docker exec keycloak /opt/jboss/keycloak/bin/add-user-keycloak.sh -u admin -p 1234
> docker restart keycloak
```

## 리소스 서버

- spring-boot-starter-oauth2-resource-server 모듈로 구현되어 있다.
-

리소스 서버는 인증된 사용자에게만 리소스를 제공해주는 서버이다.
서버는 사용자가 누구인지 눈으로 볼 수 없기 때문에, 요청을 할 때 해더에 묻어오는 인증 토큰을 가지고 판단할 수 밖에 없다. 리소스 서버가 관심을 가지는 것은 다음과 같다.

- 이 토큰이 인증서버에서 인증받은게 맞나?
- 토큰 사용 기간이 만료되지 않았나?
- 이 리소스를 사용할 수 있다고 허가한건가? (인증)
- 대상 리소스를 인증받은 사용자가 접근 가능한가? (권한)

## OAuth2Authentication : 인증 토큰

## OAuth2AccessToken : 권한 관련

- OAuth2 의 권한은 보통 Scope\_ 로 시작하는 Authentication 을 준다.
-

## 참고

- 리소스 서버 예제 : https://www.baeldung.com/spring-security-oauth-resource-server
- keycloak 도커 이미지 : https://github.com/keycloak/keycloak-containers/blob/12.0.1/server/README.md
