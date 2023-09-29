# 35_스프레드 문법

`하나로 뭉쳐 있는 여러 값들의 집합을 펼처서 개별적인 값들의 목록으로 만든다!`

`스프레드 문법을 사용할 수 있는 대상은 Array, String, Map, Set, DOM 컬렉션(NodeList, HTMLCollection), arguments 와 같이 for…of 문으로 순회할 수 있는 이터러블에 한정된다!`

`스프레드 문법의 결과는 값이 아닌 값들의 목록이기 때문에 변수에 할당할 수 없다!`

- 함수 호출문의 인수 목록
- 배열 리터럴의 요소 목록
- 객체 리터럴의 프로퍼티 목록

`Rest 파라미터와 스프레드 문법 혼동 주의! 서로 반대 개념이다.`

### 함수 호출문의 인수 목록

```jsx
const arr = [1, 2, 3];

const max = Math.max(arr); // NaN

const max = Math.max(...arr); // 3
```

### 배열 리터럴 내부에서 사용하는 경우

- concat
    
    ```jsx
    //ES5
    var arr = [1, 2].concat([3, 4]);
    console.log(arr); // [1, 2, 3, 4]
    
    //ES6
    const arr = [...[1, 2], ...[3, 4]];
    console.log(arr); // [1, 2, 3, 4]
    ```
    
- splice
    
    ```jsx
    //ES5
    var arr1 = [1, 4];
    var arr2 = [2, 3];
    arr1.splice(1, 0, arr2);
    console.log(arr1); // [1, [2, 3], 4]
    
    //ES6
    const arr1 = [1, 4];
    const arr2 = [2, 3];
    arr1.splice(1, 0, ...arr2);
    console.log(arr1); // [1, 2, 3, 4]
    ```
    
- slice(배열 복사)
    
    ```jsx
    //ES5
    var origin = [1, 2];
    var copy = origin.slice();
    console.log(copy); // [1, 2]
    console.log(copy === origin); // false 얕은 복사
    
    //ES6
    const origin = [1, 2];
    const copy = [...origin];
    console.log(copy); // [1, 2]
    console.log(copy === origin); // false 얕은 복사
    ```
    
- 이터러블을 배열로 반환(apply, call) → 이터러블, 이터러블이 아닌 유사 배열 객체를 배열로 변환

### 객체 리터럴 내부에서 사용하는 경우

- 객체 리터럴의 프로퍼티 목록에서도 스프레드 문법을 사용할 수 있다. 스프레드 문법의 대상은 이터러블이어야 하지만 스프레드 프로퍼티 제안은 일반 객체를 대상으로도 스프레드 문법의 사용을 허용한다.
- 객체 복사, 객체 병합, 특정 프로퍼티 변경, 프로퍼티 추가