# 49장 Babel과 Webpack을 이용한 ES6+/ES.NEXT 개발 환경 구축

## 49.1 Babel

### Babel은 ES6+/ES.NEXT로 구현된 최신 사양의 소스코드를 IE 같은 구형 브라우저에서도 동작하는 ES5 사양의 소스코드로 변환(트랜스파일링)할 수 있다

```Js
// ES6 이상
[1, 2, 3].map(n => n ** n);

// ES5 사양
"use strict";

[1, 2, 3].map(function (n) {
    return Math.pow(n, n);
});
```

- Babel 개발 환경 구축 순서

1. Babel 설치

2. Babel 프리셋 설치와 babel.config.json 설정 파일 작성

3. 트랜스파일링

4. Babel 플러그인 설치

5. 브라우저에서 모듈 로딩 테스트

## 49.2 Webpack

### Webpack은 의존 관계에 있는 자바스크립트, CSS, 이미지 등의 리소스들을 하나(또는 여러 개)의 파일로 번들링하는 모듈 번들러다

- Webpack을 사용하면 의존 모듈이 하나의 파일로 번들링되므로 별도의 모듈 로더가 필요 없다.

- 여러 개의 자바스크립트 파일을 하나로 번들링하므로 HTML 파일에서 script 태그로 여러 개의 자바스크립트 파일을 로드해야 하는 번거로움도 사라진다.

<img width="557" alt="스크린샷 2022-08-16 오후 4 18 49" src="https://user-images.githubusercontent.com/95524491/184820606-5e0ac7ad-ea7b-4c27-9066-7eca81480a7c.png">

- Webpack과 Babel을 이용하여 ES6+/ES.NEXT 개발 환경을 구축 순서

1. Webpack 설치

2. babel-loader 설치

3. webpack.config.js 설정 파일 작성

4. babel-polyfill 설치
