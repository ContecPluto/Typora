## URL Namespace

```python
app_name = 'articles'
urlpatterns = [    
    path('', views.index, name='index'),
    path('new/', views.new, name='new'),
    path('create/', views.create, name='create'),
    path('<int:pk>/', views.detail, name='detail'),
    path('<int:pk>/delete/', views.delete, name='delete'),
    path('<int:pk>/edit/', views.edit, name='edit'),
    path('<int:pk>/update/', views.update, name='update'),
]
```



1. 하드코딩 URL제거

{% url  'name' %} template tag

**문제점**

app이 여러개가 되면, 단순히 url name만 가지고는 어떤 app의 url인지 알 수 없다.



2. URL namespace 설정

따라서 app_name 을 정해주어 namespace를 설정합니다.

```html
  a href="{% url 'articles:edit' article.pk %}">[EDIT]</a>
```

이후 다음과 같이 코딩하여 앱네임과 url name 그리고  필요하다면 변수도 작성합니다



## URI

- 인터넷에 자원을 나타내는 유일한 주소
- 인터넷에서 요구도는 기본조건으로서 http 에 항상 붙어 다닌다.



## URL

- 인터넷 상에서 자원이 어디 있는지 알려주기 위한 규약



https://www.google.com

- 서버 주소 (URL이면서 URI 이다.)



https://github.com/ss-02-djpy2/TIL/blob/master/03_django/markdown/Django_04.md

- 주소 + 디렉토리 파일의 주소(자원의 위치)
- URL 이면서 URI



https://www.google.com/search?q=삼성

- 주소 + 특정 문자열(query string)(`search?q=`)
- search 까지가 URL + `q=삼성` 이라는 식별자가 필요하므로 URI이지만 URL은 아니다.

일반적 : scheme/protocol + Host + Port + path



GET / POST / PATCH(PUT) / DELETE

실제로 HTTP 에서는 공식적으로 GET POST만 공식적으로 사용된다.



같은 주소로 들어가는데 get 이냐 post 냐에 따라 행동을 다르게할 것이다.(**new**(GET) + **create**(POST))

GET articles/create/ 글을 작성하는 페이지

POST articles/create/ 글이 실제로 작성



form tag 에 action 이 없다면, 현재 머물고 있는 URL로 요청을 보낸다.



## Model Instance Method

### 1. `get_absolute_url()`

```python
from django.urls import reverse
from django.db import models


# Create your models here.

class Article(models.Model):
    title = models.CharField(max_length=20)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    update_at = models.DateTimeField(auto_now=True)

    #객체 표현
    def __str__(self):
        return self.title

    def get_absolute_url(self):
        # return f'/articles/{ self.pk }/'
        # return reverse('articles:detail', args=[self.pk]) # articles/10/
        return reverse('articles:detail', kwargs={'pk': self.pk}) # articles/10/
        # 주의사항
        # reverse 함수에 args 랑 kwargs를 동시에 인자로 보낼 수 없다.
```



## URL Reverse를 수행하는 함수들

### 1. reverser()

- 리턴 값 : string(문자열)

```python
reverse('articles:index') # '/articles/'
```



### 2. redirect()

- 리턴 값 : httpResponseRedirect(객체)
- 내부적으로 `resolve_url()`을 사용
- view 함수에서 특정 url 로 돌려보내고자 할 때 사용

```python
redirect('articles:article')
# <HttpResponseRedirect status_code200, "text/html; charset=utf-8, url=/articles/">
```



### 3. url template tag({% url %})

- 내부적으로  `reverse()`를 사용



### 4. redirect(`모델 인스턴스`)를 통해서 모델 인스턴스의 get_absolute_url()함수를 자동으로 호출





