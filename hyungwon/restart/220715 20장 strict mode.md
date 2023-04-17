# 20장 strict mode

<br>
<br>
<br>

## 20-1 strict mode란?

<br>

선언되지 않은 변수 `x=10과 같은`에 대해 실행은 할 수 없지만 암묵적으로 전역 객체에 x프로퍼티를 동적 생성하여 전역 변수처럼 사용할 수 있으므로 이를 암묵적 전역이라고 한다. 이것은 여러 문제를 야기할 수 있기 때문에 반드시 선언을 한 후에 할당하도록 하자.

하지만 휴먼 에러는 언제나 발생할 수 있기 때문에, ES6에서 strict mode가 추가되었다. 오류를 발생시킬 가능성이 높거나, Javascript 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 명시적인 에러를 노출시킨다.

---

<br>
<br>
<br>

## 20-2 strict mode의 적용

<br>

strict mode를 적용하려면 우선 스크립트 전역의 선두 또는 함수 몸체의 선두에 'use strict'를 추가한다.
typescript를 javascript로 컴파일하면 나오는 것과 동일하다.(는 내 생각)

---

<br>
<br>
<br>

## 20-3 전역에 strict mode를 적용하는 것은 피하자

<br>

strict mode를 스크립트 단위가 아닌 전역적으로 선언하게 될 경우,
외부 라이브러리 등에서 적용이 안되어 오류를 일으킬 수 있기 때문이다.

---

<br>
<br>
<br>

## 20-4 함수 단위로의 적용도 피하자

<br>

함수 하나하나마다 따로 명시를 해 주어야 하기 때문에 피하자

그냥 React 컴포넌트 하나에 use strict 박고 시작하는 게 제일 나을 것 같다. 아니면 typescript 쓰던가

---

<br>
<br>
<br>

## 20-5 strict mode가 발생시키는 에러

<br>

### 5-1 암묵적 전역

- 선언하지 않은 변수를 참조하면 referenceError가 발생한다.

### 5-2 변수, 함수, 매개변수의 삭제

- delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생한다.

### 5-3 매개변수 이름의 중복

- 중복된 매개변수를 사용하면 SyntaxError가 발생한다.

### 5-4 with문의 사용

- with문을 사용하면 SyntaxError가 발생한다.

---

<br>
<br>
<br>

## 20-6 strict mode 적용에 의한 변화

<br>

### 6-1 일반 함수의 this

- strict mode에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩된다. 일반함수 내부에서는 this를 사용할 수 없기 때문에.

### 6-2 arguments 객체

- strict mode에서는 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다.

---

<br>
<br>
<br>
