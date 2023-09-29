# 37_Set과 Map

`Set 객체는 중복되지 않는 유일한 값들의 집합!`

`배열과 다르게 요소 순서에 의미가 없고 인덱스로 요소에 접근할 수 없다`

`수학적 집합을 구현하기 위한 자료구조!`

### Set

- set객체 생성 → set 생성자 함수(인수 전달하지 않으면 빈 set 객체 생성)
    
    ```jsx
    const set = new Set();
    console.log(set); // set(0) {}
    
    const set1 = new Set([1, 2, 3, 4]);
    console.log(set1); // Set(3) {1, 2, 3}
    
    const set2 = new Set('hello');
    console.log(set2); // Set(4) {"h", "e", "l", "o"}
    ```
    
- 요소 개수 확인 → Set.prototype.size(getter 함수만 존재하는 접근자 프로퍼티)
    
    ```jsx
    const {size} = new Set([1, 2, 3, 3]);
    console.log(size); // 3
    ```
    
- 요소 추가 → Set.prototype.add(새로운 요소가 추가된 Set 객체를 반환, 연속 호출 가능)
    
    ```jsx
    const set = new Set();
    set.add(1);
    console.log(set); // Set(1) {1}
    set.add(2).add(3);
    console.log(set); // Set(3) {1, 2, 3}
    ```
    
- 요소 존재 여부 확인 → Set.prototype.has(불리언 값 반환)
    
    ```jsx
    const set = new Set([1, 2, 3]);
    console.log(set.has(4)); // false
    ```
    
- 요소 삭제 → Set.prototype.delete(인수는 삭제하려는 요소값, 불리언 값 반환, 연속 호출 불가능)
    
    ```jsx
    const set = new Set([1, 2, 3]);
    set.delete(2);
    console.log(set); // Set(2) {1, 3}
    ```
    
- 요소 일괄 삭제 → Set.prototype.clear(언제나 undefined 반환)
    
    ```jsx
    const set = new Set([1, 2, 3]);
    set.clear();
    console.log(set); // Set(0) {}
    ```
    
- 요소 순회 → Set.prototype.forEach(콜백 함수 내부에서 this로 사용될 객체(옵션)를 인수로 전달, 인수는 총 3개)
    
    첫 번째 인수: 현재 순회 중인 요소값
    
    두 번째 인수: 현재 순회 중인 요소값 // Array.prototype.forEach 메서드와 인터페이스 통일 목적
    
    세 번째 인수: 현재 순회 중인 Set 객체 자체
    
    ```jsx
    const set = new Set([1, 2, 3]);
    set.forEach((v, v2, set) => console.log(v, v2, set));
    ```
    
    - Set 객체는 이터러블이기 때문에 for…of 문으로 순회 가능, 스프레드 문법, 디스트럭처링 사용 가능
    - Set 객체는 요소의 순서에 의미를 갖지 않지만 Set 객체를 순회하는 순서는 요소가 추가된 순서를 따른다 → 다른 이터러블의 순회와 호환성을 유지하기 위한 목적
- 집합 연산 → (교집합, 합집합, 차집합, 부분 집합, 상위 집합)

### Map

`Map 객체는 키와 값의 쌍으로 이루어진 컬렉션. 객체와의 차이점은 키로 사용할 수 있는 값이 객체를 포함한 모든 값이고 이터러블이며 요소 개수 확인은 map.size로 수행한다.`

- Map 객체 생성 → Map 생성자 함수(요소 미전달시 빈 Map 객체 생성)
    
    ```jsx
    const map = new Map();
    console.log(map); // Map(0) {}
    ```
    
    Map 생성자 함수는 이터러블을 인수로 전달받아 Map 객체를 생성. 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성되어야 한다.
    
    인수로 전달된 이터러블에 중복된 키를 갖는 요소가 존재하면 값이 덮어써진다. → Map 객체에는 중복된 키를 갖는 요소가 존재할 수 없다.
    
    ```jsx
    const map = new Map([['key1', 'value1'], ['key1', 'value2']]);
    console.log(map); // Map(1) {"key1" => "value2"}
    ```
    
- 요소 개수 확인 → Map.prototype.size
- 요소 추가 →Map.prototype.set(새로운 요소가 추가된 Map 객체 반환, 연속 호출 가능)
    
    ```jsx
    const map = new Map();
    Map.set('key1', 'value1');
    console.log(map); // Map(1) {"key1" => "value1"}
    ```
    
    Map 객체는 키 타입에 제한이 없다. `(일반 객체와 가장 두드러지는 차이점!)`
    
- 요소 취득 → Map.prototype.get(인수로 전달한 키를 갖는 값을 반환, 없으면 undefined)
- 요소 존재 여부 확인 → Map.prototype.has
- 요소 삭제 → Map.prototype.delete
- 요소 일괄 삭제 → Map.prototype.clear
- 요소 순회 → Map.prototype.forEach
    
    첫 번째 인수: 현재 순회 중인 요소값
    
    두 번째 인수: 현재 순회 중인 요소키
    
    세 번째 인수: 현재 순회 중인 Map 객체 자체
    
    - Map 객체는 이터러블이면서 동시에 이터레이터인 객체를 반환하는 메서드 제공
        - Map.prototype.keys
        - Map.prototype.values
        - Map.prototype.entries