# 9주차 summary

### 웹 표준

: 웹에서 표준적으로 사용되는 기술이나 규칙으로 어떤 브라우저든 웹 페이지가 동일하게 보이도록 함 (크로스 브라우징)

## HTML 기초

HTML (Hyper Text Markup Language): 웹 페이지를 작성(구조화)하기 위한 언어

Hyper Text : 하이퍼링크를 통해 사용자가 한 문서에서 다른 문서로 즉시 접근할 수 있는 텍스트

Markup Language : 태그 등을 이용하여 문서, 데이터의 구조를 명시하는 언어

## HTML 기본구조

-   html: 문서의 최상위(root) 요소
-   head: 문서 메타데이터 요소
    -   문서 제목, 인코딩, 스타일, 외부 파일 로딩 등
    -   일반적으로 브라우저에 나타나지 않는 내용
-   body: 문서 본문 요소

### head 예시

-   title : 브라우저 상단 타이틀
-   meta : 문서 레벨 메타데이터 요소
    -   Open Graph Protocol : 메타데이터를 표현하는 새로운 규약, HTML문서의 메타 데이터를 통해 문서의 정보 전달, 메타정보에 해당하는 제목 설명 등을 쓸 수 있도록 정의
    -   `<meta property=”og.title” content=”content”>`
-   link : 외부 리소스 연결 요소
-   script : 스크립트 요소
-   style : CSS

### 요소 (element)

-   HTML의 요소는 태그와 내용으로 구성
    -   요소는 태그로 내용을 감싸는 것으로 정보와 성격, 의미를 정의 함
    -   내용이 없는 태그들도 존재 (닫는 태그 없음) : br, hr, img, input, link, meta
-   요소는 중첩 가능함
    -   요소의 중첩을 통해 하나의 문서를 구조화 함
    -   태그의 쌍 확인 필수

### 속성 (attribute)

-   속성을 통해 태그의 부가적 정보 설정 가능
-   요소는 속성을 가질 수 있으며 경로, 크기와 같은 추가적 정보를 제공함
-   요소의 시작 태그에 작성, 보통 이름과 값이 하나의 쌍으로 존재함
-   태그와 상관없이 사용가능한 속성들도 존재 (HTML Global Atrribute)

-   HTML Global Attribute : 모든 HTML 요소가 공통으로 사용할 수 있는 대표적인 속성
    -   id : 문서 전체에서 유일한 고유 식별자 지정
    -   class : 공백으로 구분된 해당 요소의 클래스 목록
    -   data-\* : 페이지에 개인 사용자 정의 데이터를 저장하기 위해 사용
    -   style : inline 스타일
    -   title : 요소에 대한 추가 정보 지정
    -   tabindex : 요소의 탭 순서

렌더링 (Rendering) : 웹 사이트 코드를 사용자가 보게 되는 웹 사이트로 바꾸는 과정

### DOM (Document Object Model 트리)

: 텍스트 파일인 HTML 문서를 브라우저에서 렌더링 하기 위한 구조

-   HTML 문서에 대한 모델을 구성
-   HTML 문서 내의 각 요소에 접근, 수정에 필요한 프로퍼티와 메서드를 제공

### 인라인 / 블록 요소

-   인라인 요소 : 글자처럼 취급
-   블록 요소 : 한 줄 모두 사용

### 텍스트 요소

-   ` <a>` `</a>`
    : href 속성 활용해 다른 url로 연결하는 하이퍼링크 생성
-   `<b></b>`, `<strong></strong>` : 굵은 글씨 요소, 중요한 강조 표시 요소
-   `<i></i>`, `<em></em> `: 기울임 글씨 요소, 중요한 강조 표시 요소
-   `<br>` : 텍스트 내 줄 바꿈 생성
-   `<img> `: src 속성 활용해 이미지 표현, alt 속성 활용해 대체 텍스트 표현
-   `<span></span>` : 의미 없는 인라인 컨테이너

### 그룹 컨텐츠

-   `<p></p>` : 하나의 문단
-   `<hr>` : 문단 레벨 요소에서 주제의 분리를 의미, 수평선으로 표현됨
-   `<ol></ol>`,`<ul></ul>` : 순서가 있는 리스트, 순서가 없는 리스트
-   `<pre></pre>` : HTML에 작성한 내용을 그대로 표현, 보통 고정폭 글꼴이 사용되며 공백문자를 유지함
-   `<blockquote></blockquote>` : 텍스트가 긴 인용문, 주로 들여쓰기 한 것으로 표현됨
-   `<div></div>` : 의미 없는 블록 레벨 컨테이너

## CSS 기초

CSS (Cascading Style Sheets) : 스타일을 지정하기 위한 언어

```css
h1 {
	color: blue;
	font-size: 12px;
}

선택자{
	속성: 값; => 선언
}
```

-   각 쌍은 선택한 요소의 속성과 속성에 부여할 값을 의미
    -   속성 (property): 어떤 스타일 기능을 변경할지 결정
    -   값 (value): 어떻게 스타일 기능을 변경할지 결정

### CSS 정의 방법

-   인라인 (inline)
-   내부 참조 (embedding) - `<style>`
-   외부 참조 (link file) - 분리된 CSS 파일

### CSS 기초 선택자

-   요소 선택자 : HTML 태그를 직접 선택
-   클래스 (class) 선택자 : `.` 문자로 시작, 해당 클래스가 적용된 항목 선택
-   아이디 (id) 선택자 : `#` 문자로 시작, 일반적으로 하나의 문서에 1번만 사용 (단일 id 사용)

## CSS 기본 스타일

### 크기 단위

-   px
    -   모니터 해상도의 한 화소 픽셀 기준, 고정적인 단위
-   %
    -   백분율 단위, 가변적 레이아웃에서 주로 사용
-   em
    -   부모 요소에 대한 상속 영향 받음, 배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈
-   rem
    -   부모 요소에 대한 상속 영향 받지 않음, 최상위 요소의 사이즈를 기준으로 배수 단위를 가짐
-   viewport
    -   웹 페이지를 방문한 유저에게 바로 보여지는 웹 컨텐츠의 영역 (디바이스 화면), 디바이스 viewport 기준으로 상대적 사이즈 결정 (반응형 웹에서 사용)

### 색상 단위

-   색상 키워드: 대소문자 구분X, 특정 색을 직접 글자로 나타냄
-   RGB : 16진수 표기법 또는 함수형 표기법으로 특정 색상 표현 (+rgba)
-   HSL : 색상, 채도, 명도를 통해 특정 색상 표현

### CSS 문서 표현

-   텍스트: 서체, 서체 스타일, 자간, 단어간격, 행간 등
-   컬러, 배경
-   기타 HTML 태그별 스타일링 : 목록, 표

## CSS 선택자

### 선택자 유형

-   기본 선택자
-   결합자
-   의사 클래스/요소

-   요소 선택자 : HTML 태그를 직접 선택
-   클래스 선택자: `.` 로 시작하며 해당 클래스가 적용된 항목을 선택
-   아이디 선택자: `#` 로 시작하며 해당 아이디가 적용된 항목을 선택

### CSS 적용 우선순위 (cascading order)

`인라인 > id > class, 속성, pseudo-class 요소, pseudo-element`

### CSS 상속

: CSS 는 상속을 통해 부모 요소의 속성을 자식에게 상속함, 속성 중에는 상속 되는 것과 되지 않는 것이 있음

## CSS Box model

: 모든 요소는 박스 모델이고 위에서 아래로, 왼쪽에서 오른쪽으로 쌓임

박스 영역: margin, border, padding, content

### box-sizing

: 기본적으로 모든 요소의 box-sizing 영역은 content-box로 padding 제외한 순수 contents 영역만 box로 지정 ⇒ 일반적인 영역을 사용할 때는 border-box 설정하는 것이 좋음

## CSS Display

-   `display : block`
-   `display : inline`
-   `display : inline-block`
-   `display : none`

### 블록 레벨 요소와 인라인 레벨 요소

-   blcok : `div, ul, ol. li, p, hr, form` 등
-   inline : `span, a, img, input, label, b, em, i` 등

> inline-block : 4px 공백 존재

## CSS Position

: 문서 상에서 요소의 위치를 지정

static: 모든 태그 default 값 (기준 위치), 일반적인 요소의 배치 순서 (좌측 상단), 부모 요소 내에서 배치될 때는 부모 요소의 위치를 기준으로 배치

좌표 프로퍼티를 사용하여 이동가능: relative, absolute, fixed, sticky

-   relative : 상대 위치
-   absolute : 절대 위치
-   fixed : 고정 위치
-   sticky : 스크롤에 따라 static 에서 fixed로 변경

## CSS Layout

: display, position float, flexbox, gird

### Float

: 요소가 nomal flow 벗어나게 함

```css
.box {
	float: right;
}
```

### Flexbox

: 행과 열 형태로 아이템을 배치하는 1차원 레이아웃 모델

-   축 : main axis, cross axis
-   구성요소
    -   Flex container : flexbox 레이아웃을 형성하는 가장 기본적 모델, Flexitems 들이 놓이는 영역, `display: flex` , `display: inline-flex`
    -   Flex item : 컨테이너에 속해 있는 컨텐츠

Flex 속성

-   배치
    -   flex-direction : row, row-reverse, column, column-reverse
    -   flex-wrap : warp, nowrap
    -   flex-flow : (shorthand) flex-direction flex-wrap
-   공간 나누기
    -   justify-content : flex-star, flex-end, center, space-between, space-around, space-evenly
    -   align-content : flex-star, flex-end, center, space-between, space-around, space-evenly
-   정렬
    -   align-items : stretch, flex-start, flex-end, center, baseline
    -   align-self : stretch, flex-start, flex-end, center
-   기타 속성
    -   flex-grow : 남은 영역을 분배
    -   order : 배치 순서

## 시맨틱 태그

: HTML 태그가 특정 목적, 역할 및 의미적 가치(semantic value)를 가지는 것

Non semantic 요소: div, span 등

### 대표적인 시맨틱 태그

-   header : 문서 전체나 섹션의 헤더
-   nav : 내비게이션
-   asdie : 사이드에 위치한 공간, 메인 컨텐츠와 관련성이 적은 컨텐츠
-   section : 문서의 일반적인 구분, 컨텐츠의 그룹 표현
-   article : 문서, 페이지, 사이트 안에서 독립적으로 구분되는 영역
-   footer : 문서 전체나 섹션의 푸터

### 시맨틱 태그를 사용해야 하는 이유

의미론적 마크업

-   개발자 및 사용자 뿐만 아니라 검색엔진 등에 의미 있는 정보의 그룹을 태그로 표현
-   단순히 구역을 나누는 것 뿐 아니라 ‘의미’를 가지는 태그들을 활용하기 위한 노력
-   요소의 의미가 명확해져서 코드의 가독성이 높아지고 유지보수가 용이하게 됨
-   검색엔진 최적화(SEO)를 위해 메타태그, 시맨틱 태그 등을 통한 마크업을 효과적으로 활용해야 함
