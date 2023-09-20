# 15_let, const 키워드와 블록 레벨 스코프

### var 키워드로 선언한 변수

- ES5까지 변수를 선언할 수 있는 유일한 방법은 var 키워드의 사용이었다.
- var 키워드로 선언한 변수는 중복 선언이 가능하다.
- 오직 함수의 코드 블록만을 지역 스코프로 인정한다. → 함수 레벨 스코프 → 전역 변수 남발 가능성 높인다.
    
    ```jsx
    var x = 1;
    if (true) {
    	var x = 10;
    }
    console.log(x); // 10
    ```
    
- 변수 호이스팅 → 가독성을 떨어뜨리고 오류를 발생시킬 여지가 있다.

### let 키워드

- 변수 중복 선언 금지(같은 스코프 내에서)
    
    ```jsx
    let bar = 1;
    let bar = 2; // SyntaxError
    ```
    
- 모든 코드 블록(함수, if문, for문, while문, try/catch문 등)을 지역 스코프로 인정하는 블록 레벨 스코프를 따른다.
    
    ```jsx
    let foo = 1; // 전역
    {
    	let foo = 2; // 지역
    	let bar = 3; // 지역
    }
    console.log(foo); // 1
    console.log(bar); // ReferenceError: bar is not defined.
    ```
    
- 변수 호이스팅이 발생하지 않는 것처럼 동작하지만 실제론 동작한다.
    
    ```jsx
    let foo = 1; // 전역
    {
    	console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
    	let foo = 2; // 지역
    }
    ```
    
- 선언 단계와 초기화 단계가 분리되어 진행된다.
- 스코프의 시작 지점부터 초기화 시작 지점(변수 선언문)까지 변수를 참조할 수 없다 → 일시적 사각지대
    
    ```jsx
    console.log(foo); // ReferenceError: foo is not defined.
    let foo; // 변수 선언문에서 초기화 단계 진행
    console.log(foo); // undefined
    foo = 1; // 할당문에서 할당 단계 실행
    console.log(foo); // 1
    ```
    
- ES6에서 모든 선언은 호이스팅된다. 단, let, const, class를 사용한 선언문은 호이스팅이 발생하지 않는 것처럼 동작한다.
- var 키워드로 선언한 전역 변수와 전역 함수, 암묵적 전역(선언하지 않은 변수에 값을 할당)은 전역 객체 window의 프로퍼티가 된다. let 킨워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다. 보이지 않는 개념적인 블록 내에 존재한다.

### const 키워드

- 반드시 선언과 동시에 초기화해야 한다.
- 재할당이 금지된다. (상태 유지, 가독성, 유지보수의 편의)
- 예외적으로 const 키워드로 선언된 객체는 값을 변경 가능하다. (프로퍼티 동적 생성, 삭제, 프로퍼티 값의 변경)

### 요약

- ES6를 사용한다면 var 키워드 사용 금지
- 재할당이 필요한 경우에 한정해 let 키워드 사용하고 최대한 변수의 스코프를 좁게 만든다.
- 변경이 발생하지 않고 읽기 전용으로 사용하는 원시 값과 객체에는 const 키워드를 사용(var, let 키워드보다 안전하다)