# Javascript 2

: 모든 웹 브라우저에서 작동, 다양한 JS 공개 API 사용가능, 다양한 라이브러리/프레임워크 사용가능

`<script>` 태그 안에 js 작성, HTML문서 어디에서든 사용가능, `<script>`태그는 한 문서 내에서 여러개 사용 가능함, 태그가 삽입된 곳에서 코드 실행

외부 스크립트 파일 연결하기

: 이름.js로 저장 후 해당 파일을 `<script>` 태그로 HTML 문서와 연결

`<script src=”위치/이름.js”></script>`

js도 css처럼 따로 폴더에 저장

처음에는 html 문서에 작성해서 작동하는지 확인 후에 잘라내서 옮기는 편이 좋음

사용자 입력값 받기 : prompt( ) 함수

prompt( )는 사용자로부터 입력을 받고자 할 때 사용

`prompt( ); , prompt(”입력하세요”);`

알림창으로 출력하기 : alert( ) 함수

: 웹 브라우저 화면에서 간단한 알림 내용을 출력함

alert(”알림 내용”);

웹 브라우저 화면에 출력하기 - document.write( ) 함수

: 결과 값을 웹 브라우저 화면에 출력

document 객체는 현재 문서를 의미

write( ) 출력하는 함수

```jsx
var name = prompt(”이름을 입력하세요: ”);
document.write(”<b>” + name + “</b>님,  환영합니다.”)
```

콘솔에 출력하기 - console.log( ) 함수

: 괄호 안의 내용을 콘솔 창에 출력

```jsx
var name = prompt(”이름: ”);
console.log(name + "님, 어서오세요");
```

자바스크립트 규칙

-   대소문자 구분하여 소스 작성
-   읽기 쉽게 들여쓰기
-   세미콜론으로 문장 구분
-   소수에 주석으로 메모
-   식별자는 정해진 규칙을 지켜서 작성
-   예약어는 식별자로 사용불가

# 변수와 자료형, 연산자

변수 : 변할 수 있는 값, 덮어 쓸 수 있기 때문에 변함

자료형 : 데이터 타입

연산자 :

## 변수

변수를 선언하는 규칙 세가지

-   이름을 의미있게 지어야 함
-   여러 단어를 연결한 변수 이름은 대문자로 구분 (lastDay)
-   변수 이름의 첫글자는 반드시 문자나 밑줄(\_), $로 시작해야 함

변수 선언과 값/식 할당

-   var 다음에 변수 이름을 적어서 변수를 선언하고
-   변수 오른쪽에 = 기호를 붙이고 오른쪽에 저장할 값이나 식을 작성

(변수 선언과 값 할당을 동시에 할 수 도 있음)

`*변수는 선언과 동시에 초기화를 하자`

carlc () :함수 , 괄호 안에 넣는 것이 매개변수(인자값, 파라메터, 아규먼트)

```jsx
<script>
function calc( ) { //함수 선언과 구현
	var currentYear = 2022; //현재 년도를 변수에 저장
	var birthYear = prompot(”태어난 연도를 입력하세요”, “YYYY”); //사용자로부터 입력 받은 값을 변수에 저장
	var age = 0; //변수 초기화
	age = currentYear - birthYear + 1; //실제 나이를 구하기 위한 값을 변수에 대입
	document.querySelector(”#result”).innerHTML = “당신의 나이는” + age + “세 입니다.”; //현재 문서에서 #result인 웹 요소를 찾아와서 그 영역에 대입한 값으로 대체함
	}
</script>
```

## 자료형

자료형 : 컴퓨터가 처리하는 자료의 형태

자료형의 종류

<기본형>

-   number : 따옴표 없이 표기한 숫자 (정수, 실수-js에서는 정밀한 실수 계산 못함)
-   string : 문자열, 작은따옴표나 큰따옴표로 묶어 나타냄 (숫자도 따옴표로 묶으면 문자형이 됨)
-   boolean : 논리형, 참과 거짓(true false) 만 있는 유형 (프로그램에서 조건을 확인할 때 많이 사용)
-   undefined : 자료형을 지정하지 않았을 때의 유형, 변수를 선언만 하고 값을 지정하지 않았을 경우 등 (처음부터 변수에 값이 할당되지 않았다 > 쓰레기 값이 들어 있는 경우)
-   null : 값이 유효하지 않을 때의 유형 (다음에 할당된 값이 더이상 유효하지 않다는 의미)

<복합형>

-   array : 배열, 하나의 변수에 여러 값을 저장하는 유형
-   object : 객체, 함수와 속성이 함께 포함된 유형

디버깅 : 크롬 콘솔창을 사용해서도 가능함

자바스크립트 자료형의 특징

: 느슨한 자료형 체크, 자바스크립트는 미리 변수의 자료형을 지정하지 않음, 변수를 지정하고 원하는 값을 할당만 하면 됨

```jsx
<script>
function showPrice( ) {

var originPrice = document.querySelector(”#oPrice”).value;

var rate = document.querySelector(”#rate”).value;

var savedPrice = originPrice * (rate/100);

var resultPrice = originPrice - savePrice;

document.querySeletor(”#showResult”).innerHTML = “상품의 원래 가격은” + originPrice + “원이고, 할인율은: + rate + “%입니다.” + savedPrice + “원을 절약한” + resultPrice + “원에 살 수 있습니다.”;

}

</script>
```

# OOP

Object Oriented Programming

:객체지향적 프로그래밍

자바스크립트 > 멀티패러다임

```jsx
function Song(singer, title, release) {
	this.singer = singer;
	this.title = title;
	this.release = release;
	this.release = new Date(release);
	// 표준시로 표시됨
}
const song1 = new Song("LimKim", "Sal-Ki", "2019");
// new 키워드를 사용해서 인스턴스화 (안하면 window로 this 설정 됨)
```

```jsx
class Song {
	constructor(singer, title, release) {
		this.singer = singer;
		this.title = title;
		this.release = release;
	}
	getReleaseDay() {
		return this.release.getDay();
	}
}
```

# DOM

document object model

```jsx
// const title = document.getElementById("title");
// const list = document.getElementsByClassName("list");
//배열로 반환

const title = document.querySelector("#title");
const list = document.querySelector(".list");
// 쿼리셀렉터는 오브젝트로 반환
const items = document.querySelectorAll(".item");
// 배열로 반환됨
const btn = document.querySelector("#btn");
const naver = document.querySelector(".naver");

title.style.color = "red";
title.style.backgroundColor = "green";
title.innerHTML = "<input type = 'text'/ >";
btn.innerText = "button";

// list.remove();
list.firstElementChild.remove();
list.lastElementChild.innerHTML = "<a>link</a>";

btn.addEventListener("click", function () {
	alert("야호");
});

naver.addEventListener("click", (e) => {
	e.preventDefault();
	alert("네이버");
});
```

# HTTP API

GET 방식: 주소에 포함

POST 방식 : body에 포함

```jsx
// http request
const url =
	"https://api.covid19api.com/country/south-korea/status/confirmed?from=2021-03-01T00:00:00Z&to=2020-04-01T00:00:00Z";
// const corona = fetch(url).then(function(res){
//     return res.json()
// }).then((data)=> console.log(data))

const corona = fetch(url)
	.then((res) => res.json())
	.then((data) => console.log(data));
//인자와 결과값이 하나인 경우 화살표 함수로 쓰면 코드가 좀 더 간단해짐
```
