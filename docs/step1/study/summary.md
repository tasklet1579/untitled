### ✏️ AssertJ Exception Assertions

AssertJ
- assertion 을 제공하는 자바 라이브러리
- 다양한 검증 메서드를 제공하고 있어서 테스트 코드를 더욱 쉽게 작성할 수 있다.
- 메서드 체이닝을 지원하여 직관적인 테스트 흐름을 나타낼 수 있다.

assertThatThrownBy
```
import static org.assertj.core.api.Assertions.assertThatThrownBy;

@DisplayName("위치 값을 벗어나면 Exception 이 발생한다.")
@Test
void charAt_throwException_givenIndexGreaterThanLength() {
    assertThatThrownBy(() -> {
        // ...
    }).isInstanceOf(IndexOutOfBoundsException.class)
      .hasMessageContaining("Index: 2, Size: 2");
}
```

assertThatExceptionOfType
```
import static org.assertj.core.api.Assertions.assertThatExceptionOfType;

@DisplayName("위치 값을 벗어나면 Exception 이 발생한다.")
@Test
void charAt_throwException_givenIndexGreaterThanLength() {
    assertThatExceptionOfType(IndexOutOfBoundsException.class)
        .isThrownBy(() -> {
            // ...
    }).withMessageMatching("Index: \\d+, Size: \\d+");
}
```

자주 발생하는 Exception 의 경우 아래의 메서드를 제공하고 있다.
- assertThatIllegalArgumentException()
- assertThatIllegalStateException()
- assertThatIOException()
- assertThatNullPointerException()

Behaviour-Driven Development
```
import static org.assertj.core.api.Assertions.catchThrowable;

@DisplayName("위치 값을 벗어나면 Exception 이 발생한다.")
@Test
void charAt_throwException_givenIndexGreaterThanLength() {
    Throwable thrown = catchThrowable(() -> { throw new ...  });
    
    assertThat(thrown).isInstanceOf(IndexOutOfBoundsException.class)
                      .hasMessageContaining("...");
}
```

### ✏️ JUnit 5 Parameterized Tests

다른 값을 사용하여 하나의 테스트 코드를 여러번 반복 
