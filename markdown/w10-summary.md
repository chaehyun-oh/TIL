# 10주차 summary

## Table

table : `<thead> <tbody> <tfoot>` 필수요소는 아님

`<tr> <th> </th> </tr> <tr> <td></td> </tr>`

### table 태그 기본 구성

-   thead : tr > th
-   tbody : tr > td
-   tfoot : tr > td
-   caption : 표 설명, 제목
-   colspan, rowspan : 셀 병합

## Form

: 서버에 정보(데이터)를 제출하기 위해 사용하는 태그

### form 기본 속성

-   action : form을 처리한 서버의 URL (데이터를 보낼 곳)
-   method : form을 제출할 때 사용할 HTTP 메서드 (GET, POST)
-   enctype : 메서드가 post인 경우 데이터 유형
    -   application/x-www-form-urlencoded : 기본값
    -   multipart/form-data : 파일 전송시 (input type - file 인 경우)
    -   text/plain : HTML5 디버깅용 (잘 사용X)

### input

: 다양한 타입을 가지는 입력 데이터 유형과 위젯 제공됨

`<input>` 대표적 속성

-   name : form control에 적용되는 이름
-   value : form control에 적용되는 값 (이름-값 페어로 전송)
-   required, readonly, autofocus, autocomplete, disabled … ect

```html
<form action="/search" method="GET">
	<input type="text" name="p" />
</form>
```

input label

: label 을 클릭해 input 자체에 초점을 맞추거나 활성화

```html
<label for="agreement"> 개인정보 수집에 동의합니다.</label>
<input type="checkbox" name="agreement" id="agreement" />
```

input 기타 유형

-   color : color picker
-   date : date picker
-   hidden : 사용자에게 보이지 않는 input, 사용자 입력을 받지 않고 서버에 전송되어야 하는 값 설정

## Bootstrap

설치 외에도 CDN 으로 간편하게 사용할 수 있음

### spacing (margin, padding)

`{property}{sides}-{size}`

`<div class="mt-3 ms-5">bootstrap-spacing</div>`

-   property : m - margin , p - padding
-   sides : t - top, b - bottom, s - (start) left / right, e - (end) right / left, x - set both _-left & _-right, y - set both _-top & _-bottom, blank - set margin or padding all 3 sides of element
-   size : 0 , 1 - $spacer _ 0.25, 2 - $spacer _ 0.5, 3 - $spacer, 4 - $spacer _ 1.5, 5 - $spacer _ 3, auto - margin auto

| class name | rem  | px  |
| ---------- | ---- | --- |
| m-1        | 0.25 | 4   |
| m-2        | 0.5  | 8   |
| m-3        | 1    | 16  |
| m-4        | 1.5  | 24  |
| m-5        | 3    | 48  |

### Color

: bootstrap class 별 기본 색상 지정되어 있어 활용 가능

### Text

: class 로 텍스트 정렬, 시작점, 스타일, 굵기 등 지정 가능

### Display

: class 로 인라인, 블록, 박스 등 지정 가능

### Position

: class 로 fixed-top 등 position 지정 가능

## Bootstrap 컴포넌트

### Components

: Bootstrap의 다양한 UI 요소 활용 가능, 기본 제공된 Components를 변환해서 활용

-   Buttons
-   Dropdowns : dropdown, dropdown-menu, dropdown-item
-   Form > Form-controls
-   Navbar
-   Carousel
-   Modal : ID 주의 ~ JS 연결 target 과 일치시키기

## Bootstrap Grid system

### Grid System

: 요소들의 디자인과 배치에 도움을 주는 시스템

<기본요소>

-   Column : 실제 컨텐츠 포함하는 부분
-   Gutter : Column 사이 간격
-   Container : Column들을 담고 있는 공간

### Bootstrap grid system

: flex box로 제작됨, container, rows, coulmn 으로 컨텐츠 배치, 정렬함

column 12개, grid breakpoints 6개

```html
<div class="row">
	<div class="box col-9">col-9</div>
	<div class="box col-4">col-4</div>
	<div class="box col-3">col-3</div>
</div>

<div class="row">
	<div class="box col-sm-8 col-md-4 col-lg-5">1</div>
	<div class="box col-8 col-sm-2 col-md-4 col-lg-2">2</div>
	<div class="box col-2 col-sm-2 col-md-4 col-lg-5">3</div>
</div>
```
