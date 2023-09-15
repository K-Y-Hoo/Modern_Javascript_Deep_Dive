# 08_제어문

### 블록문

- 0개 이상의 문을 중괄호로 묶은 것으로, 블록 또는 코드 블록이라고 부른다.
- 단독으로 사용할 수도 있으나 일반적으로 제어문이나 함수를 정의할때 사용한다.
- 자체 종결성에 의해 세미콜론을 붙이지 않는다.

### 조건문

- 조건식(불리언 값으로 평가될 수 있는 표현식)의 평가 결과에 따라 블록문의 실행을 결정한다.
- `if 문`, `if … else 문`, `if … else if … else 문`
    - 코드 블록 내의 문이 하나뿐이라면 중괄호를 생략할 수 있다.
    
    ```jsx
    if (num > 0) kind = '양수';
    ```
    
    - 대부분의 if .. else 문은 삼항 조건 연산자로 바꿔 쓸 수 있다. 하지만 표현식이 아닌 문이기 때문에 삼항 조건 연산자 표현식처럼 값으로 사용할 수 없다.(변수에 할당할 수 없다)
- switch문
    - switch문의 표현식은 불리언 값보다는 문자열이나 숫자 값인 경우가 많다.
    - 폴스루 → switch문이 끝날 때까지 switch문을 탈출하지 않고 모든 case문과 default문을 실행한 것 → break 미사용이 그 이유
    - default문에는 break 생략
    - break 문을 생략한 폴스루가 유용한 경우도 있다. (예: 윤년인지 판별해서 2월의 일수를 계산)

### 반복문

`for문`, `while문`, `do … while문`

- for문
    
    ```jsx
    for (var i = 0; i < 2; i++) {
    	console.log(i);
    } // 0 1
    ```
    
    ```jsx
    for (var i = 1; i >= 0; i--) {
    	console.log(i);
    } // 1 0
    ```
    
    ```jsx
    for (;;) { ... } // 무한루프
    ```
    

- while문
    
    ```jsx
    while (true) { ... } // 무한루프
    ```
    
    break 문으로 코드 블록을 탈출 가능
    

- do .. while 문
    
    코드 블록을 먼저 실행하고 조건식을 평가 → 코드 블록은 무조건 한 번 이상 실행된다.
    

### break 문

- 모든 코드 블록을 탈출하는 것이 아니라 레이블 문, 반복문, switch문의 코드 블록을 탈출한다.

```jsx
if (true) {
	break; // Uncaught SyntaxError: Illegal break statement
}
```

- 레이블 문은 중첩된 for 문 외부로 탈출할 때 유용하지만 그 밖의 경우에는 일반적으로 권장되지 않는다.

### continue 문

- 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킨다.
- continue 문을 사용하면 if 문 밖에 코드를 작성할 수 있다.
    
    ```jsx
    for (var i = 0; i < string.length; i++) {
    	if (string[i] !== search) continue;
    
    	count++;
    	//code
    	//code...
    }
    ```