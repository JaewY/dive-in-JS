# 30장 Date

### 표준 빌트인 객체인 Date는 날짜와 시간(연, 월, 일, 시, 분, 초, 밀리초(millisecond/ms. 천분의 1초))을 위한 메서드를 제공하는 빌트인 객체이면서 생성자 함수다.

- UTC(협정 세계시 Coordinated Universal Time)는 국제 표준시를 말한다.

- UTC는 GMT(그리니치 평균시 Greenwich Mean Time)로 불리기도 한다.

- UTC와 GMT는 초의 소수점 단위에서만 차이가 나기 때문에 일상에서는 혼용되어 사용된다.

- 기술적인 표기에서는 UTC가 사용된다.

- KST(한국 표준시Korea Standard Time)는 UTC에 9시간을 더한 시간이다.

- 즉, KST는 UTC보다 9시간이 빠르다. 예를 들어, UTC 00:00 AM은 KST 09:00 AM이다.

## 30.1 Date 생성자 함수

- Date는 생성자 함수다.

- Date 생성자 함수로 생성한 Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값을 갖는다.

- Date 생성자 함수로 객체를 생성하는 방법은 다음과 같이 4가지가 있다.

### 30.1.1 new Date()

- Date 생성자 함수를 인수 없이 new 연산자와 함께 호출하면 현재 날짜와 시간을 가지는 Date 객체를 반환한다.

- Date 객체는 내부적으로 날짜와 시간을 나타내는 정수값을 갖지만 Date 객체를 콘솔에 출력하면 기본적으로 날짜와 시간 정보를 출력한다.

```Js
new Date(); //  Mon Jul 06 2020 01:03:18 GMT+0900 (대한민국 표준시)
```

- Date 생성자 함수를 new 연산자 없이 호출하면 Date 객체를 반환하지 않고 날짜와 시간 정보를 나타내는 문자열을 반환한다.

### 30.1.2 new Date(milliseconds)

- Date 생성자 함수에 숫자 타입의 밀리초를 인수로 전달하면 1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 밀리초만큼 경과한 날짜와 시간을 나타내는 Date 객체를 반환한다.

### 30.1.3 new Date(dateString)

- Date 생성자 함수에 날짜와 시간을 나타내는 문자열을 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체를 반환한다.

- 이때 인수로 전달한 문자열은 Date.parse 메서드에 의해 해석 가능한 형식이어야 한다

```Js
new Date('May 26, 2020 10:00:00');
//  Tue May 26 2020 10:00:00 GMT+0900 (대한민국 표준시)

new Date('2020/03/26/10:00:00');
//  Thu Mar 26 2020 10:00:00 GMT+0900 (대한민국 표준시)
```

### 30.1.4 new Date(year, month[, day, hour, minute, second, millisecond])

- Date 생성자 함수에 연, 월, 일, 시, 분, 초, 밀리초를 의미하는 숫자를 인수로 전달하면 지정된 날짜와 시간을 나타내는 Date 객체를 반환한다.

- 이때 연, 월은 반드시 지정해야 한다.

- 지정하지 않은 옵션 정보는 0 또는 1로 초기화된다.

## 30.2 Date 메서드

### 30.2.1 Date.now

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 현재 시간까지 경과한 밀리초를 숫자로 반환한다.

### 30.2.2 Date.parse

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간(new Date(dateString)의 인수와 동일한 형식)까지의 밀리초를 숫자로 반환한다.

```Js
// UTC
Date.parse('Jan 2, 1970 00:00:00 UTC'); //  86400000

// KST
Date.parse('Jan 2, 1970 09:00:00'); //  86400000

// KST
Date.parse('1970/01/02/09:00:00');  //  86400000
```

### 30.2.3 Date.UTC

- 1970년 1월 1일 00:00:00(UTC)을 기점으로 인수로 전달된 지정 시간까지의 밀리초를 숫자로 반환한다.

- Date.UTC 메서드는 new Date(year, month[, day, hour, minute, second, millisecond])와 같은 형식의 인수를 사용해야 한다

### 30.2.4 Date.prototype.getFullYear

- Date 객체의 연도를 나타내는 정수를 반환한다.

```Js
new Date('2020/07/24').getFullYear(); //  2020
```

### 30.2.5 Date.prototype.setFullYear

- Date 객체에 연도를 나타내는 정수를 설정한다.

- 연도 이외에 옵션으로 월, 일도 설정할 수 있다.

```Js
const today = new Date();

// 년도 지정
today.setFullYear(2000);
today.getFullYear(); //  2000

// 년도/월/일 지정
today.setFullYear(1900, 0, 1);
today.getFullYear(); //  1900
```

### 30.2.6 Date.prototype.getMonth

- Date 객체의 월을 나타내는 0 ~ 11의 정수를 반환한다.

- 1월은 0, 12월은 11이다.

```Js
new Date('2020/07/24').getMonth(); //  6
```

### 30.2.7 Date.prototype.setMonth

- Date 객체에 월을 나타내는 0 ~ 11의 정수를 설정한다.

- 1월은 0, 12월은 11이다.

- 월 이외에 옵션으로 일도 설정할 수 있다.

### 30.2.8 Date.prototype.getDate

- Date 객체의 날짜(1 ~ 31)를 나타내는 정수를 반환한다.

```Js
new Date('2020/07/24').getDate(); //  24
```

### 30.2.9 Date.prototype.setDate

- Date 객체에 날짜(1 ~ 31)를 나타내는 정수를 설정한다.

### 30.2.10 Date.prototype.getDay

- Date 객체의 요일(0 ~ 6)을 나타내는 정수를 반환한다

- 일요일은 0, 토요일은 6

```Js
new Date('2020/07/24').getDay(); //  5
```

### 30.2.11 Date.prototype.getHours

- Date 객체의 시간(0 ~ 23)을 나타내는 정수를 반환한다.

```Js
new Date('2020/07/24/12:00').getHours(); //  12
```

### 30.2.12 Date.prototype.setHours

- Date 객체에 시간(0 ~ 23)을 나타내는 정수를 설정한다.

- 시간 이외에 옵션으로 분, 초, 밀리초도 설정할 수 있다.

### 30.2.13 Date.prototype.getMinutes

- Date 객체의 분(0 ~ 59)을 나타내는 정수를 반환한다.

```Js
new Date('2020/07/24/12:30').getMinutes(); //  30
```

### 30.2.14 Date.prototype.setMinutes

- Date 객체에 분(0 ~ 59)을 나타내는 정수를 설정한다.

- 분 이외에 옵션으로 초, 밀리초도 설정할 수 있다.

### 30.2.15 Date.prototype.getSeconds

- Date 객체의 초(0 ~ 59)를 나타내는 정수를 반환한다.

```Js
new Date('2020/07/24/12:30:10').getSeconds(); //  10
```

### 30.2.16 Date.prototype.setSeconds

- Date 객체에 초(0 ~ 59)를 나타내는 정수를 설정한다.

- 초 이외에 옵션으로 밀리초도 설정할 수 있다.

### 30.2.17 Date.prototype.getMilliseconds

- Date 객체의 밀리초(0 ~ 999)를 나타내는 정수를 반환한다.

```Js
new Date('2020/07/24/12:30:10:150').getMilliseconds(); //  150
```

### 30.2.18 Date.prototype.setMilliseconds

- Date 객체에 밀리초(0 ~ 999)를 나타내는 정수를 설정한다.

### 30.2.19 Date.prototype.getTime

- 1970년 1월 1일 00:00:00(UTC)를 기점으로 Date 객체의 시간까지 경과된 밀리초를 반환한다.

```Js
new Date('2020/07/24/12:30').getTime(); //  1595561400000
```

### 30.2.20 Date.prototype.setTime

- Date 객체에 1970년 1월 1일 00:00:00(UTC)를 기점으로 경과된 밀리초를 설정한다.

### 30.2.21 Date.prototype.getTimezoneOffset

- UTC와 Date 객체에 지정된 로캘(locale) 시간과의 차이를 분 단위로 반환한다.

- KST는 UTC에 9시간을 더한 시간이다.

- 즉, UTC = KST - 9h다.

```Js
const today = new Date();   // today의 지정 로캘은 KST다.

//UTC와 today의 지정 로캘 KST와의 차이는 -9시간이다.
today.getTimezoneOffset() / 60; // -9
```

### 30.2.22 Date.prototype.toDateString

- 사람이 읽을 수 있는 형식의 문자열로 Date 객체의 날짜를 반환한다.

```Js
const today = new Date('2020/7/24/12:30');

today.toString();     //  Fri Jul 24 2020 12:30:00 GMT+0900 (대한민국 표준시)
today.toDateString(); //  Fri Jul 24 2020
```

### 30.2.23 Date.prototype.toTimeString

- 사람이 읽을 수 있는 형식으로 Date 객체의 시간을 표현한 문자열을 반환한다.

```Js
const today = new Date('2020/7/24/12:30');

today.toString();     //  Fri Jul 24 2020 12:30:00 GMT+0900 (대한민국 표준시)
today.toTimeString(); //  12:30:00 GMT+0900 (대한민국 표준시)
```

### 30.2.24 Date.prototype.toISOString

- ISO 8601형식으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환한다

### 30.2.25 Date.prototype.toLocaleString

- 인수로 전달한 로캘을 기준으로 Date 객체의 날짜와 시간을 표현한 문자열을 반환한다.

- 인수를 생략한 경우 브라우저가 동작 중인 시스템의 로캘을 적용한다

```Js
const today = new Date('2020/7/24/12:30');

today.toString(); //  Fri Jul 24 2020 12:30:00 GMT+0900 (대한민국 표준시)
today.toLocaleString(); //  2020. 7. 24. 오후 12:30:00
today.toLocaleString('ko-KR'); //  2020. 7. 24. 오후 12:30:00
today.toLocaleString('en-US'); //  7/24/2020, 12:30:00 PM
today.toLocaleString('ja-JP'); //  2020/7/24 12:30:00
```

### 30.2.26 Date.prototype.toLocaleTimeString

- 인수로 전달한 로캘을 기준으로 Date 객체의 시간을 표현한 문자열을 반환한다.

- 인수를 생략한 경우 브라우저가 동작 중인 시스템의 로캘을 적용한다.

```Js
const today = new Date('2020/7/24/12:30');

today.toString(); //  Fri Jul 24 2020 12:30:00 GMT+0900 (대한민국 표준시)
today.toLocaleTimeString(); //  오후 12:30:00
today.toLocaleTimeString('ko-KR'); //  오후 12:30:00
today.toLocaleTimeString('en-US'); //  12:30:00 PM
today.toLocaleTimeString('ja-JP'); //  12:30:00
```
