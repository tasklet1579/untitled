✔️ 테스트 대상

```
지하철 노선도 서비스

기능
- 역 관리
- 노선 관리
- 구간 관리
- 구간 검색

구성
- 프록시 (Nginx) ↔ 웹 (Tomcat) ↔ 데이터베이스 (MySQL)

* 성능 부하 테스트는 Bastion 서버에서 진행함
```

✔️ 목표값 계산

```
1일 사용자 수 : 10,000
피크 시간대의 집중률 : 최대 트래픽이 평균 트래픽 보다 3배 높다고 가정
1명당 1일 평균 요청 건수 : 50

Throughput : 시간당 평균, 최대 처리량 
- 1일 사용자 수 X 1명당 1일 평균 요청 건수 = 1일 총접속 수 = 500,000
- 1일 총접속 수 / 86,400s = 1일 평균 RPS = 5.787
- 1일 평균 RPS X 피크 시간대의 집중률 = 1일 최대 RPS = 17.361

Latency : 지연 시간
- 100ms 이하

VUser : 가상 사용자
- Request Rate : measured by the number of requests per second
- R : the number of requests per VU iteration
- T : a value larger than the time needed to complete a VU iteration

T = (R * http_req_duration) (+L) ; 내부망에서 테스트할 경우 예상 latency를 추가한다
VUser = (목표 rps * T) / R

예를 들어, 8개의 요청이 있고 왕복 시간이 0.5s, 지연 시간을 1s로 한다면 
평균 트래픽 VUser = 5.787 * 5 / 8 = 3.616 → 4
최대 트래픽 VUser = 17.361 * 5 / 8 = 10.850 → 11
```

✔️ 목표값 설정

```
Smoke
- VUser : 1~2
- Throughput : ~17.361
- Latency : ~100ms
- 소유 시간 : 10분

Load
- 평균 VUser : 4
- 최대 VUser : 11
- Throughput : ~17.361
- Latency : ~100ms
- 소유 시간 : 30분

Stress
- VUser : 점진적으로 증가시킨다
- 측정 시간 : 20분
```

✔️ ㅇㅇ

✔️ ㅇㅇ

✔️ ㅇㅇ
