### ✏️ 일급 컬렉션

https://jojoldu.tistory.com/412

### ✏️ equals 및 hashCode


### ✏️ 책임과 역할 분리

- Number :
- Numbers : 문자열 덧셈 계산기 핵심 도메인. 숫자의 합을 반환하는 기능을 제공한다.
- StringUtils : 문자열 관련 기능을 제공한다.
    - null 또는 empty 문자열이 입력된 경우 "0"을 반환한다.
    - 정상적인 문자열이 입력되지 않은 경우 Exception을 발생시킨다.
- StringRegex : 숫자 이외의 값이 입력되었는지 확인한다.
- StringSeparator : 구분자를 기준으로 문자열에서 숫자를 분리하고 String 배열로 반환한다.
- StringAddCalculator : 문자열에서 숫자를 분리하고 각 숫자의 합을 반환한다.
