2022.04.12 모던 자바스크립트 Deep Dive

7장 연산자


1. object.is(비교대상1,비교대상2)메서드

 - 타입을 비교해주는 메서드이다. 타입이 대상1과 대상2의 타입이 같다면 true , 다르다면 false 를 반환한다.

</br>
</br>
2. 삼항연산자
3. </br>

   - 조건이 1개인경우 if문 보다 삼항연산자가 가독성이높다
    
   - 삼항연산자는 변수에 담아서 사용 가능하다.
   
   - if문은 삼항연산자와 다르게 변수에 담을수 없다.
</br>
    
삼항 조건 연산자

<img width="430" alt="스크린샷 2022-04-12 오전 9 46 26" src="https://user-images.githubusercontent.com/94230809/162856209-aadfed6c-5209-4a75-b839-17bd7fac8a25.png">

// 2%2는 0 이고 0은 false로 암묵적 타입 변환된다.


</br>
아래 예제는 if...else문을 사용해 삼항 조건 연산자 표현식과 유사하게 처리한 형태입니다.
</br>
</br>
<img width="368" alt="스크린샷 2022-04-12 오전 9 51 33" src="https://user-images.githubusercontent.com/94230809/162856669-c488aecb-e535-4618-978f-beb7cfa076fa.png">

// 2%2는 0 이고 0은 false로 암묵적 타입 변환된다.
</br>
</br>
</br>
3. null

typeOf null을 하면 Object 라고 반환한다.
이것은 자바스크립트의 첫 번재 버전의 버그이다. 하지만 기존 코드에 영향을 줄 수 있기 때문에 아직까지 수정되지 못하고 있다.

따라서 값이 null 인지 확인할 경우 typeOf 연산자를 사용하지말고 일치 연산자(===)를 사용하자.

<img width="197" alt="스크린샷 2022-04-12 오전 10 08 31" src="https://user-images.githubusercontent.com/94230809/162859912-5b24301f-7543-41d5-aee6-e27b95e696c0.png">

위와 같이 확인할 수 있다.


