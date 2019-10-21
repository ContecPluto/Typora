# 2019-10-21

## 1. http

1. 비연결지향(connectionless)
2. 상태정보 유지 안함(sateless, 무상태) : 연결이 끊어지는 순간 클라이언트와 서버간의 통신이 끝남(각각 완벽하게 독립적)

### 1. 쿠키(cookie)

- 클라이언트의 로컬에 저장되는 키 값의 작은 데이터파일
- 웹페이지에 접속하면 요청한 웹페이지를 서버로부터 받고 쿠키를 로컬에 저장하고, 클라이언트가 재요청시에 웹페이지 요청과 함께 쿠키 값도 함께 전송
- 아이디 자동완성/ 공지 메세지 하루 안보기/ 팝업 안보기 체크/ 비로그인 장바구니에 담기 등 편의를 위하되 지워지거나 유출되도 큰 일은 없을 정보들을 저장



### 2. 세션(session)

- 사이트와 특정 브라우저(클라이언트) 사이의 상태를 유지시키는 것
- 일정 시간동안 같은 브라우저로부터 들어오는 일련의 요구를 하나의 상태로 보고 상태를 유지하는 기술
- 클라이언트가 서버에 접속하면 서버가 특정 session id 를 발급하고, 클라이언트는 session id를 쿠키를 사용해 저장, 클라이언트가 다시 서버에 접속하면 해당 쿠키(session id가 담긴)를 이용해 서버에 session id를 전달한다.
- Django 는 특정 session id를 포함하는 쿠키를 사용해서 각각의 브라우저와 사이트가 연결된 세션을 알아낸다. 실질적인 session의 DataBase에 기본 설정 값으로 저장된다.(이는 쿠키 안에 데이터를 저장하는 것보다 더 보안에 유리하고, 쿠키는 악의적인 사용자들에게 취약하기 때문)
- 세션을 남발하면 사용자가 많은 서버일 경우 서버 부하가 발생합니다.
- 쿠키를 지우면 로그아웃은 왜?? 서버에서는 session에 사용자 로그인 정보를 가지고 있지만, 그것이 내꺼라는걸 증명할 session id 가 쿠키에서 사라졌기 때문

### 3. 차이

- 쿠키 : 클라이언트 로컬에 파일로 저장
- 세션 :  서버에 저장(이때 session id는 쿠키의 형태로 클라이언트의 로컬에 저장)

### 4. 캐시(cache)

- 가져오는데 비용이 드는 데이터를 한 번 가져온 뒤에는 임시로 저장.
- 사용자의 컴퓨터 또는 중간 역할을 하는 서버에 저장.



```ipython
In [3]: request.session._session
Out[3]:
{'_auth_user_id': '1',
 '_auth_user_backend': 'django.contrib.auth.backends.ModelBackend',
 '_auth_user_hash': 'e06e91e37c3b263492c4fb9c24c3afeb9854c2e4'}
```

django에서 session은 딕셔너리형태로 제공됨



```python
def index(request):
    # session에 visits_num 키로 접근해 값을 가져온다.
    # 기본적으로 존재하지 않는 키이기 때문에 키가 없다면(방문한적이 없다면) 0 값을 가져오도록 한다.
    visits_num = request.session.get('visits_num', 0)
    # 그리고 가져온 값을 session 에 visits_num 에 매번 1씩 증가한 값으로 할당한다.(유저의 다음 방문을 위해)
    request.session['visits_num'] = visits_num + 1
    # session data 안에 있는 새로운 정보를 수정했다면 django 는 수정한 사실을 알아채지 못하기 때문에 다음과 같이 설정.
    request.session.modified = True
    embed()
```

session에 새로운 key값 추가



## 2. User

직접 폼을 작성하지않는다

**Authentication(인증) - 신원확인**

- 자신이 누구라고 주장하는 사람의 신원을 확인하는 것

**Authorization(권한, 허가) - 권한 부여**

- 가고 싶은 곳으로 가도록 혹은 원하는 정보를 얻도록 허용하는 과정

https://docs.djangoproject.com/en/2.2/topics/auth/default/

> 유저 관련

### 2.1 sign up

- user를 create



### 2.2 login

- session 을 create



```python
from django.contrib.auth.forms import UserCreationForm, AuthenticationForm
# Create your views here.

def signup(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
    else:
        form = UserCreationForm()
    context = {'form':form,}
    return render(request, 'accounts/signup.html', context)

def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()
    context = {'form':form,}
    return render(request, 'accounts/login.html', context)
```



### 2.3 logout

- sesion을 delete

```python
def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```



로그인 사용자에 대한 접근 제한

- django는 세션과 미들웨어를 통해 인증 시스템을 request 객체에 연결한다.
- request는 현재 사용자를 나타내는 모든 요청에서 `request.user`를 제공한다.



`is_authenticated`

- User model의 속성(attributes)들 중 하나.
- 사용자가 인증 되었는지 알 수 잇는 방법
- User 에는 항상 True/ `AnonymousUser` 에 대해서만 항상 False
- 단, 이것은 권한(permission)과는 관련이 없으며 사용자가 활동중(active)이거나 유효한 세션(valid session)을 가지고 있는지도 확인하지 않는다.

- dlfqkswjrdmfh `request.user` 에서 이속성을 사용하여 미들웨어의 `    django.contrib.auth.middleware.AuthenticationMiddleware`를 통과햇는지 확인한다.



#### The `login_required` decorator

```python
from django.contrib.auth.decorators import login_required
```

If the user isn't logged in, redirect to [`settings.LOGIN_URL`](https://docs.djangoproject.com/ko/2.2/ref/settings/#std:setting-LOGIN_URL), passing the current absolute path in the query string. Example: `/accounts/login/?next=/polls/3/`.





**`next` query string parameter**

- @login_required  데코레이터가 기본적으로 인증 성공후 사용자를 리다이렉트 할 경로를 next라는 문자열 매개 변수에 저장한다.

- 우리가 url로 접근하려고 했던 그 주소가 로그인하지 않으면 볼 수 없는 곳이라서, django가 로그인 페이지로 강제로 리다이렉트 했는데, 로그인을 다시 정상적으로 하고 나면 원래 요청했던 주소로 보내주기위해 keep 해주는 것,

---

**코멘트에 @login_required를 사용햇을경우**

@required_POST가 있는 함수에 @login_required가 성정된다면 로그인 이후 "next" 매개변수를 따라 해당 함수로 다시 redirect되면서 @required_POST 때문에 405에러가 발생.



### 회원 탈퇴

### 회원수정

`from django.contrib.auth.forms import UserChangeForm`

**`get_user_model()`**

- `User`를 직접 참조하는 대신 `django.contrib.auth.get_user_model()` 를 사용하여 User model을 참조해야 한다.
- 이 함수는 현재 활성화(active)된 User model 을 return 한다.



### 비밀번호 변경

- 비밀번호 변경 후 로그아웃 되버림
- 비밀번호가 변경되면서 기존세션과의 회원 인증 정보가 일치하지 않게 되어 버렸기 때문

**`update_session_auth_hash`**

- 현재 사용자의 인증 세션이 무효화 되는 것을 막고, 세션을 유지한 상태로 업데이트
- 현재 request와 새로운 session hash 가 생긴 업데이트 된 user 객체 간 적절히 업데이트

```python
@login_required
def change_password(request):
    if request.method == 'POST':
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
            form.save()
            update_session_auth_hash(request, form.user)
            return redirect('articles:index')
    else:
        form = PasswordChangeForm(request.user)
    context = {'form':form,}
    return render(request, 'accounts/auth_form.html', context)
```



