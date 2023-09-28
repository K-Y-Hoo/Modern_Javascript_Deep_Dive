# 32_String

### String 생성자 함수

```jsx
const strObj = new String();

const strObj2 = new String('Kim');
```

- String 래퍼 객체는 배열과 유사하게 인덱스를 사용하여 각 문자에 접근할 수 있다.(유사 배열 객체이면서 이터러블) 단 문자열은 원시 값이므로 변경할 수 없다.
- new 연산자를 사용하지 않고 String 생성자 함수를 호출하면 String 인스턴스가 아닌 문자열을 반환한다.(명시적 타입 변환)

### length 프로퍼티

- String 래퍼 객체는 배열과 마찬가지로 length 프로퍼티를 갖는다.

### String 메서드

`원본 String 래퍼 객체를 직접 변경하는 메서드는 존재하지 않는다.(언제나 새로운 문자열 반환)`

- String.prototype.indexOf → 대상 문자열(인덱스를 호출한 문자열)에서 인수로 전달받은 문자열을 검색하여 첫 번째 인덱스를 반환, 검색 실패하면 -1 반환
    - 두 번째 인수로 검색을 시작할 인덱스 전달
    - 대상 문자열에 특정 문자열 존재하는지 확인할 때 유용
- String.prototype.search → 인수로 전달받은 정규 표현식과 매치하는 문자열 검색하여 일치하는 문자열의 인덱스를 반환.
- String.prototype.includes → 인수로 전달받은 문자열이 포함되어 있는지 확인하여 불리언 값 반환
    - 두 번째 인수로 검색을 시작할 인덱스 전달
- String.prototype.startsWith → 인수로 전달받은 문자열로 시작하는지 확인하여 불리언 값 반환
    - 두 번째 인수로 검색을 시작할 인덱스 전달
- String.prototype.endsWith → 인수로 전달받은 문자열로 끝나는지 확인하여 불리언 값 반환
    - 두 번째 인수로 검색할 문자열의 길이를 전달
- String.prototype.charAt → 인수로 전달받은 인덱스에 위치한 문자를 검색하여 반환
    - 인덱스가 문자열의 범위를 벗어난 정수인 경우 빈 문자열 반환
- String.prototype.substring → 첫 번째 인수로 전달받은 인덱스에 위치하는 문자부터 두 번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 **이전 문자**까지의 부분 문자열 반환
    - 두 번째 인수 생략하면 첫 번째 인수부터 마지막까지
- String.prototype.slice → substring과 동일하나 음수를 인수로 전달 가능. 인수가 음수이면 대상 문자열의 뒤에서부터 시작하여 문자열 잘라내어 반환
- String.prototype.toUpperCase → 대상 문자열을 모두 대문자로 변경한 문자열 반환
- String.prototype.toLowerCase → 대상 문자열을 모두 소문자로 변경한 문자열 반환
- String.prototype.trim → 대상 문자열 앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열 반환
    
    ```jsx
    const str = '      foo  ';
    str.trim(); // 'foo'
    ```
    
- String.prototype.repeat → 대상 문자열을 인수로 전달받은 정수만큼 반복해 연결한 새로운 문자열 반환
    - 정수가 0이면 빈 문자열 반환
    - 음수면 RangeError
    - 생략하면 기본값 0
- String.prototype.replace → 첫 번째 인수로 전달받은 문자열 또는 정규표현식을 검색하여 두 번째 인수로 전달한 문자열로 치환한 문자열을 반환
    - 검색된 문자열이 여럿 존재할 경우 첫 번째로 검색된 문자열만 치환
    - 두 번째 인수로 치환 함수를 전달 가능
- String.prototype.split → 문자열을 구분한 후 분리된 각 문자열로 이루어진 배열을 반환
    
    ```jsx
    const str = 'How are you';
    str.split(' '); // ["How", "are", "you"]
    str.split(''); // ["H", "o", "w", " ", "a", "r", "e", " ", "y", "o", "u"]
    str.split(); // ["How are you]
    
    두 번째 인수로 배열의 길이를 지정 가능
    str.split(' ', 2); // ["How", "are"]
    ```