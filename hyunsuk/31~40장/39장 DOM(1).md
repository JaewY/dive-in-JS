# 39장 DOM (1)

## DOM(Document Object Model)은 HTML 문서의 계층적 구조와 정보를 표현하며 이를 제어할 수 있는 API, 즉 프로퍼티와 메서드를 제공하는 트리 자료구조다.

<hr>

## 39.1 노드

### 39.1.1 HTML 요소와 노드 객체

- HTML요소는 HTML 문서를 구성하는 개별적인 요소를 의미한다.

<img width="531" alt="스크린샷 2022-07-26 오후 11 39 36" src="https://user-images.githubusercontent.com/95524491/181035756-8e3595a5-114e-4ffb-9727-b372c242a33d.png">

- HTML 요소는 렌더링 엔진에 의해 파싱되어 DOM을 구성하는 요소 노드 객체로 변환된다

- HTML 요소의 어트리뷰트는 어트리뷰트 노드로, HTML 요소의 텍스트 콘텐츠는 텍스트 노드로 변환된다.

- HTML 요소 간에는 중첩 관계에 의해 계층적인 부자관계가 형성된다.

- 이러한 HTML 요소 간의 부자 관계를 반영하여 HTML 문서의 구성 요소인 HTML 요소를 객체화한 모든 노드 객체들을 트리 자료구조로 구성한다

<img width="370" alt="스크린샷 2022-07-26 오후 11 41 30" src="https://user-images.githubusercontent.com/95524491/181036240-43b0bfb8-adcc-4b4a-9f7e-15e07f309c3d.png">

### 트리 자료 구조

#### 트리 자료구조는 노드들의 계층 구조로 이뤄진다

- 트리 자료구조는 부모 노드와 자식 노드로 구성되어 노드 간의 계층적 구조(부자, 형제 관계)를 표현하는 비선형 자료구조를 말한다

- 최상위 노드는 부모 노드가 없으며, 루트 노드root node라 한다. 루트 노드는 0개이상의 자식 노드를 갖는다.

- 자식 노드가 없는 노드를 리프 노드라 한다

- 노드 객체들로 구성된 트리 자료구조를 DOM이라 한다

- DOM을 DOM 트리라고 부르기도 한다.

<img width="231" alt="스크린샷 2022-07-26 오후 11 44 54" src="https://user-images.githubusercontent.com/95524491/181037093-abd2eca5-b5c0-422e-b2c8-6cbe47d7b759.png">

### 39.1.2 노드 객체의 타입

```HTML
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <ul>
            <li id="apple">Apple</li>
            <li id="banana">Banana</li>
            <li id="orange">Orange</li>
        </ul>
        <script src="app.js"></script>
    </body>
    </html>
```

<img width="565" alt="스크린샷 2022-07-26 오후 11 51 48" src="https://user-images.githubusercontent.com/95524491/181038641-958dd796-b8e2-4964-a599-8ebbdd03b7db.png">

- 노드 객체는 종류가 있고 상속 구조를 갖는다.

- 노드 객체는 총 12개의 종류(노드 타입)가 있다.

- 주석을 위한 Comment 노드, DOCTYPE을 위한 DocumentType 노드, 복수의 노드를 생성하여 추가할 때 사용하는 DocumentFragment 노드 등 총 12개의 노드 타입이 있다

- 이 중에서 중요한 노드 타입은 다음과 같이 4가지다.

1. 문서 노드

- 문서 노드는 DOM 트리의 최상위에 존재하는 루트 노드로서 document 객체를 가리킨다

- 요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다

2. 요소 노드

- 요소 노드는 HTML 요소를 가리키는 객체다

3. 어트리뷰트 노드

- 어트리뷰트 노드는 HTML 요소의 어트리뷰트를 가리키는 객체다

- 어트리뷰트 노드에 접근하여 어트리뷰트를 참조하거나 변경하려면 먼저 요소 노드에 접근해야 한다.

4. 텍스트 노드

- 텍스트 노드는 HTML 요소의 텍스트를 가리키는 객체다

- 텍스트 노드에 접근하려면 먼저 부모 노드인 요소 노드에 접근해야 한다.

### 39.1.3 노드 객체의 상속 구조

- DOM을 구성하는 노드 객체는 자신의 구조와 정보를 제어할 수 있는 DOM API를 사용할 수 있다.

- 이를 통해 노드 객체는 자신의 부모, 형제, 자식을 탐색할 수 있으며, 자신의 어트리뷰트와 텍스트를 조작할 수도 있다

- DOM은 HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류, 즉 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API로 제공한다.

- 이 DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작할 수 있다.

<img width="564" alt="스크린샷 2022-07-27 오전 12 01 17" src="https://user-images.githubusercontent.com/95524491/181040850-d95d4b2e-a106-4e18-951f-763c81d27866.png">

<img width="283" alt="스크린샷 2022-07-27 오전 12 01 29" src="https://user-images.githubusercontent.com/95524491/181040903-775af12d-6765-4201-ae5c-5c337ead069f.png">

<img width="561" alt="스크린샷 2022-07-27 오전 12 03 03" src="https://user-images.githubusercontent.com/95524491/181041283-3489516d-f05e-4143-88de-247722052184.png">

<hr>

## 39.2 요소 노드 취득

### 39.2.1 id를 이용한 요소 노드 취득

- Document.prototype.getElementById 메서드는 인수로 전달한 id 어트리뷰트 값(id값)을 갖는 하나의 요소 노드를 탐색하여 반환한다.

- id 값은 HTML 문서 내에서 유일한 값이어야 한다.

- HTML 문서 내에는 중복된 id 값을 갖는 요소가 여러 개 존재하는 경우 getElementById 메서드는 인수로 전달된 id 값을 갖는 첫 번째 요소 노드만 반환한다

- 인수로 전달된 id 값을 갖는 HTML 요소가 존재하지 않는 경우 getElementById 메서드는 null을 반환한다

- HTML 요소에 id 어트리뷰트를 부여하면 id 값과 동일한 이름의 전역 변수가 암묵적으로 선언되고 해당 노드 객체가 할당되는 부수 효과가 있다.

- id 값과 동일한 이름의 전역 변수가 이미 선언되어 있으면 이 전역 변수에 노드 객체가 재할당되지 않는다

### 39.2.2 태그 이름을 이용한 요소 노드 취득

- Document.prototype/Element.prototype.getElementsByTagName 메서드는 인수로 전달한 태그 이름을 갖는 모든 요소 노드들을 탐색하여 반환한다.

- 여러 개의 요소 노드 객체를 갖는 DOM 컬렉션 객체인 HTMLCollection 객체를 반환한다.

- HTMLCollection 객체는 유사 배열 객체이면서 이터러블이다

- HTML 문서의 모든 요소 노드를 취득하려면 getElementsByTagName 메서드의 인수로 \*를 전달한다

- 인수로 전달된 태그 이름을 갖는 요소가 존재하지 않는 경우 getElementsByTagName 메서드는 빈 HTMLCollection 객체를 반환한다.

### 39.2.3 class를 이용한 요소 노드 취득

- Document.prototype/Element.prototype.getElementsByClassName 메서드는 인수로 전달한 class 어트리뷰트 값(class 값)을 갖는 모든 요소 노드들을 탐색하여 반환한다.

- 여러 개의 class를 지정할 수 있다.

- HTMLCollection 객체를 반환

- 인수로 전달된 class 값을 갖는 요소가 존재하지 않는 경우 getElementsByClassName 메서드는 빈 HTMLCollection 객체를 반환한다.

### 39.2.4 CSS 선택자를 이용한 요소 노드 취득

- CSS 선택자는 스타일을 적용하고자 하는 HTML 요소를 특정할 때 사용하는 문법이다

```CSS
/* 전체 선택자: 모든 요소를 선택 */
* { ... }
/* 태그 선택자: 모든 p 태그 요소를 모두 선택 */
p { ... }
/* id 선택자: id 값이 'foo'인 요소를 모두 선택 */
#foo { ... }
/* class 선택자: class 값이 'foo'인 요소를 모두 선택 */
.foo { ... }
/* 어트리뷰트 선택자: input 요소 중에 type 어트리뷰트 값이 'text'인 요소를 모두 선택 */
input[type=text] { ... }
/* 후손 선택자: div 요소의 후손 요소 중 p 요소를 모두 선택 */
div p { ... }
/* 자식 선택자: div 요소의 자식 요소 중 p 요소를 모두 선택 */
div > p { ... }
/* 인접 형제 선택자: p 요소의 형제 요소 중에 p 요소 바로 뒤에 위치하는 ul 요소를 선택 */
p + ul { ... }
/* 일반 형제 선택자: p 요소의 형제 요소 중에 p 요소 뒤에 위치하는 ul 요소를 모두 선택 */
p ~ ul { ... }
/* 가상 클래스 선택자: hover 상태인 a 요소를 모두 선택 */
a:hover { ... }/* 가상 요소 선택자: p 요소의 콘텐츠의 앞에 위치하는 공간을 선택   일반적으로 content 프로퍼티와 함께 사용된다. */
p::before { ... }
```

#### Document.prototype/Element.prototype.querySelector 메서드는 인수로 전달한 CSS 선택자를 만족시키는 하나의 요소 노드를 탐색하여 반환한다.

- 인수로 전달한 CSS 선택자를 만족시키는 요소 노드가 여러 개인 경우 첫 번째 요소 노드만 반환한다.
- 인수로 전달된 CSS 선택자를 만족시키는 요소 노드가 존재하지 않는 경우 null을 반환한다.
- 인수로 전달한 CSS 선택자가 문법에 맞지 않는 경우 DOMException 에러가 발생한다.

#### Document.prototype/Element.prototype.querySelectorAll 메서드는 인수로 전달한 CSS 선택자를 만족시키는 모든 요소 노드를 탐색하여 반환한다

- NodeList 객체를 반환한다

- NodeList 객체는 유사 배열 객체이면서 이터러블이다.

- 인수로 전달된 CSS 선택자를 만족시키는 요소가 존재하지 않는 경우 빈 NodeList 객체를 반환한다.

- 인수로 전달한 CSS 선택자가 문법에 맞지 않는 경우 DOMException 에러가 발생한다.

- HTML 문서의 모든 요소 노드를 취득하려면 querySelectorAll 메서드의 인수로 전체 선택자 '\*'를 전달한다.

### 39.2.5 특정 요소 노드를 취득할 수 있는지 확인

- Element.prototype.matches 메서드는 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인한다.

### 39.2.6 HTMLCollection과 NodeList

- DOM 컬렉션 객체인 HTMLCollection과 NodeList는 DOM API가 여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체다

- HTMLCollection과 NodeList는 모두 유사 배열 객체이면서 이터러블이다.

- for...of 문으로 순회할 수 있으며 스프레드 문법을 사용하여 간단히 배열로 변환할 수 있다

### HTMLCollection

- getElementsByTagName, getElementsByClassName 메서드가 반환하는 HTMLCollection 객체는 노드 객체의 상태 변화를 실시간으로 반영하는 살아 있는 DOM컬렉션 객체(살아있는 객체)다

- 유사 배열 객체이면서 이터러블인 HTMLCollection 객체를 배열로 변환하면 부작용을 발생시키는 HTMLCollection 객체를 사용할 필요가 없고 유용한 배열의 고차 함수(forEach, map, filter, reduce 등)를 사용할 수 있다.

```Js
// 유사 배열 객체이면서 이터러블인 HTMLCollection을 배열로 변환하여 순회
// $elems = [HTMLCollection]
[...$elems].forEach(elem => elem.className = 'blue');
```

### NodeList

- querySelectorAll 메서드는 DOM 컬렉션 객체인 NodeList 객체를 반환한다.

- 이때 NodeList 객체는 실시간으로 노드 객체의 상태 변경을 반영하지 않는 객체다

- NodeList 객체는 NodeList.prototype.forEach 메서드를 상속받아 사용할 수 있다.

- childNodes 프로퍼티가 반환하는 NodeList 객체는 HTMLCollection 객체와 같이 실시간으로 노드 객체의 상태 변경을 반영하는 live 객체로 동작하므로 주의가 필요하다.

- 노드 객체의 상태 변경과 상관없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하는 것을 권장한다

- 스프레드 문법이나 Array.from 메서드를 사용하여 간단히 배열로 변환할 수 있다.
