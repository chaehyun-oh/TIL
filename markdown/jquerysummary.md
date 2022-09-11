# J-Query

자바스크립트의 가장 대표적인 라이브러리 언어.
자바스크립트 프로그래밍을 단순화 간결한 코드로 많은 동작 구현

cdn연결

`https://developers.google.com/speed/libraries#jquery`

3.x snippet:

`<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>`

2.x snippet:

`<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.2.4/jquery.min.js"></script>`

1.x snippet:

`<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>`

site:

[jquery.com](http://jquery.com/)

---

# j-Query 기본 문법

-jQuery를 정의하거나 접근하기 $ 사용
-$로 시작 (구문은 jQuery를 사용하겠다는 의미)

```jsx
<script>
$(document).ready(function () {
		$(‘css선택자’).css(‘스타일 속성명, ‘’값’)
});
</script>
```

간단하게 아래 처럼 쓸 수 있음

```jsx
<script>
$(function () {
		$(‘css선택자’).css(‘스타일 속성명, ‘’값’)
});
</script>
```

예시

```jsx
<script>
			$(function (){
				$(".hide").click(function(){
					$("#box").hide();
				});
				$(".show").click(function(){
					$("#box").show();
				})
			})
		</script>
```

# 이펙트

## 화면효과

show() - 선택자를 이용하여 찾아진 문서 객체를 보여주는 메서드
$(selector).show(duration, easing, callback)

hide () - 선택자를 이용하여 찾아진 문서 객체를 숨기는 메서드
$(selector).hide(duration, easing, callback)

toggle() - 선택자를 이용하여 찾아진 문서 객체를 보여주거나 숨기는 메서드
$(selector).toggle(duration, easing, callback )

fadeIn() - 선택자를 이용하여 찾아진 문서 객체를 보여주는 메서드
$(selector).fadeIn(duration, easing, callback)

fadeOut() - 선택자를 이용하여 찾아진 문서 객체를 숨기는 메서드
$(selector).fadeOut(duration, easing, callback)

fadeToggle() - 선택자를 이용하여 찾아진 문서 객체를 보여주거나 숨기는 메서드
$(selector).fadeToggle(duration, easing,callback )

fadeTo() - 투명도 지정가능

$(selector).fadeTo(duration, easing,callback )

slideDown() - 선택자를 이용하여 찾아진 문서 객체를 보여주는 메서드
$(selector).slideDown(duration, easing, callback)

(네비게이션작업할때 활용)

slideUp() - 선택자를 이용하여 찾아진 문서 객체를 숨기는 메서드
$(selector).slideUp(duration, easing, callback)

slideToggle() - 선택자를 이용하여 찾아진 문서 객체를 보여주거나 숨기는 메서드
$(selector).slideToggle(duration, easing, callback )

### 클릭 이벤트 적용 시 기본 이벤트 차단하기

return false / preventDefault()
`<a>`요소에 click이나 dbclick을 등록하면 클릭할 때마다 `<a>` 에 링크된 주소로 이동하는 문제가 발생한다.

`<form>`요소의 제출버튼(submit)도 action에 등록된 점수로 이동시키는 문제가 발생한다. 이 때 이벤트를 정상적으로
수행하려면 이러한 기본 이벤트를 차단해야 한다.
Return false를 이용한 차단 방식

```jsx

$(‘a 또는 form’).이벤트 메서드(function() {
	자바스크립트 코드
	return false;
})
//가장 밑에 해줘야 함 > false때문에 다른 코드 실행X
```

preventDefault() 메서드를 이용한 차단 방식

```jsx

$(‘a 또는 form’).이벤트 메서드(function(e) {
	e.preventDefault()
	자바스크립트 코드
})
```

사용자 정의 효과
2-1. animate( )
animate() 함수는 수치 CSS 속성을 제어하여 에니메이션(움직임) 효과를 만들어 낸다.

`$(selector). animate(properties, duration, easing, callback )`

메서드 중첩가능 > 순차적으로 진행

```jsx
**$(".big").click(function(){
					$("#box").stop().animate({"width":"300px", "opacity":0.5},500,"linear", function(){
						alert("크고 불투명하게 하기");
					}).hide();
					// 속성이 2개 이상일때는 {}로 묶어서 그룹핑, 1000=1초
					//.stop()은 애니메이션 넣을때 같이넣어주는게 좋음
				})**
```

# 선택자

$(”선택요소”).children(”태그명”)

선택요소를 기준으로 자식 요소들 선택

```jsx
$("#parent>.child") = $("#parent").children(".child")
//직계 자손
$("#parent .find") = $("#parent").find(".find")
//직계 후손
```

$(”선택요소”).prev()

선택요소를 기준으로 형제 요소 중 이전 요소 선택

$(”선택요소”).prevAll()

선택요소 기준으로 이전 형제요소 전체 선택

$(”선택요소”).next()

선택요소를 기준으로 형제 요소 중 다음 요소 선택

$(”선택요소”).nextAll()

선택 요소 기준으로 다음 형제 요소 전체 선택

$(”선택요소”).sibilings(”태그명”)

선택요소를 기준으로 형제 요소들 모두 선택

부모 요소 선택자
선택한 요소를 감싸고 있는 직계부모 요소 선택
$(‘요소선택’).parent();

직계 부모 보다 상위에 있는 부모 선택

$(”요소선택”).parents();

하위 요소 선택자
선택한 요소를 기준으로 하위 요소를 선택
$(‘요소선택1 요소선택2’)

자식 요소 선택자
선택한 요소를 기준으로 자식 요소를 선택
$(‘요소선택1 >요소선택2’)

$(”:종류”);

폼의 input 요소 중 종류(type)가 일치하는 요소들 선택

```jsx
$(function () {
	$(".basis").click(function () {
		$(".basis").prev().css("background", "royalblue");
		$(".basis").prevAll("p").css("background", "royalblue");
		$(".basis").next().css("background", "rosybrown");
		$(".basis").siblings("p").css("background", "rosybrown");
	});
});
```

eq(index)/ lt(index) / gt(index)
eq(index) 선택자는 선택한 요소 중 지정한 인덱스가 참조하는 요소만 선택.
lt(index) 선택자는 선택한 요소 중 지정한 인덱스보다 작은 인덱스를 참조하는 요소만 선택.
gt(index) 선택자는 선택한 요소 중 지정한 인덱스보다 큰 인덱스를 참조하는 요소만 선택.

```jsx
$('요소선택:eq(index)') 또는 $('요소선택'). eq(index)
$('요소선택:lt(index)');
$('요소선택:gt(index)');
```

# 이벤트

mouseover/out: 자손요소 포함 안함 부모자손 따로 인식

mouseenter :/leave 자손요소 포함

focus, blur: 부모 요소에는 이벤트 전달 안됨

focusin, out: 부모 요소에도 이벤트 전달 됨

resize() 크기를 조정할 때 발생하는 이벤트

```jsx
$(window).resize(function () {
	h = $(window).height();
});
```

## 그룹이벤트

### 그룹 이벤트 등록 메서드

대상에 한가지 동작 이상의 이벤트를 등록

```jsx
$('선택자').on('이벤트1 이벤트2....',function() {
자바스크립트 코드
})
```

```jsx
$('선택자').on( {'이벤트1 이벤트2....':function() {
자바스크립트 코드
}
})
```

```jsx
$('선택자').on( {
'이벤트 종류1':function() {자바스크립트 코드 1 },
'이벤트 종류2':function() {자바스크립트 코드 2 },
'이벤트 종류3':function() {자바스크립트 코드 3 }
})
2 이벤트
```

```jsx
$(".enter").on("focusin click", fuction(){
	$(".enter").css("background","rosybrown");
});
```

이벤트객체 속성

# 이벤트가 발생한 요소 추적하기

## $(this)선택자

이벤트 핸들러에서 $(this)를 사용하면 이벤트가 발생한 요소를 선택하여 이벤트가 발생한 요소를 추적할 수 있다.

```jsx
$(‘#gnb>li>a’).on(‘click’, function() {
	$(this)
})
```

```jsx
$(function () {
	$(".basis").click(function () {
		$(this).next().css("background", "blue");
		//$(this)가 자동으로 $(".basis")로 인식해서 적용
	});
});
```

## 인덱스 반환 메서드

index( )인덱스 반환 메서드는 이벤트를 등록한 요소 중 이벤트가 발생한 요소의 인덱스값을 반환한다.

```jsx
$(‘선택자’).on(‘이벤트의 종류’, function() {
$(‘선택자’).index(this);
})
$(this).index();
```

팝업창 만들기

```jsx
**<script>
        $(function(){
            $(".open-ovl").show();

            $(".btn-menu").click(function(e){
                e.preventDefault();
                $(this).next().show();
            })

            $(".btn-close").click(function(){
                $(".overlay, .open-ovl").hide();
            })


        })
    </script>**
```

# 메서드

1 속성 조작 메서드
1-1.1 attr() / removeAttr()
attr() 메서드는 선택한 요소의 새 속성을 생성하거나 기존의 속성을 변경할 때나 요소의 속성을 불러올 때 사용.
removeAttr()메서드는 선택한 요소에서 기존의 속성을 삭제할 때 사용

```jsx
$(‘요소선택’).attr(‘속성명’);
$(‘요소선택’).attr(‘속성명’, ‘새값’);
$(‘요소선택’).attr(‘속성명1’ : ‘새값1’, ‘속성명2’ : ‘새값2’, ………. );
```

1-1.2 addClass( ) / removeClass()/toggleClass( ) / hasClass( )
addClass() 는 선택한 요소의 클래스를 생성. removeClass()는 선택한 요소에서 지정한 클래스 삭제.
toggleClass()는 선택한 요소에 지정한 클래스가 없으면 생성하고 있으면 삭제.
hasClass()는 선택한 요소에 지정한 클래스가 있으면 true를 반환 없으면 false를 반환.

```jsx
$(‘요소선택’). addClass(‘클래스값’);
$(‘요소선택’). removeClass(‘클래스값’);
$(‘요소선택’). toggleClass(‘클래스값’);
$(‘요소선택’). hasClass(‘클래스값’)
```

1-1.3 html( ) / text( )
html() 메서드는 선택한 요소의 하위 요소를 가져와 문자열로 반환하거나 하위 요소를 전부 제거하거나 새 요소로
바꿀 때 사용.
text()메서드는 선택한 요소에포함되어 있는 전체 텍스트를 가져오거나 선택한 하위 요소를 전부 제거하고 새 텍스트를 생성할 때 사용.

```jsx
$(‘요소선택’).html();
$(‘요소선택’).html(‘새 요소’);
$(‘요소선택’).text();
$(‘요소선택’).text(‘새 텍스트’);
```

```jsx
$(function () {
	// let h = $(".ht").html();
	// console.log(h);
	let h = $(".ht").html("<h3>html</h3>");
	//h2를 h3으로 변경
	let h = $(".te").text("속성조작 메서드");
	//텍스트 내용 변경
});
```

```jsx
<script>
	$(function()
	{$(".color").click(function () {
		let myColor = $(this).text();
		$(this).css("background", myColor);
	})}) //텍스트 내용을 추출해서 사용 가능
</script>
```

1-1.4 val()
선택한 폼 요소의 value속성값을 가져 오거나 새 값을 적용할 때 사용

```jsx
$(‘요소선택’).val();
$(‘요소선택’).val(‘새 값’)
```

1-1.5 prop()
선택한 폼 요소(선택 상자, 체크 박스, 라디오 버튼)의 상태속성값을 가져 오거나 새롭게 설정할 때 사용

```jsx
$(‘요소선택’). prop(‘[checked | selected]’);
$(‘요소선택’). prop (‘[checked | selected]’, [true | false]);
$(‘요소선택’). prop (‘[tagName | nodeType | selectedIndex | defaultValue]’, [true | false]);
```

스크롤바 위치 메서드
scrollTop()메서드는 브라우저의 스크롤바가 수직 / 수평으로 이동한 위칫값을 불러오거나 변경할 때 사용

```jsx

$(‘요소선택’).scrollTop(); / $(‘요소선택’). scrollTop(‘값’);
$(‘요소선택’). scrollLeft(); / $(‘요소선택’). scrollLeft( ‘값’);
```

수치 조작 메서드
2-1.1 요소의 높이 / 너비 메서드
안쪽 여백과 선을 제외한 너비값과 높이값을 반환하거나 변환한다

```jsx

$(‘요소선택’).height(); / $(‘요소선택’).height(‘값’);
$(‘요소선택’).width(); / $(‘요소선택’).width(‘값’);
```

안쪽 여백을 포함한 너비값과 높이값을 반환하거나 변환한다

```jsx

$(‘요소선택’).innerHeight(); / $(‘요소선택’). innerHeight(‘값’);
$(‘요소선택’).innerWidth(); / $(‘요소선택’). innerWidth( ‘값’);
```

안쪽 여백과 선을 포함한 너비값과 높이값을 반환하거나 변환한다

```jsx

$(‘요소선택’).outerHeight(); / $(‘요소선택’). outerHeight(‘값’);
$(‘요소선택’).outerWidth(); / $(‘요소선택’). outerWidth( ‘값’);
```

요소 위치 메서드
선택한 요소의 **‘포지션’** 위치값을 반환한다.

선택 요소의 부모요소에 position 지정되어있어야 함

```jsx
$(‘요소선택’).position(); [left | right | top | bottom]
```

선택한 요소가 문서에서 수평/수직으로 얼마나 떨어져 있는지에 대한 값을 반환한다.
브라우저 상단에서부터 거리

```jsx
$(‘요소선택’).offset(); [left | top]
```

setInterval(실행문, 시간간격) : 해당 간격으로 실행문을 반복적으로 수행

(1000 = 1초)

clearInterval(변수명); setInterval() 을 제거하는 명령어

```jsx
<script>
        $(function(){
            let time = setInterval(function(){
                // letf : "+=100"

            $(".round").stop().animate({left:"+=100"}, 300);
            },1000);

            $(".round").mouseover(function(){
                clearInterval(time);
            })
        });
    </script>
```

객체 편집 메서드
선택한 요소를 복제하거나 새 요소를 생성하는 메서드를 복제하거나 새로 생성한 요소를 의도한 위치에 삽입하고 선택한 요소를 삭제 한다.

3-1.1 before() / insertBefore() / after() / insertAfter()
before() , insertBefore()메서드는 선택한 요소의 이전 위치의 새 요소를 생성하고 after() , insertAfter() 메서드는 선택한 요소의 다음 위치에 새 요소를 생성한다.

$(‘요소선택’).before(‘새요소’) ; / $(‘새요소’).insertBefore(‘요소선택’);
$(‘요소선택’).after(‘새요소’) ; / $(‘새요소’).insertAfter(‘요소선택’);

3-1.2 append() / appendTo() / prepend() / prependTo()
append() , appendTo() 메서드는 선택한 요소 내의 마지막 위치에 새 요소를 생성하고 추가.
prepend() , prependTo() 메서드는 선택한 요소 내의 앞 위치에 새 요소를 생성하고 추가.

```jsx
$(‘요소선택’). append(‘새요소’) ; / $(‘새요소’). appendTo(‘요소선택’);
$(‘요소선택’). prepend(‘새요소’) ; / $(‘새요소’). prependTo(‘요소선택’);

```

```jsx
<script>
        $(function(){
            $("#pre").click(function(){
                $("#list").prepend("<li>prepend</li>");
            });
            $("#next").click(function(){
                $("#list").append("<li>append</li>");
            });
        })
    </script>
```

```jsx
<script>
        $(function(){
            $("#pre").click(function(){
                $("#list li").last().prependTo("#list");
            });
            $("#next").click(function(){
                $("#list li").first().appendTo("#list");
            });
        })
    </script>
```

3-1.3 clone() / empty() / remove()
clone()메서드는 선택한 요소를 복제. empty() 메서드는 선택한 요소의 모든 하위 요소를 삭제. remove()메서드는 선택한 요소를 삭제

```jsx
$(‘요소선택’).clone([true | false]) ;
$(‘요소선택’).empty() ;
$(‘요소선택’).remove() ;

```

3-1.4 replaceAll() / replaceWith()
replaceAll() , replaceWith()메서드는 선택한 모든 새 요소를 한꺼번에 바꿀 때 사용.

$(‘새요소’). replaceAll(‘요소선택’) ; / $(‘요소선택’). replaceWith(‘새요소’);

3-1.5 unwrap() / wrap() / wrapAll() / wrapInner()
unwrap()메서드는 선택한 요소의 부모 요소를 삭제한다. wrap() 메서드는 선택한 요소를 각각 새 요소로 감싼다.
wrapAll()메서드는 선택한 요소를 한꺼번에 새 요소로 감싼다. wrapInner() 메서드는 선택한 요소의 모든 하위 요소를 새 요소로 감싼다.

$(‘요소선택’). unwrap(); / $(‘요소선택’). wrap()(‘새요소’);
$(‘요소선택’). wrapAll(‘새요소’) ; / $(‘요소선택’). WrapInner(‘새요소’) ;
