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
