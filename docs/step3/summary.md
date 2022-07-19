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

🧪 테스트 격리

@DirtiesContext
- 효과적인 테스트 수행을 위해 스프링에서는 context caching 기능 지원
- @DirtiesContext를 활용하여 캐시 기능을 사용하지 않게 설정
- 매번 Context를 새로 구성하다보니 시간이 많이 걸림

DatabaseCleanup
- EntityManager를 활용하여 테이블 이름 조회 후 각 테이블 Truncate 수행
- ID auto increment 숫자를 1로 복구 시킴

[인수테스트에서 테스트 격리하기](https://tecoble.techcourse.co.kr/post/2020-09-15-test-isolation/)

### ✏️ @Transactional(readOnly = true)

```
A boolean flag that can be set to true if the transaction is effectively read-only, allowing for corresponding optimizations at runtime.  
Defaults to false.  
This just serves as a hint for the actual transaction subsystem; it will not necessarily cause failure of write access attempts. 
A transaction manager which cannot interpret the read-only hint will not throw an exception when asked for a read-only transaction but rather silently ignore the hint. 
```

> readOnly는 현재 해당 그 트랜잭션 내에서 데이터를 읽기만 할건지 설정하는 겁니다. 이걸 설정하면 DB 중에 read 락(lock)과 write 락을 따로 쓰는 경우 해당 트랜잭션에서 의도치 않게 데이터를 변경하는 일을 막아줄 뿐 아니라, 하이버네이트를 사용하는 경우에는 FlushMode를 Manual로 변경하여 dirty checking을 생략하게 해준다거나 DB에 따라 DataSource의 Connection 레벨에도 설정되어 약간의 최적화가 가능합니다. 아마 이 부분에서 특정 DB는 말씀하신대로 isolation 레벨이 READ_UNCOMMITED 처럼 동작할 여지도 있는 것 같습니다. 그런데 그게 꼭 좋은 건지는 생각해 봐야겠네요. READ_UNCOMMITED 면 팬텀 Read가 가능하단 거니까 isolation level을 명시적으로 선언해야 할지도 모르겠네요.

***DBMS 별 Transaction Read Only에 대한 동작 방식***

먼저 readOnly는 DB의 옵션이 아닌, 힌트입니다.
힌트라는 것은 해당 벤더사의 드라이버를 구현하는 측에서 활용을 할 수도 있고, 활용하지 않을 수 있다는건데요.
위와 같은 이유로 DB 벤더사 마다 다르게 동작합니다 ㅎㅎ
말씀하신 것과 같이 readOnly 옵션을 보고 캐시 영역에서의 변경 감지나 플러시는 작동하지 않게 구현한 벤더사도 있고, SELECT 쿼리에 대해 Read DB를 통해서만 조회하도록 구현한 벤더사도 있습니다~


### ✏️ @Embedded And @Embeddable



[출처](https://www.baeldung.com/jpa-embedded-embeddable)

### ✏️ Raw 타입은 사용하지 말자



[출처](https://mangkyu.tistory.com/137)

### ✏️ Map보다 DTO 클래스를 사용해야 하는 이유



[출처](https://mangkyu.tistory.com/164)

### ✏️ Map보다 DTO 클래스를 사용해야 하는 이유

StationRequest을 사용하면 추가로 생성자나 set 메서드를 작성해야는데 그렇지 않아도 objectmapper가 알아서 readValue해주기 때문에 어떤 의도로 물어보신지 궁금해요
