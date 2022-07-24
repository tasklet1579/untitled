### ✏️ 웹 성능 개선하기

Web Server
- 매우 작은 데이터를 대량으로 전송하거나,하드디스크 읽기와 쓰기가 발생하지 않는 경우에 적합하다.
- 클라이언트와의 커넥션을 어떻게 효율적으로 관리할지 집중한다.
  - 캐싱 설정
  - CDN 사용하기
    - 여러 노드를 가진 네트워크에 컨텐츠를 저장하여 제공하는 프록시의 일종
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
- 비즈니스 로직 개선, 조회 성능 개선에 집중한다.
  - 비즈니스 로직 개선
  - 조회 성능 개선
  - 비동기 처리
  - 데이터 캐싱 등
    - ETag
    - Cache-Control
      - 일부 파일에 변경이 발생한 경우 배포 시간 또는 버전 등을 활용해 URL을 변경한다.

### ✏️ Servlet이란?

- 자바 진영에서 동적인 웹 페이지를 구현하기 위해 만든 표준 모델
- Servlet 표준에 대한 interface 구현체는 Servlet Container(tomcat, jetty)가 제공함

요청, 응답 과정

1. 사용자가 브라우저를 통해 서버에 HTTP 요청을 보낸다.
2. 요청을 받은 서블릿 컨테이너는 request, response 두 객체를 만든다.
3. 서블릿 컨테이너는 요청을 처리할 수 있는 서블릿을 찾아서 스레드를 할당하고 request, response 객체를 전달한다
4. HTTP method 에 따라 doGet(), doPost() 등 메소드를 호출한다.
5. 요청 결과를 응답한 후 request, response 객체를 제거하고 자원을 반납한다.

### ✏️ SQL 기본

```
SELECT Country
    ,  COUNT(*) AS `고객 수` 
  FROM Customers 
 WHERE Country <> 'Norway'
 GROUP BY Country
HAVING COUNT(Country) = 1
 ORDER BY Country;

1. FROM에서 데이터 집합을 만든다.
2. WHERE는 FROM에서 만든 데이터 집합을 조건에 맞게 걸러낸다.
3. GROUP BY는 WHERE에서 필터링한 (조건에 맞는 데이터를 걸러낸) 데이터를 그룹화한다.
4. HAVING은 GROUP BY에서 집계한 데이터 집합을 다시 조건에 맞게 필터링한다.
5. SELECT에서는 그룹화하고 필터링한 데이터 집합을 집계한다.
6. 모두 진행한 이후, ORDER BY를 통해 집계한 데이터 집합을 정렬한다.
```

***서브쿼리***
```
SELECT (SELECT COUNT(*) FROM [Customers] WHERE Country = 'Germany') AS `Germany인 사람`
    ,  (SELECT COUNT(*) FROM [Customers] WHERE Country = 'Mexico') AS `Mexico인 사람`
```
SELECT 절에 추가하기

```
SELECT Country
    ,  CustomerName
  FROM (SELECT * FROM Customers);

```
FROM 절에 추가하기

```
SELECT * 
  FROM Products 
 WHERE Price = (SELECT MAX(Price) FROM Products);

```
WHERE 절에 추가하기

***조인문***
```
SELECT * FROM Products 
  JOIN OrderDetails 
    ON Products.ProductID = OrderDetails.ProductID 
 WHERE Products.ProductID IN (1, 30)
```

