# 2019-09-25_django_form

> https://docs.djangoproject.com/en/2.2/ref/templates/builtins/

articles => forms.py 

```python
from django import forms

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField()
    
```







`is_valid`

- form 객체의 유효성 검사를 한는데 가장 중요한 역할.
- form 객체가 생성되면, 유효성 검사를 하고 유효한지 아닌지 여부를 boolean으로 반환.



`cleaned_data`

- 유효성 검사 후 깔끔하고 정제된 dict 형태에서 데이터를 가져오는 방법
- `request.POST.get()` 의 방식은 절대 추천하지 않는다.



`Forms as HTML`

- `as_p()` : 각 필드가 단락(paragraph)으로 렌더링
- `as_ul()` : 각 필드가 목록 항목(list item)으로 렌더링

- `as_table()` : 각 필드가 테이블 행으로 렌더링

```
In [8]: form.as_p()
Out[8]: '<p><label for="id_title">Title:</label> <input type="text" name="title" value="몇번째 지" maxlength="10" required id="id_title"></p>\n<p><label for="id_content">Content:</label> <input type="text" name="content" value="모르겟네" required id="id_content"></p>'

In [9]: form.as_table()
Out[9]: '<tr><th><label for="id_title">Title:</label></th><td><input type="text" name="title" value="몇번째 지" maxlength="10" required id="id_title"></td></tr>\n<tr><th><label for="id_content">Content:</label></th><td><input type="text" name="content" value="모르겟네" required id="id_content"></td></tr>'

In [10]: form.as_ul()
Out[10]: '<li><label for="id_title">Title:</label> <input type="text" name="title" value="몇번째 지" maxlength="10" required id="id_title"></li>\n<li><label for="id_content">Content:</label> <input type="text" name="content" value="모르겟네" required id="id_content"></li>'
```







form 을 사용하는 3가지 방법

```html
{{ form.title.label_tag }}
{{ form.title }}
{{ form.content.label_tag }}
{{ form.content }}

{% for field in form  %}
{{ field.label_tag }}
{{ field }}
{% endfor %}

{{ form.as_p }}
```

```
In [1]: form
Out[1]: <ArticleForm bound=True, valid=Unknown, fields=(title;content)>

In [2]: request.POST
Out[2]: <QueryDict: {'csrfmiddlewaretoken': ['UtbwCKbE85sw2RbXjTXJgYV6mx8CJTwTf4sztQRv46sp4CCFRyeoR2V4nYqNsuQx'], 'title': ['몇번째 지'], 'content': ['모르겟네']}>

In [3]: type(form)
Out[3]: articles.forms.ArticleForm

In [4]: form.is_valid()
Out[4]: True

In [5]: form
Out[5]: <ArticleForm bound=True, valid=True, fields=(title;content)>
```

```ipython
form.cleaned_data
{'title': '몇번째 지', 'content': '모르겟네'}
```



### `widget`

- django form 을 사용하면 기본적으로 field 에 맞는 default widget을 사용한다.
- 그러네 다른 widget 을 사용하고 싶다면 `widget`인자를 통해 field를 새로 정의할 수 있다.



### get_object_or_404()

- 해당 객체가 있다면 `objects.get()`을 실행하고, 없으면  **ObjectDoesNotExist** 예외가 아닌 **Http404(HttpResponseNotFound)**를 raise한다.

왜 404 error 가 나올 상황에 django 는 500 error를 발생시켰을까?

- `.get()` 메서드는 조건에 맞는 데이터가 없는 경우에 에러를 뿜게 설계되어있다. 코드 단계에서 발생한 에러에 대해서는 브라우저는 **500 Internal Server Error** 로 인식.
- 클라이언트 입장에서 `서버에 오류가 발생하여 요청을 수행할 수 없다(500)` 라는 원인이 정확하지 않은 에러를 마주하기 떄문에 올바른 에러를 예외처리하고 발생 시키는 것 또한 개발에서 중요한 요소 중 하나이다.



### initial

- form 이 나타날 때 해당 필드의 초기 값
- HTML input 태그의 `value` 속성을 사용했던 것과 동일.
- 초기 값을 설정하는 인수는 딕셔너리자료형이어야 한다.



## django ModelForm

- 일반 form과 다르게 Model 로부터 Form을 자동으로 생성하는 기능
- form class 안에 Meta 클래스를 정희하고, Meta 클래스 안에 Model 속성에 해당하는 모델 클래스를 지저한다. 즉, 어떤 모델을 기반으로 form을 작성할 것인지를 지정한는 것이다.
- 일반 Form 에 비해 모델 정의를 다시 하지 않아서 쉽고 간결하게 작성 가능하다.

- django가 해당 모델에서 양식에 필요한 대부분의 정보를 이미 정의하게 된다.
- 어떤 모델의 레코드를 만들어야 할지 이미 알고 있으므로 유효성 검사 후 바로 저장(`save()`)이 가능하다.

Form class를 반드시 forms.py 에 작성할 필요는 없다.

- 하지만 되도록 해당 app폴더 안에 `forms.py`에 작성하는 것이 바람직하다.



url_name 확인

```
In [5]: request.resolver_match.url_name
Out[5]: 'create'
```



> https://django-bootstrap4.readthedocs.io/en/latest/quickstart.html#example-template

