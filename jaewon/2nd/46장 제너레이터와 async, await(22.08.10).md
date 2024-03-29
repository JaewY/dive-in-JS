## 46장 제너레이터와 async/await

### 📌 제너레이터란?
- 제너레이터란 코드 블록의 실행을 일시 중지했다가 필요한 시점을 재개할 수 있는 특수한 함수다.
  - 제너레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양도할 수 있다.
  - 제너레이터 함수는 함수 호출자와 함수의 상태를 주고받을 수 있다.
  - 제너레이터 함수를 호출하면 제너레이터 객체를 반환한다.
<br>

### 📌 제너레이터 함수의 정의
- 제너레이터 함수는 function* 키워드로 선언한다.
- 하나 이상의 yield 표현식을 포함한다.
- 이것을 제외하면 일반 함수를 정의하는 방법과 같다.
- 제너레이터 함수는 화살표 함수로 정의할 수 없다.
- 제너레이터 함수는 new 연산자와 함께 생성자 함수로 호출할 수 없다.
```js
function* getDecFunc() {
  yield 1;
}

const genExpFunc = function* () {
  yield 1;
}

const obj = {
  * genObjMethod() {
    yield 1;
  }
};
```
<br>

### 📌 제너레이터 객체
- 제너레이터 함수를 호출하면 일반 함수처럼 함수 코드 블록을 실행하는 것이 아니라 제너레이터 객체를 생성해 반환한다.
- 제너레이터 함수가 반환한 제너레이터 객체는 이터러블이면서 동시에 이터레이터다.
<br>

### 📌 제너레이터의 일시 중지와 재개
- 제너레이터는 yield 키워드와 next 메서드를 통해 실행을 일시 중지했다가 필요한 시점에 다시 재개할 수 있다.
- yield 키워드는 제너레이터 함수의 실행을 일시 중지시키거나 yield 키워드 뒤에 오는 표현식의 평가 결과를 제너레이터 함수 호출자에게 반환한다.
<br>

### 📌 제너레이터의 활용
#### 이터러블의 구현
- 제너레이터 함수를 사용하면 이터레이션 프로토콜을 준수해 이터러블을 생성하는 방식보다 간단히 이터러블을 구현할 수 있다.
#### 비동기 처리
- 제너레이터 함수는 next 메서드와 yield 표현식을 통해 함수 호출자와 함수의 상태를 주고받을 수 있다.
- 이러한 특성을 활용하면 프로미스를 사용한 비동기 처리를 동기 처리처럼 구현할 수 있다.
<br>

### 📌 async/await
- async/await는 프로미스를 기반으로 동작한다.
- 프로미스의 then/catch/finally 후속 처리 메서드에 콜백 함수를 전달해서 비동기 처리 결과를 후속 처리할 필요 없이 마치 동기 처리처럼 프로미스를 사용할 수 있다.

#### async 함수
- await 키워드는 반드시 async 함수 내부에서 사용해야 한다.
- async 함수는 async 키워드를 사용해 정의하며 언제나 프로미스를 반환한다.
- async 함수가 명시적으로 프로미스를 반환하지 않더라도 async 함수는 암묵적으로 반환값을 resolve하는 프로미스를 반환한다.

#### await 키워드
- await 키워드는 프로미스가 settled 상태(비동기 처리가 수행된 상태)가 될 때까지 대기하다가 settled 상태가 되면 프로미스가 resolve한 처리 결과를 반환한다.
- await 키워드는 반드시 프로미스 앞에서 사용해야 한다. 
