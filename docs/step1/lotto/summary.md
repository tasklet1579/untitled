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

### ✏️ 일급 컬렉션과 불변 객체

Collection을 Wrapping하면서, Wrapping한 Collection 외 다른 멤버 변수가 없는 상태를 일급 컬렉션이라고 한다.

```
public class Lottery {
    private final List<Number> numbers;
    
    public Lottery(List<Number> numbers) {
        validate(numbers);
        this.numbers = new LinkedList<>(numbers);
    }
    
    private void validate(List<Number> numbers) {
        ...
    }
    
    public List<Number> getNumbers() {
        return Collections.unmodifiableList(numbers);
    }
    
    public boolean contains(Number number) {
        return numbers.contains(number);
    }
    
    ...
}
```

일급 컬렉션의 장점
- 이름을 통해 의미를 부여할 수 있고 비즈니스에 종속적인 자료구조를 만들 수 있다.
- validation을 통해 객체의 상태를 보장할 수 있다.
- 로직을 한 곳에서 관리하기 때문에 유지보수에 유리하고 중복 코드를 줄일 수 있다.
- 필요에 따라서 객체의 불변성을 보장할 수 있고 목적에 맞는 값만 반환하는 것도 하나의 방법이 될 수 있다.

불변 객체
- 객체 생성 이후 내부의 상태가 변하지 않는 객체이다.
- read-only 메소드만을 제공하며, 방어적 복사를 통해 값을 제공한다.
- 대표적인 불변 객체로는 String이 있는데 내부적으로 문자열을 복사해서 반환한다.
- [불변 객체(Immutable Object) 및 final을 사용해야 하는 이유](https://mangkyu.tistory.com/131)

불변 객체 만들기
- 객체의 상태를 변경하는 메서드를 제공하지 않는다.
- 클래스를 확장할 수 없도록 한다. (public final class)
- 모든 필드를 final과 private으로 선언한다.
- 불변 객체의 인스턴스가 너무 많이 만들어진다면 정적 팩토리 메서드와 캐싱을 적용해 보자.

정적 팩토리 메서드
- 이름을 가짐으로써 객체 생성의 의도를 나타낼 수 있다.
- 호출될 때마다 인스턴스를 새로 생성하지 않아도 된다.
- 반환 타입의 하위 타입 객체를 반환할 수 있다.
- 입력 값에 따라 매번 다른 클래스의 객체를 반환할 수 있다.

정적 팩토리 메서드 네이밍 규칙
- valudeOf(), of() : 인자로 전달되는 값에 해당하는 인스턴스를 반환
- getInstance(), newInstance() : 보통 자신과 같은 Type의 인스턴스를 반환
- getType(), newType() : 자신과 다른 Type의 인스턴스를 반환

Q. [방어적 복사와 Unmodifiable의 차이점은?](https://steady-coding.tistory.com/559#%EB%B0%A9%EC%96%B4%EC%A0%81_%EB%B3%B5%EC%82%AC%EC%99%80_Unmodifiable%EC%9D%98_%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80?)

> 방어적 복사는 A 리스트와 B 리스트 사이의 참조를 끊는 행위이지만, Unmodifiable은 참조를 끊지 않고 단순히 특정 리스트에서 요소의 변경이 일어날 경우 예외를 던진다. 그래서 생성자 단계에서 방어적 복사를 취하지 않고, getter에서 Unmodifiable만 취할 경우 초기 생성자로 주입한 컬렉션의 변화가 생기면 불변성이 깨진다.

Q. [방어적 복사를 사용하면 항상 불변성을 보장하는가?](https://steady-coding.tistory.com/559#%EB%B0%A9%EC%96%B4%EC%A0%81_%EB%B3%B5%EC%82%AC%EB%A5%BC_%EC%82%AC%EC%9A%A9%ED%95%98%EB%A9%B4_%ED%95%AD%EC%83%81_%EB%B6%88%EB%B3%80%EC%84%B1%EC%9D%84_%EB%B3%B4%EC%9E%A5%ED%95%98%EB%8A%94%EA%B0%80?)

> 그렇지 않다. 방어적 복사는 컬렉션의 요소에 대해 얕은 복사를 수행하므로 컬렉션의 참조 타입이 가변 객체라면, 복사하려는 컬렉션의 요소가 변경될 경우 불변성이 깨진다.

### ✏️ 객체지향적으로 개발하기


저희가 계속 불변 객체를 만드는 등의 작업을 해주는 이유는 값이 중간에 바뀌는 변수 혹은 객체들은 다루기가 어렵기 때문입니다. 전역 변수도 클래스 내에서 어디에서나 접근이 가능하기 때문에 값이 변경될 수 있고 그런 경우 해당 변수는 사용하는 입장에서는 해당 값이 자신이 원하는 값인지 확인하는 작업을 추가로 해주어야 합니다.

지금의 경우는 성우님이 작성하신 코드이고, 코드량도 많아봐야 100 line 내외라서 전역변수의 영향이 잘 느껴지지 않습니다만, 다른 사람이 작성한 코드이고 코드량이 몇만줄 정도 될 경우(실제 실무의 레거시 코드는 이런 경우가 종종 있습니다 ㅎ.ㅎ;;) 전역변수는 사용하기 정말 어려운 값이 됩니다. 반대로 안쓰자니 안쓰는 값을 필드로 가지고 있는 것도 이상하구요... 그래서 전역변수는 가능한 쓰지 않는 편이 좋을 것 같고, 마지막으로 저희들의 선배분이 말씀하신 내용으로 코멘트 마치도록 하겠습니다 : )


인스턴스를 생성할 때 방어적 복사를 통해서 외부와 내부의 관계를 끊어주고 get과 같은 값을 반환하는 메서드를 호출할 때는 Collections.unmodifiableList 처리하면 될까요?

### ✏️ 디미터 법칙

K. Lieberherr를 비롯한 몇몇 사람들은 디미터라는 이름의 프로젝트를 진행하던 도중 다른 객체들과의 협력을 통해 프로그램을 완성해나가는 객체지향 프로그래밍에서 객체들의 협력 경로를 제한하면 결합도를 효과적으로 낮출 수 있다는 사실을 발견했고 디미터 법칙을 만들었다.

현재 디미터 법칙은 객체 간 관계를 설정할 때 객체 간의 결합도를 효과적으로 낮출 수 있는 유용한 지침 중 하나로 꼽히며 객체 지향 생활 체조 원칙 중 한 줄에 점을 하나만 찍는다.로 요약되기도 한다.

https://tecoble.techcourse.co.kr/post/2020-06-02-law-of-demeter/

정적 팩토리 메서드 잘 적용해주셨습니다 👍
다만 정적 팩토리 메서드는 파라미터가 한개일 땐 from을 관습적으로 사용합니다!

from : 매개변수를 하나 받아서 해당 타입의 인스턴스를 반환하는 형변환 메서드
ex) Date d = Date.from(instant)
of : 여러 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계 메서드
ex) Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);
valueOf : from 과 of 의 더 자세한 버전
ex) BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
- 클린 코드


getter는 단순히 데이터를 가져오는 메서드이기 때문에 책임이 데이터를 처리하기 좋은 클래스에서 이탈하는 경우가 있는 것 같습니다. getter 관련해서 좋은 내용이 있어 첨부드립니다 : )

https://tecoble.techcourse.co.kr/post/2020-04-28-ask-instead-of-getter/


### ✏️ 객체지향적으로 개발하기

우선 service layer를 만들어주신 이유 설명 주셔서 감사합니다 ㅎㅎ
첨부해주신 글에서도 언급하듯 service layer에는

다른 기능의 Service를 호출하거나 다수의 DAO를 연결하는 역할을 한다.
Transaction과 Cache 적용과 같은 infra 적용을 위한 단위가 된다.
Service는 가능한 가볍게 구현한다.(thin layer)
Service에 핵심 비즈니스 로직을 구현하지 말고, 로직은 상태 값을 가지고 있는 모델(또는 도메인)이 담당해야 한다.
로 정리해주셨네요. 이제 저희 서비스를 봤을 때 DB 등 infra에 접근하는 곳이 없어서 저는 service layer는 따로 없어도 될 것 같고, 데이터를 처리하는 순서를 담당하는 controller와 데이터를 보여주는 view, 마지막으로 로직을 처리하는 model만 존재하면 될 것 같습니다! 성우님께서는 어떻게 생각하시는지 궁금합니다 : )

둘째로 LotteryProducer 외에도 상태를 갖지 않는 클래스들(예를 들어 LotteryStore)은 인스턴스화로 얻는 이득이 없으므로, private 생성자로 인스턴스화를 막는 것이 좋아보입니다!

