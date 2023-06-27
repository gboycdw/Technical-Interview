# JavaScript

## 기본 지식

1. 자바스크립트는 자바스크립트 엔진이 있는 모든 디바이스에서 동작하며, HTML/CSS와 완전한 통합이 가능하다.
2. 엔진의 동작원리
   - 파싱 : 엔진이 스크립트를 읽는다.
   - 컴파일 : 스크립트를 기계어로 전환한다.
   - 실행 : 기계어로 전환된 코드 실행한다.
3. 동일 출처 정책 : 브라우저 내 탭과 창은 서로의 정보를 알 수 없다.
   cf) JavaScript를 통해 다른 창을 열때는 예외이나, 도메인/프로토콜/포트가 다르면 페이지에 접근할 수 없음.
4. JavaScript의 파생 언어
   - TypeScript : Microsoft가 개발, 자료형의 명시화에 집중하여 만듬
5. 공식 문서 : ECMA 명세서 (특히 6버전으로 넘어갈 때의 자료가 많이 중요하니 반드시 알아두기 바람 - 추후 별도로 정리)
6. HTML에서 script태그를 사용하여 JavaScript를 읽을 수 있으나, inline 속성으로  ``src``가 있을 경우, 태그 내부의 코드는 무시된다.
7. JavaScript의 코드 구조
   - 일반적으로 줄바꿈은 세미콜론을 의미(세미콜론 자동 삽입), 하지만 추정하지 못하는 경우도 있다.
   - 특히 대괄호 앞에는 세미콜론이 있다고 가정하지 않음에 주의할 것.
8. JavaScript의 엄격 모드
   - ES5에서 추가된 기능으로 인해 발생한 호환성 문제를 해결하기 위한 대책으로, JavaScript 엔진이 변경사항을 활성화할 수 있도록 하기 위해서 스크립트 최상단에 ``"use strict"``를 작성하여 사용한다.
   - 스크립트 최상단이 아닐 경우 동작하지 않고, 어떤 방법으로도 이 모드를 해제할 수 없다!
   - 브라우저 콘솔(개발자 도구) 에는 기본적으로 적용되어 있지 않음에 주의해야 한다.
   - 단, 클래스와 모듈을 사용해 구성된 코드에서는 엄격 모드가 자동으로 적용된다!

## 변수와 상수, 자료형, 형변환, 연산자 놓치기 쉬운 개념

1. 변수는 ``let``을 사용해 생성, 상수는 ``const``를 사용해 생성한다.
   * 이전에는 변수(variable)를 ``var``로 선언하였으나, 현재는 사용하지 않는 방식이다.
   * ``var``를 쓰지 않는 이유 : 블록 스코프가 없다! (함수 스코프 혹은 전역 스코프만 존재)
     => 스코프와 호이스팅 부분에서 다시 정리
   * 변수는 값을 변경할 수 있다. 상수는 값을 변경할 수 없다.
2. 예약어(변수 혹은 상수로 사용할 수 없는 단어)의 종류
   * 조건문/반복문 관련 : ``for, while, do, break, continue, if, else, in, of``
   * 모듈 생성/호출 관련 : ``export, import``
   * 함수 관련 : ``function, return``
   * 선택자와 호이스팅 관련 : ``this, super, switch, case``
   * 에러 핸들링 관련 : ``try, catch, finally``
   * 선언 관련 : ``class, new, var, const``
   * 기타 : ``true, false, null``
   * strict mode 사용 시 : ``let, static, yield``
   * module code 혹은 비동기 함수 내에서 : ``await``
3. JavaScript의 8가지 자료형
   * number
   * BigInt
   * string
   * boolean
   * null
   * undefined
   * object
   * symbol
4. JavaScript의 자료형 판단 연산자 ``typeof`` 을 사용할 때 주의해야 하는 경우
   * ``typeof Math`` object
   * ``typeof null`` object ===> ※ 이것은 진짜로 객체 형태라는 것이 아님에 주의해야 한다.
   * ``typeof alert`` function
5. JavaScript의 Boolean 값 중 특이한 속성을 가지는 경우(falsy value)
   * ``false, null, undefined, 0, "", NaN`` : 이 값들은 falsy한 값으로, if문의 조건으로 받을 때 ``false``를 return 한다.
     이때 주의해야 할 점은 빈 배열이나 객체는 ``true``를 return 한다.
6. 형변환 특이 케이스
   * ``console.log(+"")``> 0
   * ``console.log(+null)`` > 0
   * ``console.log(+undefined)`` > NaN
   * ``console.log(+NaN)`` > NaN
   * ``console.log(+false)`` > 0
7. 브라우저 내장 명령어
   * ``alert("Hello World!!")`` : 경고 모달을 띄움.
   * ``result = prompt(title, [defaultValue])`` : 입력값을 받아서 저장함.
   * ``result = confirm(question)`` : 컨펌 대화상자를 띄움.
8. 문자열로의 형변환
   * ``String(value)`` 혹은 ``value.toString()`` 이 모두 가능하다.
   * 단, ``null``이나 ``undefined``에 대한 형변환을 시도하는 경우, ``toString()`` 메서드는 Cannot read 오류를 발생시킨다.
9. 숫자로의 형변환
   * ``Number(string)`` 혹은 ``parseInt(string)`` 혹은 ``+string`` 등의 방법이 있다.
   * 문자열에 숫자 연산이 적용될 경우 숫자형으로 자동변환 후 연산이 진행된다.
   * ``Number`` 함수를 사용할 경우 명시적 형변환이 일어나고, 숫자가 아닌 것이 포함된 문자열은 ``NaN``을 return 한다.
   * ``parseInt`` 함수를 사용할 경우 암묵적 형변환이 일어나고, 숫자가 아닌 것들을 제외하고 나머지를 숫자형태로 return 한다.
   * 가령, ``let c = "012a"`` 에 대하여 ``Number(c) > NaN`` 이고, ``parseInt(c) > 12`` 이다.
   * 또한, 위에서 언급한 falsy value의 경우 특이한 형변환이 일어난다.
     1. undefined => NaN
     2. null => 0
     3. true => 1
     4. false => 0
10. nullish 병합 연산자 (최근에 추가됨)
    * ``x = a ?? b`` 의 의미?
      다음 코드와 같다. ``x = (a !== null && a !== undefined) ? a : b``
    * 이때 ``||``와 ``??``의 차이점을 정확하게 알아야 한다. or 연산자는 첫 번째 truthy 값을, ??는 첫 번째 정의된 값을 return 한다.
      무슨 말인고.. 하니, ``let gomao = 0``와 ``let cute = 1``에 대하여 다음과 같은 연산이 이루어진다.
      1. ``console.log(gomao || 100)`` > 100
      2. ``console.log(gomao ?? 100)`` > 0
      3. ``console.log(cute || 100)`` > 1
      4. ``console.log(cute ?? 100)`` > 1
    * 각각의 경우에 대해 정확하게 이해하는 것이 필요하다!
11. 반복문의 lable 개념
    * ``gomao: for (let i = 0; i < 3; i++){...}``이와 같은 반복문에 대하여
      ``break gomao``를 선언할 경우, 해당 반복문 안에 있는 모든 반복문이 중단된다.
    * 마찬가지로 ``continue gomao`` 또한 같은 로직으로 동작한다.
    * label을 붙이지 않을 경우, 가장 가까운 반복문에 대해서만 break 혹은 continue가 동작한다.
