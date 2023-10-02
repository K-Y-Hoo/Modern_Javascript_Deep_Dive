# 40_이벤트

### 이벤트 드리븐 프로그래밍

`이벤트와 그에 대응하는 이벤트 핸들러(함수)를 통해 사용자와 애플리케이션의 상호작용, 프로그램의 흐름을 이벤트 중심으로 제어하는 프로그래밍 방식`

- 이벤트 핸들러: 이벤트가 발생했을 때 호출될 함수
- 이벤트 핸들러 등록: 이벤트가 발생했을 때 브라우저에게 이벤트 핸들러의 호출을 위임하는 것

### 이벤트 타입

- 마우스 이벤트
- 키보드 이벤트
- 포커스 이벤트
- 폼 이벤트
- 값 변경 이벤트
- DOM 뮤테이션 이벤트
- 뷰 이벤트
- 리소스 이벤트

### 이벤트 핸들러 등록 3가지 방법

- 이벤트 핸들러 어트리뷰트 방식(on 접두사와 이벤트 타입)
    
    ```jsx
    <body>
    	<button onclick="sayHi('Lee')">Click me!</button>
    	<script>
    		function sayHi(name) {
    			console.log(`Hi! ${name}.`);
    		}
    	</script>
    </body>
    ```
    
    - 이벤트 핸들러 어트리뷰트 값으로 함수 참조가 아닌 함수 호출문 등의 문을 할당
    - 이벤트 핸들러 어트리뷰트 값은 암묵적으로 생성될 이벤트 핸들러의 함수 몸체를 의미한다.
        
        ```jsx
        function onclick(event) {
        	sayHi('lee');
        } // 이벤트 핸들러에 인수를 전달하기 위해 이처럼 동작한다!
        ```
        
- 이벤트 핸들러 프로퍼티 방식
    
    ```jsx
    <body>
    	<button>Click me!</button>
    	<script>
    		const $button = document.querySelector('button');
    		$button.onclick = function () {
    			console.log('button click');
    		};
    	</script>
    </body>
    ```
    
    - 이벤트 핸들러 프로퍼티에 하나의 이벤트 핸들러만 바인딩할 수 있다는 단점이 있다.
    - 이벤트 핸들러 어트리뷰트 방식의 HTML과 자바스크립트가 뒤섞이는 문제를 해결할 수 있다.
- addEventListener 메서드 방식
    
    ```jsx
    <body>
    	<button>Click me!</button>
    	<script>
    		const $button = document.querySelector('button');
    		$button.addEventListener('click', function() {
    			console.log('button click');
    		};
    	</script>
    </body>
    ```
    
    - 이벤트 핸들러 프로퍼티 방식은 이벤트 핸들러 프로퍼티에 이벤트 핸들러를 바인딩하지만 addEventListener 메서드 방식은 이벤트 핸들러를 인수로 전달한다.
    - 동일한 HTML 요소에 하나 이상의 이벤트 핸들러를 등록할 수 있다.(등록된 순서대로 호출)
    - 참조가 동일한 이벤트 핸들러(함수)를 중복 등록하면 하나만 등록된다.
    
- 이벤트 핸들러 제거(EventTarget.removeEventListener)
    - addEventListener 메서드에 전달한 인수와 같은 인수를 전달해야 이벤트 핸들러를 제거한다.
    - 인수로 전달한 이벤트 핸들러가 같아야 한다. → 무명 함수를 이벤트 핸들러로 등록한 경우 제거 불가능(이벤트 핸들러를 제거하려면 이벤트 핸들러의 참조를 변수나 잘구조에 저장하고 있어야 함)
    - arguments.callee로 무명 함수를 제거할 순 있지만 코드 최적화를 방해하므로 strict mode에서 사용 금지!
    - 이벤트 핸들러 프로퍼티 방식으로 등록한 이벤트 핸들러는 removeEventListener로 제거 불가능 → 이벤트 핸들러 프로퍼티에 null을 할당해야 함
        
        ```jsx
        <body>
        	<button>Click me!</button>
        	<script>
        		const $button = document.querySelector('button');
        		const handleClick = () => console.log('button click');
        		$button.onclick = handleClick;
        		$button.onclick = null;
        	</script>
        </body>
        ```
        
- 이벤트 객체
    - 이벤트가 발생하면 관련한 정보를 담고 있는 이벤트 객체가 동적으로 생성됨. 생성된 이벤트 객체는 이벤트 핸들러의 첫 번째 인수로 전달됨. (이벤트 핸들러의 첫 번째 인수로 전달되어 매개변수 e에 암묵적으로 할당)
    - 이벤트 핸들러 어트리뷰트 방식으로 이벤트 핸들러를 등록했다면 매개변수 이름을 event만 사용 가능
    - 이벤트 객체도 생성자 함수에 의해 생성됨, 프로토타입 체인의 일원이 됨
    - 이벤트 객체의 target 프로퍼티는 이벤트를 발생시킨 객체(DOM 요소)를 나타낸다.
    - 이벤트 객체의 currentTarget 프로퍼티는 이벤트 핸들러가 바인딩된 DOM 요소를 가리킨다.
        - 일반적으로 이벤트 객체의 target 프로퍼티와 currentTarget 프로퍼티는 동일한 DOM 요소를 가리키지만 이벤트 위임을 통해 서로 다른 DOM 요소를 가리킬 수 있다.
        

### 이벤트 전파

`DOM 트리 상에 존재하는 DOM 요소 노드에서 발생한 이벤트가 DOM 트리를 통해 전파되는 것`

- 캡처링 단계: 이벤트가 상위 요소에서 하위 요소 방향으로 전파
- 타깃 단계: 이벤트가 이벤트 타깃에 도달
- 버블링 단계: 이벤트가 하위 요소에서 상위 요소 방향으로 전파
- 이벤트 핸들러 어트리뷰트/프로퍼티 방식으로 등록한 이벤트 핸들러는 타깃, 버블링 이벤트만 캐치
- addEventListener 메서드 방식으로 등록한 이벤트 핸들러는 타깃, 버블링, 캡처링 모두 캐치 가능

### 이벤트 위임

`여러 개의 하위 DOM 요소에 각각 이벤트 핸들러를 등록하는 대신 하나의 상위 DOM 요소에 이벤트 핸들러를 등록하는 방법` → 성능 향상, 유지보수 적합

- 하위 요소 중에서 이벤트를 발생시킨 모든 DOM 요소에 반응하기 때문에 이벤트 반응이 필요한 DOM 요소에 한정하여 이벤트 핸들러가 실행되도록 이벤트 타깃을 검사해야 한다. (조건문)
    
    ```jsx
    function activate({ target }) {
    // 이벤트를 발생시킨 요소(target)이 ul#fruits의 자식 요소가 아니라면 무시한다.
    	if (!target.matches('#fruits > li')) return;
    }
    ```
    

### DOM 요소의 기본 동작 조작

- 이벤트 객체의 preventDefault 메서드 → DOM 요소의 기본 동작을 중단시킨다.
- 이벤트 객체의 stopPropagation 메서드 → 이벤트 전파를 중지시킨다.

### 이벤트 핸들러 내부의 this

- 이벤트 핸들러 어트리뷰트 방식
    - 일반 함수로서 호출되는 함수 내부의 this는 전역 객체 window를 가리킴
    - 이벤트 핸들러를 호출할 때 인수로 전달한 this는 이벤트를 바인딩한 DOM 요소를 가리킴
- 이벤트 핸들러 프로퍼티, addEventListener 메서드 방식
    - 이벤트 핸들러 함수 내부의 this는 이벤트를 바인딩한 DOM 요소를 가리킴(currentTarget 프로퍼티와 같다)
    - 화살표 함수로 정의한 이벤트 핸들러 내부의 this는 상위 스코프의 this를 가리킨다.(화살표 함수는 함수 자체의 this 바인딩을 갖지 않는다)

### 이벤트 핸들러에 인수 전달

- 이벤트 핸들러 내부에서 함수를 호출하면서 인수를 전달할 수 있다.
- 이벤트 핸들러를 반환하는 함수를 호출하면서 인수를 전달할 수도 있다.

### 커스텀 이벤트

`개발자가 의도로 생성한 이벤트`

```jsx
// KeyboardEvent 생성자 함수로 keyup 이벤트 타입의 커스텀 이벤트 객체를 생성
const keyboardEvent = new keyboardEvent('keyup');
console.log(keyboardEvent.type); // keyup
```

- 생성된 커스텀 이벤트 객체는 버블링되지 않으며 preventDefault 메서드로 취소할 수 없다. (bubbles와 cancelable 프로퍼티 값이 false로 기본 설정)
- true로 설정하려면 이벤트 생성자 함수의 두 번째 인수로 bubbles 또는 cancelable 프로퍼티를 갖는 객체를 전달
- 커스텀 이벤트 객체에는 bubbles 또는 cancelable 프로퍼티뿐만 아니라 이벤트 타입에 따라 가지는 이벤트 고유의 프로퍼티 값을 지정할 수 있다.
- 이벤트 생성자 함수로 생성한 커스텀 이벤트는 isTrusted 프로퍼티의 값이 언제나 false다. 커스텀 이벤트가 아닌 사용자의 행위에 의해 발생한 이벤트에 의해 생성된 이벤트 객체의 isTrusted 프로퍼티 값은 언제나 true다.
- 커스텀 이벤트 디스패치(dispatchEvent)
    - 생성된 커스텀 이벤트는 dispatchEvent 메서드로 디스패치(이벤트를 발생시키는 행위)할 수 있다.
    - 일반적으로 이벤트 핸들러는 비동기 방식으로 동작하지만 dispatchEvent 메서드는 이벤트 핸들러를 동기 처리 방식으로 호출 → dispatchEvent 메서드를 호출하면 커스텀 이벤트에 바인딩된 이벤트 핸들러를 직접 호출하는 것과 같다. → dispatchEvent 메서드로 이벤트를 디스패치 하기 이전에 커스텀 이벤트를 처리할 이벤트 핸들러를 등록해야 한다.
- CustomEvent → 기존 이벤트 타입이 아닌 임의의 이벤트 타입을 지정하여 이벤트 객체를 생성하는 경우 CustomEvent 생성자 함수를 사용. 반드시 addEventListener 메서드 방식으로 이벤트 핸들러를 등록해야 한다.