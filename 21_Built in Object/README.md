# 21_빌트인 객체

### 자바스크립트 객체의 분류

- 표준 빌트인 객체
- 호스트 객체
- 사용자 정의 객체

### 표준 빌트인 객체

- `Object, String, Number, Boolean, Symbol, Date, Math, RegExp, Array, Map/Set, Function, Promise` 등 40여 개의 표준 빌트인 객체를 제공한다.
- Math, Reflect, JSON(정적 메서드만 제공)을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할 수 있는 생성자 함수 객체다. → 프로토타입 메서드와 정적 메서드(인스턴스 없이 호출 가능한 빌트인 정적 메서드)를 제공
    
    ```jsx
    const numObj = new Number(1.5); // Number 생성자 함수에 의한 Number 객체 생성
    console.log(numObj.toFixed()); // 2
    
    console.log(Number.isInteger(0.5)); // false
    isInteger는 Number의 정적 메서드다.
    ```
    

### 원시값과 래퍼 객체

- 원시값을 객체처럼 사용하면 자바스크립트 엔진은 암묵적으로 연관된 객체를 생성하여 생성된 객체로 프로퍼티에 접근하거나 메서드를 호출하고 다시 원시값으로 되돌린다. → 이러한 임시 객체를 래퍼 객체라 한다.
    
    ```jsx
    const str = 'hi';
    console.log(str.length);
    console.log(str.toUpperCase); // 원시 타입인 문자열이 래퍼 객체인 String 인스턴스로 
    															// 변환된다.
    console.log(typeof str); // 래퍼 객체로 프로퍼티에 접근하거나 메서드를 호출한 후, 
    												 // 다시 원시값으로 되돌린다.(래퍼 객체는 가비지 컬렉션 대상이 됨)
    ```
    
- 따라서 String, Number, Boolean 생성자 함수를 new 연산자와 함께 호출하여 인스턴스를 생성할 필요가 없다.

### 전역 객체

`코드가 실행되기 이전 단계에 어떤 객체보다도 먼저 생성되는 특수한 객체(어떤 객체에도 속하지 않은 최상위 객체)`

- 개발자가 의도적으로 생성할 수 없다.(전역 객체를 생성할 생성자 함수가 없다)
- 전역 객체의 프로퍼티를 참조할 때 window(또는 global)를 생략할 수 있다.
    
    ```jsx
    window.parseInt('F', 16);
    parseInt('F', 16);
    window.parseInt === parseInt; // true
    ```
    
- 브라우저 환경의 모든 자바스크립트 코드는 하나의 전역 객체 window를 공유한다 → 분리되어 있는 자바스크립트 코드는 하나의 전역을 공유한다.
- built-in 전역 프로퍼티
    - Infinity
    - NaN
    - undefined
- built-in 전역 함수(전역 객체의 메서드)
    - eval(문자열을 인수로 전달받음) → 최적화 문제 때문에 사용 금지 권장
    - isFinite(인수가 유한수이면 true 반환)
    - isNaN
    - parseInt(두 번째 인수로 진법을 나타내는 기수를 전달 가능)
    - parseFloat
    - encodeURI / decodeURI
    - encodeURIComponent / decodeURIComponent
    - 암묵적 전역
        
        ```jsx
        var x = 10;
        function foo() {
        	y = 20;           // window.y = 20;
        }
        foo();
        console.log(x + y); // 30
        // 선언하지 않은 식별자에 값을 할당하면 전역 객체의 프로퍼티가 되기 때문
        // 단지 프로퍼티이므로 y는 변수가 아니다. -> 변수 호이스팅 발생 X
        // 변수가 아니고 프로퍼티이므로 delete 연산자로 삭제할 수 있다.
        // 전역 변수는 프로퍼티이지만 delete로 삭제 불가!
        ```