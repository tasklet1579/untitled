### ✏️ 커밋 메시지

커밋 메시지는 작업한 내용에 대한 이해가 가능하도록 작성한다.

***커밋 메시지 구조***

```
<type>(<scope>): <subject>      -- 제목 줄
<blank line>                    -- 빈 줄
<body>                          -- 본문
<blank line>                    -- 빈 줄
<footer>                        -- 바닥 글
```

type은 커밋의 성격을 나타내며 scope는 변경된 위치를, subject에는 간단하게 요약해서 적는다.

```
feat : 새로운 기능에 대한 커밋
fix : 버그 수정에 대한 커밋
build : 빌드 관련 수정에 대한 커밋
chore : 그 외 자잘한 수정에 대한 커밋
ci : CI 관련 설정 수정에 대한 커밋
docs : 문서 수정에 대한 커밋
style : 코드 스타일 혹은 포맷 등에 관한 커밋
refactor : 코드 리팩토링에 대한 커밋
test : 테스트 코드에 대한 커밋
```

body는 헤더에서 생략한 내용을 상세하게 작성합니다. 헤더로 충분한 표현이 가능하다면 생략이 가능하다.

footer는 선택 사항이므로 모든 커밋에 작성할 필요 없고 어떤 이슈에서 왔는지와 같은 참조 정보를 추가하는 용도로 사용한다.

### ✏️ 불필요한 객체 생성을 피하라

생성 비용이 큰 객체가 있다면 매번 생성하기 보다는 객체 하나를 재사용하는 것이 훨씬 빠르고 효율적이다.

특히 Pattern은 입력받은 정규표현식에 해당하는 유한 상태 머신(finite state machine)을 만들기 때문에 인스턴스 생성 비용이 높다.

> String.matches() 메서드는 Pattern.matches()를 이용하는데 Pattern.matches() 내부에서 Pattern 객체를 생성(compile)한 후 Matcher와 비교한 후 바로 GC 대상으로 바꿔버리기 때문이다.

미리 컴파일해두고 사용하면 비용을 줄일 수 있지 않을까?

```
import java.util.regex.Pattern;

public class StringRegex {
    private static final Pattern INVALID_STRING_PATTERN = Pattern.compile("[a-zA-Z가-힣]+");

    public static boolean isInvalid(String input) {
        return INVALID_STRING_PATTERN.matcher(input)
                                     .find();
    }
}
```

### ✏️ 불필요한 객체 생성을 피하라

https://junit.org/junit5/docs/current/user-guide/#writing-tests-classes-and-methods

### ✏️ 일급 컬렉션

https://jojoldu.tistory.com/412


### ✏️ 의미있는 테스트 케이스


### ✏️ equals 및 hashCode 


### ✏️ equals 및 hashCode
책임과 역할을 분리

### ✏️ 생성자 활용
