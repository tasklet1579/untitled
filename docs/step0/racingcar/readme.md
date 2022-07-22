### ✏️ 기능 요구사항

- 주어진 횟수 동안 n대의 자동차는 전진 또는 멈출 수 있다.
- 각 자동차에 이름을 부여할 수 있다.
- 전진하는 자동차의 이름을 출력한다.
- 자동차 이름은 쉼표(,)를 기준으로 구분하며 5자 이하만 가능하다.
- 사용자는 몇 번의 이동을 할 것인지를 입력할 수 있어야 한다.
- 0-9 사이에 임의의 값이 4 이상일 경우 전진, 3 이하일 경우 멈춘다.
- 자동차 경주 게임을 완료한 후 누가 우승했는지를 알려준다.
- 우승자가 한 명 이상일 경우, 쉼표(,)로 이름을 구분해 출력한다.
- 사용자가 잘못된 값을 입력할 경우 IllegalArgumentException을 발생시킨다.
- Exception과 함께 "[ERROR]"로 시작하는 메시지를 출력 후 다시 입력을 받는다.

### ✏️ 프로그래밍 요구사항

- JDK 8에서 정상 동작하지 않은 경우 0점 처리한다.
- 테스트가 실패할 경우 0점 처리한다.
- [mission-utils](https://github.com/woowacourse-projects/mission-utils) 에서 제공하는 API를 사용하여 구현해야 한다.
- 자바 코드 컨벤션을 준수한다.
- 들여쓰기 깊이는 1단계를 초과하지 않는다.
- 자바 8 Stream을 사용하지 않는다.
- else를 사용하지 않는다.
- 메서드는 하나의 기능만 수행한다.
- 도메인 로직에 단위 테스트를 구현한다.
- [일급콜렉션을 활용해 구현한다.](https://developerfarm.wordpress.com/2012/02/01/object_calisthenics_/)
- [모든 원시 값과 문자열을 포장한다.](https://developerfarm.wordpress.com/2012/01/27/object_calisthenics_4/)

### 🖨️ 입력과 출력

```
경주할 자동차 이름을 입력하세요.(이름은 쉼표(,) 기준으로 구분)
pobi,crong,honux
시도할 횟수는 몇회인가요?
5

실행 결과
pobi : -
crong :
honux : -

pobi : --
crong : -
honux : --

pobi : ---
crong : --
honux : ---

pobi : ----
crong : ---
honux : ----

pobi : -----
crong : ----
honux : -----

최종 우승자: pobi, honux
```

### 💻 프로그램 순서

- [x] "경주할 자동차 이름을 입력하세요." 메시지를 출력한다.
- [x] 

### 🔑️️️ 책임과 역할 분리

- domain
