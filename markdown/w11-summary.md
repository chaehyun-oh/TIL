# 11주차 summary

## JavaScript

: 브라우저를 조작할 수 있는 (거의) 유일한 언어, 브라우저 화면을 동적으로 만들기 위한 프로그래밍 언어 ⇒ 브라우저를 조작하기 위한 프로그래밍 언어

### DOM (Document Object Model)

-   HTML, XML과 같은 문서를 다루기 위한 문서 프로그래밍 인터페이스
-   문서를 구조화, 구조화된 구성 요소를 하나의 객체로 취급해 다루는 논리적 트리 모델
-   문서가 구조화되어 있음, 각 요소는 객체(Object)
-   속성 접근, 메서드 활용 뿐 아니라 프로그리맹 언어적 특성 활용한 조작 가능
-   주요 객체 : window, document, navigator, location, history, screen

-   DOM - 해석
    -   파싱 (Parsing) : 구문 분석, 해석 / 브라우저가 문자열을 해석해 DOM Tree로 만드는 과정 (Parse > Style > Layout)

### BOM (Browser Object Model)

-   JS가 브라우저와 소통하기 위한 모델
-   브라우저의 창, 프레임을 추상화해서 프로그래밍적으로 제어할 수 있도록 제공하는 수단 (버튼, URL 입력창, 타이틀 바 등 브라우저 윈도우 및 웹 페이지 일부분 제어 가능)

## DOM 조작

: 선택 (Select) ⇒ 변경 (Manipulation)

### DOM 객체의 상속 구조

-   Event Target : Event Listner를 가질 수 있는 객체가 구현하는 DOM 인터페이스
-   Node : 여러 DOM 타입들이 상속하는 인터페이스
-   Element : Document 안의 모든 객체가 상속하는 범용적인 인터페이스 (부모인 Node, EventTarget 속성 상속)
-   Document : 브라우저가 불러온 웹 페이지, DOM 트리의 진입점 (entry point) 역할
-   HTML Element : 모든 종류의 HTML 요소, 부모 element 속성 상속

### DOM 선택

-   `document.querySelector(selector)` : 선택자와 일치하는 element 하나 선택 (선택자를 만족하는 첫 번째 element 객체 반환, 없으면 null)
-   `document.querySelector(selector)` : 선택자와 일치하는 여러 element 선택, 선택자에 일치하는 NodeList 반환
-   `getElementById(id)`
-   `getElementsByTagName(name)`
-   `getElementsByClassName(names)`

### DOM 변경

-   `document.createElement()` : 작성한 태그 명의 HTML 요소 생성 후 반환
-   `Element.append()` : 특정 부모 Node의 자식 NodeList 중 마지막 자식 다음에 Node 객체나 DOMString 삽입, 여러 개의 Node 객체, DOMString 추가 가능, 반환 값 없음
-   `Node.appendChild()` : 한 Node를 특정 부모 Node의 자식 NodeList 중 마지막 자식으로 삽입 (Node만 추가 가능), 한번에 하나의 Node만 추가 가능 (만약 주어진 Node가 이미 문서에 존재하는 다른 Node를 참조하면 새로운 위치로 이동)
-   `Node.innerText` : Node 객체와 그 자손의 텍스트 컨텐츠(DOMString) 표현 (내부 raw text)
-   `Element.innetHTML` : element 내 포함된 HTML 마크업 반환 (사용시 보안 취약 유의)

### DOM 삭제

-   `ChildNode.remove()` : Node 가 속한 트리에서 해당 Node 제거
-   `Node.removeChild()` : DOM에서 자식 Node를 제거 후 제거된 Node 반환

### DOM 속성

-   `Element.setAttribute(name, value)` : 지정된 요소의 값 설정, 속성 이미 존재하면 값 갱신 없으면 지정된 이름, 값으로 새 속성 추가
-   `Element.getAttribute(attributeName)` : 해당 요소의 지정된 값(문자열) 반환, 인자= 값을 얻고자 하는 속성 이름

## ECMA Script

### 코딩 스타일 가이드

-   코딩 스타일의 핵심 = 합의된 원칙, 일관성
-   코딩 스타일 = 코드의 품질에 직결되는 중요한 요소 (가독성, 유지보수 등)

## 변수, 식별자

-   `let` : 재할당 가능 , 재선언 불가, 블록 스코프
-   `const` : 재할당 불가, 재선언 불가, 블록 스코프
-   `var` : 재선언, 재할당 가능, 함수 스코프
    -   `var`는 호이스팅되는 특성 때문에 문제 발생 가능
    -   호이스팅(hoisting) :인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미. `var`로 선언한 변수의 경우 호이스팅 시 `undefined`로 변수를 초기화함

## 데이터 타입

-   원시 타입 (Primitive type) : 객체가 아닌 기본 타입, 다른 변수에 복사할 때 실제 값이 복사 됨
    -   number, string, boolean, undifined, null, symbol
-   참조 타입 (Reference type) : 객체 타입의 자료형, 다른 변수에 복사할 때 참조값이 복사 됨
    -   arraym function 등

## 연산자

-   할당 연산자
-   비교 연산자
-   동등 비교 연산자 (==) : 암묵적 타입 변환 후 값 일치 비교
-   일치 비교 연산자 (===) : 타입, 값 둘 다 일치 비교
-   논리 연산자 : `&&`, `||`, `!`
-   삼항 연산자 : `n > 4 ? 'Yes' : 'No'`

## 조건문

-   if statement
-   switch statement : 조건 표현식의 결과값이 어느 case에 해당하는지 판별

## 반복문

-   while
-   for
-   for … in : 주로 객체의 속성 순환 시 사용
-   for … of : 반복 가능한 객체를 순회하며 값을 꺼낼 때 사용

## 함수

: 참조 타입 중 하나로 function 타입에 속함

-   함수 선언식 (function declaration)
-   함수 표현식 (function expression) : 익명 함수로 정의 가능

-   Rest Parameter (…) : 함수가 정해지지 않은 수의 매개변수를 배열로 받음
    ```jsx
    const restOpr = function (arg1, arg2, ...restArgs) {
    	return [arg1, arg2, restArgs];
    };
    ```
-   Spread operator : 배열 인자를 전개하여 전달 가능
    ```jsx
    const spreadOpr = function (arg1, arg2, arg3) {
    	return arg1 + arg2 + arg3;
    };
    const numbers = [1, 2, 3];
    spreadOpr(...numbers);
    ```

## 화살표 함수

: 함수를 비교적 간결하게 정의할 수 있는 문법

```jsx
const arrow = (name) => `hello, ${name}`;
```

## 문자열

-   `.includes()`
-   `.split()`
-   `.replace(from, to)` , `.replaceAll(from, to)`
-   `.trim()`, `.trimStart()` ,`.trimEnd()`

## 배열

-   `.reverse()`
-   `.push()` `.pop()`
-   `.unshift()` `.shift()`
-   `.includes()`
-   `.indexOf()`
-   `.join([separator])`

-   `.forEach(callback(element, [index, [array]])`
    ```jsx
    onst fruits = ['딸기', '수박', '사과', '체리']
    fruits.forEach((fruit, index) => {
    console.log(fruit, index)
    })
    ```
-   `.map(callback(element, [index, [array]])`
-   `.filter(callback(element, [index, [array]])`
-   `.reduce(callback(element, [index, [array]], initialValue)`
-   `.find()`
-   `.some()`
-   `.every()`

## 객체

: 속성 (property)의 집합, 중괄호 내부에 key, value 쌍으로 표현 (key 문자열 타입만 가능)

JSON (JavaScript Object Notation) : key - value 쌍 형태로 데이터를 표기하는 언어 독립적 표준 포맷, 문자열 타입

-   `JSON.parse()` : JSON ⇒ 자바스크립트 객체
-   `JSON.stringify()` : 자바스크립트 객체 ⇒ JSON
