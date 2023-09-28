# 28_Number

`원시 타입인 숫자를 다룰 때 유용한 프로퍼티와 메서드를 제공`

### Number 생성자 함수

```jsx
const numObj = new Number();
console.log(numObj); // Number {[PrimitiveValue]: 0}

const numObj2 = new Number(10);
console.log(numObj2); // Number {[PrimitiveValue]: 10}

//인수로 숫자가 아닌 값 전달하면 숫자로 강제 변환
const numObj3 = new Number('10');
console.log(numObj3); // Number {[PrimitiveValue]: 10}

const numObj4 = new Number('hello');
console.log(numObj4); // Number {[PrimitiveValue]: NaN}
```

new 연산자 없이 Number 생성자 함수를 호출하면 Number 인스턴스가 아닌 명시적 타입 변환된 숫자를 반환한다.

### Number 프로퍼티

- Number.EPSILON 은 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이
    
    ```jsx
    function isEqual(a, b) {
    	return Math.abs(a - b) < Number.EPSILON;
    }
    isEqual(0.1 + 0.2, 0.3); // true
    ```
    
- Number.MAX_VALUE 자바스크립트에서 표현할 수 있는 가장 큰 양수값. 더 큰 숫자는 Infinity 뿐이다.
    
    ```jsx
    Number.MAX_VALUE;
    Infinity > Number.MAX_VALUE;
    ```
    
- Number.MIN_VALUE 가장 작은 양수 값. 더 작은 숫자는 0이다.
    
    ```jsx
    Number.MIN_VALUE;
    Number.MIN_VALUE > 0; // true
    ```
    
- Number.MAX_SAFE_INTEGER 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값
- Number.MIN_SAFE_INTEGER 안전하게 표현할 수 있는 가장 작은 정수값
- Number.POSITIVE_INFINITY 양의 무한대. Infinity와 같다
- Number.NEGATIVE_INFINITY 음의 무한대. -Infinity와 같다
- Number.NaN 숫자가 아님을 나타내는 숫자값. window.NaN와 같다

### Number 메서드

- Number.isFinite → 정적 메서드. 인수로 전달된 숫자값이 정상적인 유한수인지 검사하여 불리언 값 반환 (빌트인 전역 함수 isFinite와 다르게 암묵적 타입 변환하지 않는다)
    
    ```jsx
    Number.isFinite(null); // false
    isFinite(null); // true
    ```
    
- Number.isInteger → 정적 메서드. 인수 숫자값이 정수인지 검사하여 불리언 반환. 검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다.
- Number.isNaN → 정적 메서드. 인수로 전달된 숫자값이 NaN인지 검사, 불리언 반환
    
    ```jsx
    Number.isNaN(undefined); // false
    isNaN(undefined); // true 암묵적 타입 변환
    ```
    
- Number.isSafeInteger → 정적 메서드. 인수로 전달된 숫자값이 안전한 정수인지 검사. 불리언 반환
- Number.prototype.toExponential → 숫자를 지수 표기법으로 변환하여 문자열로 반환. 인수로 소수점 이하로 표현할 자릿수를 전달
- Number.prototype.toFixed → 숫자를 반올림하여 문자열로 반환. 반올림하는 소수점 이하 자릿수 0~ 20. 생략하면 기본값 0.
- Number.prototype.toPrecision → 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환
- Number.prototype.toString → 숫자를 문자열로 변환하여 반환. 진법을 나타내는 2~36 사이 정수값을 인수로 전달. 생략하면 기본값 10진법.