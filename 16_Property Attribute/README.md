# 16_프로퍼티 어트리뷰트

### 내부 슬롯, 내부 메서드

- ECMAScript 사양에 등장하는 이중 대괄호 `[[]]` 로 감싼 이름
- 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공 → 모든 객체가 가진 `[[Prototype]]` 내부 슬롯은 원칙적으로 직접 접근할 수 없지만 `__proto__` 를 통해 간접적으로 접근할 수 있다.

### 프로퍼티 어트리뷰트, 프로퍼티 디스크립터 객체

- 프로퍼티를 생성할 때 프로퍼티의 상태(`value, writable, enumerable, configurable`)를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.
- `Object.getOwnPropertyDescriptor` 메서드는 프로퍼티 어트리뷰트 정보를 간접적으로 제공하는 프로퍼티 디스크립터 객체를 반환한다. `Object.getOwnPropertyDescriptor**s**` 는 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 디스크립터 객체**들**을 반환한다.

### 데이터 프로퍼티와 접근자 프로퍼티

- 데이터 프로퍼티: 키와 값으로 구성된 일반적인 프로퍼티 `value, writable, enumerable, configurable`
- 접근자 프로퍼티: 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티 `get, set, enumerable, configurable`

### 프로퍼티 정의

- 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의하는 것
- `Object.defineProperty` `Object.defineProperties`

### 객체 변경 방지

- `Object.preventExtensions` → 프로퍼티 추가 금지 → `Object.isExtensible` 메서드로 확인
- `Object.seal` → 읽기, 쓰기만 가능 → `Object.isSealed` 메서드로 확인
- `Object.freeze` → 읽기만 가능 → `Object.isFrozen` 메서드로 확인
- 불변 중첩 객체를 만드려면 `Object.freeze` 메서드를 모든 프로퍼티에 대해 재귀적으로 호출해야 한다.