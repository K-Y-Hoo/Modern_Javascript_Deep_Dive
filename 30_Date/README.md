# 30_Date

`빌트인 객체이면서 생성자 함수`

`UTC 국제 표준시가 기준`

1970년 1월 1일 00:00:00(UTC) 기점

### Date 생성자 함수

- new Date() → 현재 날짜와 시간을 가지는 Date 객체를 반환
    
    Date() → 날짜와 시간 정보를 나타내는 문자열 반환(객체를 반환하지 않는다)
    
- new Date(milliseconds) → 기점을 기준으로 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date 객체를 반환
- new Date(dataString) → Date.parse 메서드에 의해 해석 가능한 형식의 문자열을 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체 반환
- new Date(year, month[, day, hour, minute, second, millisecond]) → 연, 월은 반드시 지정, Date 객체 반환

### Date 메서드

- Date.now → 기점을 기준으로 현재 시간까지 경과한 밀리초를 숫자로 반환
- Date.parse → 기점을 기준으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환
- Date.UTC → 기점을 기준으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환
- Date.prototype.getFullYear → Date 객체의 연도를 나타내는 정수를 반환
- Date.prototype.setFullYear → Date 객체에 연도를 나타내는 정수를 설정(월, 일도 가능)
- Date.prototype.getMonth → 0 ~11 정수를 반환. (1월은 0, 12월은 11)
- Date.prototype.setMonth → 0 ~11 정수를 월로 설정
- getDate → 1 ~ 31 정수 반환
- setDate → 1 ~ 31 정수 설정
- getDay → 요일(0~6)을 나타내는 정수를 반환(0은 일요일, 6은 토요일)
- getHours → 0 ~ 23 정수 반환
- setHours → 0 ~ 23 정수 설정
- getMinutes → 0 ~ 59 정수 반환
- setMinutes → 0 ~ 59 정수 설정
- getSeconds → 0 ~ 59 정수 반환
- setSeconds → 0 ~ 59 정수 설정
- getMilliseconds → 0 ~ 999 정수 반환
- setMilliseconds → 0 ~ 999 정수 설정
- getTime → 기점을 기준으로 Date 객체의 시간까지 경과된 밀리초 반환
- setTime → 기점을 기준으로 경과된 밀리초를 설정
- getTimezoneOffset → UTC와 로컬 시간과의 차이를 분 단위로 반환
- toDateString → Date 객체의 날짜를 문자열로 반환
- toTimeString → Date 객체의 시간을 문자열로 반환
- toISOString → Date 객체의 날짜와 시간을 문자열로 반환(ISO 8601 형식)
- toLocaleString → 인수로 전달한 로켈을 기준으로 Date 객체의 날짜와 시간을 문자열로 반환
- toLocaleTimeString → 인수로 전달한 로켈을 기준으로 Date 객체의 시간을 문자열로 반환