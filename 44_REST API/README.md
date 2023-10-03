# 44_REST API

`REST는 HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍처`

`REST API는 REST를 기반으로 서비스 API를 구현한 것`

`REST의 기본 원칙을 성실히 지킨 서비스 디자인을 RESTful 이라고 표현한다.`

### REST API의 구성

`자원(URI), 행위(HTTP 요청 메서드), 표현(페이로드)`

REST는 자체 표현 구조로 구성되어 REST API만으로 HTTP 요쳥의 내용을 이해할 수 있다.

### REST API 설계 원칙

1. `URI는 리소스를 표현하는 데 집중`
    - 리소스를 식별할 수 있는 이름은 동사보다는 명사를 사용
    
    ```jsx
    // 좋은 예시
    GET /todos/1 
    
    // 나쁜 예시
    GET /getTodos/1
    GET /todos/show/1
    ```
    
2. `HTTP 요청 메서드를 통해 행위에 대한 정의`
    - GET, POST, PUT, PATCH, DELETE를 사용하여 CRUD 구현
    
    ```jsx
    // 좋은 예시
    DELETE /todos/1
    
    // 나쁜 예시
    GET /todos/delete/1
    ```