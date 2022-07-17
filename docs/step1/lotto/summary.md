### ✏️ 자바의 리플렉션

```
import java.lang.reflect.Field;

public class Console {
    private static Scanner scanner;
    
    ...
    
    private static boolean isClosed() {
        try {
            final Field sourceClosedField = Scanner.class.getDeclaredField("sourceClosed");
            sourceClosedField.setAccessible(true);
            return sourceClosedField.getBoolean(scanner);
        } catch (final Exception e) {
            System.out.println("unable to determine if the scanner is closed.");
        }
        return true;
    }
}
```

자바의 리플렉션은 클래스 구조를 분석하여 동적 로딩을 할 수 있다.

new 키워드를 사용하지 않아도 인스턴스를 생성할 수 있고 프로그램 재실행없이 소스 코드를 교체할 수 있는 데다가 탐색을 통해서 외부에서 인스턴스를 할당할 수 있다.

단, 탐색을 하는데 상당한 비용이 들어가고 이미 메모리에 로드가 되었는데 소스 코드가 교체된다면 에러가 발생할 수 있다.

리플렉션의 활용적인 측면을 놓고 봤을 때 동적으로 할당된 클래스를 Object에 넣게 되면 Object의 기본 메서드뿐만 아니라 해당 클래스의 구조를 분석해서 메서드를 검색하고 실행할 수 있다.

getMethod를 사용하면 같은 이름의 메서드라도 파라미터의 설정에 따라서 호출을 다르게 할 수고 생성자 역시 다양하게 획득할 수 있는데 getMethod 이외에도 아래의 메서드를 사용할 수 있다.

- getMethods : Object에서부터 해당 클래스까지 있는 모든 메서드를 찾는다.
- getDeclaredMethods : 해당 클래스에 있는 메서드만을 찾는다.

이 기능을 잘 활용하면 private이나 protected처럼 접근이 제한되어 있는 메서드도 실행할 수 있기 때문에 테스트에서 메서드의 결과를 확인할 수 있다.

Console에서 Scanner는 정적으로 선언하였고 getDeclaredField로 sourceClosed 변수에 접근을 가능하게 하였는데 이렇게 프로그램 실행 도중 클래스의 멤버 변수에 접근해서 값을 확인하면 실제로 Scanner가 close 되었는지 알 수 있다.

### ✏️ 불변 객체

방어적 복사3

복사를 할 때 Arrays.asList를 사용하게 되면 Arrays의 이너 클래스인 ArrayList를 반환하게 되네요
해당 클래스는 AbstractList를 상속하고 있고 add와 같은 메서드를 호출하면 UnsupportedOperationException 에러가 발생합니다
불변 처리한 객체에 add와 같은 메서드를 만들지는 않겠지만.. 그런 경우가 발생할 수도 있을까요?

### ✏️ 일급 컬렉션

https://jojoldu.tistory.com/412



static block 캐시


### ✏️ ENUM

### ✏️ 책임과 역할 분리

- Number :
- Numbers : 문자열 덧셈 계산기 핵심 도메인. 숫자의 합을 반환하는 기능을 제공한다.
- StringUtils : 문자열 관련 기능을 제공한다.
    - null 또는 empty 문자열이 입력된 경우 "0"을 반환한다.
    - 정상적인 문자열이 입력되지 않은 경우 Exception을 발생시킨다.
- StringRegex : 숫자 이외의 값이 입력되었는지 확인한다.
- StringSeparator : 구분자를 기준으로 문자열에서 숫자를 분리하고 String 배열로 반환한다.
- StringAddCalculator : 문자열에서 숫자를 분리하고 각 숫자의 합을 반환한다.



저희가 계속 불변 객체를 만드는 등의 작업을 해주는 이유는 값이 중간에 바뀌는 변수 혹은 객체들은 다루기가 어렵기 때문입니다. 전역 변수도 클래스 내에서 어디에서나 접근이 가능하기 때문에 값이 변경될 수 있고 그런 경우 해당 변수는 사용하는 입장에서는 해당 값이 자신이 원하는 값인지 확인하는 작업을 추가로 해주어야 합니다.

지금의 경우는 성우님이 작성하신 코드이고, 코드량도 많아봐야 100 line 내외라서 전역변수의 영향이 잘 느껴지지 않습니다만, 다른 사람이 작성한 코드이고 코드량이 몇만줄 정도 될 경우(실제 실무의 레거시 코드는 이런 경우가 종종 있습니다 ㅎ.ㅎ;;) 전역변수는 사용하기 정말 어려운 값이 됩니다. 반대로 안쓰자니 안쓰는 값을 필드로 가지고 있는 것도 이상하구요... 그래서 전역변수는 가능한 쓰지 않는 편이 좋을 것 같고, 마지막으로 저희들의 선배분이 말씀하신 내용으로 코멘트 마치도록 하겠습니다 : )


인스턴스를 생성할 때 방어적 복사를 통해서 외부와 내부의 관계를 끊어주고 get과 같은 값을 반환하는 메서드를 호출할 때는 Collections.unmodifiableList 처리하면 될까요?
