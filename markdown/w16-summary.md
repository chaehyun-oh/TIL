# 16주차 summary

## 이미지 업로드

### Media 관련 필드

-   ImageField : 이미지 업로드에 사용하는 모델 필드, FileField 상속받는 서브클래스 (사용하려면 pillow 라이브러리 필요)
-   FileField : 파일 업로드에 사용하는 모델 필드, 인자 - `upload_to` , `storage`

### 모델설정

-   `upload_to` : 문자열 경로 지정 또는 함수 호출

    ```python
    class Article(models.Model):
    	image = models.ImageField(upload_to="images/")
    ```

    ```python
    def article_image_path(instance, filename):
    	return f`user_{instance.user.pk}/{filename}`

    class Article(models.Model):
    	image = models.ImageField(upload_to=article_image_path)
    ```

-   `blank` : True 인 경우 필드 비워둘 수 있음, 유효성 검사에서 빈 값 가능

### URL 설정

-   MEDIA_ROOT : 사용자가 업로드한 파일들을 보관할 디렉토리 절대 경로 (django는 성능을 위해 업로드 파일을 DB에 저장하지 않음, 실제 DB에 저장되는 것은 파일 경로)
-   MEDIA_URL : MEDIA_ROOT 에서 제공되는 미디어를 처리하는 URL, 업로드 된 파일의 주소 생성 역할

### HTML 설정

-   form - enctype(인코딩) 속성
    -   `multipart/form-data` : 파일/이미지 업로드 시 반드시 사용 (전송되는 데이터 형식 지정)
    -   `application/x
        www form urlencoded
    -   `text/plain` : 인코딩 하지 않은 문자 상태로 전송, 공백은 + 기호로 변환, 특수문자는 인코딩X

### 이미지 업로드 설정

Pillow 설치: python 이미지 라이브러리

⇒ `model.py`에 이미지 필드 지정

```python
class Article(models.Model):
    title = models.CharField(max_length=20)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    image = ProcessedImageField(
        upload_to="images/",
        blank=True,
        processors=[ResizeToFill(500, 400)],
        format="JPEG",
        options={"quality": 80},
    )
    thumbnail = ImageSpecField(
        source="image",
        processors=[Thumbnail(400, 300)],
        format="JPEG",
        options={"quality": 60},
    )
```

⇒ `form.py`에서 image 추가

```python
class ArticleForm(forms.ModelForm):
    class Meta:
        model = Article
        fields = ["title", "content", "image"]
```

⇒ `HTML form` 태그에 `enctype="multipart/form-data"` 지정

```html
<form action="" method="POST" enctype="multipart/form-data">
	{% csrf_token %} {% bootstrap_form article_form %} {% if
	request.resolver_match.url_name == 'create' %} {%bootstrap_button
	button_type="submit" content="등록"%} {% else %} {%bootstrap_button
	button_type="submit" content="수정"%} {% endif %}
</form>
```

⇒ `views.py`에서 create, update 함수 수정 : `request.FILES` 추가

```python
def create(request):
    if request.method == "POST":
        article_form = ArticleForm(request.POST, request.FILES)
        if article_form.is_valid():
            article_form.save()
            return redirect("articles:index")
    else:
        article_form = ArticleForm()
    context = {
        "article_form": article_form,
    }
    return render(request, "articles/form.html", context)

def update(request, article_pk):
    article = Article.objects.get(pk=article_pk)
    if request.method == "POST":
        article_form = ArticleForm(request.POST, request.FILES, instance=article)
        if article_form.is_valid():
            article_form.save()
            return redirect("articles:detail", article.pk)
    else:
        article_form = ArticleForm(instance=article)
    context = {
        "article_form": article_form,
    }
    return render(request, "articles/form.html", context)
```

⇒ `settings.py`에서 MEDIA_URL, MEDIA_ROOT 설정 & imagekit INSTALLED_APPS에 추가

```python
MEDIA_ROOT = BASE_DIR / "images"
MEDIA_URL = "/media/"
```

⇒ `url.py`에 static 경로 추가

```python
urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include("articles.urls")),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

⇒ templates에 가져오기

```html
{% if article.image %}
<img src="{{ article.image.url }}" alt="{{ article.image }}" width="100%" />
{% endif %}
```

## 이미지 resizing

`django-imagekit` 라이브러리 사용, 업로드 될 때 이미지 자체를 resizing

model.py에서 image 속성수정

```python
from imagekit.models import ProcessedImageField
from imagekit.processors import ResizeToFill
from django.db import models
# Create your models here.

class Article(models.Model):
    title = models.CharField(max_length=20)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    image = ProcessedImageField(upload_to='images/', blank=True,
                                processors=[ResizeToFill(400, 300)],
                                processors=[ResizeToFill(1200, 960)],
                                format='JPEG',
                                options={'quality': 80})
```

## Message 추가

views.py에 messages 등록

```python
from django.contrib import messages

def create(request):
    if request.method == "POST":
        article_form = ArticleForm(request.POST, request.FILES)
        if article_form.is_valid():
            article_form.save()
            messages.success(request, "글이 등록되었습니다.")
            return redirect("articles:index")
    else:
        article_form = ArticleForm()
    context = {
        "article_form": article_form,
    }
    return render(request, "articles/form.html", context)
```

⇒ templates에 가져오기

```html
{% if messages %} {% for message in messages %}
<div
	class="alert alert-{{message.tags}} alert-dismissible fade show"
	role="alert"
>
	{{ message }}
	<button
		type="button"
		class="btn-close"
		data-bs-dismiss="alert"
		aria-label="Close"
	></button>
</div>
{% endfor %} {% endif %}
```

## 댓글 기능 구현

models.py에서 Comment 모델 정의

```python
class Comment(models.Model):
    content = models.TextField(max_length=150)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
```

⇒ forms.py에서 ModelForm 작성

```python
class CommentForm(forms.ModelForm):
    class Meta:
        model = Comment
        fields = [
            "content",
        ]
```

⇒ detail 함수에 CommentForm 추가

```python
def detail(request, article_pk):
    article = Article.objects.get(pk=article_pk)
    comment_form = CommentForm()
    context = {
        "article": article,
        "comments": article.comment_set.all(),
        "comment_form": comment_form,
    }
    return render(request, "articles/detail.html", context)
```

⇒ 댓글 작성 함수 추가, url 지정

```python
def comment_create(request, article_pk):
    article = Article.objects.get(pk=article_pk)
    comment_form = CommentForm(request.POST)
    if comment_form.is_valid():
        comment = comment_form.save(commit=False)
        comment.article = article
        comment.save()
    return redirect("articles:detail", article_pk)
```

⇒ templates

```html
<div class="mt-3">
	<h5>댓글</h5>
	<form action="{% url 'articles:comment_create' article.pk %}" method="POST">
		{% csrf_token %} {% comment %} {% bootstrap_form comment_form %} {%
		endcomment %} {% comment %} {%bootstrap_button button_type="submit"
		content="등록"%} {% endcomment %}
		<div class=" input-group">
			{%render_field comment_form.content class+="form-control" rows="1"
			cols="70"%}
			<button
				class="btn btn-outline-primary"
				type="submit"
				id="button-addon2"
			>
				등록
			</button>
		</div>
	</form>
	<div class="mt-4  card">
		<ul class="list-group list-group-flush">
			{% for comment in comments %}
			<li class="list-group-item">
				{{ comment.content }}
				<span>| {{ comment.created_at }}</span>
			</li>
			{% empty %}
			<li class="list-group-item">작성된 댓글이 없습니다.</li>
		</ul>
	</div>
	{% endfor %}
</div>
```

## Comment에 유저 추가

한 명의 유저가 여러 comment 작성 가능

⇒ Comment 모델에 User 모델 참조 외래키 작성

```python
class Comment(models.Model):
    content = models.TextField(max_length=150)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
```

⇒ CommentForm 필드 수정

```python
class CommentForm(forms.ModelForm):
    class Meta:
        model = Comment
        exclude = (
            "article",
            "user",
        )
```

⇒ views.py 내 함수에서외래키 누락 해결

```python
@login_required
def comment_create(request, article_pk):
    article = Article.objects.get(pk=article_pk)
    comment_form = CommentForm(request.POST)
    if comment_form.is_valid():
        comment = comment_form.save(commit=False)
        comment.article = article
        comment.user = request.user
				# 댓글 작성자 저장
        comment.save()
    return redirect("articles:detail", article_pk)
```

⇒ templates에 출력

```html
<div class="mt-4  card">
	<ul class="list-group list-group-flush">
		{% for comment in comments %}
		<li class="list-group-item">
			{{comment.user.username}} | {{ comment.content }}
			<span>| {{ comment.created_at }}</span>
		</li>
		{% empty %}
		<li class="list-group-item">작성된 댓글이 없습니다.</li>
	</ul>
</div>
{% endfor %}
```

+) 유저 프로필 페이지에서 작성 글, 작성 댓글 목록 출력

```html
<h1>{{ user.username }}님의 프로필</h1>
<p>{{ user.full_name }} | {{user.email}}</p>
<h4>작성한 글</h4>
<p>게시글 : {{user.article_set.count}} 개</p>
{% for article in user.article_set.all %}
<p>
	{{ forloop.counter }}
	<a href="{% url 'articles:detail' article.pk %}">{{ article.title }}</a>
</p>
{% endfor %}

<h4>작성한 댓글</h4>
<p>댓글: {{user.comment_set.count}} 개</p>
{% for comment in user.comment_set.all %}
<p>
	{{forloop.counter}}
	<a href="{% url 'articles:detail' comment.article_id %}">
		{{comment.content}}
	</a>
</p>
{% endfor %}
```
