# 13주차 summary

## Django

```bash
$ mkdir 0926
    # 새 디렉토리 생성
$ cd 0926
    # 경로 이동
$ ls
    # 확인
$ python -m venv 0926-venv
    # 해당 디렉토리 가상환경 생성
$ source 0926-venv/Scripts/activate
(0926-venv)
    # 가상환경 실행
$ pip list
    # pip 확인
$ pip install django==3.2.13
    # django 설치
$ pip list
    # django 설치 확인
$ django-admin startproject pjt0926 .
(0926-venv)
    # 새 django 프로젝트 생성
$ python manage.py startapp articles
    # 앱 생성, settings.py에 추가
$ ls
    # manage.py 확인
$ code .
    # vs code 실행
---
$ python manage.py makemigrations

$ python manage.py migrate

--
$ pip freeze > requirements.txt
```

### Template inheritance

: 템플릿 상속 ⇒ 코드 재사용성

-   `{% extends 'base.html' %}` : 하위 템플릿 최상단에 작성하여 상속 받을 템플릿 알림
-   `{% block content %}` , `{% endblock content %}` : 하위 템플릿에 재지정 할 수 있는 블록 정의
-   추가 템플릿 경로 추가 : 기본 템플릿을 앱 안의 templates 가 아닌 프로젝트 최상단 templates에 위치하고 싶을 경우

    ```python
    TEMPLATES = [
    {
    	'BACKEND': 'django.template.backends.django.DjangoTemplates',
    	'DIRS': [BASE_DIR / 'templates',], # 다른 경로 추가
    	'APP_DIRS': True,
    	'OPTIONS': {
    		'context_processors': [
    			'django.template.context_processors.debug',
    			'django.template.context_processors.request',
    			'django.contrib.auth.context_processors.auth',
    			'django.contrib.messages.context_processors.messages',
    		],
    	},
    },
    ]
    ```

### Variable routing 작성

: 변수는 `<>` 에 정의, view 함수의 인자로 할당, 기본타입 - string

-   str `index/<name>/`
-   int `index/<int: num>/`
-   slug
-   uuid
-   path

### View 함수 작성

```python
 def hello(request, name):
	context = {
		'name' : name,
	}
	return render(request, 'index.html', context)
```

### Sending form data (Client)

### HTML form element

-   데이터가 전송되는 방법을 정의, HTTP 요청을 서버에 보내는 가장 편리한 방법
-   웹에서 사용자 정보를 입력하는 여러 방식을 제공, 사용자로부터 할당된 데이터를 서버로 전송하는 역할
-   데이터를 어디로 (action) 어떤 방식으로 (method) 보낼지

-   action : 입력 데이터가 전송될 URL 지정 , 데이터를 어디로 보낼 것인지 지정, 반드시 유효한 URL이어야 함, 속성 지정하지 않을 시 현재 페이지의 URL로 보내짐
-   method : 데이터를 어떻게 보낼 것인지 정의 , 입력 데이터의 HTTP request methods 를 지정, GET 방식, POST 방식

### HTML input element

-   사용자로부터 데이터를 입력 받기 위해 사용, type 속성에 따라 동작 방식 변경
-   name : name 으로 넘겨지는 값 연결, form 을 통해 데이터를 submit 했을 때 name 속성에 설정된 값을 서버로 전송, 서버는 name 속성에 설정된 값을 통해 사용자가 입력한 데이터 값에 접근 / 주요 용도 : GET, POST 방식으로 서버에 전달하는 파라미터로 매핑 (GET방식에서는 URL형식으로 데이터 전달)

### HTTP request methods

-   HTTP : HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜
-   웹에서 이뤄지는 모든 데이터 교환의 기초, HTTP 는 주어진 리소스가 수행하길 원하는 작업을 나타내는 request methods 정의
-   리소스에 대한 행위(수행하려는 동작) 정의, 주어진 리소스에 수행하길 원하는 행동
-   HTTP method : GET, POST, PUT, DELETE

### GET

-   서버로 부터 정보를 조회하는데 사용, 즉 서버에게 리소스를 요청하기 위해 사용
-   데이터를 가져올 때만 사용해야함, 데이터를 서버로 전송할 때 Query String Parameters 통해 전송 (데이터는 URL에 포함되어 서버로 전송됨)
    ```html
    <form action="#" method="GET">
    	<label>throw</label>
    	<input type="text" , name="message" />
    	<input type="submit" />
    </form>
    ```

### Query String Parameters (Query String)

-   사용자가 입력 데이터를 전달하는 방법 중 하나, url 주소에 데이터를 파라미터를 통해 전송
-   `http://host:port/path?key=value&key=value`
-   파라미터가 여러개일 경우 & 을 붙여 여러개의 파라미터를 넘김

## Retrieving thd data (Server)

: 데이터 가져오기 (검색하기)

-   서버는 클라이언트로 받은 key, value 쌍의 목록과 같은 데이터를 받음
-   접근 방법은 특정 프레임워크에 따라 상이함
    `<form action="/catch/" method="GET">`
-   모든 요청 데이터는 view 함수의 첫번째 인자 request에 들어있음 ⇒ request 객체 확인

```python
def catch(request):
	message = request.GET.get('message')
	context = {
		'message' : message,
		}
	return render(request, 'catch.html', context)
```

### Request and Response objects

: 요청과 응답 객체 흐름

1. 페이지가 요청되면 Django는 요청에 데한 메타데이터를 포함하는 HTTP Request object 생성
2. 해당하는 적절한 view 함수 로드 후 HTTP Request를 첫번쨰 인자로 전달
3. view 함수를 HTTP Request object 반환

### Django URLs

### Trailing Slashes

: Django는 URL 끝에 / 없으면 기본설정으로 / 를 자동으로 붙임

### App URL mapping

: 프로젝트 내 전체 app들의 path() 들을 프로젝트 `urls.py` 에서 모두 관리하는 것은 유지보수에 용이하지 않음 ⇒ urls.py 를 각 app 에 매핑

하나의 프로젝트에 여러 앱이 존재 할 때 각각 앱 폴더안에 urls.py를 만들고 path()를 작성한 뒤 전체 프로젝트 urls.py에 include로 연결

```python
# articles/urls.pyt
from django.urls import path
from . import views

urlpatterns = [
	path('', views.index),
]

#-----------------------

# pjt/urls.py

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
	path('admin/', admin.site.urls),
	path('articles/', include('articles.urls')),
]
```

### include()

: 다른 URLconf (app/urls.py) 들을 참조할 수 있도록 돕는 함수, include()를 만나면 URL의 그 시점까지 일치하는 부분을 잘라내고 남은 문자열 부분을 include된 URLconf 로 전달함

### Template namespace

: Django는 기본적으로 `app/templates/` 경로에 있는 templates 파일들만 찾을 수 있음, `settings.py` 의 INSTALLED_APPS 에 작성한 app 순서로 template 검색 후 렌더링

다른 앱에 있어도 templates 안에 있는 파일은 한 곳에 모이는 느낌… 앱은 다르지만 같은 폴더라고 인식하고 있어야 함

이를 분리하기 위해서는 templates 안에 앱 이름과 같은 폴더를 생성해서 html 파일 작성

하나의 base.html을 여러 앱에서 사용하려면 ⇒ 프로젝트 전체 폴더에 따로 폴더 생성 후 base.html 작성 하고 프로젝트의 `settings.py` 에서 아래와 같은 경로 추가

```python
# settings.py 경로 변경
"DIRS": [BASE_DIR / "templates"],
```

### Namespace

: 개체를 구분할 수 있는 범위를 나타냄

### URL namespace

: URL namespace를 사용하면 서로 다른 앱에서 동일한 URL 이름을 사용해도 구분해서 사용 가능 해짐

-   각 앱의 `urls.py`에 app_name 지정
-   url tag : `{% url 'articles:index' %}`

### Naming URL patterns

: path() 함수의 name 인자를 정의해서 사용, 특정 주소를 쉽게 참조할 수 있음

`{% url 'index' %}`

> <DRY 원칙 - Don’t Repeat Yourself>
> : 소스 코드에서 동일한 코드를 반복하지 말자

## Django 구조 이해하기 (MTV Design Pattern)

design = 설계

: 클라이언트 - 서버 의 구조도 SW 디자인 패턴 중 하나

### MTV

-   Model : 응용프로그램의 데이터 구조 정의, DB 기록 관리
-   Template : 화면 상 UI 구조, 레이아웃 정의
-   View : 클라이언트의 요청에 대해 처리를 분기하는 역할 (Controller)

### Model

ORM (Object Relational Mapping)

: Django는 Model을 통해 데이터에 접근, 조작함 / 일반적으로 각각의 모델은 하나의 데이터베이스 테이블에 매핑

### `models.py` 작성

```python
class Article(models.Model):
	title = models.CharField(max_length=10)
	content = models.TextField()
```

### Django Model Field

: Django에서는 데이터 유형에 따라 다양한 모델 필드 제공

TextField(), CharField(), IntegerField(), DateTimeField() 등

### Migrations

: 모델에 변경사항이 생길 때 새로운 migration 생성, 모델의 변경사항과 데이터베이스 동기화

```bash
$ python manage.py makemigrations
$ python manage.py migrate
```

### Update

: 수정에는 사용자의 입력을 받을 페이지를 렌더링할 함수와 사용자가 입력한 데이터를 전송 받아 DB에 저장할 함수가 필요함

```python
# urls.py

urlpatterns = [
	path("edit/<int:post_pk>", views.edit, name="edit"),
  path("update/<int:post_pk>", views.update, name="update"),
	}
```

```python
# views.py
def edit(request, post_pk):
    post = Post.objects.get(pk=post_pk)
    context = {
        "post": post,
    }
    return render(request, "posts/edit.html", context)

def update(request, post_pk):
    post = Post.objects.get(pk=post_pk)
    title = request.GET.get("title")
    content = request.GET.get("cont")

    # 수정
    post.title = title
    post.content = content
    post.save()
    return redirect("posts:detail", post_pk)
```

```html
<!-- edit.html -->
<form action="{% url 'posts:update' post.pk %}">
	<label for="title">제목</label>
	<input type="text" name="title" value="{{ post.title }}" />
	<label for="cont">내용</label>
	<input type="text" name="cont" value="{{ post.content }}" />
	<button type="submit">게시</button>
</form>
```
