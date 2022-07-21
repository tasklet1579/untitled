### 🎯 학습 목표

![image](../image/step8/image01.png)

- HTTP 개선에 따른 차이를 이해하고 Reverse Proxy 성능 개선을 해봅니다.
- HTTP Cache 전략을 이해하여 적절한 정책을 설정해봅니다.
- 쿼리를 최적화하여 조회 성능을 개선해봅니다.
- 인덱스를 설정하여 조회 성능을 개선해봅니다.

---

### 1. 화면 응답 개선하기

✏️ 요구사항
- 부하테스트 각 시나리오의 요청시간을 목푯값 이하로 개선
  - 개선 전 / 후를 직접 계측하여 확인

---

### 2. 스케일 아웃

✏️ 요구사항
- springboot에 HTTP Cache, gzip 설정하기
- Launch Template 작성하기
- Auto Scaling Group 생성하기
- Smoke, Load, Stress 테스트 후 결과를 기록

---

### 3. 쿼리 최적화

✏️ 요구사항
- 활동중인(Active) 부서의 현재 부서관리자(manager) 중 연봉 상위 5위안에 드는 사람들이 최근에 각 지역별로 언제 퇴실(O)했는지 조회해보세요.
- 인덱스 설정을 추가하지 않고 1s 이하로 반환합니다. 

---

### 4. 인덱스 설계

✏️ 요구사항
- 주어진 데이터셋을 활용하여 아래 조회 결과를 100ms 이하로 반환 
  - [Coding as a Hobby](https://insights.stackoverflow.com/survey/2018#developer-profile-_-coding-as-a-hobby) 와 같은 결과를 반환하세요.
  - 프로그래머별로 해당하는 병원 이름을 반환하세요. (covid.id, hospital.name)
  - 프로그래밍이 취미인 학생 혹은 주니어(0-2년)들이 다닌 병원 이름을 반환하고 user.id 기준으로 정렬하세요. (covid.id, hospital.name, user.Hobby, user.DevType, user.YearsCoding)
  - 서울대병원에 다닌 20대 India 환자들을 병원에 머문 기간별로 집계하세요. (covid.Stay)
  - 서울대병원에 다닌 30대 환자들을 운동 횟수별로 집계하세요. (user.Exercise)
