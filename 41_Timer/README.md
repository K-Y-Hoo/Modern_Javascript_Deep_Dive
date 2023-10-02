# 41_타이머

### 호출 스케줄링

`함수를 명시적으로 호출하면 함수가 즉시 실행됨. 함수를 명시적으로 호출하지 않고 일정 시간이 경과된 이후에 호출되도록 함수 호출을 예약하려면 타이머 함수를 사용 → 호출 스케줄링`

- 타이머 생성: setTimeout, setInterval
- 타이머 제거: clearTimeout, clearInterval
- 타이머 함수는 ECMAScript 빌트인 함수가 아닌 브라우저 환경, Node.js 환경의 전역 객체 메서드이면서 호스트 객체다.
- 자바스크립트 엔진은 싱글 스레드로 동작하기 때문에 타이머함수는 비동기 처리 방식으로 동작

### 타이머 함수

- setTimeout/clearTimeout → 생성된 타이머를 식별할 수 있는 고유한 타이머 id 반환
    
    ```jsx
    setTimeout(() => console.log('Hi!'), 1000); 
    // 1초(1000ms) 후 타이머가 만료되면 콜백함수 호출
    
    setTimeout(name => console.log(`Hi! ${name}.`), 1000, 'Kim'); 
    // 콜백 함수에 'Kim'을 인수로 전달
    
    setTimeout(() => console.log('Hello!)); 
    // 두 번째 인수 생략하면 기본값 0 지정
    
    const timerId = setTimeout(() => console.log('Hi!'), 1000);
    clearTimeout(timerId); 
    // 타이머가 취소되면 setTimeout 함수의 콜백 함수가 실행되지 않는다.
    ```
    
- setInterval / clearInterval
    
    ```jsx
    let count = 1;
    //1초 후 타이머가 만료될 때마다 콜백 함수가 호출된다.
    const timeoutId = setInterval(() => {
    	console.log(count); // 1 2 3 4 5
    	if (count++ === 5) clearInterval(timeoutId);
    }, 1000);
    //count가 5이면 타이머를 취소한다.
    ```
    

### 디바운스, 스로틀

- 짧은 시간 간격으로 연속해서 발생하는 이벤트(scroll, resize, input, mousemove 등)에 바인딩한 이벤트 핸들러는 과도하게 호출되어 성능에 문제를 일으킬 가능성이 존재.
- 디바운스와 스로틀은 이러한 이벤트를 그룹화해서 과도한 이벤트 핸들러의 호출을 방지하는 프로그래밍 기법이다.
- 디바운스와 스로틀의 구현에는 타이머 함수가 사용된다.
- 디바운스: 짧은 시간 간격으로 이벤트가 연속해서 발생하면 이벤트 핸들러를 호출하지 않다가 일정 시간이 경과한 이후 이벤트 핸들러가 한 번만 호출되도록 한다.
- 스로틀: 짧은 시간 간격으로 이벤트가 연속해서 발생하더라도 일정 시간 간격으로 이벤트 핸들러가 최대 한 번만 호출되도록 한다.(일정 시간 단위의 호출 주기를 만든다)
- 실무에서는 Underscore, Lodash의 debounce, throttle 함수를 사용하는 것을 권장