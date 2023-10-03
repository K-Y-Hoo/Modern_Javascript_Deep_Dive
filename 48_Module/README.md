# 48_모듈

## 모듈의 일반적 의미

`모듈이란 애플리케이션을 구성하는 개별적 요소로서 재사용 가능한 코드 조각을 말한다.`

- 모듈은 기능을 기준으로 파일 단위로 분리한다. 모듈이 성립하려면 모듈은 자신만의 파일 스코프(모듈 스코프)를 가질 수 있어야 한다.
- 자신만의 파일 스코프를 갖는 모듈의 자산(변수, 함수, 객체 등)은 기본적으로 비공개 상태, 캡슐화되어 다른 모듈에서 접근할 수 없다. 모듈은 개별적 존재로서 애플리케이션과 분리되어 존재한다. → export를 통해 공개가 필요한 자산에 한정하여 명시적으로 선택적 공개가 가능하다.
- 공개된 모듈의 자산은 다른 모듈에서 재사용할 수 있다. 모듈 사용자는 import를 통해 모듈이 공개한 자산 중 일부 또는 전체를 선택해 자신의 스코프 내로 불러들여 재사용할 수 있다.
- 재사용성이 좋아서 개발 효율성과 유지보수성을 높일 수 있다.

## 자바스크립트와 모듈

- 자바스크립트는 모듈 시스템을 지원하지 않는다. → 자바스크립트 파일을 여러 개의 파일로 분리하여 script 태그로 로드해도 분리된 자바스크립트 파일들은 결국 하나의 자바스크립트 파일 내에 있는 것처럼 동작한다. → 모든 자바스크립트 파일은 하나의 전역을 공유한다.
- 자바스크립트 런타임 환경인 Node.js는 ECMAScript 표준 사양은 아니지만 모듈 시스템을 지원한다. Node.js 환경에서는  파일별로 독립적인 파일 스코프(모듈 스코프)를 갖는다.

## ES6 모듈(ESM)

`ES6에서는 클라이언트 사이드 자바스크립트에서도 동작하는 모듈 기능을 추가했다.`

```jsx
<script type="module" src="app.mjs"></script>
//ESM임을 명확히 하기 위해 파일 확장자는 mjs를 권장
//ESM에는 클래스와 마찬가지로 기본적으로 strict mode 적용됨
```

- export 키워드
    - 선언문 앞에 사용해서 변수, 함수, 클래스 등 모든 식별자를 export 할 수 있다.
    - 선언문 앞에 매번 export 키워드를 붙이는 것이 번거롭다면 export할 대상을 하나의 객체로 구성하여 한 번에 export할 수도 있다.
    
    ```jsx
    //lib.mjs
    const pi =MAth.PI;
    
    function square(x) {
    	return x * x;
    }
    
    class Person {
    	constructor(name) {
    		this.name = name;
    	}
    }
    
    export { pi, square, Person };
    ```
    
- import 키워드
    - 다른 모듈이 export한 식별자 이름으로 import해야 한다. ESM의 경우 파일 확장자를 생략할 수 없다.
    
    ```jsx
    //app.mjs
    
    import { pi, square, Person } from './lib.mjs';
    
    //모든 식별자를 lib 객체의 프로퍼티로 모아 한번에 import
    import * as lib from './lib.mjs';
    
    //모듈이 export한 식별자 이름을 변경하여 import 가능
    import { pi as PI, square as sq, Person as P } from './lib.mjs';
    
    //모듈이 하나의 값만 export 한다면 default 키워드를 사용할 수 있다.
    //기본적으로 이름 없이 하나의 값을 export한다.
    //lib.mjs
    export default x => x * x;
    
    //var, let, const 키워드는 사용할 수 없다.
    export default const foo = () => {}; // SyntaxError
    
    //{} 없이 임의의 이름으로 import한다.
    //app.mjs
    import square from './lib.mjs';
    ```
    
    - lib.mjs는 app.mjs의 import문에 의해 로드되는 의존성이기 때문에 lib.mjs는 script 태그로 로드하지 않아도 된다.
    
    ```jsx
    <!DOCTYPE html>
    <html>
    <body>
    	<script type="module" src="app.mjs"></script>
    </body>
    </html>
    ```