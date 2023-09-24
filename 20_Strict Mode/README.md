# 20_strict mode

```jsx
function foo() {
	x = 10;
}
foo();
console.log(x);   // 10
```

암묵적 전역: 전역 스코프에도 x 변수의 선언이 존재하지 않기 때문에 ReferenceError를 발생시킬 것 같지만 자바스크립트 엔진은 암묵적으로 전역 객체에 x 프로퍼티를 동적으로 생성한다. 이 때 전역 객체의 x 프로퍼티를 마치 전역 변수처럼 사용할 수 있다. → 키워드를 사용하여 변수를 선언한 다음 사용해야 한다.

`잠재적인 오류를 발생시키기 어려운 개발 환경을 만들기 위해 ES5부터 strict mode가 추가되었다.`

```jsx
'use strict'; // 전역의 선두 또는 함수 몸체의 선두에 추가한다.
```

전역의 선두에 적용하는 것은 바람직하지 않다. 함수 단위로 적용하는 것도 바람직하지 않다. 즉시 실행 함수로 스크립트 전체를 감싸서 스코프를 구분하고 즉시 실행 함수의 선두에 strict mode를 적용하라.

```jsx
(function () {
	'use strict';
}());
```

### strict mode가 발생시키는 에러

- 암묵적 전역(선언하지 않은 변수를 참조하면 ReferenceError 발생)
- 변수, 함수, 매개변수의 삭제(delete 연산자로 삭제하면 SyntaxError 발생)
- 매개변수 이름의 중복(중복된 매개변수 이름을 사용하면 SyntaxError 발생)
- with문의 사용(성능과 가독성이 나빠지는 단점때문에 SyntaxError 발생)

### strict mode 적용에 의한 변화

- 일반 함수의 this(undefined가 바인딩됨)
- arguments 객체(매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영 X)
    
    ```jsx
    (function (a) {
    	'use strict';
    	a = 2;
    	console.log(arguments); // { 0: 1, length: 1 }
    }(1));
    ```