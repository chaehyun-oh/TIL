# 14주차 summary

## Django

### GET / POST

-   get : 리소스의 표현, 데이터를 조회할 때 사용
-   post : 서버에 상태를 변화 시키고 제출 / url이 아니라 요청 데이터 안에서 데이터를 넘김

## Django ModelForm

: 사용자의 입력 값와 DB 데이터 형식의 일치를 확인하는 유효성 검증이 필요하고 서버 사이드에서 반드시 처리해야 함

### ModelForm 선언

: 어떤 모델을 기반으로 form 작성할 것 인지에 대한 정보 ⇒ Meta 클래스에 지정

```python
# articles/forms.py

from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):

	class Meta:
		model = Article
		fields = '__all__'
```

### ModelForm 활용

-   ModelForm 객체를 context로 전달 (`views.py`)
-   Input Field 활용 (`html`)
    -   as_p() : 각 필드 p 태그로 감싸져 렌더링
    -   as_ul() : 각 필드 li 태그로 감싸져 렌더링
    -   as_table() : 각 필드 tr 태그로 감싸져 렌더링

```python
# articles/views.py

from .forms import ArticleForm

def new(request):
	form = ArticleForm()
	context = {
		'form' : form,
	}
	return render(request, 'aricles/new.html', context)
```

```html
<!-- articles/new.html -->
<form action="{% url 'articles:create' %} method="POST">
	{% csrf_token %}
	{{ form.as_p }}
	<input type="submit">
</form>
```

## ModelForm with view functions

```python
# articles/forms.py
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    class Meta:
        model = Article
        fields = ["title", "content"]
        widgets = {
            "title": forms.TextInput(
                attrs={"class": "form-control", "placeholder": "제목"}
            ),
            "content": forms.Textarea(
                attrs={"class": "form-control", "placeholder": "내용"}
            ),
        }
```

## Admin site

: 관리자 페이지 ⇒ 서버의 관리자가 활용하기 위한 페이지, 레코드 생성 여부 확인 유용, 직접 레코드 삽입도 가능

django 관리

: id, pin 생성 ⇒ `python manage.py createsuperuser`

`admin.py` 에서 관리 가능 ⇒ 모델 데이터베이스를 관리

```python
# articles/admin.py
from django.contrib import admin
from .models import Article

class ArticleAdmin(admin.ModelAdmin):
    fields = ['title']

admin.site.register(Article, ArticleAdmin)
```

## Static files

: 정적 파일도 장고 템플릿에서 경로 지정해서 사용 가능, 정적 파일들을 관리하기 위한 설정

앱 내에 static 폴더 생성 후 해당 경로에 이미지 삽입 후 경로 사용 / css, js, img 등 관리 가능함

`{% load static %}` : 파이썬의 import와 유사하다고 생각 ⇒ 최상단에 작성

### 정적 파일 활용

-   `settings.py` 에서 INSTALLED_APPS 에 `django.contrib.staticfiles` 확인
-   `settings.py` 에서 STATIC_URL 정의
-   템플릿 최상단에 `{% load static %}` 작성 후 경로에 `{% static 'images/img.jpg' %}` 와 같이 경로 지정
-   앱의 static 디렉토리 생성 후 정적 파일 저장
-   `settings.py` 에서 `STATICFILES_DIRS = [BASE_DIR / 'static']` 지정

-   STATIC_URL : STATIC_ROOT에 있는 정적 파일들을 참조할 때 사용할 URL, 실제 파일이나 디렉토리 아님, URL로만 존재
-   STATIC_ROOT : collectstatic이 배포를 위해 정적 파일을 수집하는 절대 경로, django 프로젝트에서 사용하는 모든 정적 파일을 한 곳에 모아 넣는 경로, 실 서비스 환경(배포 환경)에서 django의 모든 정적 파일을 다른 웹 서버가 직접 제공하기 위함.
-   collectstatic
    -   `settings.py` 에서 `STATIC_ROOT = BASE_DIR / ‘staticfiles’` 작성
    -   `$ python manage.py collectstatic` 명령어 실행
    -   _개발 환경에서는 사용 X_

## 템플릿 분기점

-   하나의 form.html 을 new, update 함수에 연결
-   `request.resolver_match.url_name` 속성 사용해서 create와 update url 구분하여 if 문 활용

```python
# views.py
def create(request):
    if request.method == "POST":
        movie_form = MovieForm(request.POST)
        if movie_form.is_valid():
            movie_form.save()
            return redirect("movies:index")
    else:
        movie_form = MovieForm()
    context = {
        "movie_form": movie_form,
    }
    return render(request, "movies/form.html", context=context)
```

```html
{% if request.resolver_match.url_name == 'create' %}
<h3>영화 정보 작성</h3>
{% else %}
<h3>영화 정보 수정</h3>
{% endif %}
<form action="" method="POST">
	{% csrf_token %} {% bootstrap_form movie_form %} {% buttons %}
	<button type="submit" class="btn btn-primary ">등록</button>
	{% endbuttons %}
</form>
```
