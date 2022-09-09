# CSS

※ W3C doctype
[http://www.w3.org/QA/2002/04/valid-dtd-list.html](http://www.w3.org/QA/2002/04/valid-dtd-list.html)

※HTML 유효성 검사 도구
[http://validator.w3.org/](http://validator.w3.org/)

※KLDP의 한글화된 CSS 유효성 검사 서비스
[http://css-validator.kldp.org/](http://css-validator.kldp.org/)[http://www.css-validator.org/validator.html.ko](http://www.css-validator.org/validator.html.ko)

<aside>
🔥 초기화 > 상속 > 내용 순으로

</aside>

# 스타일 시트

: 디자인적 요소를 작업

## 내부 스타일시트

:<head></head> 사이에 지정하는 것

```html
<head>
	<meta charset="utf-8" />
	<title>Embedded Style Sheet/내부스타일 시트</title>
	<style>
		h1 {
			color: yellow;
			background: red;
		}
	</style>
</head>
```

## 외부 스타일시트

: 가장 많이 쓰이는 방식, 외부에 css 파일을 만들고 그 파일을 html과 링크로 연결

css 파일은 폴더를 만들어 따로 저장

\*유지, 보수가 용이함 (여러 페이지를 하나의 css로 연결하면 편함)

```html
<head>
	<meta charset="utf-8" />
	<title>External Style Sheet/외부스타일시트</title>
	<link rel="stylesheet" href="./css/ex.css" type="text/css" />
</head>
```

`@import url(./font_nanum/nanumbarungothic2.css);`

임포트 방식

## 인라인 스타일시트

html 태그 안에 직접 저장하는 방식, 권장하지는 않음 그러나 특정 부분에만 효과 적용할때 사용가능

인라인 스타일시트는 우선순위가 가장 높아서 꼭 필요할 때 편리하게 사용가능함

우선순위: 인라인 > 내부 > 외부

효과가 겹칠 경우 인라인이 먼저 표현됨

```html
<body>
	<h1>Inline 방식</h1>
	<p style="color: rosybrown; background-color: skyblue;">
		style 요소 내에 직접 CSS 코드를 포함합니다.
	</p>
</body>
```

# 스타일 적용 우선순위

인라인 스타일 > 내부 스타일 > 외부 스타일 > 브라우저 기본값

두가지가 똑같은 등급일 때는 가장 마지막 스타일 효과를 적용함

특정도(specify)값을 계산해서 가장 많은 점수를 받은 효과가 우선적으로 적용된다.

인라인 스타일 - 1000점 / ID선택자 - 100점 / 클래스 선택자, 가상 클래스 (예: link) - 10 점 / 태그 선택자, 가상 선택자(예 first-link) - 1점

\*css작성 시 앞의 요소에 부모를 붙였으면 밑에도 동일하게 해야 우선순위 변경이 되지 않음

우선순위 변경

!important ; 꼭 필요한 요소에만 사용

`p{background:yellow !important; color:blue}`

# 선택자 (Selector)

`h1{ color:yellow; background:red; }`

선택자 속성:속성값; 속성: 속성값;

선택자를 지정해야만 효과를 적용할 수 있음

## 타입 선택자

태그 이름을 그대로 가져다 쓰는 선택자

모든 태그에 한번에 효과를 줄 때 사용

```html
<style>
	h2 {
		background-color: wheat;
	}
</style>
```

## id 선택자

id로 붙인 이름을 가져다 쓰는 선택자 # 을 붙여 표기함

같은 이름 여러번 사용 불가함

(일반적으로 레이아웃 잡을때 사용)

```html
<head>
	<style>
		#text {
			color: tomato;
		}
	</style>
</head>

<body>
	<p id="text">id명은 같은 HTML문서내에서 한번만 적용해야 합니다.</p>
</body>
```

## class 선택자

class로 붙인 이름을 가져다 쓰는 선택자 . 을 붙여 표기함

같은 이름 여러번 사용 가능

(일반적으로 디자인적 요소 적용할 때 많이 사용)

```html
<head>
	<style>
		.color {
			background-color: yellowgreen;
		}
	</style>
</head>

<body>
	<h2 class="color">class선택자</h2>
	<p>
		HTML문서내에서 여러번 사용할 수 있기 때문에 여러 가지 HTML태그를
		한꺼번에 일관된 스타일을 적용할 수 있습니다.
	</p>
	<p class="color">
		class선택자는 요소명과 클래스명을 구분할 때 마침표(.)를 이용합니다.
	</p>
</body>
```

다중 클래스

`class = " row bg btn"`

우선순위 : id > class > 태그(타입)

## 전체 선택자

페이지의 모든 요소를 가리키는 선택자 \* 을 붙여 표기함

head, body 전체 한번에 제어

블록 요소는 기본 여백이 있음 > 전체 선택자는 주로 기본 여백을 초기화할 때 사용함

```html
<style>
	* {
		margin: 0;
		padding: 0;
	}
</style>
```

## 하위선택자

부모 안에 포함되어있는 모든 후손 선택자

`.부모선택자 (중간 생략가능) .하위 선택자`

부모 지정할 경우 특정부분에만 적용 가능

```html
<Style>
.ex5 .color_txt{ color: #9abe92;}
<Style>

<body>
<div class="ex5">
<img src="./images/hurom.png" alt="휴롬">
<p class="txt">사람을 이롭게 하는 기술로<br> <span class="color_txt">건강하고 행복한 삶에 기여한다</span> </p>
<p>이익보다는 사람이 우선이라는 원칙으로 사람에게 가장 이로운 기술을 구현해 <br> 건강하고 행복한 삶에 기여합니다.</p>
```

## 그룹 선택자

135.p

선택자는 다르지만 css속성이 같을 경우 묶어서 쓰기 가능

```css
#wrap .logo,
#wrap .navi {
	text-align: center;
}
```

## 가상 클래스 선택자

p.131

링크걸린 글자에 부여

```css
a:link {
	color: #222;
}
a:visited {
	color: coral;
}
a:hover {
	color: cornflowerblue;
	text-decoration: underline;
}
a:active {
	background: gold;
}
a:focus {
	background: green;
}
```

```css
a:hover,
a:active,
a:focus {
	color: green;
	text-decoration: underline;
}
```

focus는 접근성 측면에서 사용

p.132

last-child : 같은 태그중 마지막 태그

수동클래스 선택자?

first-child

p.195

css3 속성

## 구조 가상 클래스

### nth-child(n)

부모를 기준으로 n번째 자손 요소(element)를 선택한다.

다른 형제요소도 순서에 포함하는 단점 있음

index = nth-child(1) - 일반 정수가 들어간다

even = nth-child(even) - 짝수만 선택한다

odd = nth-child(odd) – 홀수만 선택한다.

div p:nth-child(2) div요소안에서 두번째 p요소에 스타일 적용

div p:nth-child(2n+1) div요소안에서  세번째 p요소에 스타일 적용

div p:nth-child(even) div요소안에서 짝수 번째 p요소에 스타일

적용

div p:nth-child(odd)  div요소안에서 홀수 번째 p요소에 스타일

적용

:nth-last-child(n)

끝에서 부터 n번째 자식 요소에 스타일을 적용한다.

### :nth-of-type(n)

부모로 부터 지정된 요소와 지정된 값이 일치하는 요소를 찾는다.

p:nth-of-type(3) 부모로 부터 세번째 자식인 p 요소 선택

:nth-last-of-type(n)

끝에서 부터 n번째 자식 요소에 스타일을 적용한다.

## 자손/후손 선택자

`.class >p{}`

: .class 안에 있는 p 에만 속성 적용

## 형제 선택자

인접 형제 선택자

1.같은 부모를 가진 형제 요소 중 바로 옆에 있는 요소에만 스타일을 적용한다.

2.선행 선택자와 후행 선택자를 + 로 구분하여 선언한다.

[선택자]  + [선택자]

```css
/*h1 태그의 바로 뒤에 위치하는 h2 태그의
color 속성에 red 키워드를 적용합니다. */
h1 + h2 {
	color: red;
}
```

```css
/* h2 중 마지막에만 적용 */
h1 ~ h2:nth-of-type(4) {
	color: palegreen;
}
```

기본 형제 선택자

1.바로 옆에 있지 않아도 인접하여 등장하는 모든 형제 요소에

다 적용된다.

2.기본 형제 선택자를 정의할 때는 ~(틸드)로 표시한다.

[선택자] ~[선택자]

```css
/* h1 태그의 뒤에 위치하는 모든 h2 태그의
background-color 속성에 orange 키워드를 적용합니다. */
h1 ~ h2 {
	background: orange;
}
```

## before, after 선택자

::before , ::after
특정 요소의 내용 앞이나 뒤에 텍스트같은 콘텐츠를 추가할 수 있다.
p::before{content: “내용”;}

## 속성 선택자

선택자[속성] 특정한 속성이 있는 태그를 선택한다.

`img[alt]{border:3px solid black;}`

:alt 속성을 가진 이미지에만 border 적용

`input[type="text"]{background: goldenrod;}`

input 태그 중 type=”text”에만 적용

선택자[속성~=값] 속성의 값과 일치하는 요소를 찾아 스타일을 적용한다.
`h2[title~= “베스트”]{background-color:yellow;}`

선택자[속성^=값] 지정한 문자로 시작하는 속성값에 대한 스타일을 적용한다.
`a[class ^= "bg"]{font-style:italic;}`

> 처음 시작하는 속성값에 bg가 있어야 적용됨

선택자[속성$=값] 지정한 문자로 끝나는 속성값에 대한 스타일을 적용한다.
`img[src $=“.gif”{border:5px solid black;}`

선택자[속성$=값] 지정한 문자로 끝나는 속성값에 대한 스타일을 적용한다.
`img[src $=“.gif”{border:5px solid black;}`

선택자[속성*=값] 사용자가 지정한 속성 값의 앞이나 뒤, 중간등 어느 위치에 있든지 해당 값이 포함되어 있으면 스타일이 적용된다.
예를 들어 class이름이 text가 들어 있는p요소에 효과를 줄려면 다음과 같이 한다
`p[class *="text"]{font-style:italic;}`

선택자[속성 ㅣ=값] 속성값이 특정 단어 뒤에 바로 –가 있는 요소를 선택한다.

`p[class |="bg"]{background: royalblue;}`

:checked radio 체크박스 선택시

`input:nth-of-type(4):checked ~ .tab-item ul:nth-of-type(4){display: block;}`

input 선택시에만 형제메뉴 보이게 함

# 스프라이트 이미지

스프라이트 이미지 : 하나의 이미지파일에 여러개의 이미지들을 묶어놓은 것

: 하나의 이미지 판에 여러 이미지를 배치한 것

이미지 스프라이트를 사용하면 한번에 필요한 이미지를 내려받으므로 서버에 요청하는 횟수를 줄이고 데이터 전송량을 절감하게 됨

여러 이미지가 있는 한 이미지 판에서 특정 이미지 만을 좌표값을 통해 불러오는 방식

(background-position 사용)

```css
<style>
.ex{ background-image: url(./images/sp_main_v200116.png); background-repeat:  no-repeat;}
.ex1{width: 72px; height: 50px;}
.ex2{width: 48px; height: 48px; background-position: -60px -61px;}
</style>
```

# object-fit

이미지 태그로 불러온 자손 이미지나 동영상을 부모요소 안에 맞추는 것

속성값

fill : 이미지의 비율을 무시하고 부모요소에 채움

cover : 이미지의 비율을 유지하면서 긴쪽에 맞춤

container : 이미지의 비율을 유지하면서 짧은 쪽에 맞춤

# 아이콘 폰트

폰트-베타방식

아이콘을 폰트로 불러들여 깨짐현상이 없게 함

폰트 사이즈로 크기조절 가능 색 변환이 쉬움

# Transition

변환 중간 과정을 만들어줌

:hover 사용 시 에만 적용 가능

단축속성 : `{transition : 1s }`

다른 기본적인것은 생략 가능하지만 진행시간은 필수, 생략불가

:hover에 transition 주는 것보다 변형되는 개체 기본 속성에 trasition 속성을 줘야 hover 전,후 변경 효과가 자연스러움

속성:

transition-property :변형하고 싶은 속성 입력 / 기본값-all (생략가능)

transition-duration : 진행되는 시간 생략 불가, 필수

transition-timing-function: 지속시간

liner : 기본, 등속

ease :느리게 시작했다가 빨라지고 다시 느려짐

ease-in : 점점 빨라짐

ease-out : 점점 느려짐

ease-in-out : 처음과 끝이 느림

cubic-bezier(n,n,n,n) : 값을 입력하여 조정

[cubic-bezier.com](https://cubic-bezier.com/#.17,.67,.83,.67)

transition-delay: 일정 시간이 지난 후 작동함

여러속성 줄때는 , 사용

```css
.ex4 .box {
	width: 10px;
	height: 100px;
	background-color: rosybrown;
	margin: 10px;
	overflow: hidden;
	opacity: 0.1;
	transition: width 1s, opacity 2s 1s, background 1s 3s;
}
/*너비값 1초 동안 변경, 투명도 2초동안 변경 1초 후에 변경시작, 배경 1초동안 변경 2초후에 변경 시작*/
```

```css
<style>
.ball{width: 200px; height: 200px; background-color: cadetblue; transition: 0.5s;}
.ball:hover{width: 150px; height: 150px; border-radius: 50%;}
</style>
```

# Transform

transform-origin: 중심축 지정하는 속성 : 키워드, px % (기본-가운데 중심)

`transform : scale3d{x,y,z}`

3d

자손의 너비,높이 값 모를때 가운데로 보내기

`position: absolute; left: 50%; top: 50%; transform: translate(-50%, -50%)`

```css
.wrap {
	width: 400px;
	height: 400px;
	border: 5px solid darkblue;
	position: relative;
}
.box {
	background-color: darkmagenta;
	display: inline-block;
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%, -50%);
}
```

transform-style: 자손 요소에 3d 효과주는 속성

속성값: flat(2d-기본값), preserce-3d,

# 애니메이션

`@keyframes 영문이름{ from{} to{} }`

시작과 종료를 다르게 설정

animation-name: 애니메이션 이름으로 호출해서 사용

animation-duration: 애니메이션 실행 시간

animation-iteration-count: infinite; 애니메이션 반복

```css
.ball {
	width: 150px;
	height: 150px;
	background: royalblue;
	border-radius: 50%;
	text-align: center;
	line-height: 150px;
	position: absolute;
	animation-name: ballmove;
	animation-duration: 5s;
	/*애니메이션 'ballmove'호출, 애니메이션 실행시간 5초간*/
	animation-iteration-count: infinite;
}
/*애니메이션 무한반복*/
@keyframes ballmove {
	from {
		left: 10px;
		top: 50px;
		transform: rotate(0deg);
	}
	to {
		left: 1000px;
		top: 50px;
		transform: rotate(360deg);
	}
}
/*애니메이션: 각도0에서 시작해서 360도 회전해서 끝*/
```

축약

`{ animation: animation-name, duration, count, direction, timing }`

animation-direction: alternate 다시 처음 위치로 돌아감

```css
@keyframes myAni {
	0% {
		background-color: brown;
		left: 10px;
		top: 50px;
	}
	25% {
		background-color: cadetblue;
		left: 800px;
		top: 50px;
	}
	50% {
		left: 800px;
		top: 800px;
	}
	75% {
		left: 10px;
		top: 800px;
	}
	100% {
		background-color: brown;
		left: 10px;
		top: 50px;
	}
}
/* %로 지정 */
```

animation-fill-mode

: 애니메이션을 실행하기 전 대기 상태와 종료 후의 상태를 지정

속성 값: none, forwards, backwards, both

none: 대기 시에는 스타일에 적용한 효과로 적용, 종료 시에는 애니메이션 실행 전 상태로 되돌려 종료

forwards: 대기 시에는 스타일에 적용한 효과로 적용, 종료 시에는 종료 프레임에 설정한 스타일을 적용하고 종료

backwards: 대기 시에는 시작 프레임에 설정한 스타일 적용, 종료 시에는 애니메이션 실행 전 상태로 되돌려 종료

both: 대기 시에는 시작 프레임에 설정한 스타일 적용, 종료 시에는 종료 프레임에 설정한 스타일 적용하고 종료

키프레임 비율: %로 지정

전체 애니메이션 재생 시간 지정 > 전체 시간에서 각 애니메이션 시간 %계산

animation-play-state: paused/ runnging (기본값)

애니메이션을 제어하는 속성

# border-radius

1. border - radius 속성은 요소 박스 테두리 선의 둥근 모서리 형태를 지정한다.

border-radius : 속성값 (px, %);

2. 속성값은 top-left, top-right, bottom-right, bottom-left 순으로 지정한다. (시계방향, 대각선 속성끼리 동일값 지정가능 - 사선으로 같을 경우에는 한번씩만 쓰면 됨 )

3.border-\*-radius : 속성값;

border-top-left-radius (왼쪽 위)

border-top-right-radius(오른쪽 위)

border-bottom-left-radius(왼쪽 아래)

border-bottom-right-radius(오른쪽 아래)

4. border-radius : 가로 방향 값 / 세로 방향 값

# 상속

css 모두 자손이 상속을 받을 수 있게 함 > 코드를 중첩되지 않게 해서 단순하게 만들 수 있음

태그는 부모 > 자식 순으로

**상속 기준은 <p> 태그 > p 태그에 적용할 내용을 부모 태그에 넣음**

상속 받지 않을 부분은 새로 작성

배경색상, 이미지는 상속 불가

```html
<style>
	body {
		color: #665544;
		font-size: 18px;
		font-family: "Myriad Pro", sans-serif;
	}
	h1 {
		color: #0088dd;
		font-size: 50px;
		font-weight: normal;
		font-family: Georgia, "Times New Roman", Times, serif;
	}
	h2 {
		color: #0088dd;
		font-size: 30px;
		font-weight: normal;
	}
	.t1 {
		color: #0088dd;
		text-transform: uppercase;
		letter-spacing: 0.2em;
	}
	strong {
		font-weight: 100;
	}
	.t2 {
		color: #665544;
		font-weight: 700;
	}
	em {
		font-style: normal;
		color: #0088dd;
	}
</style>
```

# 서체 (Font)

글자에 관련된 속성

: 글꼴, 글자 크기, 글자 굵기, 기울임 여부, 줄 간격, 대소문자 여부, 글자 색상 등

<style type="text/css"> : HTML X 방식

## font

축약 속성

`font: {font-weight, font-style, font-variant, font-size/line-height, font-family}`

font: {12px/1.5 "Arial"}

없는 속성은 안 써도 됨 그러나 글자 크기, 글꼴 생략 불가

## font-family

1.웹문서에 사용할 폰트를 지정하는 속성이다.

2.하나이상의 폰트를 선언할 수 있으며 콤마(,)로 구분한다.

3. 사용자의 컴퓨터 시스템에 선언한 글꼴이 없을 경우를 대비해서 여러 개의 글꼴을 지정해야 한다. (비슷한 서체를 여러개 지정)

4. 폰트의 맨 마지막에는 범용 폰트 그룹을 지정해야 한다.

`선택자 {font-family:"글꼴이름" , "글꼴이름“; 범용 폰트 그룹}`> 마지막에 범용 폰트 그룹 작성

`p{font-family:"돋움", "돋움체", "굴림", "굴림체", sans-serif;}`

`p{font-family: Arial, "Times New Roman"; }`

> 영문은 "" 하지 않아도 되지만 서체 이름 중간에 스페이스가 있는 폰트의 경우 "" 안에 넣어야 함 

## font-size

웹문서의 글자 크기를 지정한다.  단위는 절대 단위와 상대 단위가있다.

절대 단위 : px 픽셀, 폰트 크기 고정, 부모 폰트 크기 변경에 영향 받지 않음

상대 단위: %, 계층구조, 폰트 자신이 속한 부모 폰트의 영향을 받음, 부모폰트에 따라 변경됨

```html
<style>
.parent{font-size: 50px;}
.f1{font-size: 12px;}
.f2{font-size: 150%;}
</style>

<body>
<div class="parent">
<p class="f1">본문 글자 크기는 12px로 지정합니다.</p>
<p class="f2">본문 글자 크기보다 1.5em크기로 지정합니다.</p>
</div>
</body>
```

글자의 기본 크기를 지정하고자할 때는 body요소에 선언하여 다른 요소가 상속받도록 할 수 있다.

## font-weight

: 두께를 지정 (속성 값 - bold, normal)

font-weight: bold / bolder / 100~900 (100~300 light, 400 nomal, 500~900 bold) / normal

`.b{font-weight: bold;}`

## font-style

속성 값 - Italic, normal

`.s{font-style: normal;}`

address 태그 : 자동 이탤릭체 적용(p.38) > 태그의 기본 속성 없앨 때도 사용함

## Text-Transform

```html
<style>
	.t1 {
		text-transform: uppercase;
	}
	.t2 {
		text-transform: lowercase;
	}
	.t3 {
		text-transform: capitalize;
	}
	.f1 {
		font-variant: small-caps;
	}
</style>
```

text-transform: 영문 대소문자 변경

uppercase : 전부 대문자
lowercase : 전부 소문자
capitalize : 첫번째 단어만 대문자

font-variant: small-caps : 소문자를 작은 대문자로 변경

```css
a {
	text-decoration: none;
	color: inherit;
}
```

a태그 초기화

inherit : 부모 색상 상속

## line height (행간)

줄 간격을 수치로 지정한다 (%, em, px)

행간은 절대 단위보다는 상대 단위를 사용 > 글자 크기에 따라 자동으로 행간 조정되게 하기 위해서

행간의 기준은 문단태그<p>

버튼 > 한 줄의 경우 행간으로 가운데 조정 > line-height 와 height를 같이 지정

`.btn{width: 170px; height: 50px; line-height: 50px;}`

css의 경우 행간을 글자의 수직중앙을 기준으로 작동함

# 문단 (Paragraph)

가로/세로 정렬, 들여쓰기, 대소문자, 줄치기, 자간 조절

## text-align

문단을 블록의 왼쪽, 가운데, 오른쪽, 양쪽 등으로 정렬

속성 값: left, center, right, justfy(양쪽)

블록요소에만 사용가능함

```html
<style>
	.align1 {
		text-align: left;
	}
	.align2 {
		text-align: right;
	}
	.align3 {
		text-align: center;
	}
	.align4 {
		text-align: justify;
	}
</style>
```

## text-indent

문단의 첫머리를 들여쓰기 함

속성 값: px, % (숫자 수치 -, + 둘 다 가능)

블록요소에만 사용가능함

```html
<style>
	.in {
		text-indent: 50px;
	}
	.out {
		text-indent: -50px;
	}
</style>
```

## text-decoration

글자에 밑줄, 윗줄, 가운데 줄을 치거나, 원래 있던 밑줄을 제거함

속성 값: underline, overline, line-throught, none(밑줄 제거)

```html
<style>
	.d1 {
		text-decoration: overline;
	}
	.d2 {
		text-decoration: line-through;
	}
	.d3 {
		text-decoration: underline;
	}
</style>
```

a 태그 링크의 언더라인 제거나 색상변경 시 사용

`a{color: black; text-decoration: none;}`

`a:hover{color: blue; text-decoration: underline;}`

> 마우스를 가져갈 때만 블루로 변경, 언더라인 생성

## letter-spacing

자간은 브라우저 마다 약간씩 다르게 보임 > 줄바꿈 약간씩 차이남

글자와 글자간의 간격을 부여 (문자간격)

속성 값: px, %

픽셀로 하려면 그냥 눈대중으로..

포토샵 그대로 하려면 `포토샵의 자간/1000em`

: 포토샵의 1000이 CSS의 1em(현재 폰트크기의 100%)과 일치

```html
<style>
	.letter {
		font-size: 20px;
		letter-spacing: -0.025em;
	}
	.word {
		word-spacing: 5px;
	}
</style>
```

## word-spacing

: 단어 사이의 간격 조정

`.word{word-spacing: 5px;}`

## 말줄임 속성

text-overflow : clip(기본값)/ellipsis

clip: 글자를 잘라냄

ellipsis : 말줄임표로 나타냄

> 한 줄만 가능함

```css
.single {
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
/*말줄임표로 나타내는 방법*/
```

white-space : 공백 처리 방법 지정

nomal, nowrap, pre, pre-line, pre-wrap

두 줄 이상일때

-webkit-line-clamp : 블록 컨테이너의 콘텐츠를 지정한 줄 수만큼으로 제한함

```css
.double {
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-box-orient: vertical;
	-webkit-line-clamp: 3;
}
```

display 속성을 -webkit-box 또는 -webkit-inline-box로

-webkit-box-orient 속성을 vertical로

overflow 속성 또한 hidden으로 설정

## word-break

word-break는 줄바꿈을 할 때 단어(공백) 기준으로 할 지 글자 기준으로 할 지 정하는 속성은 입니다.

word-break: normal | break-all | keep-all | initial | inherit;
normal : CJK 문자는 글자 기준으로, CJK 이외의 문자는 공백을 기준으로 줄바꿈합니다.
break-all : 글자 기준으로 줄바꿈합니다.
keep-all : 공백 기준으로 줄바꿈합니다.
initial : 기본값으로 설정합니다.
inherit : 부모 요소의 속성값을 상속받습니다.

word-break: 문단이 아닌 것도 줄바꿈을 해줌

## word-wrap

word-wrap 속성은 긴 텍스트를 강제로 끊어 줄바꿈을 해주는 속성이다.
word-wrap 속성값
normal : 기본값으로 글자가 끊어지지 않고 한 줄에 계속 표시.
break-word : 강제로 끊어서 줄바꿈을 함.

# 색상(Color)

\*재플린

## 색상 표기방법

RGB 색상코드 : (HEXA-16진수)

(ex: #ff0000 = #f00 같은 거 하나씩 생략가능 - 빨강 ; 앞에서부터 두자리씩 R G B)

`.color02{color: rgba(R, G, B);}`

RGBA : 투명도 적용가능

`.color02{color: rgba(R, G, B, Alpha);}` > 투명도는 1=100%

HLS

.color03{color: hsl(hue, saturation, lightness);}

`.color03{color: hsl(299, 100%, 60%);}`

HLSA

`.color04{color: hsla(299, 100%, 60%, 0.8);}`

키워드 (ex: orange) - 기본방식

# 필터

보통 이미지에 hover할 때 변경하는 용도로 사용

```css
.box1 img {
	filter: blur(10px);
}
.box2 img {
	filter: brightness(0.5);
}
.box3 img {
	filter: contrast(200%);
}
.box4 img {
	filter: grayscale(100%);
}
.box5 img {
	filter: hue-rotate(270deg);
}
.box6 img {
	filter: invert(100%);
}
.box7 img {
	filter: saturate(0.5);
}
.box8 img {
	filter: sepia(100%);
}
.box9:hover img {
	filter: grayscale(100%);
}
/*hover 시에 이미지 흑백 변경*/
```

# 배경

## 배경색 적용하기

```css
.bg1 {
	background-color: rgba(123, 165, 5, 0.4);
}
```

## 배경 이미지 적용하기

### 배경 이미지 반복

`background- image: url(파일경로);`

1.배경 이미지를 지정할 수 있다.

2.배경으로 지정된 이미지는 기본적으로 반복적으로 보여진다. (패턴처럼)

3.배경이미지와 배경색을 지정하면 background-color속성이 있어도 배경 이미지에 가려져 배경 색상이 보이지 않는다.

`background-repeat: no-repeat;`

### 배경 이미지 위치 적용

1.배경 이미지의 위치를 변경할 때 사용한다.

2.속성에는 left, top, right, bottom등의 키워드와 픽셀이나 퍼센트로 지정할 수 있다.

```css
background-position: left/ center / right top/center/bottom;

background-position: 50%  50%;

background-position: 200px   500px;
```

### 배경 이미지 고정 적용하기

`background- attachment`

1.배경 이미지를 항상 같은 자리에 고정시킬 때 사용한다. 2.속성에는 scroll과 fixed가 있고 기본값은 scroll이다.

scroll - 콘텐츠가 스크롤되면 배경도 따라서 스크롤 된다.
fixed - 배경은 고정되고 콘텐츠 내용만 스크롤 된다.

### 배경이미지 속성 단축 코드

배경 관련 속성을 하나의 속성으로 지정하는 방식이다.

`backgroun : background-image background-repeat background-position background- attachment`

```css
.bg5 {
	background: rgba(123, 165, 5, 0.4) url(./images/sun.png) no-repeat center center;
}
```

# 박스

<aside>
🔥 **width height는 블록태그에만 적용

</aside>

## width

박스의 가로 사이즈, 여백 포함하지 않는 크기 px, %, em 등의 단위로 설정 가능 (기본값 auto)

width 값은 블록 태그에만 적용 가능

블록태그 기본 width 100%

반응형 웹에서는 상대단위로 하는게 원칙 > 범위 벗어나지 않게 하기 위해서

## height

박스의 세로 사이즈, 여백 포함하지 않는 크기 px, %, em 등의 단위로 설정 가능(기본값 auto)

높이값 속성은 레이아웃 작업에서 float 해제할 대 쓰는 경우가 있음

보통 높이값은 지정 안함 > 지정하는 경우: 백그라운드 이미지 불러오는 경우... 겹치지 않게 조정

## 여백

안 여백 padding

바깥 여백 margin

테두리 border

### margin

꼭 들어감

auto : 항상 컨텐츠를 중간으로 배치 > 보통 좌우는 auto 기본

top, bottom은 블록태그에만 적용 인라인 X

margin은 border을 기준으로 바깥쪽 여백을 나타낸다.

margin-top  ; 바깥쪽 위쪽 여백

margin-right  : 바깥쪽 오른쪽 여백

margin-bottom : 바깥쪽 아래쪽 여백

margin-left : 바깥쪽 왼쪽 여백

대부분 문제가 되는건 top... >

마진 중첩현상 : 위 블록이 bottom 50px 이고 밑 블록이 top 80px일 경우 둘 중에 수치가 높은 80px로 적용됨

> > 그냥 큰 값을 한 블럭에만 마진 적용하는게 나음

margin : 상,하 좌,우 바깥쪽 여백이 같은 경우

margin : 상,하 바깥쪽 여백이 같고 좌,우 바깥쪽 여백이 같은 경우

margin : 상,하 바깥쪽 여백이 다르고 좌,우 바깥쪽 여백이 같은 경우

margin : 상,하 좌,우 바깥쪽 여백이 모두 다른 경우

### padding

padding-top ,  padding-right ,  padding-bottom , padding-left

padding 은 auto X

적용하면 박스 크기가 커짐

예) width 값 800px일 경우 패딩 상하좌우 40px주면 880px로 늘어남 > 패딩값에 따라 width값 조정

블록, 인라인(제약은 있음) 가능

축약 > top부터 시계방향으로 순서

padding : (top right bottom left); - 상,하 좌,우 안쪽 여백이 같은 경우

padding : (top bottom) (left right); - 상,하 안쪽 여백이 같고 좌,우 안쪽 여백이 같은 경우

padding : top (left right)  bottom; -  상,하 안쪽 여백이 다르고 좌,우 안쪽 여백이 같은 경우

padding : top right bottom left; -  상,하 좌,우 안쪽 여백이 모두 다른 경우

## Border 테두리

border는 요소 박스의 테두리를 지정한다.

<기본>

border-width : 박스의 경계의 선두께

border-top-width : 박스의 경계의 윗 부분의 선두께

border-right-width : 박스의 경계의 오른쪽의 선두께

border-bottom-width : 박스의 경계의 아랫 부분의 선두께

border-left-width : 박스의 경계의 왼쪽의 선두께

border-color : 박스의 경계의 선두께 색을 결정

border-style : 박스의 경계의 선두께 모양

### border 단축 속성

border-top: 선두께  스타일  색상값

border-right: 선두께  스타일  색상값

border-bottom: 선두께  스타일  색상값

border-left: 선두께  스타일  색상값

border: 선두께  스타일  색상값

```css
.b3 {
	border: 5px solid purple;
}
.b4 {
	border-bottom: 5px solid purple;
}
```

none: 보더 속성을 없애는 것, 보더를 안보이게 가릴 때 사용

`.b1{border: none}`

## Vertical-align

top, middle, bottom

img, input, select, 테이블의 th, td 에 사용

이미지와 텍스트 인라인으로 같이 넣을 경우 텍스트는 이미지보다 하단에 배치됨

이를 조정하기 위한 태그

# list-style-type 속성

list-style-type : none <ul의 불릿> <ol의 번호>

ul : disc, circle, square, none

ol : decimal, decimal-leading-zero, lower-roman, upper-roman, lower-alpha, upper-alpha, armenian, geogiam

## list-style-position 속성

불릿이나 번호 들여쓰기, 내어쓰기

## list-style-image 속성

불릿이나 번호 대신 이미지

위치지정 안됨

```css
.list5 {
	list-style-image: url(./li_bull.gif);
}
```

## background로 불릿아이콘 적용

list-style-image 대신 많이 사용

```css
.list6 {
	list-style-type: none;
}
.list6 li {
	background: url(./li_bull.gif) no-repeat 0 50%;
	padding-left: 17px;
}
```

아이콘이 배경에 위치되기 때문에 위치 조정 가능

아이콘 크기 + 리스트 글과 아이콘 사이 간격 으로 패딩넣어서 간격 조절

border-collapse: collapse;

테이블 초기화

태그전체 투명도 : opacity

# 레이아웃

## float

left, right

위로 떠서 이동 (부모 범위 밖으로 나가는 것은아님)

인라인 태그들끼리 나란히 배치하고 싶을 때 (ex 이미지 옆에 텍스트 배치할 때) 사용

자손이 부모안에서 가로로 나란히 배치되려면 자손의 너비와 여백값의 합이 부모의 너비보다 작아야만 함. 아니면 밑으로 밀려내려가서 배치

자손이 모두 float 되어 부모의 높이값이 사라질 경우

> float를 해제하는 방법

1. float된 박스들의 바로 다음 박스에 clear: both > 형제 박스들에만 적용가능, 박스 없을 경우 불가
2. float된 박스들을 감싸는 박스를 다시 float: left 한다 > 그 float까지 연쇄적으로 해제해야 하며 width값을 주어야 크로스 브라우징 됨
3. float된 박스들을 감싸는 박스에 overflow : auto (또는 hidden)한다 > 세로 스크롤바가 생길 경우 사용할 수 없으며 width값을 주어야 크로스 브라우징 됨
4. float된 박스들을 감싸는 박스에 heigt 값을 준다 > 본문내용에는 높이를 주지 않으므로 세로 사이즈가 불변일 경우 아니면 사용불가, 높이 값을 알때만 사용, 보통 height를 주면 유지 보수가 힘들기 때문에 필요한 경우가 아니면 사용X
5. float된 박스들을 감싸는 박스에 가상요소 : after를 주어 해제한다. > 실질적으로 제일 많이 씀

    ```css
    #content::after {
    	content: "";
    	display: block;
    	clear: both;
    }
    ```

    자손에 float적용하면 부모에 위에 코드 작성 > 높이값 확보위해

    또는 내용이 많은 자손 부모안에 하나 남기고 옆 블록 너비만큼 margin넣어서 조절

    > float 사용권장이나 구조에 따라 조절 가능

## clear

left right both

float 된 박스들의 아래 박스에게 주변을 흐르지 않고 원래대로 배치되도록 하는 속성

float를 해제시켜주는 역할, float 영향에서 벗어나게 함

# 플렉서블 박스 레이아웃

flexible box layout

그리드 레이아웃을 기본으로 플렉스 박스를 원하는 위치에 배치하는 것

여유공간에 따라 너비나 높이, 위치를 자유롭게 변형할 수 있음

display: flex / inline-flex

배치 요소들을 감싸는 부모 요소를 플렉스 컨테이너로 지정

flex-direction 속성

row, row-reverse, colum, colum-reverse

flex-wrap 속성

플렉스 항목을 한 줄 또는 여러 줄로 배치

no-wrap, wrap, wrap-reverse

flex-flow 속성

플렉스 배치 방향과 여러 줄 배치를 한꺼번에 지정

기본 값은 flex-flow: row nowrap

order 속성

플렉스 항목의 배치 순서 바꾸기

order값에 지정된 순서에 따라 배치됨

justify-content 속성

플렉스 항목을 주축 방향으로(가로) 배치할 때 의 배치 기준

flex-start, flex-end, center, space-between, space-around

align-content 속성

플렉스 항목 세로 정렬

flex-start, flex-end, center, space-between, space-around

align-items

flex 부모 안에 있는 요소들이 item

stretch, flex-start, flex-end, center, base-line

flex, flex-grow, flex-shrink

grow, shink : 부모의 여백따라 조정

flex 항상 일정한 비율을 유지

# 고정형/유동형 레이아웃

fixed layout : 너비값 고정, 단위 - px

liquid layout :화면, 디바이스 해상도에 따라서 너비값이 자동 조정, 단위 - %

`(자손의 너비 값 / 부모의 너비 값) * 100`

`(자손의 여백 값 / 부모의 너비 값) * 100`

단위

px, %, em, rem, vw, vh

vw(viewport width), vh(viewport height): 브라우저 화면기준/ 모바일, 반응형에 사용(상대단위)

1vw: 화면 너비의 1%

1vh : 화면 높이의 1%

vw 계산기 활용해서 계산

폰트크기의 경우 vw로 지정하면 반응형에서 오류가 날 경우가 있으니 최소크기를 같이 정해주는게 좋음

```css
.wrap h1 {
	font-size: 2vw+1rem;
	color: #fff;
	text-align: center;
}
```

# 웹폰트

[CSS Web Fonts](https://www.w3schools.com/css/css3_fonts.asp)

외부에서 웹폰트 호출: 구글웹폰트

<aside>
🔥 웹폰트는 가장 먼저 호출

</aside>

font-face

@font-face

```css
/*내부에 저장된 웹폰트 호출*/
@font-face {
	font-family: "nbg";
	src: local("NanumBarunGothic"), local("Nanum Barun Gothic"), local(
			"나눔바른고딕"
		), url(./font/NanumBarunGothic.woff2) format("woff2"), url(./font/NanumBarunGothic.woff)
			format("woff"), url(./font/NanumBarunGothic.ttf) format("truetype");
	font-weight: 400;
}
```

# 그라디언트

```css
background:linear-gradient(direction, color-stop1 location(%), color-stop2, color-stop3, ...)
background: radial-gradient(shape at position, start-color, end-color);
```

[Ultimate CSS Gradient Generator from ColorZilla](https://www.colorzilla.com/gradient-editor/)

[CSS3 Patterns Gallery](https://projects.verou.me/css3patterns/)

# 쉐도우

## 박스

box-shadw: 속성 0 0 0 0 rgba(0, 0, 0, 0);

```css
.inset {
	box-shadow: inset 0px 10px 10px rgba(0, 0, 0, 0.65);
}
.outset {
	box-shadow: 0px -10px 20px rgba(0, 0, 0, 0.65);
}
.blur {
	box-shadow: rgba(0, 0, 0, 0.65);
}
.spread {
	box-shadow: 0px 10px 40px 50px rgba(0, 0, 0, 0.65);
}
.shadow {
	box-shadow: 6px 6px 20px #f6ae00, 5px 5px 5px #ff0000, 3px 3px 3px #00f;
}
/*그림자 여러 개 적용 가능함*/
```

## 텍스트

```css
h1 {
	font-size: 50px;
	color: royalblue;
	text-shadow: 5px 5px 2px rgba(0, 0, 0, 0.7);
}
/*그림자 여러 개 적용 가능*/
```

# 디스플레이

```css
.list li {
	background-color: royalblue;
	display: inline;
}
.block span {
	background-color: sandybrown;
	width: 100px;
	height: 50px;
	margin-top: 50px;
	display: block;
}
.in-bl span {
	background-color: seagreen;
	width: 100px;
	height: 50px;
	margin-top: 50px;
	display: inline-block;
}
/*인라인이라 가로배치되면서 width, height, margin 적용됨*/
```

block : 넓이가 부모영역에 100%로 채워짐

inline-block : 넓이가 글자 크기 만큼만 채워짐

table : vertical-align을 사용하기위해 사용

table-cell : 위와 마찬가지 (table 태그가 있어야 사용가능)

```jsx
<style>
*{margin: 0; padding: 0;}
ul{list-style: none;}
a{text-decoration: none;}
.navi{width: 1000px; margin: 20px auto;}
.gnb{display: table; width: 100%;}
.gnb::after{content: "";display: block;clear: both;}
.gnb li{width: 25%;display: table-cell;background: gold; text-align: center; vertical-align: middle; height: 50px;}
.gnb li a{  }
</style>
</head>
<body>
<nav class="navi">
<ul class="gnb">
<li><a href="#">MENU1</a></li>
<li><a href="#">MENU2</a></li>
<li><a href="#">MENU3</a></li>
<li><a href="#">MENU4</a></li>
</ul>
</nav>
</body>
```

# Visibility

```css
.vi {
	visibility: hidden;
} /*자리가 그대로 비워진상태에서 사라짐*/
.di {
	display: none;
} /*자리가 아예없어지고 사라짐*/
```

# Overflow

overflow는 콘텐츠 내용이 박스의 크기를 넘어가는 경우에 사용한다.

기본값은 visible 이다.

overflow : visible;

박스 크기를 무시하고 콘텐츠 내용을 모두 보이게  한다.

overflow : hidden;

박스 크기만큼만 콘텐츠 내용이 보이고 나머지 부분은 숨긴다.

overflow : scroll;

콘텐츠 내용에 상관없이 박스에 스크롤바를 생성한다. 만약 콘텐츠 내용

보다 박스의 크기가 클 경우 스크롤 바는 비활성화 된다.

(가로, 세로 둘다 생성)

overflow : auto;

콘텐츠 내용이 박스 크기보다 많으면 자동으로 스크롤바를 생성한다.

(세로 스크롤만 생성)

# background-size

크기조절

px, %, contain, cover, auto, length

기본값: auto - 원래 이미지 사이즈

contain: 이미지가 가로 세로 중 짧은 쪽에 맞춰짐 (빈 공간이 남게 됨)

cover: 이미지가 가로 세로 중 긴 쪽에 맞춰짐

> 이미지 비율 고려, 가로를 길게

# 표스타일

```css
<style>
table{border: 1px solid #333; width: 500px;caption-side: bottom;}
tr, td, th{border: 1px solid #888;}
</style>
```

## border-collapse

table {border-collapse: collapse;}

셀 간격 초기화

## border-spacing

border-spacing: 30px;

셀 테두리 사이 거리 지정

## empty-cell

empty-cells: show/hide

기본- show

빈 셀 안보이게 함

## vertical-align

vertical-align: top / bottom / middle

셀 안에서의 수직 정렬 방법

적용 가능한 태그 한정적

## table-layout

table-layout: fixed / auto

fixed: 너비고정, 자동줄바꿈

auto: 기본값, 셀 내용에 따라 셀의 너비 변경

# box sizing

box-sizing: content-box / border-box

기본값: content-box

.`class{box-sizing: border-box;}`

# position

나란히 있는 경우에는 float 겹치는 경우에는 position

margin: 0 auto 로 가운데 정렬하는 경우는 posotion relative 일때만 가능 absolute일때 불가능

float의 경우 형제 순서에 따라 진행해야하지만 포지션은 순서 관계없이 위치 지정 가능

태그를 겹치게 할 수 있음

static : 기본값

absolute: 부모박스가 기준 : 음수입력할 경우 부모박스 밖에 있는 것 처럼 보이지만 부모안에 포함되어 있어서 같이 움직임 / 자손 전체에 포지션 주면 부모 높이 값 없어짐 -하나라도 남겨두는게 좋음 어쩔 수 없을 경우에는 부모에 height값 줘야함 / 많이 움직일때 사용

내용에 맞춰 width값 변경(지정안할시)

fixed

relative: 상대좌표값 > 포지션이 지정되는 상자 왼쪽 상단이 기준 / 조금씩 움직일때 사용

> 기준은 항상 왼쪽 위 이기때문에 부모의 가운데에 위치하고 싶을 경우 px 보다 %로 정하는게 나음

`{position:absolute; left: 50%; top: 0; margin-left: -25px;}`

이렇게 지정

`.b2{position: absolute; right: 0; top: 0;}`

```css
#wrap {
	width: 600px;
	height: 600px;
	background: #eaeaea;
	position: relative;
} /*기준이 부모임을 알려줘야 함*/
.box2 {
	width: 100px;
	height: 100px;
	background: greenyellow;
	position: absolute;
	left: 30px;
}
```

# z-index

```css
.fix {
	width: 1740px;
	margin: 0 auto;
	position: relative;
}
.header {
	height: 70px;
	border-bottom: 1px solid rgba(0, 0, 0, 0.4);
	padding-top: 10px;
	box-sizing: border-box;
	position: absolute;
	left: 0;
	top: 0;
	width: 100%;
	z-index: 1;
}
/*position absolute로 헤더영역 없애고 하단 비주얼 이미지로 채움
영역 확보 위해 width값 100%지정*/
/*z-index: position absolute로 주는 경우 밑에 비주얼이 위에 가리기 때문에 a태그 링크가 걸리지 않음 이를 위로 올려주기 위해 z-index 통해 헤더를 위로 올리는 작업을 해야 링크가 사용가능해짐*/
/*원칙상은 height값 안주는게 일반적 padding으로 조정*/
```

cursor: 마우스 커서 모양 변경

`cursor: pointer;`

# variable

반복되는 css 속성을 변수에 저장해서 사용

속성을 한번에 변경하기 용이함

```css
<style>
:root{
            --textcolor:#3e3e3e;
						--btnbg: #f8f8f8
        }

a{text-decoration: none; color: var(--textcolor);}
.visual-txt .btn-view{font-size: 14px; background-color: var(--btnbg);
display: inline-block; color: var(--textcolor); padding: 15px; margin-top: 40px;}

</style>
```

# multimedia

`<video src="./source/cycling.mp4" controls loop autoplay muted></video>`

controls : 컨트롤바 생성

muted : 사운드 삭제

loop : 반복재생

poster : 동영상 실행 전 대기상태로 보여지는 이미지 , autoplay와 같이 사용하면 안나옴

autoplay : 자동재생

iframe : 특정영역에 html이나 동영상을 보여주는 영역

src로 불러옴, frameborder 필수, width height값 넣을 수 있음

```css
<iframe width="760" height="428" src="[https://www.youtube.com/embed/TTLHd3IyErM](https://www.youtube.com/embed/TTLHd3IyErM)"
title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
allowfullscreen></iframe>
```

fullscreen

```css
<style>
        *{margin: 0; padding: 0;}
        html, body{width: 100%; height: 100%;}
        body{font-size: 20px; color: #fff; font-family: Arial, Helvetica, sans-serif;}
        #wrap{height: 100%;}
        #header{border-bottom: 1px solid #fff; height: 100px;position: absolute; width: 100%; z-index: 100;}
        #visual{position: relative;width: 100%; height: 100%;}
        #visual #screen{width: auto; height: auto;position: absolute;min-width: 100%; min-height: 100%;}
        /* 스크린에 position fixed 주면 스크롤바  사라짐 */
        #visual .txt{position: absolute; left: 0; top: 50%; transform: translateY(-50%); width: 100%; text-align: center; font-size: 100px; text-transform: uppercase; }
    </style>
</head>
<body>
    <div id="wrap">
        <header id="header">
            <div class="in">
                <h1>header</h1>
            </div>
        </header>
        <div id="visual">
            <video src="./source/exvideo.mp4"  autoplay muted id="screen"></video>
            <div class="txt">
                <h2>full-screen</h2>
            </div>
        </div>
    </div>
</body>
```

# calc()함수

calc()함수는 괄호안의 식을 계산한 결과를 속성값으로 사용해주게 하는 함수이다.
모바일이나 반응형 코딩을 하다보면 %로 값을 주기 애매한 부분들이 있는데 calc()함수를 사용하여값을 쉽게 지정할 수 있다.

1.식은 왼쪽에서 오른쪽으로 잔행. 2.곱하기, 나누기가 먼저 연산됨. 3.더하기 빼기 연산자의 경우 앞 뒤 공백을 반드시 넣어줘야 하며 곱하기 나누기는 공백이 필요하지 않음 4.오페라와 IE브라우저에서는 지원하지 않음. 5.호환성을 위해 -moz, -webkit과 같은 vender-prefix를 작성해야 함

```css
#content {
	background: orange;
	height: calc(100vh - 50px);
}
/*50px은 헤더높이 > 헤더높이 제외해서 채우기*/
```

# @media

모바일, 반응형에 사용

```css
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
body {
	font-size: 10px;
}
.wrap {
	width: 100%;
	background: #222;
	height: 200px;
}
.wrap h1 {
	font-size: 2rem;
	color: #fff;
	text-align: center;
}

@media screen and (min-width: 1000px) {
	.wrap {
		background: rgb(230, 173, 51);
		height: 200px;
	}
	.wrap h1 {
		font-size: 4rem;
		color: #111;
		text-align: left;
	}
}
```
