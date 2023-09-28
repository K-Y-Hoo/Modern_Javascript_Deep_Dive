# 29_Math

`생성자 함수가 아니다. 정적 프로퍼티와 정적 메서드만 제공한다.`

### Math 프로퍼티

- Math.PI → 원주율 값을 반환

### Math 메서드

- Math.abs → 인수로 전달된 숫자의 절대값을 반환
- Math.round → 인수로 전달된 숫자의 소수점 이하를 반올림한 정수를 반환
    
    ```jsx
    Math.round(1.4); // 1
    Math.round(1.6); // 2
    Math.round(-1.4); // -1
    Math.round(-1.6); // -2
    ```
    
- Math.ceil → 인수로 전달된 숫자의 소수점 이하를 올림한 정수를 반환
    
    ```jsx
    Math.ceil(1.4); // 2
    Math.ceil(1.6); // 2
    Math.ceil(-1.4); // -1
    Math.ceil(-1.6); // -1
    ```
    
- Math.floor → 인수로 전달된 숫자의 소수점 이하를 내림한 정수를 반환
    
    ```jsx
    Math.floor(1.9); // 1
    Math.floor(9.1); // 9
    Math.floor(-1.9); // -2
    Math.floor(-9.1); // -10
    ```
    
- Math.sqrt → 인수로 전달된 숫자의 제곱근을 반환
- Math.random → 0에서 1 미만의 실수 난수를 반환. 0은 포함, 1은 미포함
- Math.pow → 첫 번째 인수를 밑, 두 번째 인수를 지수로 거듭제곱한 결과를 반환
- Math.max → 전달받은 인수 중에서 가장 큰 수를 반환. 인수 없으면 -Infinity 반환
- Math.min → 전달받은 인수 중에서 가장 작은 수를 반환. 인수 없으면 Infinity 반환
    - 배열을 인수로 전달받아 배열의 요소 중에서 최대 최소를 구하려면 apply 혹은 스프레드 문법을 사용해야 한다.
    
    ```jsx
    Math.max.apply(null, [1, 2, 3]); // 3
    Math.min(...[1, 2, 3]); // 1
    ```