## 15장 let, const 키워드와 블록 레벨 스코프

### const 키워드
- const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다. 그렇지 않으면 다음과 같이 문법 에러가 발생한다.
```js
const foo = 1;
const foo; // SyntaxError
```
- const 키워드로 선언된 변수에 객체를 할당한 경우 값을 변경할 수 있다. 
