# 12주차 summary

## Django

웹 서비스 개발에 필요한 것

-   로그인/아웃, 회원관리, DB, 서버, 클라이언트, 보안 등
    ⇒ 0 부터 만들 필요 없이 프레임워크 등을 활용해서 개발

### Framework 이해하기

-   프레임워크 = 서비스 개발에 필요한 기능들을 미리 구현해서 모아 놓은 것
-   소프트웨어 프레임워크 = 복잡한 문제를 해결하거나 서술하는데 사용되는 기본 개념 구조
-   프레임워크를 통해 소프트웨어의 생산성, 품질을 높일 수 있음

### Django

: Python으로 작성된 프레임워크, 여러 유용한 기능, 검증된 웹 프레임워크

### 클라이언트 - 서버 구조

-   클라이언트 : 웹 사용자의 인터넷에 연결된 장치, 웹 브라우저, 서비스를 요청하는 주체
-   서버 : 웹 페이지, 사이트 또는 앱을 저장하는 컴퓨터, 요청에 대해 서비스를 응답하는 주체

## Web browser & Web page

-   Web browser : 웹에서 페이지를 찾아서 보여주고 사용자가 하이퍼링크를 통해 다른 페이지로 이동할 수 있도록 하는 프로그램, 웹 페이지 파일을 우리가 보는 화면으로 렌더링해주는 프로그램
-   Web page : 웹에 있는 문서 (사용자가 보는 화면 각 한 장 한 장)
    -   정적 웹 페이지 : Static Web page, 있는 그대로 제공하는 것을 의미, 한 번 작성된 HTML 파일의 내용이 변하지 않고 모든 사용자에게 동일하게 전달 됨
    -   동적 웹 페이지 : Dynamic Web page, 사용자의 요청에 따라 웹 페이지에 추가적 수정이 되어 클라이언트에게 전달됨, 웹 페이지의 내용 변경 주체 == 서버

## Django 구조 이해하기

-   MVC 소프트웨어 디자인 패턴
    -   Model - View - Controller : 데이터 및 논리 제어를 구현하는데 사용되는 패턴
    -   목적 : 관심사 분리, 업무의 분리와 향상된 관리, 개발 효율성 및 유지보수 용이
-   MTV 소프트웨어 디자인 패턴
    -   Model - Template - View

## Django Quick start

django - 서버를 구현하는 웹 프레임워크

```bash
$ mkdir test
# 디렉토리 생성

$ python -m venv djangoPractice
# (가상환경용 폴더생성)

$ source djangoPractice/scripts/activate
#가상환경 실행)

$ deactivate
##가상환경 끄기)

$ pip install django==3.2.13
# 장고설치

$ django-admin startproject firstpjt(프로젝트이름) .(시작경로)
# 프로젝트 생성

$ python manage.py runserver
# 서버 구동 (로컬 호스트 http:#localhost:8000/)

$ rm -r test
#가상환경 지우기
```

### django 어플리케이션

```bash
$ . venv/Scripts/activate
#가상환경 생성 / 실행

$ pip intall django==3.2.13
# Django LTS 버전 설치

$ django-admin startproject projectName .
# Django 프로젝트 생성 -가상환경 폴더 경로 확인

$ python manage.py startapp articles
# Django 앱 생성

# 앱 등록 -- setting.py > INSTALLED_APPS 에 새로 생성한 앱 가장 위에 추가

$ python manage.py runserver
# 서버 실행 테스트
```

-   Project
    -   프로젝트 ⇒ 앱의 집합 = 프로젝트에는 여러 앱이 포함 될 수 있음 / 앱은 여러 프로젝트에 있을 수 있음
-   Application
    -   실제 요청을 처리하고 페이지를 보여주는 등의 역할 담당, 일반적으로 앱은 하나의 역할 및 기능 단위로 작성 (권장)

## 요청과 응답

주문서 정의 > 로직 구현 > HTML 페이지 구성 ⇒ URL > VIEW > TEMPLATE

### URLS

: 주소, 어떤 view 파일의 어떤 함수에서 handling 할 것 인지

```python
from articles import views

urlpatterns = [
	path('admin/', admin.site.urls),
	path('index/', view.index),
]
```

### Views

: HTTP 요청을 수신, HTTP 응답 반환할 함수 작성

```python
def index(request):
	return render(request, 'index.html')

#요청에 관한 정보가 들어오기 때문에 인자 = request 명명
```

`render()` : 주어진 템플릿과 컨텍스트 데이터를 결합하고 렌더링된 텍스트와 함께 HttpRequest 객재를 반환하는 함수 `render(request, templateName, context)`

### Templates

: 실제 내용을 보여주는데 사용되는 파일, 파일의 구조나 레이아웃 정의, 앱 폴더 안에 templates 폴더 생성 후 html 생성

## Django Template

: 데이터의 표현을 제어하는 도구이자 표현에 관련된 로직을 담당함

### Django Template Language (DTL)

-   조건, 반복, 변수 치환, 필터 등의 기능 제공
-   프로그래밍적 로직 X 프레젠테이션 표현을 위한 것

### DTL Syntax

-   Variable `{{ variable }}` : key-value 와 같이 딕셔너리 형태로 넘겨지며 key에 해당하는 문자열이 template에서 사용가능한 변수명, dot 으로 변수 속성에 접근 가능
-   Filter `{{ variable|filter }}` : 표시할 변수를 수정할 때 사용 (lower … 등, 일부 필터는 인자를 받기도 함)
-   Tags `{% tag %}` : 출력 텍스트를 만들거나 반복 또는 논리를 수행해 제어 흐름을 만드는 등 변수보다 복잡한 일들 수행, 일부 태그는 시작, 종료 태그 필요 `{% if %} {% endif %}`
-   Comments `{# #}` : 라인 주석 표기 (한 줄 주석만 사용 가능), 여러줄은 `{% comment %} {% endcomment %}`
