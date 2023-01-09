# HTML 5

Hyper Text Markup Language

---

# 태그

## 블록 요소 (Block Element)

마크업 시 줄 바꿈이 일어나는 성질을 가짐

레이아웃 잡을 때 많이 사용

블록 영역은 100%

## 인라인 요소 (Inline Element)

블록 요소와 달리 줄 바꿈 성질이 없음, 한 줄로 출력 됨

인라인 영역은 안에 있는 내용 만큼만

> 블록태그로 인라인 태그를 감쌀 수는 있지만 역은 불가

---

## 제목 (Title)

`<h>`

```html
<!--

    (heading) 요소는 큰 제목 순으로 <h1>~<h6>
        
        자동으로 볼드 처리 됨

웹 표준 문서 작업 시 <h1>은 꼭 마크업 해주어야 하는데 웹 문서의 <h1>은 보통 회사나 단체의 상호명(로고)으로 처리한다.
    
    마크업 시 <h1> > <h2> > <h3>... 순서로 정의해야 하며 <h1> 다음에 반드시 <h2>가 와야하며 <h3>가 올 수 없음
        
        웹 페이지 기획 단계에서 내용의 중요도와 흐름에 따라 어느 부분을 제목으로 처리해야 할지 잘 판단해야 한다.
        -->
```

## 단락 (Paragraph)

`<p>`

텍스트들은 인라인 요소의 성질을 가지고 있기 때문에 단독으로 쓰지 않고 보통 블록요소 안에 포함시킴

\*`<br>` : 강제 줄바꿈 > 사용을 권장하지는 않음

## 구분선 (Horizontal line)

`<hr>`

## 인용문 (Quotation)

말이나 글을 인요할 때 씀

`<blockquote>` : 블록태그/ 감싼 텍스트를 들여쓰기 함

`<q>` : 인라인태그

## 텍스트 (Text)

`<em>, <strong>` 인라인 요소, 텍스트를 강조

`<em>` 이탤릭체, `<stong>` 볼드체, 둘 다 중요하다는 표시를 해줌

`<b>` 그냥 시각적으로 텍스트를 굵게 처리함 중요 표시X

`<pre>` 텍스트를 약간 변경 (소스코드) 그런데 접근성이 안좋아서 사용하지 않음

<aside>
🔥 서버 확인할때 인덱스 페이지 외 페이지는 `도메인/해당페이지파일명.html`로 확인

</aside>

## 이미지 (Image)

단독 태그, 인라인 요소

`<img src="이미지 파일명" width = "가로 길이" height = "세로 길이" alt="대체 텍스트"/>`

`<img src="파일 경로/파일명.확장자" alt="대체 텍스트">`

이미지 대체 텍스트는 접근성적으로 중요함.

alt 태그: 이미지에 대한 설명 적음

이미지를 분실했을 경우 설명을 보고 찾을 수 있음

이미지 크기를 조절해도 용량은 그대로 임

-   이미지 맵
    지금은 많이 안 씀...
    하나의 이미지에 여러 개의 링크를 적용할 수 있음
    img src = "이미지 파일명" alt="대체 텍스트" usemap = "#맵이름"/>
    <map id = "맵이름" name = "맵이름">

### 경로

상대경로

경우에 따라서 상위폴더로 이동해야하는 경우 `"../파일경로/파일명"` 활용

상위폴더로 올라갈 때 마다 `../` 반복 ex) `"../../파일경로/파일명"`

같은 폴더 `./`생략가능

## 비디오(video)

```html
<h3>동영상1</h3>
<video src="./source/cycling.mp4"></video>
<h3>동영상2</h3>
<video>
	<source src="./source/cycling.mp4" type="video/mp4" />
	<source src="./source/google-developer-stories.webm" type="video/webm" />
	<source src="./source/cycling.mp4" type="video/ogg" />
</video>
<h3>동영상-속성</h3>
<video
	src="./source/cycling.mp4"
	controls
	loop
	muted
	poster="./source/flower2.jpg"
></video>
<h3>동영상-유투브</h3>
<div class="youtube">
	<iframe
		width="760"
		height="428"
		src="https://www.youtube.com/embed/TTLHd3IyErM"
		title="YouTube video player"
		frameborder="0"
		allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
		allowfullscreen
	></iframe>
</div>
<h3>사운드</h3>
<audio src="./source/music.mp3"></audio>

<audio>
	<source src="./source/music.mp3" type="audio/ogg" />
	<source src="./source/music.mp3" type="audio/wav" />
	<source src="./source/music.mp3" type="audio/mpeg" />
</audio>
```

## 링크(Link)

`<a>`

텍스트나 이미지를 통하여 다른 곳으로 정보를 연결재 주는 역할을 담당하는 요소

텍스트 색상 블루로 변경&언더라인 생성

`<a href="url"> 텍스트 또는 이미지</a>`

절대경로 : 외부 사이트 연결시에 사용

새 창으로 연결하는 경우가 많음

`<a href="[http://www.naver.com](http://www.naver.com/)" target="_blank">네이버</a>`

target 속성의 "\_blank"는 연결된 정보 페이지를 새 창에 띄움

```html
<h3>절대경로</h3>
<p><a href="http://www.nate.com" title="네이트로 이동">네이트</a></p>

<h3>절대경로-새 창으로 연결</h3>
<p>
	<a href="http://www.naver.com" target="_blank" title="네이버로 이동"
		>네이버</a
	>
</p>

<h3>상대경로</h3>
<p><a href="../3.Image/image_ex.html">이미지파일열기</a></p>

<h3>다운로드</h3>
<p>
	<a href="./source_text.zip"
		><img src="./images/menu1.gif" alt="다운로드 하세요"
	/></a>
</p>

<h3>링크를 연결할 경로가 없는 경우</h3>
<p><a href="#">자바스크립트 연결</a></p>
```

## 리스트 (List)

목록태그, 블록요소

순차적 목록ol, 비순차적 목록ul, 정의형 목록dl

### ol (Order List)

순차적인 목록을 작성할 때 사용

ol태그와 li태그 사이에는 다른 태그 오지 못함

`<ol><li>항목의 내용</li></ol>`

### ul (Unorder List)

비순차적 목록을 작성할 때 사용

ul태그와 li태그 사이에는 다른 태그 오지 못함

`<ul><li>항목의 내용</li></ul>`

웹 내비게이션 만드는 코드

```html
<ul>
	<li><a href="#">기업소개</a></li>
	<li><a href="#">사업영역</a></li>
	<li><a href="#">제품소개</a></li>
	<li><a href="#">고객센터</a></li>
	<li><a href="#">홍보자료실</a></li>
	<li><a href="#">인재채용</a></li>
</ul>
```

### dl (definition List)

정의 내리고자 하는 용어에 대한 정의 리스트

`<dl><dt>용어</dt><dd>용어정의</dd></dl>`

## header 태그

<header> 헤더

## nav 태그

<nav> 네비게이션

## main 태그

<main> 주 컨텐츠

## footer 태그

<footer>

## section 요소

문서 내에서 의미가 같은 내용들을 묶어주는 의미적 그룹요소 보통 제목요소로 시작함

_div 태그와는 다름_

```html
<section>
	<h1>제목</h1>
	<p>내용</p>
	<h1>제목</h1>
	<p>내용</p>
	<h1>제목</h1>
	<p>내용</p>
</section>
```

## article 요소

신문 기사나 블로그의 글에 사용

독립적으로 배포 또는 재사용이 가능한 컨텐츠를 article에 포함할 수 있음

## aside 요소

주위의 내용들과 관련이 없고 메인 컨텐츠와 분리할 수 있는 독립적인 요소

메인컨텐츠의 왼쪽이나 오른쪽에 위치한 사이드바의 영역이라고 보면 됨

## form 태그

인라인 태그

<form> : 폼 전체를 감싸는 태그

<fieldset>, <legend> : 접근성 측면/폼 요소를 그룹으로 묶고 제목을 붙이는 태그

<label> : 접근성 측면/ 폼 요소에 캡션을 부르는태그/넣고 가리기

<input> : 사용자가 입력할 수있는 태그(한 줄 입력)

<select>, <option> : 드롭다운 목록을 넣는 태그

<textarea> : 여러 줄의 텍스트를입력하는 텍스트영역을 넣는 태그

<button> : 버튼을 넣는 태그

<form action=””>폼태그 </form>

action: get/post 방식 중 하나 > 근데 이건 백엔드라서 상관 무 / 비워두거나 #로 연결해두기

폼서식

<input type=””>

: 아이디나 검색어를 입력하는 텍스트 박스나 로그인 버튼 처럼 다양한 폼 서식을 마크업 할 때 사용

html5에서 새로운 유형의 폼요소가 많이 생성되었지만 주로 모바일. 아직까지 웹브라우저에서 지원 안하는 요소들도 있다.

폼은 크게 사용자가 내용을 입력하는 폼필드와 입력한 내용을서버로 보내주는 폼버튼으로 나눌 수 있다.

input태그에서 type 속성에 따라 폼의 종류가 결정된다.

<input type=”폼 유형” 속성-”속성값”>

type=”text”

한 줄 짜리 텍스트를 입력하는 필드. 주로 아이디나 비밀번호, 이름, 주소와 같은 텍스트를 입력

name: 텍스트 필드를 구별할 수 있는 이름을 지정 / name으로 연결

size: 텍스트 필드의 길이를 지정. 필드에 입력할 수 있는 글자수로 지정 (주로 css에서 조정)

영문글자 단위로 지정하며 한글은 자음, 모음 두 글자에 해당

value: 입력한 내용이 웹브라우저에서 텍스트 필드로 보여진다.

maxlength : 텍스트 필드에 입력할 수 있는 최대 글자수

```html
<label for=”userid”> 아이디 (6자 이상)</labe><input type="text" id="userid" name="userid" size="20" maxlength="20">
```

type=”search”

웹브라우저에서 검색상자 필드를 만든다.

크롬이나 사파리 브라우저에서 검색상자 안에 검색어를 입력해보면 오른쪽에 X가 표시된다

X를 클릭하면 검색 상자 안에 입력된 검색어를 손쉽게 지울 수 있다.

```html
<label for="ser"></label> <input type="search" /><input type="submit" />
```

type=”url”

텍스트 필드에 입력하는 정보가 웹주소라는 사실을 알 수 있도록 한다.

절대경로만 가능함

type=”email”

텍스트 필드에 입력하는 정보가 이메일 주소라는사실을 알 수 있도록 한다.

기존html에서는 자바스크립트가 @라는 문자가 들어있는지 체크했지만 html5에서는

type=”email”만 입력해도 자동으로 체크해준다

type=”tel”

텍스트 필드에 입력하는 정보가 전화번호라는 사실을 알려줌

type=”number”, type”=”range”

number타입은 숫자를 입력하고자 할 때 사용한다. 웹브라우저에서 스핀박스에 화살표를 눌러 숫자를 입력할 수 있다.

range타입은 숫자를 입력하는

type=”radio”

radio 타입은 여러 항목 중에서 원하는 항목 한가지만 선택할 수 있다.

이미 선택된 항목이 있을 경우

checked : 속성 넣어서 선택 고정가능

type=”checkbox”

여러 항목중 다수 선택 가능

type=”color”

사용자가 색상표에서 색상을 선택할 수 있게 해줌, 일부 웹에서만 지원

많이 쓰이지는 않음 > 자바스크립트에서 활용

type=”datetime”

날짜와 시간을 입력하고자 할 때 사용 > 실질적으로는 자바스크립트로 활용

datetiem, date, month, week

입력한 일시의 타임존을 국제적인 표준시 UTC를 기준으로 표시

유효한 형식: 날짜를 나타내는 문자열 연도4월2일2

```html
<label for="reser">예약가능일시</label>
<input
	type="datetime"
	name="reser"
	id="reser"
	min="2021-12-28T00:00:00Z"
	max="2022-01-31T12:00:00Z"
/>

<label for="reser">예약가능일시</label>
<input type="date" name="reser" id="reser" min="2021-12-28" max="2022-01-31" />
<!--달력형식-->
```

required: 필수로 입력해야하는 속성에 required 쓸 경우 해당 칸 미작성시 경고창이 뜸

```html
<input
	type="tel"
	name="user-tel"
	id="user-tel"
	size="11"
	maxlength="11"
	class="txt"
	required
/>
```

placeholder : 입력창에 입력하기 전에 문구를 넣어둘 수 있음

```html
<label for="user-txt" class="hide">문의내용을 입력해주세요</label>
<textarea
	name="txt"
	id="txt"
	cols="80"
	rows="20"
	placeholder="문의 내용을 입력해주세요."
></textarea>
```

autocomplete: 이전에 작성해 제출한 내용 그대로 불러오기 가능

`autocomplete="on”`

autofocus: 선택하지 않아도 자동으로 입력창이 활성화 된 상태로 만들어줌

`<input type="email" name="user-mail" id="user-mail" class="txt" autofocus>`

disabled: 입력창 비활성화 > 자바스크립트로 일정 조건달성되면 활성화되도록 변경가능

readonly: 읽게만 할 수 있음

```html
<label for="id">ID</label> <input type="text" id="id" />
<label for="pass">P/W</label> <input type="password" id="pass" />
```

label, input이 서로 떨어져 있어도 이름이 같으면 연결함

<fieldset> 블록태그

하나의 폼 안에서 여러 구역을 나눠 표시할 때 사용

태그 사이의 폼들을 하나의 영역으로 묶고 외곽선을 그려준다 (보더 생성)

<legend>

이름 지정하고 묶는 방식

fieldset으로

폼버튼

type=”submit”

폼에 입력된 데이더를 서버에 전송

type=”reset”

폼에 입력된 데이터를 모두 초기화

type=”button”

자바스크립트 실행을 위한 용도

<button> </button>

# 그룹핑(Grouping)

`<div>` : 블록 요소

`<span>` : 인라인 요소

# 테이블(Table)

`<table>`

웹 문서에서 표를 만드는 요소, 블록 요소 (+부분적으로 인라인 요소를 가짐)

항상 행 먼저, 셀의 갯수는 다 같이해야함

`<tr>` : 행을 만드는 요소

`<td>` : 열을 만드는 요소 (셀-cell)

```html
<table>
	<tr>
		<th>table title</th>
		<td>A</td>
		<td>B</td>
	</tr>
	<tr>
		<td>C</td>
		<td>D</td>
	</tr>
</table>
```

셀 병합

`<td colspan = "열 합치기 개수"></td>`

`<td rowspan = "행 합치기 개수"></td>`

셀 제목

`<th>`

### 접근성 고려

> 퍼블리셔로 가면 중요해 코딩할때 생각하면서 하자

`<thead>` 제목

`<tbody>` 본문

`<tfoot>` 결과

순서는 thead > tfoot > tbody 순서

제목과 결과 듣고 내용은 나중에

scope 스크린 리더의 읽는 순서, 방향을 지시 (간단한 테이블에 사용)

header, id : id로 지정해서 header로 연결해서 읽어줌 (복잡한 테이블에 사용)

테이블 설명:

```html
<h2>테이블 설명</h2>
<p>
	이 표는 태블릿PC와 스마트폰 판매현황으로 상반기와 하반기의 판매현황을 비교할
	수 있습니다.
</p>
<!--p태그를 css에서 안보이게 할 수 있음, 스크린 리더에만 읽힐 수 있게 하는 방법-->
```

```html
<h2>테이블 설명</h2>
<!--html5에서 새로 생긴 figure, figcaption을 이용, css로 안보이게 할 수 있음-->
<figure>
	<figcaption>
		이 표는 태블릿PC와 스마트폰 판매현황으로 상반기와 하반기의 판매현황을
		비교할 수 있습니다.
	</figcaption>
	<table border="1" width="400" height="300">
		<caption>
			태블릿 PC와 스마트폰 판매현황
		</caption>
		<thead>
			<tr>
				<th>구분</th>
				<th>태블릿</th>
				<th>스마트폰</th>
			</tr>
		</thead>
		<tfoot>
			<tr>
				<th>총 판매수</th>
				<td>5만대</td>
				<td>16만대</td>
			</tr>
		</tfoot>
		<tbody>
			<tr>
				<th>상반기 판매수</th>
				<td>2만대</td>
				<td>5만대</td>
			</tr>
			<tr>
				<th>하반기 판매수</th>
				<td>3만대</td>
				<td>11만대</td>
			</tr>
		</tbody>
	</table>
</figure>
```

<caption>으로도 가능0

# 파비콘

<link rel=”shortcut icon” href=”경로”>

# 인클루드

include(인클루드) 란?
기존에 입력한 소스를 불러와 작업 페이지에서 이미작업된 페이지를 가져다 활용함으로 작업했던 내용을 또 작업하는 내용이 없도록 시간적 공간적 절약을 위해 사용된다.
include(인클루드) 왜 사용되는가?
코딩시에 프로젝트 전반적으로 자주 사용되는 반복 구간을 매번 새로운 소스를 입력하여 작업하는건 시간적으로도 프로젝트내에서도 좋지않고, 소스를 새로입력하는것보다, 기존에 입력되어있는소스를 리딩하여 해당소스는 공통적으로
통합 관리하기 위함으로 사용된다.

include(인클루드) 사용법?

```jsx

// JQUERY
<script src="[//code.jquery.com/jquery-3.11.0.min.js](notion://code.jquery.com/jquery-3.11.0.min.js)"></script>
<script>
$(document).ready( function() {
$("#header").load("common/header.html"); //헤더 인클루드
$("#footer").load("common/footer.html"); //푸터부분 인클루드
}
);
</script>
<div id="header"></div>
<div id="footer"></div>
```

```php

// PHP
--상대경로시
<? include("../경로.php");?>

--절대경로시
<?php include("../경로.php");?>
<?php include ("header.php");?>
```

# 크로스브라우징

크로스 브라우징은 웹 표준 기술을 채용하여 다른 기종/플랫폼에 따라 달리 구현되는 기술을
비슷하게 만듦과 동시에 어느 한쪽에 최적화되어 치우치지 않도록 공통요소를 사용하여 웹 페
이지를 제작하는 기법을 말한다. 흔히들 모든 브라우저에서 동일한 페이지가 출력되도록 하는
것을 크로스 브라우징이라고 하는데 사실상 그것은 불가능하다. 각각의 플랫폼의 글꼴이 다르
며, 브라우저의 렌더링 엔진이 다르기 때문이다.

1. Can I Use를 자주 참고한다
   [https://caniuse.com/](https://caniuse.com/)

1. 코딩은 보수적으로 한다.
   [https://www.w3schools.com/](https://www.w3schools.com/)
1.
1. 브라우저의 트렌드를 간파하고 있는다.
   각 브라우져들의 기능 평가도를 보면 현재 크롬과 오페라가 가장 높고 파이어폭스와 사파리
   가 점수가 높지 않다. 점유율이 가장 높은 브라우저부터 확인하는 것이 좋다

8.최신의 브라우저에서 웹표준을 지키지 않던 브라우저(IE5,6,7 등)를 기준으로 제작된 웹페이
지를 방문하게 되면 레이아웃이 깨지거나 작동하지 않을 때가 있다. 그래서 meta태그를 사용
해서 렌더링 엔진을 선택하게 하거나, 최신 렌더링 모드로 강제로 작동하게 만들어야 한다

<meta http-equiv="X-UA-Compatible" content="IE=edge" />

# 메타태그

HTML 문서의 맨 위쪽에 위치하는 태크. HEAD 태그 사이 또는 뒤에 있어도 되지만, 반드시 BODY 태그 앞쪽에 위
치해야 한다. 브라우저와 검색 엔진을 사용할 수 있도록 문서의 정보를 포함하고 있다.
출처 TTA정보통신용어사전

<meta name="author" content="사이트 저자"/>
<meta name="subject" content="사이트 목적(주제)"/>
<meta name="copyright" content="사이트 저작권(소유권)"/>
<meta name="content-language" content="ko"/>
<meta name="viewport" content="width=device-width"/>
<meta name="description" content="사이트 설명(최대 160자 추천)"/>
<meta name="keywords" content="사이트 키워드"/>
<meta name="robots" content="ALL"/>
<meta name="robots" content="index,follow" />
: 이 문서도 긁어가고 링크된 문서도 긁어감.
<meta name="robots" content="noindex,follow" />
: 이 문서는 긁어가지 말고 링크된 문서만 긁어감.
<meta name="robots" content="index,nofollow" />
: 이 문서는 긁어가되, 링크는 무시함.
<meta name="robots" content="noindex,nofollow" />
: 이 문서도 긁지 않고, 링크도 무시함.

검색엔진에게 정보를 전달할 뿐만 아니라, 웹 브라우저에게도 정보를 전달하는 역할을 한다.

<meta http-equiv="refresh" content="5;url=http://www.naver.com/">

: 사이트 주소가 변경되었을때 유저가 방문하면 변경된 주소로 이동하도록
