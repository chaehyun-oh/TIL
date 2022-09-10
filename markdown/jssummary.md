# JavaScript

자바스크립트(JavaScript)는 객체 기반의 스크립트 프로그래밍 언어이다. 이 언어는 웹 브라우저 내에서 주로 사용하며, 다른 응용 프로그램의 내장 객체에도 접근할 수 있는 기능을 가지고 있다.

자바스크립트는 본래 넷스케이프 커뮤니케이션즈 코퍼레이션의 브렌던 아이크(Brendan Eich)가 처음에는 모카(Mocha)라는 이름으로, 나중에는 라이브스크립트(LiveScript)라는 이름으로 개발하였으며, 최종적으로 자바스크립트가 되었다.

자바스크립트가 썬 마이크로시스템즈의 자바와 구문(syntax)이 유사한 점도 있지만, 이는 사실 두 언어 모두 C 언어의 기본 구문에 바탕을 뒀기 때문이고, 자바와 자바스크립트는 직접적인 관련성이 없다.

내부/외부 방식

```jsx
객체.메서드();
document.wirte();
//한 줄 주석
/*여러 줄
주석*/
```

# BOM 객체 (브라우저 객체)

browser object model

브라우저 창에 포함된 모든 객체 요소들을 의미

<브라우저 객체의 종류>

document : 문서객체, 하위에 form, cookie, images 등이 존재

navigator : 브라우저에 대한 정보를 제공하는 객체

location : 위치(url)관련 정보를 제공하는 객체

screen : 스크린(모니터)에 대한 정보를 제공하는객체

history : 인터넷 방문 기록에 대한 정보를 제공하는 객체

위의 모든 객체들은 최상위 객체인 window(창)아래에 존재함

`<window>` : 모든 객체의 최상위 객체

메서드(window 객체 생략 가능)

open(”경로”, “창이름”, “옵션”) : 새 창으로 문서를 열 때 사용

(open 메서드 옵션종류: width (px), height (px), left (px), top (px), scrollbars (y/n), menubar (y/n), toolbar (y/n), location (y/n), status (y/n), resizeable (y/n))

alert(”문자”) : 경고창을 열 때 사용

prompt(”질문”, “기본응답”) : 질문/응답 창을 열 때 사용

confilm(”질문”) : 확인/취소창을 열 때 사용

setTimeout(실행문, 시간간격) : 해당 시간간격 뒤에 실행문을 한 번만 수행

setInterval(실행문, 시간간격) : 해당 간격으로 실행문을 반복적으로 수행

(1000 = 1초)

classList

add( String [, String [, ...]] )
지정한 클래스 값을 추가한다. 만약 추가하려는 클래스가 엘리먼트의 class 속성에 이미 존재한다면 무시한다.
remove( String [, String [, ...]] )
지정한 클래스 값을 제거한다.
item( Number )
콜렉션의 인덱스를 이용하여 클래스 값을 반환한다.
toggle( String [, force] )
하나의 인수만 있을 때: 클래스 값을 토글링한다. 즉, 클래스가 존재한다면 제거하고 false를 반환하며, 존재하지
않으면 클래스를 추가하고 true를 반환한다.
두번째 인수가 있을 때: 두번째 인수가 true로 평가되면 지정한 클래스 값을 추가하고 false로 평가되면 제거한다.
contains( String )
지정한 클래스 값이 엘리먼트의 class 속성에 존재하는지 확인한다.
replace( oldClass, newClass )
존재하는 클래스를 새로운 클래스로 교체한다.

## Window 객체 속성

document 브라우저 창에 표시된 웹 문서에 접근 가능

frameElement 현재 창이 다른 요소 안에 포함되어 있으면 그 요소를 반환하고 포함되어 있지 않으면 null을 반환

innerHeight 내용 영역의 높이

innerWidth 내용 영역의 너비

localStorage 웹 브라우저에서 데이터를 저장하는 로컬 스토리지를 반환

location Window 객체의 위치/ 현재URL

name 브라우저창에 이름을 가져오거나 수정

outerHeight 브라우저창에 바깥 높이

outerWidth 브라우저창에 바깥 너비

pageXOffset 스크롤했을 때 수평으로 이동하는 픽셀 수, scrollX

pageYOffset 스크롤했을 때 수직으로 이동하는 픽셀 수, scrollY

parent 현재 창이나 서브 프레임의 부모 프레임입니다.

screenX 전체 모니터 스크린에서의 x좌표 위치를 반환.

screenY 전체 모니터 스크린에서의 y좌표 위치를 반환.

scrollX 스크롤했을 때 수평으로 이동하는 픽셀 수

scrollY 스크롤했을 때 수직으로 이동하는 픽셀 수

sessionStorage 웹 브라우저에서 데이터를 저장하는 세션 스토리지를 반환.

## 자바스크립트 높이, 너비

1. offsetWidth, offsetHeight
   높이와 너비를 구할 때 가장 많이 쓰이는 속성으로 padding, border 값을 포함한 컨텐츠의 높이를 가져온다. (margin은 포함하지 않는다.)
2. clientWidth, clientHeight
   컨텐츠 높이, 너비과 padding 값만 적용해서 값을 계산한다. border 값은 포함하지 않는다.
3. scrollWidth, scrollHeight
   padding값을 포함한 컨텐츠 안에 숨겨진 스크롤 영역까지 계산한다.
   4.Element.getBoundingClientRect()
   메서드는 엘리먼트의 크기와 뷰포트에 상대적인 위치 정보를 제공하는 DOMRect 객체를 반환.
   DOMRect 인터페이스는 직사각형의 크기와 위치
4.

# 변수

변화하는 값을 저장하는 공간

변수 : 데이터를 저장하는 공간

변수선언

`var num = 10;`

<변수명 작성 주의사항>

대소문자의 구분

변수명 맨 앞에는 영문, \_, $ 등만 가능

변수명에는 영문, \_, $, 숫자만 가능

## var

var은 변수의 재선언, 재할당이 모두 가능하다.
이미 선언된 변수 name을 한번 더 선언해도 에러 없이 새로운 값이 할당된다.
다루기 쉽다는 장점이 있는 반면, 코드가 복잡해지면 변수를 관리하기 어려워진다.

## let

let은 변수의 재선언은 불가능하지만, 재할당은 가능하다.

(블록 스코프)

## const

const는 변수의 재선언, 재할당 모두 불가능하다.
이러한 이유로 const는 재할당을 하지 않은 전역변수에 주로 쓰인다.

재할당이 필요한 경우는 let을 사용한다

(블록 스코프; 스코프-중괄호로 묶이는 구역)

사용불가능한 이름

# 자료형

문자열(string), 숫자, 불린(boolean), 언디파인드, 널(null)

# 연산자

== 값 비교

=== 자료형까지 비교

# 함수

```jsx
function plus() {
	var result = 100 + 200;
	document.write(result);
}
```

return

반환 값 지정

```jsx
<script>
    var num1 = prompt("숫자를 입력하세요", "");
    var num2 = prompt("또 다른 숫자를 입력하세요", "")
    num1=Number(num1);
    num2=Number(num2);

    var result = myPlus(num1,num2);
    document.write("두 수의 합은" + result + "입니다.")

    function myPlus(num1, num2){

        var sum = num1 + num2;
        return sum;

	    }
</script>
```

즉시 실행 함수

> 즉시 실행 함수는 호출없이 작성시 바로 작동

```jsx
var result2 = (function (a, b) {
	return a + b;
})(2, 2);
document.write(result2);
```

# 객체

## DOM객체 (문서 객체)

웹 문서는 여러 요소(태그)들이 각각의 역할에 따라 구조화 되어있음

html 문서 구조를 가르켜 문서객체 라고 함

선택자

`객체.getElemenById(”id이름”);`

객체.getElementById(”id이름”).style.background=”gold”;

객체.getElementById(”id이름”).style.fontSize=”30px”;

객체.getElementsByClassName( );

객체.getElementsByTagName( );

css하고 겹칠 경우 자바스크립트가 우선 적용(js는 인라인속성으로 들어감)

```jsx
<head>
<script>
        window.onload=function(){
            const $sel = document.getElementsByTagName("p");
            $sel[0].style.background="rosybrown";
            $sel[0].style.fontSize="30px"

						document.getElementById("tit").style.background="#eaeaea";
            document.getElementsByClassName("txt")[1].style.background="gold";

        }
        // 여러개인 경우 인덱스번호로 지정해야함
        // if(window.addEventListener){
        //     window.addEventListener("load",loadFnc,false);
        // }

    </script>
</head>
<body>
    <h1 id="tit">문서객체</h1>
    <p class="txt">웹 문서는 여러 요소(태그)들이 각각의 역할에 따라 구조화 되어있다.</p>
    <p class="txt">웹 문서는 여러 요소(태그)들이 각각의 역할에 따라 구조화 되어있다.</p>
    <p class="txt">웹 문서는 여러 요소(태그)들이 각각의 역할에 따라 구조화 되어있다.</p>

</body>
```

## 내장객체

Date, Array, Math, String 등

new 연산자를 이용해서 새로운 객체를 생성

`var todayObj = new Date();`

### math

```jsx
<script>
        let num1 = 2.64262;
        let num2 = "20.6px";
        let num3 = 40;
        let num4 = 3.14235239;

        document.write(Math.max(10, 4, 76, 30), "<br>");
        // 최대값 반환

        document.write(Math.min(10, 4, 76, 30), "<br>");
        // 최솟값 반환

        document.write(Math.round(num1), "<br>");
        // 소수점첫째자리 반올림

        document.write(Math.ceil(num4), "<br>");
        // 소수점 강제 반올림

        document.write(Math.floor(num4), "<br>");
        // 소수점 삭제
        document.write(Math.abs(-10), "<br>");
        // 절대값 반환

        document.write(parseInt(num4+num3), "<br>");
        // 데이터를 정수로 반환

        document.write(parseFloat(num4+num3), "<br>");
        // 데이터를 실수로 반환

        document.write(parseInt(num2)+num3, "<br>");
        // parseInt는 문자형안에 있는 숫자라도 풀어서 연산가능하게 함

        document.write(Math.random()*(20-0))+0;
        // random - 0~1사이의 난수를 발생시킴
        // (Math.random()*(최대값-최소값))+최소값
    </script>
```

querySelector

```jsx
<script>
        window.onload=function(){
            const $obj = document.querySelector("#box");
            $obj.style.width="300px";
            $obj.style.height="300px";
            $obj.style.background="gold";

            const $obj2 = document.querySelector(".box2");
            $obj2.style.width="300px";
            $obj2.style.height="300px";
            $obj2.style.background="green";

            const $obj3 = document.querySelector("#box>h2");
            $obj3.style.color="#fff";

						const $obj4 = document.querySelectorAll("#list li");
            $obj4[0].style.border="1px solid red";
        }
        // id, class 다 가능

    </script>
</head>
<body>
    <div id="box">
        <h2>querySelector</h2>
    </div>
    <div class="box2">

    </div>
</body>
```

```jsx
<script>
function tab(target, sh){
            document.querySelector(target).style.visibility=sh;
        }
//함수도 중복되는 경우는 매개변수 넣어서 사용 가능함
</script>
<body>
    <div id="wrap">
        <button onclick="tab('#box', 'visible');">SHOW</button>
        <button onclick="tab('#box', 'hidden');">HIDE</button>
/*자바스크립트는 "" 안에 또 "" 넣을 수 없기 때문에 '' 로 넣어야 함 반대로 ''안에는 ""*/
        <div id="box">BOX</div>
    </div>
</body>
```

메서드

`setAttribute( );`

접근한 객체의 속성값을 변경하는 메서드

`getAttribute( );`

객체의 속성에 접근

for(let 반복할 요소가 담길 변수명 of 반복시킬 그룹){반복 실행할 구문}

# navigator

# location

연결

```jsx
<script>
        let myAgent = navigator.userAgent.toLowerCase();
        let mobile = ["iphone", "ipad", "android", "blackberry", "window ce", "nokia"];
        for (let i = 0; i < mobile.length; i++) {
            if (myAgent.indexOf(mobile[i]) >= 0) {
                location.href = "http://chaehyunoh.com/cgv/mIndex.html"
            }
        }
    </script>
```
