# 27_배열

`자바스크립트에 배열이라는 타입은 존재하지 않는다. 배열은 객체 타입이다.`

```jsx
const arr = [1, 2, 3];
typeof arr; // object
```

배열의 생성

- 배열 리터럴
- Array 생성자 함수
- Array.of
- Array.from

`일반 객체와 배열을 구분하는 차이는 값의 순서와 length 프로퍼티`

### 자바스크립트 배열은 배열이 아니다

`일반적인 배열의 동작을 흉내 낸 특수한 객체`

- 배열의 요소를 위한 각각의 메모리 공간이 동일한 크기를 갖지 않아도 된다
- 연속적으로 이어져 있지 않을 수 있다 → 희소 배열

일반적인 배열과 자바스크립트 배열의 장단점 정리

```jsx
일반적인 배열은 인덱스로 요소에 빠르게 접근 가능하지만 특정 요소를 검색하거나 삽입 또는 삭제
하는 경우에는 효율적이지 않다.
자바스크립트 배열은 해시 테이블로 구현된 객체. 인덱스로 요소에 접근하는 경우 일반적인 배열보다
성능적인 면에서 느리다. 하지만 특정 요소를 검색, 삽입, 삭제하는 경우에는 일반적인 배열보다
빠르다.
```

### length 프로퍼티와 희소 배열

- 현재 length 프로퍼티 값보다 작은 숫자 값을 할당하면 배열의 길이가 줄어든다.
    
    ```jsx
    const arr = [1, 2, 3, 4, 5];
    arr.length = 3;
    console.log(arr); // [1, 2, 3]
    ```
    
- 큰 숫자 값을 할당하는 경우 → 희소 배열
    
    ```jsx
    const arr = [1];
    arr.length = 3;
    console.log(arr.length); // 3
    console.log(arr) // [1, empty x 2]
    ```
    
    값 없이 비어 있는 요소를 위해 메모리 공간을 확보하지 않으며 빈 요소를 생성하지도 않는다.
    
- 희소배열의 length는 희소 배열의 실제 요소 개수보다 언제나 크다.
- 배열에는 같은 타입의 요소를 연속적으로 위치시키는 것이 최선이다.

### 배열 생성

- 배열 리터럴
    
    ```jsx
    const arr = [1,  2, 3];
    ```
    
- Array 생성자 함수
    
    ```jsx
    const arr = new Array(5);
    console.log(arr); // [empty x 5]
    console.log(arr.length); // 5
    
    new Array(); // []
    
    new Array(1, 2, 3); // [1, 2, 3]
    new Array({}); // [{}]
    
    Array(1, 2, 3); // [1, 2, 3]
    //Array 생성자 함수는 new 연산자와 함께 호출하지 않더라도, 즉 일반 함수로서 호출해도 배열
    을 생성하는 생성자 함수로 동작한다. Array 생성자 함수 내부에서 new.target을 확인하기 때문
    ```
    
- Array.of
    
    ```jsx
    Array.of(1); // [1]
    Array.of(1, 2, 3); // [1, 2, 3]
    Array.of('string'); // ['string']
    ```
    
- Array.from ( 유사 배열 객체 또는 이터러블 객체를 인수로 전달받아 배열로 변환하여 반환 )
    
    ```jsx
    Array.from({ length: 2, 0: 'a', 1: 'b' }); // ['a', 'b'] 유사 배열 객체를 변환
    Array.from('Hello'); // ['H', 'e', 'l', 'l', 'o'] 이터러블을 변환(문자열은 이터러블)
    ```
    
    두 번째 인수로 전달한 콜백 함수를 통해 값을 만들면서 요소를 채울 수 있다.
    
    ```jsx
    Array.from({ length: 3}, (_, i) => i); // [0, 1, 2]
    ```
    

### 배열 요소의 참조

- 대괄호 표기법 사용
- 존재하지 않는 요소에 접근하면 undefined 반환
- 희소 배열의 존재하지 않는 요소를 참조해도 undefined 반환

### 배열 요소의 추가와 갱신

- 요소를 동적으로 추가 가능(존재하지 않는 인덱스를 사용하여 값을 할당)
    
    ```jsx
    const arr = [0];
    arr[1] = 1;
    console.log(arr); // [0, 1]
    ```
    
- 현재 배열의 length 프로퍼티 값보다 큰 인덱스로 새로운 요소를 추가하면 희소 배열이 됨
    
    ```jsx
    arr[100] = 100;
    console.log(arr); // [0, 1, empty x 98, 100]
    console.log(arr.length); // 101
    ```
    
- 인덱스에 0이상의 정수(또는 정수 형태의 문자열)가 아닌 값을 사용하면 요소가 생성되는 것이 아니라 프로퍼티가 생성된다. 이때 추가된 프로퍼티는 length에 영향을 주지 않는다.
    
    ```jsx
    const arr = [];
    arr[0] = 1;
    arr['1'] = 2;
    arr['foo'] = 3;
    arr.bar = 4;
    arr[1.1] = 5;
    arr[-1] = 6;
    console.log(arr); // [1, 2, foo: 3, bar: 4, '1.1': 5, '-1': 6]
    console.log(arr.length); // 2
    ```
    

### 배열 요소의 삭제

- 배열은 객체이기 때문에 특정 요소 삭제에 delete 연산자를 사용 가능하다. 하지만 length 값은 변하지 않는 희소 배열이 되기 때문에 사용하지 않는 것이 좋다.
- Array.prototype.splice 메서드를 사용하는 것이 좋다. (희소 배열을 만들지 않는다)
    
    ```jsx
    const arr = [1, 2, 3];
    arr.splice(1, 1);
    console.log(arr); // [1, 3]
    console.log(arr.length); // 2
    ```
    

### 배열 메서드

- `Array.isArray`    생성자 함수의 정적 메서드. 전달된 인수가 배열이면 true
    
    ```jsx
    Array.isArray([]);
    Array.isArray([1, 2]);
    Array.isArray(new Array());
    ```
    
- `Array.prototype.indexOf`    인수로 전달된 요소를 검색하여 인덱스를 반환
    
    ```jsx
    중복되는 요소가 여러 개 있다면 첫 번째로 검색된 요소의 인덱스 반환
    존재하지 않으면 -1 반환
    두 번째 인수는 검색을 시작할 인덱스(생략하면 처음부터 검색)
    ```
    
- `Array.prototype.push`    원본 배열의 마지막 요소로 추가, 변경된 length 프로퍼티 값 반환, 원본 배열 직접 변경
    
    ```jsx
    const arr = [1, 2];
    let result = arr.push(3, 4);
    console.log(result); // 4
    console.log(arr); // [1, 2, 3, 4]
    ```
    
- `Array.prototype.pop`    마지막 요소를 제거하고 제거한 요소를 반환, 원본 배열 직접 변경
    
    ```jsx
    const arr = [1, 2];
    let result = arr.pop();
    console.log(result); // 2
    ```
    
- `Array.prototype.unshift`    인수로 전달받은 모든 값을 원본 배열 앞에 추가, 변경된 length 프로퍼티 값 반환, 원본 배열 직접 변경
    
    ```jsx
    const arr = [1, 2];
    let result = arr.unshift(3, 4);
    console.log(result); // 4
    console.log(arr); // [3, 4, 1, 2]
    ```
    
- `Array.prototype.shift`    첫 번째 요소를 제거하고 제거한 요소 반환, 원본 배열 직접 변경
    
    ```jsx
    const arr = [1, 2];
    let result = arr.shift();
    console.log(result); // 1
    console.log(arr); // [2]
    ```
    
- `Array.prototype.concat`    인수로 전달된 값들(배열 혹은 원시값)을 원본 배열 마지막 요소로 추가한 새로운 배열 반환. 인수가 배열인 경우 배열을 해체하여 새로운 배열의 요소로 추가. 원본 배열 변경되지 않음
    
    ```jsx
    const arr1 = [1, 2];
    const arr2 = [3, 4];
    let result = arr1.concat(arr2);
    console.log(result); // [1, 2, 3, 4]
    console.log(arr1); // [1, 2]
    
    //ES6의 스프레드 문법으로 대체 가능
    result = [...[1, 2], ...[3, 4]];
    console.log(result); // [1, 2, 3, 4]
    ```
    
- `Array.prototype.splice`    원본 배열의 중간에 요소를 추가하거나 중간에 있는 요소를 제거하는 경우 사용, 3개의 매개변수, 원본 배열 직접 변경
    
    ```jsx
    const arr = [1, 2, 3, 4];
    const result = arr.splice(1, 2, 20, 30);
    console.log(result); // [2, 3]
    console.log(arr); // [1, 20, 30, 4]
    
    const arr2 = [1, 2, 3, 4];
    const result2 = arr2.splice(1, 0, 100);
    console.log(arr2); // [1, 100, 2, 3, 4];
    
    const arr3 = [1, 2, 3, 4];
    const result3 = arr3.splice(1, 2);
    console.log(arr3); // [1, 4]
    ```
    
- `Array.prototype.slice`    인수로 전달된 범위의 요소들을 복사하여 배열로 반환, 원본 배열 변경되지 않음, 인수를 모두 생략하면 원본 배열의 복사본 생성하여 반환(얕은 복사)
    
    ```jsx
    const arr = [1, 2, 3];
    arr.slice(0, 1); // [1]
    ```
    
- `Array.prototype.join`    원본 배열의 모든 요소를 문자열로 변환, 구분자로 연결한 문자열 반환, 기본 구분자는 콤마(,)
    
    ```jsx
    const arr = [1, 2, 3, 4];
    arr.join(); // '1, 2, 3, 4';
    arr.join(''); // '1234';
    arr.join(':'); // '1:2:3:4'
    ```
    
- `Array.prototype.reverse`    원본 배열의 순서를 뒤집는다. 원본 배열 변경
    
    ```jsx
    const arr = [1, 2, 3];
    const result = arr.reverse();
    console.log(arr); // [3, 2, 1]
    console.log(result); // [3, 2, 1]
    ```
    
- `Array.prototype.fill`    인수로 전달받은 값을 배열의 처음부터 끝까지 요소로 채운다. 원본 배열 변경
    
    ```jsx
    const arr = [1, 2, 3];
    arr.fill(0);
    console.log(arr); // [0, 0, 0]
    ```
    
- `Array.prototype.includes`    배열 내 특정 요소 포함되어 있는지 확인하여 boolean값 반환
- `Array.prototype.flat`    인수로 전달한 깊이만큼 재귀적으로 배열을 평탄화

### 배열 고차 함수

- 불변성 지향
- 순수 함수를 통해 부수 효과 최대한 억제
- `Array.prototpype.sort`    배열 요소 오름차순 정렬, 원본 배열 직접 변경, 정렬된 배열 반환, 기본 정렬 순서가 유니코드 코드 포인트 순서를 따르기 때문에 배열 요소가 숫자 타입이라도 배열의 요소를 일시적으로 문자열로 변환한 후 유니코드 코드 포인트의 순서를 기준으로 정렬 → 숫자 요소로 이루어진 배열을 정렬할때 주의 필요
- `Array.prototype.forEach`    고차 함수로서 내부에서 반복문을 통해 자신을 호출한 배열을 순회하면서 수행해야 할 처리를 콜백 함수로 전달받아 반복 호출, 원본 배열(this)을 변경하지 않는다. break, continue 사용 불가 → 중간에 순회 중단 불가, 항상 undefined 반환
    
    ```jsx
    const numbers = [1, 2, 3];
    const pows = [];
    numbers.forEach(item => pows.push(item ** 2));
    console.log(pows); // [1, 4, 9]
    // 콜백 함수도 3번 호출
    ```
    
- `Array.prototype.map`   콜백 함수의 반환값들로 구성된 새로운 배열 반환, 원본 배열 변경 X
- `Array.prototype.filter`    콜백 함수의 반환값이 true인 요소만 추출한 새로운 배열 반환
- `Array.prototype.reduce`    하나의 결과값을 만들어 반환, 원본 배열 변경 X
- `Array.prototype.some`    반환값이 단 한 번만이라도 참이면 true
- `Array.prototype.every`    반환값이 단 한번만이라도 거짓이면 false
- `Array.prototype.find`    콜백 함수 호출하여 반환값이 true인 첫 번째 요소를 반환
- `Array.prototype.findIndex`    콜백 함수호출하여 반환값이 true인 첫 번째 요소의 인덱스 반환
- `Array.prototype.flatMap`    m