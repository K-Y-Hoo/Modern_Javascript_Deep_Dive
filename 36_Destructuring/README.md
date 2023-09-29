# 36_디스트럭처링 할당

`구조화된 배열과 같은 이터러블 또는 객체를 비구조화하여 1개 이상의 변수에 개별적으로 할당하는 것!`

`배열과 같은 이터러블 또는 객체 리터럴에서 필요한 값만 추출하여 변수에 할당할 때 유용하다!`

### 배열 디스트럭처링 할당

- 배열 디스트럭처링 할당의 대상(할당문의 우변)은 이터러블이어야 한다. 할당 기준은 배열의 인덱스다.(순서대로 할당)
    
    ```jsx
    const arr = [1, 2, 3];
    const [one, two, three] = arr;
    console.log(one, two, three); // 1 2 3
    
    //왼쪽에 값을 할당받을 변수를 선언해야 한다. 배열 리터럴 형태로 선언
    const [x, y] = [1, 2];
    
    //우변에 이터러블을 할당하지 않으면 에러 발생
    const [x, y]; // SyntaxError: Missing initializer in destructuring declaration
    const [a, b] = {}; // TypeError: {} is not iterable
    
    //선언과 할당을 분리 가능하나 const 키워드로 변수 선언 불가능하므로 권장하지 않는다.
    let x, y;
    [x, y] = [1, 2];
    
    //변수의 개수와 이터러블의 요소 개수가 일치할 필요는 없다.
    const [c, d] = [1];
    console.log(c, d); // 1 undefined
    
    const [e, f] = [1, 2, 3];
    console.log(e, f); // 1 2
    
    const [g, , h] = [1, 2, 3];
    console.log(g, h); // 1 3
    
    //변수에 기본값 설정 가능하다.
    const [a, b, c = 3] = [1, 2];
    console.log(a, b, c); // 1 2 3
    
    //기본값보다 할당 값이 우선
    const [e, f = 10, g = 3] = [1, 2];
    console.log(e, f, g); // 1 2 3
    
    //Rest 파라미터와 유사하게 Rest 요소를 사용 가능하다. 마지막에 위치해야 한다.
    const [x, ...y] = [1, 2, 3];
    console.log(x, y); // 1 [ 2, 3 ]
    ```
    

### 객체 디스트럭처링 할당

- ES5에서 객체에 각 프로퍼티를 객체로부터 디스트럭처링하여 변수에 할당하기 위해서는 프로퍼티 키를 사용해야 한다.
    
    ```jsx
    var user = { firstName: 'hoo', lastName: 'kim' };
    var firstName = user.firstName;
    var lastName = user.lastName;
    console.log(firstName, lastName); // hoo kim
    ```
    
- ES6에서 객체 디스트럭처링 할당의 대상(할당문의 우변)은 객체이어야 하며 할당 기준은 프로퍼티 키다. 순서에 의미는 없으며 선언된 변수 이름과 프로퍼티 키가 일치하면 할당된다.
    
    ```jsx
    const user = { firstName: 'hoo', lastName: 'kim' };
    const {lastName, firstName } = user;
    console.log(firstName, lastName); // hoo kim
    ```
    
    - 우변에 객체 또는 객체로 평가될 수 있는 표현식(문자열, 숫자, 배열 등)을 할당하지 않으면 에러 발생
    - 객체의 프로퍼티 키와 다른 변수 이름으로 프로퍼티 값을 할당받고 싶을 때
        
        ```jsx
        const { lastName: ln, firstName: fn } = user;
        console.log(fn, ln); //hoo kim
        ```
        
    - 변수에 기본값 설정 가능
        
        ```jsx
        const { firstName = 'hoo', lastName } = { lastName: 'kim'};
        console.log(firstName, lastName); // hoo kim
        
        const { firstName: fn = 'hoo', lastName: ln } = { lastName: 'kim'};
        console.log(fn, ln); hoo kim
        ```
        
    - 객체에서 프로퍼티 키로 필요한 프로퍼티 값만 추출하여 변수에 할당하고 싶을 때 유용
        
        ```jsx
        const str = 'Hello';
        const { length } = str;
        console.log(length); // 5
        ```
        
    - 객체를 인수로 전달받는 함수의 매개변수에도 사용 가능
    - 배열의 요소가 객체인 경우 배열 디스트럭처링 할당과 객체 디스트럭처링 할당 혼용 주의
    - 중첩 객체
        
        ```jsx
        const user = {
        	name: 'kim',
        	address: {
        		zipCode: '01111',
        		city: 'Seoul'
        	}
        };
        
        const { address: { city } } = user;
        console.log(city); // 'Seoul'
        ```
        
    - Rest 프로퍼티(반드시 마지막에 위치)
        
        ```jsx
        const { x, ...rest } = { x: 1, y: 2, z: 3 };
        console.log(x, rest } = 1 { y: 2, z: 3 }
        ```