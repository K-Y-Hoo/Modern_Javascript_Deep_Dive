# 22_this

`동작을 나타내는 메서드는 자신이 속한 객체의 상태, 즉 프로퍼티를 참조하고 변경할 수 있어야 한다!`

`자신이 속한 객체를 가리키는 식별자를 참조할 수 있어야 한다!`

- this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다.
- this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다.
    
    `바인딩이란? 식별자와 값을 연결하는 과정`
    
- 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.
- 함수가 호출되는 방식에 따라 this 바인딩이 동적으로 결정된다.
    
    ```jsx
    // 전역에서 this는 전역 객체 window를 가리킨다.
    console.log(this); // window
    
    function square() {
    // 일반 함수 내부에서 this는 전역 객체 window를 가리킨다.
    	console.log(this); // window
    }
    
    const person = {
    	name: 'kim',
    	getName() {
    //메서드 내부에서 this는 메서드를 호출한 객체를 가리킨다.
    		console.log(this); // {name: "kim", getName: f}
    		return this.name;
    	}
    };
    
    fuction Person(name) {
    	this.name = name;
    // 생성자 함수 내부에서 this는 생성자 함수가 생성할 인스턴스를 가리킨다.
    	console.log(this); // Person {name: "kim"}
    }
    const me = new Person('kim');
    ```
    

### 함수 호출 방식과 this 바인딩

렉시컬 스코프(함수 상위 스코프를 결정하는 방식)는 함수 정의가 평가되어 함수 객체가 생성되는 시점에 상위 스코프를 결정하지만 this 바인딩은 함수 호출 시점에 결정된다.

- 일반 함수 호출 → 객체를 생성하지 않는 일반 함수에서 this는 의미가 없다. strict mode에서 undefined가 바인딩된다.
- 메서드 호출 → 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다.
- 생성자 함수 호출 → 생성자 함수가 미래에 생성할 인스턴스가 바인딩된다.
- Function.prototype.apply/call/bind 메서드에 의한 간접 호출
    
    `콜백 함수 내부의 this를 외부 함수 내부의 this와 일치시켜야 한다. 이때 bind 메서드를 사용`