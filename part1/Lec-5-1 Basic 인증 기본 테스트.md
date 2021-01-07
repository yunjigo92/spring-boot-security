## 실습 예

- 기본적으로 SPA로만 서비스하는 사이트이다. 그래서 form 로그인이 필요없다.
- 아래와 같이 필터체인을 설정하고

  ```java

  @EnableWebSecurity
  public class SecurityConfig extends WebSecurityConfigurerAdapter {

      @Override
      protected void configure(AuthenticationManagerBuilder auth) throws Exception {
          auth.inMemoryAuthentication()
                  .withUser(User.withDefaultPasswordEncoder()
                          .username("user1")
                          .password("1111")
                          .roles("USER")
                  .build())
                  ;
      }

      @Override
      protected void configure(HttpSecurity http) throws Exception {
          http
                  .httpBasic()
                  ;
      }

  }

  ```

- 다음과 같이 리소스를 서비스한 다음

  ```java
  @RestController
  public class HomeController {

      @RequestMapping("/greeting")
      public String hello(){
          return "Hello jongwon";
      }

  }
  ```

- 아래와 같이 테스트를 진행하면 된다.

  ```java
  @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
  public class BasicTokenTest {

      @LocalServerPort
      int port;

      private RestTemplate restTemplate = new RestTemplate();

      @DisplayName("1. Basic Token Test")
      @Test
      void test_1(){

          String url = format("http://localhost:%d%s", port, "/greeting");
          HttpHeaders headers = new HttpHeaders();
          headers.add(HttpHeaders.AUTHORIZATION, "basic "+ Base64.getEncoder().encodeToString("user1:1111".getBytes()));
          HttpEntity entity = new HttpEntity("", headers);

          ResponseEntity<String> response = restTemplate.exchange(url,
                  HttpMethod.GET, entity, String.class);

          assertEquals("Hello jongwon", response.getBody());
      }

  }

  ```
