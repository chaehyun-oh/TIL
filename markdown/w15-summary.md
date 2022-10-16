# 15주차 summary

## Django Auth

: Django authenthication system (인증 시스템)은 인증(Authentication) 과 권한(Authorization) 부여를 함꼐 제공

⇒ user, 권한 및 그룹, 암호 해시 시스템, Form 및 View 도구, 기타 적용 가능한 시스템 (암호화)

-   Authentication (인증) : 신원 확인
-   Authorization (권한, 허가) : 권한 부여, 인증된 사용자가 수행할 수 있는 작업 결정

### User model 활용하기

: Django는 기본적인 인증 시스템과 여러 필드가 포함된 User model 제공

Django auth 에 존재하는 user model 사용 ⇒ `auth_user` 가져와서 ⇒ 클래스 상속으로 사용하기

대부분의 개발 환경에서 기본 User model ⇒ Custom User Model 로 대체

⇒ Custom User Model 사용하면 기본 User Model 과 동일하게 작동 하면서도 이후 필요시 맞춤 설정이 가능함

### AUTH_USER_MODEL

: 프로젝트에서 User를 나타낼 때 사용하는 모델, 프로젝트 진행되는 동안 변경 불가, 프로젝트 시작 시 설정하기 위함, 참조하는 모델은 첫 번째 migration에서 사용가능해야 함

기본 값 `AUTH_USER_MODEL='auth.User'`

### 대체하기

AbstractUser 상속 받는 Custom User class 작성 ⇒ Django 프로젝트에서 User 나타내는데 사용하는 모델을 앞서 생성한 Custom User Model 로 지정 `AUTH_USER_MODEL = ’accounts.User’` ⇒ admin.py 에 Custom User Model 등록 `admin.site.register(User, UserAdmin)`

### User 객체

: 인증 시스템의 가장 기본

기본 속성 : username, password, email, first_name, last_name

-   생성 `user = User.objects.create_user('luke', 'luke@gmail.com', 'q1w2e3r4!')`
-   password 변경 `user = User.objects.get(pk=2) \n User.set_password('new password') \n User.save()`
-   인증 (password confirm) `from django.contrib.auth import authenticate \n user = authenticate(username='luke', password='q1w2e3r4!')`

### 암호 관리

: 일반적으로 회원가입시 password 저장은 필수적, 별도 처리 필요

Django에서는 기본 PBKDF2(Password-Based Key Derivation Function) 를 사용해 저장 : 단방향 해시함수 활용해 password를 다이제스트로 암호화 (복호화 불가능) 그러나 단방향 해시함수의 경우 레인보우 공격 및 무차별 대입 공격들에 문제 발생 가능. 이를 보완하기위해 솔팅(Salting), 키 스트레칭(Key Stretching)을 추가적으로 활용

-   Salting : password에 임의의 문자열 추가하여 다이제스트 생성
-   Key Stretching : 해시를 여러번 반복하여 시간 늘림

## 회원가입

### UserCreationFrom

: 주어진 username, password로 권한 없는 새 user 생성하는 ModelForm

필드 : username, password1, password2

### UserCreationForm() custom

: 기존 UserCreationForm 상속받아 user model 재정의

`get_user_model()` 현 프로젝트에서 활성화된 사용자 모델 반환

```python
# accounts/forms.py

from django contrib auth import get_user_model
from django contrib auth forms import UserCreationForm

class CustomUserCreationForm(UserCreationForm):
	class Meta(UserCreationForm Meta):
		model = get_user_model()
```

# Django 10

## 로그인에 대한 이해

HTTP : Hyper Text Transfer Protocol, HTML 문서 같은 리소스들을 가져올 수 있도록 해주는 프로토콜, 웹에서 이뤄지는 모든 데이터 교환의 기초

HTTP 특징

-   비연결지향 (connectionless) : 서버는 요청에 대한 응답 보낸 후 연결 끊음
-   무상태 (stateless) : 연결을 끊는 순간 클라이언트-서버 간 통신이 끝남, 상태 정보 유지 X, 클라이언트-서버 간 주고받는 메세지들은 서로 독립적

그럼에도 로그인 상태가 유지되는 이유 ⇒ 클라이언트-서버 간 지속적 상태유지를 위해 쿠키 & 세션이 존재

### 쿠키 (Cookie)

: 서버가 사용자의 웹 브라우저(클라이언트)에 전송하는 작은 데이터 조각, 쿠키- 서로 다른 요청이 동일 브라우저에서 발생한 것인지 판단할 때 주로 사용

쿠키 사용 목적 : 세션 관리, 개인화, 트래킹

쿠키 Lifetime : Session cookie-현 세션 종료시 삭제, Persistent cookie-expires 속성에 지정된 날짜 or Max-Age 속성에 지정된 기간 지나면 삭제

### 세션 (Session)

: 사이트-특정 브라우저 간 상태(state)를 유지시키는 것, 클라이언트가 서버에 접속하면 서버가 특정 session id 발급 ⇒ 클라이언트는 session id 쿠키에 저장 / session id는 세션 구별위해 필요, 쿠키에는 session id만 저장

### Session in Django

: Django는 database-backed sessions 저장 방식 (기본 값) session 정보 ⇒ Django DB > django_session 테이블에 저장 (설정 통해 변경 가능)

Django는 특정 session id 포함하는 쿠키 사용해 각 브라우저-사이트가 연결된 session을 확인

## login

### AuthenticationForm

: 로그인을 위한 built-in form, 로그인 하려는 사용자 정보를 입력 받음(username, password), 일반 Form 상속 받음, ModelForm X , request가 첫번째 인자

-   `login(request, user, backend=None)` : 인증된 사용자 로그인 (유저 정보 반드시 인증된 유저 정보여야 함 ⇒ `authenticate()` 함수로 인증 or AuthenticationForm, `.is_valid()`
-   `get_user()` :AuthenticationForm의 인스턴스 메서드, 유효성 검사 통과하면 로그인한 사용자 객체 반환함

```python
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login

def login(request):
    if request.method == "POST":
        form = AuthenticationForm(request, data=request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect(request.GET.get("next") or "articles:index")
    else:
        form = AuthenticationForm()
    context = {
        "form": form,
    }
    return render(request, "accounts/login.html", context)
```

## Authentication with User

템플릿에서 context 없이 `{{ user }}` 로 사용자 출력이 가능한 이유

⇒ settings.py > context processors 설정 > `‘django.contrib.auth.context_processors.auth’`

context processors : 템플릿이 렌더링될 때 호출 가능한 context 데이터 목록, django에서 자주 사용하는 데이터 목록을 미리 템플릿에 로드해 둔 것

## logout

`logout()` : 요청 유저에 대한 세션 정보를 삭제, 사용자가 로그인한 경우 오류 발생 X

```python
from django.contrib.auth import logout as auth_logout

def logout(request):
    auth_logout(request)
    return redirect("articles:index")
```

## Limiting access to logged-in users

: 로그인 사용자에 대한 접근 제한 ⇒ `is_authenticated` attribute 를 활용한 조건문, login_required decorator 활용한 view 제한

-   is_authenticated : User model 속성 중 하나, 사용자 인증 여부를 알 수 있음, 일반적으로 `request.user.is_authenticated` 로 사용
-   login_required decorator : `@login_required` 로그인 하지 않은 경우 settings.py > LOGIN_URL 문자열 주소로 redirect (기본 /accounts/login/ )
    -   로그인 페이지 리다이렉트, URL 확인 : 인증 성공 시 redirect 되야하는 경로 ‘next’ 쿼리문자열 매개 변수에 저장됨 `return redirect(request.GET.get("next") or "articles:index")`
    -   ‘next’ query string parameter : 만약 login 템플릿 form action 작성된 경우 동작 안함 주의.

## 회원정보 수정

1번 유저, 2번 유저… 방식 X ⇒ 로그인한 유저의 정보를 수정

### UserChangeForm

: 사용자 정보, 권한 변경을 위해 admin 인터페이스에서 사용되는 ModelForm ⇒ instance 인자로 user 데이터 정보 받는 구조

### CustomUserChangeForm fields 재정의

: 세부 필드들 직접 fields 정의해서 원하는 형식으로 활용

```python
from django.contrib.auth.forms import UserCreationForm, UserChangeForm
from django.contrib.auth import get_user_model

class CustomUserCreationForm(UserCreationForm):
    class Meta:
        model = get_user_model()
        fields = ("username",)

class CustomUserChangeForm(UserChangeForm):
    class Meta:
        model = get_user_model()
        fields = (
            "first_name",
            "last_name",
            "email",
        )
```

## 비밀번호 변경

### PasswordChangeForm

: 사용자가 비빌번호를 변경할 수 있도록 하는 form, 기존 비밀번호 입력해서 비밀번호 변경

### AbstractBaseUser의 모든 subclass와 호환되는 forms

-   forms.ModelForm
    -   UserCreationForm
    -   UserChangeForm
-   forms.Form
    -   AuthenticationForm
    -   SerPasswordForm
    -   PasswordChangeForm
    -   AdminPasswordChangeForm

### 암호 변경 시 세션 무효화 방지

`update_session_auth_hash(request, user)`

: 현재 요청과 새 세션 데이터가 파생될 업데이트된 사용자 객체를 가져오고 세션 데이터를 적절히 업데이트 해 줌, 암호가 변경되어도 로그아웃 되지 않도록 새 암호와 세션 데이터로 세션을 업데이트 함

```python
from django.contrib.auth import update_session_auth_hash
from django.contrib.auth.forms import PasswordChangeForm

def change_password(request):
    if request.method == "POST":
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
            form.save()
            update_session_auth_hash(request, form.user)
            # 변경 시 세션무효화 방지
            return redirect("articles:index")
    else:
        form = PasswordChangeForm(request.user)
    context = {
        "form": form,
    }
    return render(request, "accounts/change_password.html", context)
```
