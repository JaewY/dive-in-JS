# 37장 Set과 Map

## 37.1 Set

### Set 객체는 중복되지 않는 유일한 값들의 집합이다.

- Set 객체는 배열과 유사하지만 다음과 같은 차이가 있다.

<img width="378" alt="스크린샷 2022-09-10 오후 9 58 02" src="https://user-images.githubusercontent.com/95524491/189484406-0649d37d-350b-492a-8e29-473c6f693fb8.png">

### 37.1.1 Set 객체의 생성

- Set 객체는 Set 생성자 함수로 생성한다.

- Set 생성자 함수에 인수를 전달하지 않으면 빈 Set 객체가 생성된다.

```Js
const set = new Set();
console.log(set); // Set(0) {}
```

- Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성한다.

- 이때 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않는다.

```Js
const set1 = new Set([1, 2, 3, 3]);
console.log(set1); // Set(3) {1, 2, 3}

const set2 = new Set('hello');
console.log(set2); // Set(4) {"h", "e", "l", "o"}

// Set을 사용한 배열의 중복 요소 제거
const uniq = array => [...new Set(array)];
console.log(uniq([2, 1, 2, 3, 4, 3, 4])); // [2, 1, 3, 4]
```

### 37.1.2 요소 개수 확인

- Set 객체의 요소 개수를 확인할 때는 Set.prototype.size 프로퍼티를 사용한다.

```Js
const { size } = new Set([1, 2, 3, 3]);
console.log(size); // 3
```

- size 프로퍼티는 setter 함수 없이 getter 함수만 존재하는 접근자 프로퍼티다.

- 따라서 size 프로퍼티에 숫자를 할당하여 Set 객체의 요소 개수를 변경할 수 없다.

```Js
const set = new Set([1, 2, 3]);

console.log(Object.getOwnPropertyDescriptor(Set.prototype, 'size'));
// {set: undefined, enumerable: false, configurable: true, get: }

set.size = 10; // 무시된다.
console.log(set.size); // 3
```

### 37.1.3 요소 추가

- Set 객체에 요소를 추가할 때는 Set.prototype.add 메서드를 사용한다.

- add 메서드는 새로운 요소가 추가된 Set 객체를 반환한다.

- 따라서 add 메서드를 호출한 후에 add 메서드를 연속적으로 호출method chaining할 수 있다.

- Set 객체에 중복된 요소의 추가는 허용되지 않는다.

- 이때 에러가 발생하지는 않고 무시된다.

- Set 객체는 NaN과 NaN을 같다고 평가하여 중복 추가를 허용하지 않는다

```Js
const set = new Set();
console.log(set); // Set(0) {}

// 연속 호출은 가능, 중복된 요소의 추가는 허용하지 않는다.
set.add(1).add(2).add(3).add(3);
console.log(set); // Set(1,2,3) {}
```

- Set 객체는 객체나 배열과 같이 자바스크립트의 모든 값을 요소로 저장할 수 있다.

```Js
const set = new Set();

set
    .add(1)
    .add('a')
    .add(true)
    .add(undefined)
    .add(null)
    .add({})
    .add([])
    .add(() => {});

console.log(set); // Set(8) {1, "a", true, undefined, null, {}, [], () => {}}
```

### 37.1.4 요소 존재 여부 확인

- Set 객체에 특정 요소가 존재하는지 확인하려면 Set.prototype.has 메서드를 사용한다.

- has 메서드는 특정 요소의 존재 여부를 나타내는 불리언 값을 반환한다.

```Js
const set = new Set([1, 2, 3]);

console.log(set.has(2)); // true
console.log(set.has(4)); // false
```

### 37.1.5 요소 삭제

- Set 객체의 특정 요소를 삭제하려면 Set.prototype.delete 메서드를 사용한다.

- delete 메서드는 삭제 성공 여부를 나타내는 불리언 값을 반환한다.

- delete 메서드에는 인덱스가 아니라 삭제하려는 요소값을 인수로 전달해야 한다.

- Set 객체는 배열과 같이 인덱스를 갖지 않는다.

- 만약 존재하지 않는 Set 객체의 요소를 삭제하려 하면 에러 없이 무시된다.

```Js
const set = new Set([1, 2, 3]);

// 요소 2를 삭제한다.
set.delete(2);
console.log(set); // Set(2) {1, 3}

// 요소 1을 삭제한다.
set.delete(1);
console.log(set); // Set(1) {3}
```

- delete 메서드는 삭제 성공 여부를 나타내는 불리언 값을 반환한다.

- 따라서 Set.prototype.add 메서드와 달리 연속적으로 호출method chaining할 수 없다

```Js
const set = new Set([1, 2, 3])

// delete는 불리언 값을 반환한다.
set.delete(1).delete(2); // TypeError: set.delete(...).delete is not a function
```

### 37.1.6 요소 일괄 삭제

- Set 객체의 모든 요소를 일괄 삭제하려면 Set.prototype.clear 메서드를 사용한다.

- clear 메서드는 언제나 undefined를 반환한다.

```Js
const set = new Set([1, 2, 3]);

set.clear();
console.log(set); // Set(0) {}
```

### 37.1.7 요소 순회

- Set 객체의 요소를 순회하려면 Set.prototype.forEach 메서드를 사용한다.

- 콜백 함수는 다음과 같이 3개의 인수를 전달받는다.

  - 첫 번째 인수: 현재 순회 중인 요소값

  - 두 번째 인수: 현재 순회 중인 요소값

  - 세 번째 인수: 현재 순회 중인 Set 객체 자체

- 첫 번째 인수와 두 번째 인수는 같은 값이다.

- Set 객체는 순서에 의미가 없어 두번째 인수에 배열과 같이 인덱스를 갖지 않는다.

```Js
const set = new Set([1, 2, 3]);

set.forEach((v, v2, set) => console.log(v, v2, set));

/*
1 1 Set(3) {1, 2, 3}
2 2 Set(3) {1, 2, 3}
3 3 Set(3) {1, 2, 3}
*/
```

- Set 객체는 이터러블이다.

- for...of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 될 수도 있다.

### 37.1.8 집합 연산

- Set 객체는 수학적 집합을 구현하기 위한 자료구조다.

- 따라서 Set 객체를 통해 교집합, 합집합, 차집합 등을 구현할 수 있다

## 37.2 Map

### Map 객체는 키와 값의 쌍으로 이루어진 컬렉션이다.

- Map 객체는 객체와 유사하지만 다음과 같은 차이가 있다.

<img width="464" alt="스크린샷 2022-09-10 오후 10 26 06" src="https://user-images.githubusercontent.com/95524491/189485443-59c73ede-8dae-4168-b3f9-c7695008e4b4.png">

### 37.2.1 Map 객체의 생성

- Map 객체는 Map 생성자 함수로 생성한다.

- Map 생성자 함수에 인수를 전달하지 않으면 빈 Map 객체가 생성된다.

```Js
const map = new Map();
console.log(map); // Map(0) {}
```

- Map 생성자 함수는 이터러블을 인수로 전달받아 Map 객체를 생성한다.

- 이때 인수로 전달되는 이터러블은 키와 값의 쌍으로 이루어진 요소로 구성되어야 한다.

```Js
const map1 = new Map([['key1', 'value1'], ['key2', 'value2']]);

console.log(map1); // Map(2) {"key1" => "value1", "key2" => "value2"}

const map2 = new Map([1, 2]); // TypeError: Iterator value 1 is not an entry object
```

- Map 생성자 함수의 인수로 전달한 이터러블에 중복된 키를 갖는 요소가 존재하면 값이 덮어써진다.

- 따라서 Map 객체에는 중복된 키를 갖는 요소가 존재할 수 없다.

```Js
const map = new Map([['key1', 'value1'], ['key1', 'value2']]);

console.log(map); // Map(1) {"key1" => "value2"}
```

### 37.2.2 요소 개수 확인

- Map 객체의 요소 개수를 확인할 때는 Map.prototype.size 프로퍼티를 사용한다.

```Js
const { size } = new Map([['key1', 'value1'], ['key2', 'value2']]);
console.log(size); // 2
```

- size 프로퍼티는 setter 함수 없이 getter 함수만 존재하는 접근자 프로퍼티다.

- 따라서 size 프로퍼티에 숫자를 할당하여 Map 객체의 요소 개수를 변경할 수 없다.

```Js
const map = new Map([['key1', 'value1'], ['key2', 'value2']]);

console.log(Object.getOwnPropertyDescriptor(Map.prototype, 'size'));
// {set: undefined, enumerable: false, configurable: true, get: }

map.size = 10; // 무시된다.
console.log(map.size); // 2
```

### 37.2.3 요소 추가

- Map 객체에 요소를 추가할 때는 Map.prototype.set 메서드를 사용한다.

- set 메서드는 새로운 요소가 추가된 Map 객체를 반환한다.

- 따라서 set 메서드를 호출한 후에 set 메서드를 연속적으로 호출할 수 있다.

- Map 객체에는 중복된 키를 갖는 요소가 존재할 수 없기 때문에 중복된 키를 갖는 요소를 추가하면 값이 덮어써진다.

- 이때 에러가 발생하지는 않는다.

- Map 객체는 NaN과 NaN을 같다고 평가하여 중복 추가를 허용하지 않는다.

```Js
const map = new Map();
console.log(map); // Map(0) {}

map.set('key1', 'value1');
console.log(map); // Map(1) {"key1" => "value1"}
```

- 객체는 문자열 또는 심벌 값만 키로 사용할 수 있다.

- 하지만 Map 객체는 키 타입에 제한이 없다.

- 따라서 객체를 포함한 모든 값을 키로 사용할 수 있다.

- 이는 Map 객체와 일반 객체의 가장 두드러지는 차이점이다.

```Js
const map = new Map();

const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

// 객체도 키로 사용할 수 있다.
map
    .set(lee, 'developer')
    .set(kim, 'designer');

console.log(map);
// Map(2) { {name: "Lee"} => "developer", {name: "Kim"} => "designer" }
```

### 37.2.4 요소 취득

- Map 객체에서 특정 요소를 취득하려면 Map.prototype.get 메서드를 사용한다.

- get 메서드의 인수로 키를 전달하면 Map 객체에서 인수로 전달한 키를 갖는 값을 반환한다.

- Map 객체에서 인수로 전달한 키를 갖는 요소가 존재하지 않으면 undefined를 반환한다.

```Js
const map = new Map();

const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

map
    .set(lee, 'developer')
    .set(kim, 'designer');

console.log(map.get(lee)); // developer
console.log(map.get('key')); // undefined
```

### 37.2.5 요소 존재 여부 확인

- Map 객체에 특정 요소가 존재하는지 확인하려면 Map.prototype.has 메서드를 사용한다.

- has 메서드는 특정 요소의 존재 여부를 나타내는 불리언 값을 반환한다.

```Js
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

console.log(map.has(lee)); // true
console.log(map.has('key')); // false
```

### 37.2.6 요소 삭제

- Map 객체의 요소를 삭제하려면 Map.prototype.delete 메서드를 사용한다.

- delete 메서드는 삭제 성공 여부를 나타내는 불리언 값을 반환한다.

- 만약 존재하지 않는 키로 Map 객체의 요소를 삭제하려 하면 에러 없이 무시된다.

```Js
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

map.delete(kim);
console.log(map); // Map(1) { {name: "Lee"} => "developer" }
```

- delete 메서드는 삭제 성공 여부를 나타내는 불리언 값을 반환한다.

- 따라서 set 메서드와 달리 연속적으로 호출할 수 없다.

```Js
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

map.delete(lee).delete(kim); // TypeError: map.delete(...).delete is not a function
```

### 37.2.7 요소 일괄 삭제

- Map 객체의 요소를 일괄 삭제하려면 Map.prototype.clear 메서드를 사용한다.

- clear 메서드는 언제나 undefined를 반환한다.

```Js
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);
map.clear();
console.log(map); // Map(0) {}
```

### 37.2.7 요소 순회

- Map 객체의 요소를 순회하려면 Map.prototype.forEach 메서드를 사용한다

- 콜백 함수는 다음과 같이 3개의 인수를 전달받는다.

  - 첫 번째 인수: 현재 순회 중인 요소값

  - 두 번째 인수: 현재 순회 중인 요소키

  - 세 번째 인수: 현재 순회 중인 Map 객체 자체

```Js
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

map.forEach((v, k, map) => console.log(v, k, map));

/*
developer {name: "Lee"} Map(2) {
    {name: "Lee"} => "developer",
    {name: "Kim"} => "designer"
}
designer {name: "Kim"} Map(2) {
    {name: "Lee"} => "developer",
    {name: "Kim"} => "designer"}
*/
```

- Map 객체는 이터러블이다.

- 따라서 for...of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링 할당의 대상이 될 수도 있다.

- Map 객체는 이터러블이면서 동시에 이터레이터인 객체를 반환하는 메서드를 제공한다.

<img width="546" alt="스크린샷 2022-09-10 오후 10 48 26" src="https://user-images.githubusercontent.com/95524491/189486332-2c687479-1063-4c51-ad1d-e2a91a2064c5.png">
