# 22장 this

## 22.1 this 키워드

### this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수다. 
### this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메서드를 참조할 수 있다.
### this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 의해 동적으로 결정된다


- 객체는 프로퍼티와(상태를 나타냄) 메소드(동작을 나타냄)으로 구성되어 있다.
- 메서드는 자신이 속한 객체의 포로퍼티를 참조하고 변경할 수 있어야 한다. 
- 메서드가 자신이 속한 객체의 프로퍼티를 참조하려면 먼저 자신이 속한 객체의 식별자를 참조할 수 있어야 한다.

- 객체 리터럴의 메서드 내부에서의 this는 메서드를 호출한 객체, 즉 circle을 가리킨다.
```Js
const circle = {
  radius : 5;
  getDiameter(){
    return 2 * this.radius;
  }
};

console.log(circle.getDiameter) // 10
```

- 생성자 함수 내부의 this는 생성자 함수가 생성할 인스턴스를 가리킨다

```Js
function Circle(radius){
  // this는 생성자 함수가 생성할 인스턴스를 가리킨다
  radius : this.radius;
};

Circle.prototype.getDiameter = function(){
  // this는 생성자 함수가 생성할 인스턴스를 가리킨다
  return 2 * this.radius;
}

// 인스턴스 생성 
const circle = new Circle(5);
console.log(circle.getDiameter()); // 10

```

## 22.2 함수 호출 방식과 this 바인딩

### this 바인딩은 함수 호출 방식 , 즉 함수가 어떻게 호출되었는지에 따라 동적으로 결정된다. 

- 참고 : 렉시컬 스코프는 생성 되는 시점에 상위 스코프가 결정됨
#### 함수 호출 방식은 4가지가 있다.
1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. Function.prototype.apply/call/bind 메서드에 의한 간접 호출

### 22.2.1 일반 함수 호출

#### 기본적으로 this에는 전역 객체가 바인딩된다. 
#### 일반 함수로 호출하면 함수 내부의 this에는 전역객체가 바인딩된다.
#### strict mode를 사용하면 this에는 undefined가 바인딩된다.

```Js
function foo() {
  console.log(this); // window
  function bar() {
    console.log(this); // window
  }
  bar();
}
foo();
```

- 외부 함수인 메서드와 중첩 함수 또는 콜백 함수의 this가 일치하지 않는다는 것은 중첩 함수 또는 콜백 함수를 헬퍼 함수로 동작하기 어렵게 만든다

```Js
var value = 1;

const obj = {
  value: 100,
  foo() {
    // 메서드의 this는 해당 객체를 참조
    console.log(this) // { value : 100 , foo : f }
    console.log(this.value) // 100
    // 콜백 , 중첩함수, 일반함수 등 어떤 함수라도 내부의 this는 전역 객체가 바인딩
    setTimeout(function() {
      console.log(this); // window
      console.log(this.value); // 1
     }, 100);
   }
 };
 
 obj.foo();

```

- 매서드 내부의 중첩 함수나 콜백 함수의 this를 메서드의 this를 일치시키는 방법
1. this 바인딩을 변수로 만들어서 할당시키기
```Js
var value = 1;

const obj = {
  value: 100,
  foo() {
    // this 바인딩(obj)을 변수 that에 할당한다.
    const that = this;
    
    // 콜백 함수 내부에서 this 대신 that을 참조한다.
    setTimeout(function() {
      console.log(that.value); // 100
     }, 100);
   }
 };
 
 obj.foo();

```
2. call/apply/bind 메서드 사용
3. 화살표 함수 사용 (화살표 함수 내부의 this는 상위 스코프의 this를 가리킨다)

```Js
var value = 1;

const obj = {
  value : 100,
  foo() {
    setTimeout(()=> console.log(this.value),1000);  // 100 전역인 1을 참조하지 않는다.
  }
};

obj.foo();

```

### 22.2.2 메서드 호출

#### 메서드를 호출할 때 메서드 이름 앞의 마침표 연산자 앞에 기술한 객체가 바인딩된다.
#### 주의할것은 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다는 것이다.

- person 객체의 getName 프로퍼티가 가리키는 함수 객체는 person 객체에 포함된 것이 아니라 독립적으로 존재하는 별도의 객체다

```Js
const person = {
  name: 'Lee',
  getName() {
    // 메서드 내부의 this는 메서드를 호출한 객체에 바인딩된다.
    return this.name;
   }
  };

// 메서드 getName을 호출한 객체는 person이다.
console.log(person.getName()); // Lee
```
![스크린샷 2022-07-17 오후 4 37 23](https://user-images.githubusercontent.com/95524491/179388757-9a925c56-b74b-40d8-98db-69f2ae0fbb81.png)

- 메서드는 다른 객체의 프로퍼티에 할당하여 다른 객체의 메서드가 될 수도 있고 일반 변수에 할당하여 일반 함수로 호출될 수도 있다.
```Js
const anotherPerson = { 
  name: 'Kim'
};
// getName 메서드를 anotherPerson 객체의 메서드로 할당
anotherPerson.getName = person.getName;

// getName 메서드를 호출한 객체는 anotherPerson이다.
console.log(anotherPerson.getName()); // Kim

// getName 메서드를 변수에 할당
const getName = person.getName;

// getName 메서드를 일반 함수로 호출
console.log(getName()); // ''
// 일반 함수로 호출된 getName 함수 내부의 this.name은 브라우저 환경에서 window.name과 같다.
// 브라우저 환경에서 window.name은 브라우저 창의 이름을 나타내는 빌트인 프로퍼티이며 기본값은 '' 이다
```
![스크린샷 2022-07-17 오후 4 40 48](https://user-images.githubusercontent.com/95524491/179388861-e219a2eb-83e4-4c0f-96d0-4a79e02cef3c.png)

- 프로토타입 메서드 내부에서 사용된 this도 일반 메서드와 마찬가지로 해당 메서드를 호출한 객체에 바인딩된다.

![스크린샷 2022-07-17 오후 4 41 50](https://user-images.githubusercontent.com/95524491/179388884-e36e4cdf-dd15-48e3-a2f0-8429066a0a4c.png)

### 22.2.3 생성자 함수 호출

#### 생성자 함수 내부의 this에는 생성자 함수가 (미래에)생성할 인스턴스가 바인딩된다.

### 22.2.4 Function.prototype.apply/call/bind 메서드에 의한 간접 호출

- apply, call, bind 메서드는 Function.prototype의 메서드다.
- apply와 call 메서드의 본질적인 기능은 함수를 호출하는 것이다.
- apply와 call은 함수를 호출하면서 첫 번째 인수로 전달한 특정 객체를 호출한 함수의 this에 바인딩한다.
- 둘은 호출할 함수에 인수를 전당하는 방식만 다를 뿐 동일하게 동작한다.
- apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달한다. 
- call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달한다. 
- 이처럼 apply와 call 메서드는 호출할 함수에 인수를 전달하는 방식만 다를 뿐 this로 사용할 객체를 전달하면서 함수를 호출하는 것은 동일하다.
- arguments 객체는 배열이 아니기 때문에 Array.prototype.slice 같은 배열의 메서드를 사용할 수 없으나 apply와 call 메서드를 이용하면 가능하다.
```Js
function getThisBinding() { 
  console.log(arguments); 
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

// getThisBinding 함수를 호출하면서 인수로 전달한 객체를 getThisBinding 함수의 this에 바인딩한다.
// apply 메서드는 호출할 함수의 인수를 배열로 묶어 전달한다.
console.log(getThisBinding.apply(thisArg, [1, 2, 3]));
// Arguments(3) [1, 2, 3, callee: , Symbol(Symbol.iterator): ]
// {a: 1}

// call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달한다.
console.log(getThisBinding.call(thisArg, 1, 2, 3));
// Arguments(3) [1, 2, 3, callee: , Symbol(Symbol.iterator): ]
// {a: 1}
```

- bind 메서드는 함수를 호출하지 않는다. 다만 첫 번째 인수로 전달한 값으로 this 바인딩이 교체된 함수를 새롭게 생성해 반환한다.

```Js
function getThisBinding() {  
  return this;
}

// this로 사용할 객체
const thisArg = { a: 1 };

// bind 메서드는 첫 번째 인수로 전달한 thisArg로 this 바인딩이 교체된
// getThisBinding 함수를 새롭게 생성해 반환한다.
console.log(getThisBinding.bind(thisArg)); // getThisBinding
// bind 메서드는 함수를 호출하지는 않으므로 명시적으로 호출해야 한다.
console.log(getThisBinding.bind(thisArg)()); // {a: 1}
```

- bind 메서드는 메서드의 this와 메서드 내부의 중첩 함수 또는 콜백 함수의 this가 불일치하는 문제를 해결하기 위해 유용하게 사용된다

```Js
const person = {  
  name: 'Lee', 
  foo(callback) {  
  // bind 메서드로 callback 함수 내부의 this 바인딩을 전달   
  setTimeout(callback.bind(this), 100);  
  }
};

person.foo(function () { 
  console.log(Hi! my name is ${this.name}.); // Hi! my name is Lee.
});
```

### 정리

![스크린샷 2022-07-17 오후 5 03 15](https://user-images.githubusercontent.com/95524491/179389516-69640b41-7991-4f91-9dfe-04598ccafd5f.png)
