### ✏️ ATDD

요구사항을 검증하는 테스트로 소프트웨어를 개발하는 프로세스

TDD는 작은 단위의 요구 사항을 테스트하지만 ATDD는 시나리오 형태의 요구 사항을 테스트한다.

인수 테스트는 블랙 박스 테스트의 성격을 가지고 있기 때문에 클라이언트는 결과물의 내부 구현이나 사용된 기술을 기반으로 검증하기 보다는 표면적으로 확인할 수 있는 요소를 바탕으로 검증하려고 한다.

🧰 인수 테스트 도구

Spring Boot Test
- 테스트에 사용할 ApplicationContext를 쉽게 지정하게 도와줌
- 기존 @ContextConfiguration의 발전된 기능
- SpringApplication에서 사용하는 ApplicationContext를 생성해서 작동
- [Testing Spring Boot Applications](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing.spring-boot-applications)

WebEnvironment
- @SpringBootTest의 webEnvironment 속성을 사용하여 테스트 서버의 실행 방법을 설정
  - MOCK: Mocking된 웹 환경을 제공, MockMvc를 사용한 테스트를 진행할 수 있음
  - RANDOM_PORT: 실제 웹 환경을 구성
  - DEFINED_PORT: 실제 웹 환경을 구성, 지정한 포트를 listen
  - NONE: 아무런 웹 환경을 구성하지 않음

RestAssured
- REST-assured는 REST API의 테스트 및 검증을 단순화하도록 설계
- HTTP 작업에 대한 검증을 위한 풍부한 API를 활용 가능

```
@DisplayName("지하철역 관련 기능")
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.DEFINED_PORT)
public class StationAcceptanceTest {
    @LocalServerPort
    int port;
    
    @BeforeEach
    public void beforeEach() {
        if (RestAssured.port == RestAssured.UNDEFINED_PORT) {
            RestAssured.port = port;
        }
    }
    
    @Test
    void createStation() {
        ...
                
        createStation(request);
    }
    
    ExtractableResponse<Response> createStation(StationRequest request) {
        return RestAssured.given().log().all()
                          .body(request)
                          .contentType(MediaType.APPLICATION_JSON_VALUE)
                          .when().post("/stations")
                          .then().log().all()
                          .extract();
    }
}
```

🆚 MockMvc vs WebTestClient vs RestAssured
- MockMvc
  - @SpringBootTest의 webEnvironment.MOCK과 함께 사용 가능하며 mocking 된 web environment(ex tomcat) 환경에서 테스트
- WebTestClient
  - @SpringBootTest의 webEnvironment.RANDOM_PORT나 DEFINED_PORT와 함께 사용, Netty를 기본으로 사용
- RestAssured
  - 실제 web environment(Apache Tomcat)을 사용하여 테스트

### ✏️ 커밋 메시지

### ✏️ 커밋 메시지

### ✏️ 커밋 메시지

### ✏️ 커밋 메시지
