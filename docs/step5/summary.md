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



참고 자료

[테스트하기 쉬운 코드로 개발하기](https://www.youtube.com/watch?v=Cz_a2gQp63c)

[더즈, 티키의 Classic TDD VS Mockist TDD](https://www.youtube.com/watch?v=n01foM9tsRo)

[의식적인 연습으로 TDD, 리팩토링 연습하기](https://www.youtube.com/watch?v=cVxqrGHxutU)

[레거시코드에 테스트 추가하는 또 하나의 방법](https://www.youtube.com/watch?v=Dct4bGKCmI8)
