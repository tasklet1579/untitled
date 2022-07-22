### ✏️ Sociable and Solitary

```
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

import java.util.Arrays;

public class LineTest {
    @DisplayName("구간 추가")
    @Test
    void addSection() {
        // given
        Station 강남역 = new Station("강남역");
        Station 잠실역 = new Station("잠실역");
        Station 역삼역 = new Station("역삼역");
        Line 2호선 = new Line("2호선", "green", 강남역, 잠실역, 10);

        // when
        2호선.addSection(잠실역, 역삼역);

        // then
        Assertions.assertThat(2호선).containsExactly(Arrays.asList(강남역, 잠실역, 역삼역));
    }
}
```

협력 객체를 실제 객체로 사용하는지 Mock(가짜) 객체로 사용하는지에 따라 테스트 구현이 달라짐

- 실제 객체를 사용 하면 협력 객체의 행위를 협력 객체 스스로가 정의
- 가짜 객체를 사용 하면 협력 객체의 행위를 테스트가 정의

***실제 객체를 사용할 경우***

실제 객체를 사용 할 경우 협력 객체의 상세 구현에 대해서 알 필요가 없음

하지만 협력 객체의 정상 동작 여부에 영향을 받음

***가짜 객체를 사용할 경우***

테스트 대상을 검증할 때 외부 요인(협력 객체)으로 부터 철저히 격리

하지만 테스트가 협력 객체의 상세 구현을 알아야 함

### ✏️ Classist vs Mockist

***Classist의 단위 테스트***

테스트를 격리해야하는 대상은 코드가 아니라 또 다른 테스트

테스트 간의 공유하는 의존성이 아니라면 실제 객체를 사용

***Mockist의 단위 테스트***

테스트 대상을 협력 객체로부터 격리하기 위해 테스트 대상이 의존하는 모든 것을 가짜 객체로 대체

참고 자료
- [테스트하기 쉬운 코드로 개발하기](https://www.youtube.com/watch?v=Cz_a2gQp63c)
- [더즈, 티키의 Classic TDD VS Mockist TDD](https://www.youtube.com/watch?v=n01foM9tsRo)
- [의식적인 연습으로 TDD, 리팩토링 연습하기](https://www.youtube.com/watch?v=cVxqrGHxutU)
- [레거시코드에 테스트 추가하는 또 하나의 방법](https://www.youtube.com/watch?v=Dct4bGKCmI8)
