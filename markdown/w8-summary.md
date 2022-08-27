# 8주차 summary

## Join

: 관계형 데이터베이스의 가장 큰 장점이자 핵심적 기능

일반적으로 레코드는 기본키{PK}나 외래키(FK) 값의 관계에 의해 결합함

-   INNER JOIN: 조건에 일치하는 (동일한 값이 있는) 행만 반환
    ```sql
    SELECT * FROM 테이블1 [INNER] JOIN 테이블2 ON 테이블1.컬럼 = 테이블2.컬럼;
    ```
-   OUTER JOIN: 동일한 값이 없는 행도 반환
    ```sql
    SELECT * FROM 테이블1 [LEFT|RIGHT|FULL] OUTER JOIN 테이블2 ON 테이블1.컬럼 = 테이블2.컬럼;
    ```
-   CROSS JOIN: 모든 데이터의 조합 / 모든 가능한 경우의 수의 Join
    ```sql
    SELECT * FROM 테이블1 CROSS JOIN 테이블2;
    ```

```sql
-- 3개의 테이블 조인
SELECT * FROM 테이블1
JOIN 테이블2 ON 테이블1.컬럼 = 테이블2.컬럼
JOIN 테이블3 ON 테이블2.컬럼 = 테이블3.컬럼;
```

## 모델링

데이터베이스 구조나 형식으로 모델 구조만 보고 어떤 데이터를 다루는지 알 수 있음

-   개념적 데이터 모델링
-   논리적 데이터 모델링
-   물리적 데이터 모델링

## ERD (Entity Relation Diagram) 개체 관계 모델

-   엔터티 Entity : 업무가 관여하는 정보
-   속성 Atrribute : 엔터티가 가지는 성격, 데이터 타입과 크기 및 제약사항 지정
-   관계 Relationship : 엔터티 간의 관계, 연관성

### 관계

-   카디널리티(Cardinality): 수적 관계

    -   1:1 관계
    -   1:N 관계 : A는 B를 여러 개 가지고 B는 A의 하나에 해당
    -   M:N 관계 : A는 B를 여러 개 가지고 B도 A를 여러 개 가짐

-   옵셔널리티
    -   필수
    -   선택

### 정규화

: 데이터베이스 테이블을 설계하는 과정에서 중복성을 제거해 성능을 향상 / 테이블을 규칙에 맞게 나누는 과정

역졍규화: 지나치게 많이 나눠져 있는 테이블들을 합치는 과정

-   제 1 정규화 : 도메인 원자값
-   제 2 정규화 : 부분적 함수 종속성 제거
-   제 3 정규화 : 이행적 함수 종속성 제거

## ORM

Object Relational Mapping
객체 지향 프로그래밍 언어를 사용하여 호환되지 않는 유형의 시스템간의 데이터를 변환하는 프로그래밍 기술

객체로 DB를 조작 / 파이썬 코드로 데이터를 조작

```python
from django.db import models

class Genre(models.Model):
	name = models.CharField(max_length=30)
```

### 모델 설계 및 반영

1. 클래스 생성하여 원하는 DB구조 작성
2. 클래스 내용으로 DB에 반영하기 위한 마이그레이션 파일 생성
3. DB에 migrate 함

### Migration

model에 생긴 변화를 DB에 반영하기 위한 방법, 마이그레이션 파일을 만들어 DB스키마를 반영

> 모델 변경되면 `makemigrations`

```bash
$ python manage.py makemigrations
$ python manage.py migrate
```

DB 조작 : `ClassName.objects.all()`

## ORM 기본 조작

Create

```python
Genre.objects.create(name='Rock')
#----
genre = Genre()
genre.name = 'Jazz'
genre.save()
```

Read

```python
Genre.objects.all()

Genre.objects.get(id=1)

Genre.objects.filter(id=1)
```

Update

```python
genre = Genre.objects.get(id=1)
genre.name = 'Swing'
genre.save()
```

Delete

```python
genre = Genre.objects.get(id=1)
genre.delete()
```

## QuerySet API

gt, gte

```python
Entry.objects.filter(id__gt = 4)
Entry.objects.filter(id__gte = 4)
```

```sql
SELECT ... WHERE id > 4;
SELECT ... WHERE id >= 4;
```

lt, lte

```python
Entry.objects.filter(id__lt = 4)
Entry.objects.filter(id__lte = 4)
```

```sql
SELECT ... WHERE id < 4;
SELECT ... WHERE id <= 4;
```

in

```python
Entry.objects.filter(id__in=[1, 3, 4])
Entry.objects.filter(headline__in='abc')
```

```sql
SELECT ... WHERE id IN (1, 3, 4);
SELECT ... WHERE headline IN ('a', 'b', 'c');
```

startswith, istartswith

```python
Entry.objects.filter(headline__startswith='Lennon')
Entry.objects.filter(headline__istartswith='Lennon')
```

```sql
SELECT ... WHERE headline LIKE 'Lennon%';
SELECT ... WHERE headline ILIKE 'Lennon%';
```

endswith

```python
Entry.objects.filter(headline__endswith='Lennon')
Entry.objects.filter(headline__iendswith='Lennon')
```

```sql
SELECT ... WHERE headline LIKE '%Lennon';
SELECT ... WHERE headline ILIKE '%Lennon';
```

contains

```python
Entry.objects.get(headline__contains='Lennon')
Entry.objects.get(headline__icontains='Lennon')
```

```sql
SELECT ... WHERE headline LIKE '%Lennon%';
SELECT ... WHERE headline ILIKE '%Lennon%';
```

range

```python
import datetime
start_date = datetime.date(2005, 1, 1)
end_date = dateime.date(2005, 3, 31)
Entry.objects.filter(pub_date__range=(start_date, end_date))
```

```sql
SELECT ... WHERE pub_date BETWEEN '2005-01-01' and '2005-03-31';
```

복합 활용

```python
inner_qs = Blog.objects.filter(name__contains='Cheddar')
entries = Entry.objects.filter(blog__in = inner_qs)
```

```sql
SELECT … WHERE [blog.id](http://blog.id) IN (SELECT id FROM … WHERE NAME LIKE ‘%Cheddar%’);
```

활용

```python
Entry.objects.all()[0]
Entry.objects.order_by('id')
Entry.objects.order_by('-id')
```

```sql
SELECT ... LIMIT 1;
SELECT ... ORDER BY id;
SELECT ... ORDER BY id DESC;
```

## ORM 확장 (1:N)

### Foreign Key (외래키)

-   키를 사용하여 부모 테이블의 유일한 값을 참조 (참조 무결성)
-   외래 키의 값이 반드시 부모 테이블의 기본 키일 필요는 없지만 유일한 값이어야 함

ForeignKey 사용하면 자동으로 변수이름뒤에 id 붙여줌

### models.ForeignKey 필드

-   2개의 필수 위치 인자
    -   Model class : 참조 모델
    -   on_delete : 외래 키가 참조하는 객체가 삭제되었을 때 처리 방식
        -   CASCADE : 부모 객체가 삭제 됐을 때 이를 참조하는 객체도 삭제
        -   PROTECT : 삭제되지 않음
        -   SET_NULL : NULL 설정
        -   SET_DEFAULT : 기본 값 설정

```python
class Genre(models.Model):
	name = models.CharField(max_length=30)

class Artist(models.Model):
	name = models.CharField(max_length=30)
	debut = models.DateField()

class Album(models.Model):
	name = models.CharField(max_length=30)
	genre = models.ForeignKey('Genre', on_delete=models.CASCADE)
	artist = models.ForeignKey('Artist', on_delete=models.CASCADE)

#Create
artist = Artist.objects.get(id=1)
genre = Genre.objects.get(id=1)

album = Album()
album.name = 'album1'
album.artist = artist
album.genre = genre
album.save()

#참조
album = Album.objects.get(id=1)
album.artist
album.genre

#역참조
genre = Genre.objects.get(id=1)
genre.album_set.all()
```
