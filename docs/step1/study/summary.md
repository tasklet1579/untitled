### ✏️ AssertJ Exception Assertions

AssertJ
- assertion을 제공하는 자바 라이브러리
- 다양한 검증 메서드를 제공하고 있어서 테스트 코드를 더욱 쉽게 작성할 수 있다.
- 메서드 체이닝을 지원하여 직관적인 테스트 흐름을 나타낼 수 있다.

*assertThatThrownBy*
```
import static org.assertj.core.api.Assertions.assertThatThrownBy;

@DisplayName("위치 값을 벗어나면 Exception이 발생한다.")
@Test
void charAt_throwException_givenIndexGreaterThanLength() {
    assertThatThrownBy(() -> {
        // ...
    }).isInstanceOf(IndexOutOfBoundsException.class)
      .hasMessageContaining("Index: 2, Size: 2");
}
```

*assertThatExceptionOfType*
```
import static org.assertj.core.api.Assertions.assertThatExceptionOfType;

@DisplayName("위치 값을 벗어나면 Exception이 발생한다.")
@Test
void charAt_throwException_givenIndexGreaterThanLength() {
    assertThatExceptionOfType(IndexOutOfBoundsException.class)
        .isThrownBy(() -> {
            // ...
    }).withMessageMatching("Index: \\d+, Size: \\d+");
}
```

자주 발생하는 Exception의 경우 아래의 메서드를 제공하고 있다.
- assertThatIllegalArgumentException()
- assertThatIllegalStateException()
- assertThatIOException()
- assertThatNullPointerException()

*Behaviour-Driven Development*
```
import static org.assertj.core.api.Assertions.catchThrowable;

@DisplayName("위치 값을 벗어나면 Exception이 발생한다.")
@Test
void charAt_throwException_givenIndexGreaterThanLength() {
    Throwable thrown = catchThrowable(() -> { throw new ...  });
    
    assertThat(thrown).isInstanceOf(IndexOutOfBoundsException.class)
                      .hasMessageContaining("...");
}
```

### ✏️ JUnit 5 Parameterized Tests

다른 값을 사용하여 하나의 테스트 코드를 반복해서 실행할 수 있다.

@ParameterizedTest를 추가하는 것을 제외하고는 다른 테스트와 동일하다.

*Simple Values*
- 테스트 메서드에 값을 순서대로 하나씩 전달할 때 사용할 수 있다.
- 지원하는 자료형은 다음과 같다.
  - short, byte, int, long, float, double, char, java.lang.String, java.lang.Class
```
public class Strings {
    public static boolean isBlank(String input) {
        return input == null || input.trim().isEmpty();
    }
}
```
```
@ParameterizedTest
@ValueSource(strings = {"", "  "})
void isBlank_ShouldReturnTrueForNullOrBlankStrings(String input) {
    assertTrue(Strings.isBlank(input));
}
```

Null and Empty Values
```

```

Enum
```

```

CSV Literals
```

```

Method
```

```

Customizing Display Names
```

```
