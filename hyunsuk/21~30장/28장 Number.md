# 28장 Number

## 28.1 Number 생성자 함수

- 표준 빌트인 객체인 Number 객체는 생성자 함수 객체다.

- 따라서 new 연산자와 함께 호출하여 Number 인스턴스를 생성할 수 있다.

- Number 생성자 함수에 인수를 전달하지 않고 new 연산자와 함께 호출하면 [[NumberData]] 내부 슬롯에 0을 할당한 Number 래퍼 객체를 생성한다.

- Number 생성자 함수의 인수로 숫자가 아닌 값을 전달하면 인수를 숫자로 강제 변환한 후, [[NumberData]] 내부 슬롯에 변환된 숫자를 할당한 Number 래퍼 객체를 생성한다.

- 인수를 숫자로 변환할 수 없다면 NaN을 [[NumberData]] 내부 슬롯에 할당한 Number 래퍼 객체를 생성한다

```Js
const numObj = new Number();
console.log(numObj); // Number {[[PrimitiveValue]]: 0}

const numObj2 = new Number(10);
console.log(numObj2); // Number {[[PrimitiveValue]]: 10}


let numObj3 = new Number('10');
console.log(numObj3); // Number {[[PrimitiveValue]]: 10}
numObj3 = new Number('Hello');
console.log(numObj3); // Number {[[PrimitiveValue]]: NaN}
```

- new 연산자를 사용하지 않고 Number 생성자 함수를 호출하면 Number 인스턴스가 아닌 숫자를 반환한다

```Js
// 문자열 타입 => 숫자 타입
Number('0');		//  0
Number('-1');		//  -1
Number('10.53');	//  10.53

// 불리언 타입 => 숫자 타입
Number(true);	//  1
Number(false);	//  0
```

## 28.2 Number 프로퍼티

### 28.2.1 Number.EPSILON

- 1과 1보다 큰 숫자 중에서 가장 작은 숫자와의 차이와 같다

- Number.EPSILON은 부동소수점으로 인해 발생하는 오차를 해결하기 위해 사용한다

### 28.2.2 Number.MAX_VALUE

- Number.MAX_VALUE는 자바스크립트에서 표현할 수 있는 가장 큰 양수 값이다.

- Number.MAX_VALUE보다 큰 숫자는 Infinity다.

### 28.2.3 Number.MIN_VALUE

- Number.MIN_VALUE는 자바스크립트에서 표현할 수 있는 가장 작은 양수 값(5 10-324)이다.

- Number.MIN_VALUE보다 작은 숫자는 0이다.

### 28.2.4 Number.MAX_SAFE_INTEGER

- Number.MAX_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 큰 정수값(9007199254740991)이다.

### 28.2.5 Number.MIN_SAFE_INTEGER

- Number.MIN_SAFE_INTEGER는 자바스크립트에서 안전하게 표현할 수 있는 가장 작은 정수값(-9007199254740991)이다.

### 28.2.6 Number.POSITIVE_INFINITY

- Number.POSITIVE_INFINITY는 양의 무한대를 나타내는 숫자값 Infinity와 같다.

### 28.2.7 Number.NEGATIVE_INFINITY

- Number.NEGATIVE_INFINITY는 음의 무한대를 나타내는 숫자값 -Infinity와 같다.

### 28.2.8 Number.NaN

- Number.NaN은 숫자가 아님(Not-a-Number)을 나타내는 숫자값이다.

- Number.NaN은 window.NaN과 같다.

## 28.3 Number 메서드

### 28.3.1 Number.isFinite

- Infinity 또는 -Infinity가 아닌지 검사하여 그 결과를 불리언 값으로 반환한다.

- 만약 인수가 NaN이면 언제나 false를 반환한다.

- Number.isFinite는 전달받은 인수를 숫자로 암묵적 타입 변환하지 않는다.

```Js
// 인수가 정상적인 유한수이면 true를 반환한다.
Number.isFinite(0);	//  true
Number.isFinite(Number.MAX_VALUE);	//  true
Number.isFinite(Number.MIN_VALUE);	//  true

// 인수가 무한수이면 false를 반환한다.
Number.isFinite(Infinity);  //  false
Number.isFinite(-Infinity); //  false

Number.isFinite(NaN); //  false

// Number.isFinite는 인수를 숫자로 암묵적 타입 변환하지 않는다.
Number.isFinite(null); //  false

// isFinite는 인수를 숫자로 암묵적 타입 변환한다. null은 0으로 암묵적 타입 변환된다.
isFinite(null); //  true
```

### 28.3.2 Number.isInteger

- 인수로 전달된 숫자값이 정수인지 검사하여 그 결과를 불리언 값으로 반환한다.

- 검사하기 전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

```Js
// 인수가 정수이면 true를 반환한다.
Number.isInteger(0)	//  true
Number.isInteger(123)	//  true
Number.isInteger(-123)	//  true

// 0.5는 정수가 아니다.
Number.isInteger(0.5)	//  false
// '123'을 숫자로 암묵적 타입 변환하지 않는다.
Number.isInteger('123')	//  false
// false를 숫자로 암묵적 타입 변환하지 않는다.
Number.isInteger(false)	//  false
// Infinity/-Infinity는 정수가 아니다.
Number.isInteger(Infinity)  //  false
Number.isInteger(-Infinity) //  false
```

### 28.3.3 Number.isNaN

- 인수로 전달된 숫자값이 NaN인지 검사하여 그 결과를 불리언 값으로 반환한다.

- 전달받은 인수를 숫자로 암묵적 타입 변환하지 않는다.

```Js
// 인수가 NaN이면 true를 반환한다.
Number.isNaN(NaN); //  true

// Number.isNaN은 인수를 숫자로 암묵적 타입 변환하지 않는다.
Number.isNaN(undefined); //  false
```

### 28.3.4 Number.isSafeInteger

- 인수로 전달된 숫자값이 안전한 정수인지 검사하여 그 결과를 불리언 값으로 반환한다.

- 검사전에 인수를 숫자로 암묵적 타입 변환하지 않는다.

### 28.3.5 Number.prototype.toExponential

- 숫자를 지수 표기법으로 변환하여 문자열로 반환한다.

- 숫자 리터럴과 함께 메서드를 사용할 경우 혼란을 방지하기 위해 그룹 연산자를 사용할 것을 권장한다.

```Js
(77.1234).toExponential();  //  "7.71234e+1"
(77.1234).toExponential(4); //  "7.7123e+1"
(77.1234).toExponential(2); //  "7.71e+1"

(77).toExponential(); //  "7.7e+1"
```

### 28.3.6 Number.prototype.toFixed

- 숫자를 반올림하여 문자열로 반환한다.

- 반올림하는 소수점 이하 자릿수를 나타내는 0~20 사이의 정수값을 인수로 전달할 수 있다.

- 인수를 생략하면 기본값 0이 지정된다.

```Js
// 소수점 이하 반올림. 인수를 생략하면 기본값 0이 지정된다.
(12345.6789).toFixed(); //  "12346"
// 소수점 이하 1자릿수 유효, 나머지 반올림
(12345.6789).toFixed(1); //  "12345.7"
// 소수점 이하 2자릿수 유효, 나머지 반올림
(12345.6789).toFixed(2); //  "12345.68"
// 소수점 이하 3자릿수 유효, 나머지 반올림
(12345.6789).toFixed(3); //  "12345.679"
```

### 28.3.7 Number.prototype.toPrecision

- 인수로 전달받은 전체 자릿수까지 유효하도록 나머지 자릿수를 반올림하여 문자열로 반환한다.

- 인수로 전달받은 전체 자릿수로 표현할 수 없는 경우 지수 표기법으로 결과를 반환한다.

- 전체 자릿수를 나타내는 0~21 사이의 정수값을 인수로 전달할 수 있다.

- 인수를 생략하면 기본값 0이 지정된다.

```Js
// 전체 자릿수 유효. 인수를 생략하면 기본값 0이 지정된다.
(12345.6789).toPrecision(); //  "12345.6789"
// 전체 1자릿수 유효, 나머지 반올림
(12345.6789).toPrecision(1); //  "1e+4"
// 전체 2자릿수 유효, 나머지 반올림
(12345.6789).toPrecision(2); //  "1.2e+4"
// 전체 6자릿수 유효, 나머지 반올림
(12345.6789).toPrecision(6); //  "12345.7"
```

### 28.3.8 Number.prototype.toString

- 숫자를 문자열로 변환하여 반환한다.

- 진법을 나타내는 2~36 사이의 정수값을 인수로 전달할 수 있다.

- 인수를 생략하면 기본값 10진법이 지정된다.

```Js
// 인수를 생략하면 10진수 문자열을 반환한다.
(10).toString(); //  "10"
// 2진수 문자열을 반환한다.
(16).toString(2); //  "10000"
// 8진수 문자열을 반환한다.
(16).toString(8); //  "20"
// 16진수 문자열을 반환한다.
(16).toString(16); //  "10"
```
