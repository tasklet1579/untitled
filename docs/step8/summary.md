### ✏️ 웹 성능 개선하기

Web Server
- 매우 작은 데이터를 대량으로 전송하거나,하드디스크 읽기와 쓰기가 발생하지 않는 경우에 적합하다.
  - 캐싱 설정
  - CDN 사용하기
  - keep-alive 설정
  - gzip 압축
  - 불필요한 다운로드 제거
  - 불필요한 작업을 지연로딩
  - 스크립트 병합하여 요청수 최소화
  - HTTP 프로토콜 개선
    - TCP 기반의 HTTP는 요청마다 Connection이 생성되어 연결 비용이 매우 크다.
      - 3way handshake
      - slow start

Application Server
- 복잡한 연산 처리, 동영상 데이터 처리, 데이터베이스 처리 등에 적합하다.
  - 비즈니스 로직 개선
  - 조회 성능 개선
  - 비동기 처리
  - 데이터 캐싱 등

### ✏️ Servlet이란?

- 자바 진영에서 동적인 웹 페이지를 구현하기 위해 만든 표준 모델
- Servlet 표준에 대한 interface 구현체는 Servlet Container(tomcat, jetty)가 제공함

***요청, 응답 과정***

1. 사용자가 브라우저를 통해 서버에 HTTP 요청을 보낸다.
2. 요청을 받은 서블릿 컨테이너는 request, response 두 객체를 만든다.
3. 서블릿 컨테이너는 요청을 처리할 수 있는 서블릿을 찾아서 스레드를 할당하고 request, response 객체를 전달한다
4. HTTP method 에 따라 doGet(), doPost() 등 메소드를 호출한다.
5. 요청 결과를 응답한 후 request, response 객체를 제거하고 자원을 반납한다.
