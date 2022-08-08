# 44장 REST API

## REST : HTTP를 기반으로 클라이언트가 서버의 리소스에 접근하는 방식을 규정한 아키텍처

## REST API : REST를 기반으로 서비스 API를 구현한 것을 의미한다.

## RESTful : REST의 기본 원칙을 성실히 지킨 서비스 디자인

## 44.1 REST API의 구성

### REST API는 자원, 행위, 표현의 3가지 요소로 구성된다.

<img width="558" alt="스크린샷 2022-08-08 오후 1 34 13" src="https://user-images.githubusercontent.com/95524491/183339889-78cbd8ea-b36a-49d2-91a6-6fa258d7d391.png">

## 44.2 REST API 설계 원칙

### URI는 리소스를 표현하는 데 집중하고 행위에 대한 정의는 HTTP 요청 메서드를 통해 하는 것이 RESTful API를 설계하는 중심 규칙이다.

<br>

#### URI는 리소스를 표현해야 한다.

- URI는 리소스를 표현하는 데 중점을 두어야 한다.

- 리소스를 식별할 수 있는 이름은 동사보다는 명사를 사용한다.

- 이름에 get 같은 행위에 대한 표현이 들어가서는 안 된다.

```Js
// bad
GET /getTodos/1
GET /todos/show/1

// Good
GET /todos /1
```

#### 리소스에 대한 행위는 HTTP 요청 메서드로 표현한다.

- HTTP 요청 메서드는 클라이언트가 서버에게 요청의 종류와 목적(리소스에 대한 행위)을 알리는 방법이다.

- 주로 5가지 요청 메서드(GET, POST, PUT, PATCH, DELETE 등)를 사용하여 CRUD를 구현한다.

- 리소스에 대한 행위는 HTTP 요청 메서드를 통해 표현하며 URI에 표현하지 않는다

<img width="465" alt="스크린샷 2022-08-08 오후 1 39 15" src="https://user-images.githubusercontent.com/95524491/183340418-618a18d8-a526-41d7-b169-26062d2da98d.png">

```Js
// bad
GET /todos/delete/1

// Good
DELETE /todos/1
```
