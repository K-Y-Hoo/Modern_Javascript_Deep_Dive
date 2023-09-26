# 26_ES6 함수의 추가 기능

### 함수의 구분

- 일반 함수
- 메서드
- 화살표 함수

### 메서드

- 메서드 축약 표현으로 정의된 함수만을 의미한다. (인스턴스 생성 불가능)

### 화살표 함수

- 화살표 함수는 함수 선언문으로 정의할 수 없고 함수 표현식으로 정의해야 한다.
- 객체 리터럴을 반환하는 경우 객체 리터럴을 소괄호로 감싸 주어야 한다.
    
    ```jsx
    const create = (id, content) => ({ id, content });
    create(1, 'JavaScript'); // {id: 1, content: "JavaScript"}
    ```
    
- 함수 몸체가 여러 개의 문으로 구성된다면 함수 몸체를 감싸는 중괄호를 생략 불가능
- 즉시 실행 함수로 사용 가능
    
    ```jsx
    const person = (name => ({
    	sayHi() { return `Hi? My name is ${name}.`; }
    }))('Lee');
    console.log(person.sayHi()); // Hi? My name is Lee.
    ```
    
- 화살표 함수는 일급 객체이므로 고차 함수에 인수로 전달 가능 (콜백 함수로서 정의)
    
    ```jsx
    [1, 2, 3].map(v => v * 2); // [2, 4, 6]
    ```
    
- 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor
- 중복된 매개변수 이름 선언 불가능
- 함수 자체 this, arguments, super, [new.target](http://new.target) 바인딩을 갖지 않음(상위 스코프의 것을 참조)
- 화살표 함수에서의 this: 함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정

### Rest 파라미터

- Rest 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달받는다.
    
    ```jsx
    function foo(...rest) {
    	console.log(rest); // [1, 2, 3, 4, 5]
    }
    foo(1, 2, 3, 4, 5);
    ```
    
- Rest 파라미터는 반드시 마지막 파라미터이어야 한다.
- 단 하나만 선언할 수 있다.
- length 프로퍼티에 영향을 주지 않는다.

### 매개변수 기본값

`undefined`

방어코드가 필요하다.

매개변수 기본값 사용 ( length 프로퍼티와 arguments 객체에 아무런 영향을 주지 않음)

Rest 파라미터에는 기본값 지정 불가