# 1. 내부 슬롯과 내부 Method

<br>
내부 슬롯과 내부 메서드는 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티와 의사 메서드이다. 이중 대괄호 [[...]]로 감싼 이름들이 내부 슬롯과 메서드이다.

<br>
내부 슬롯은 자바스크립트 내부 로직이므로 직접접근할 수 없지만, <br>
일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공하기도 한다.

```
const o = {}
o.[[property]] // 접근 불가
o.__proto__ // 접근 가능
```

<br><br>

# 2. property attribute와 property descriptor 객체

<br>


자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.

<br>

##### 예제 16-3를 확인해 보자

<br><br>

# 3. 데이터 프로퍼티와 접근자 프로퍼티

<br>
데이터 프로퍼티는 키와 값으로 구성된 일반적인 프로퍼티이다. 지금까지 써본 적 있는 모든 프로퍼티가 여기에 해당.

<br>
접근자 프로퍼티는 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티이다.

<br>
<br>

## 3-1 데이터 프로퍼티
---

|프로퍼티<br> 어트리뷰트|프로퍼티 디스크립터 객체의 프로퍼티|설명|
|:-|:-|:-|
|[[Value]]|value|1. 프로퍼티 키를 통해 프로퍼티에 접근하면 반환되는 값이다. <br>2. 프로퍼티 키를 통해 값을 변경하면 [[Value]]에 값을 재할당한다. 이때 프로퍼티가 없으면 프로퍼티를 동적 생성하고 생성된 프로퍼티의 [[Value]]에 값을 저장한다.|
|[[Writable]]|writable|1. 프로퍼티 값의 변경 가능 여부를 나타내며 불리언 값을 갖는다. <br> 2. [[Writable]]값이 false인 경우 해당 프로퍼티의 [[Value]]의 값을 변경할 수 없는 읽기 전용 프로퍼티가 된다.|
|[[Enumerable]]|enumerable|1. 프로퍼티의 열거 가능 여부를 나타내며 불리언 값을 갖는다. <br> 2. [[Enumerable]]의 값이 false인 경우 해당 프로퍼티는 for...in문이나 Object.keys 등의 메서드 등으로 열거할 수 없다.|
|[[Configurable]]|configurable|1. 프로퍼티의 재정의 가능 여부를 나타내며 불리언 값을 갖는다. <br> 2. [[Configurable]]값이 false인 경우 해당 프로퍼티는 삭제, 프로퍼티 어트리뷰트의 값의 변경이 금지된다. 단, [[Writable]]이 true인 경우 [[Value]]의 변경과 [[Writable]]을 false로 변경하는 것은 허용된다.|

<br><br>

```
const person = {
    name: "lee"
}

console.log(Object.getOwnPropertyDescriptor(person, "name"))
=> {value: "lee", writable: true, enumerable: true, configurable: true}
```
<br><br>
동적으로 생성한 값 또한 이와 동일하게 나타난다.

```
const person = {
    name: "lee"
}
person.age = 20

console.log(Object.getOwnPropertyDescriptor(person))

=> {value: "lee", writable: true, enumerable: true, configurable: true},
{value: 20, writable: true, enumerable: true, configurable: true}
```
<br>

## 3-2 접근자 프로퍼티

<br>

|프로퍼티 어트리뷰트|프로퍼티 디스크립터 객체의 프로퍼티|설명|
|:-|:-|:-|
|[[Get]]|get|접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 읽을 때 호출되는 접근자 함수다. <br>즉, 접근자 프로퍼티 키로 프로퍼티 값에 접근하면 프로퍼티 어트리뷰트 [[Get]]의 값, 즉 getter함수가 호출되고 그 결과가 프로퍼티 값으로 반환된다.|
|[[Set]]|set|접근자 프로퍼티를 통해서 프로퍼티 값을 저장할 때 호출되는 접근자 함수다. <br>즉, 접근자 프로퍼티 키로 프로퍼티 값을 저장하면 프로퍼티 어트리뷰트 [[Set]]의 값 즉, setter함수가 호출되고 그 결과가 프로퍼티 값으로 저장된다.|
|[[Enumerable]]|enumerable|데이터 프로퍼티의 [[Enumerable]]과 같다.|
|[Configurable]]|configurable|데이터 프로퍼티의 [[Configurable]]과 같다.|

<br><br><br>

```
const person = {
    name: "lee",
    age: "20"
}

get personData() {
    return `${this.name}씨는 ${this.age}살입니다.`
}

set personData(user){
    [this.name, this.age] = user.split(' ')
}
```
<br>

person 객체의 name과 age 프로퍼티는 일반적인 데이터 프로퍼티다. 메서드 앞에 get,set이 붙은 메서드가 있는데,<br>  getter, setter 함수이고 getter, setter 함수 이름 personData가 접근자 프로퍼티이다.
<br><br>

||
|:-|
|1. 프로퍼티 키가 유효한지 확인한다. 프로퍼티 키는 문자열 또는 심벌이어야 한다. 프로퍼티 키 <u>"personData"는 문자열이므로</u> 유효한 프로퍼티 키다.|
|2. 프로토타입 체인에서 프로퍼티를 검색한다. person 객체에 personData 프로퍼티가 존재한다.|
|3. 검색된 personData 프로퍼티가 데이터 프로퍼티인지 접근자 프로퍼티인지 확인한다. personData는 접근자 프로퍼티이다.|
|4. 접근자 프로퍼티 personData의 프로퍼티 어트리뷰트 [[Get]]의 값, 즉 getter함수를 호출하여 그 결과를 반환한다. 프로퍼티 personData의 프로퍼티 어트리뷰트 [[Get]]의 값은 Object.getOwnPropertyDesciptor 메서드가 반환하는 프로퍼티 디스크립터 객체의 get 프로퍼티 값과 같다.|

<br><br><br><br>

|프로토타입|
|-|
|1. 프로토타입은 어떤 객체의 상위(부모) 객체의 역할을 하는 객체이다. 프로토타입은 하위(자식) 객체에게 자신의 프로퍼티와 메서드를 상속한다. 프로토타입 객체의 프로퍼티나 베서드를 상속받은 하위 객체는 자신의 프로퍼티 또는 메서드인 것처럼 자유롭게 사용할 수 있다.<br><br>2. 프로토타입 체인은 프로토타입이 단방향 링크드 리스트 형태로 연결되어 있는 상속 구조를 말한다. 객체의 프로퍼티나 메서드에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티 또는 메서드가 없다면 프로토타입 체인을 따라 프로토타입의 프로퍼티나 메서드를 차례대로 검색한다. 프로토타입 체인에 대해서는 19장 프로토타입에서 자세히 살펴보도록 하자.|
||


|접근자 프로퍼티와 데이터 프로퍼티를 구별하는 방법|
|-|
| 일반 객체의 __proto__는 접근자 프로퍼티다.
```
console.log(Object.getOwnPropertyDescriptor(Objdct.prototype, '__proto__'))
=> {get:f, set:f, enumerable: false, configuable: true}
```
함수 객체의 prototype은 데이터 프로퍼티이다.
```
console.log(Object.getOwnPropertyDescriptor(function(){}, 'prototype'))
=> {value:{...}, writable: true, enumerable: false, configuable: false}
```


















|a|b|c|
|:-|:-:|-:|
|aaseatjejdf|bafsaejejtjb|hhtaetjajtc|


