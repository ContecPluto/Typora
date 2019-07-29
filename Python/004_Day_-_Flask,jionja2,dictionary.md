[TOC]



# 04 Day

##  1.Flask

 플라스크는 기본적으로 서버를 구축하는 프로그램이다.

```python
$ FLASK_APP=hello.py flask run
```

기본적으로 app.py를 기본사양으로 잡고있으므로 파일이름을 app.py로 설정한다면 flask run 만으로도 실행이가능하다.

> 만약 다른이름의 경우 위와 같은 FLASK_APP=hello.py를 같이 써줘야한다.

​	



> datetime 함수
>
> 날짜끼리의 연사이 가능함
>
> ```python
> from datetime import datetime
> 
> today_time = datetime.now()
> # 수료 날짜
> endgame = datetime(2019, 11, 29)
> # 수료 날짜 - 오늘 날짜
> dday = endgame - today_time
> return f'{dday.days} 일 남았습니다.'
> ```



변수의 3제곱을 계산하는 사이트

```python
@app.route('/cube/<int:number>')
def cube(number):
    return f'{number}의 세제곱은 {number**3}입니다.'
```

주소의 변수(number)의 기본형은 str(string)입니다. 즉 str로 들어온 number는 계산이 안되기에 int를 적어주어 int로 변환켜 계산이 가능하도록 바꿔줍니다.



```python
rm -rd .bash_profile
code ~/.bashrc #export FLASK_ENV=development 적을것
source ~/.bashrc
ls -al
```

flask 에러가 자꾸 생성될떄

> ! + tab html 생성시 양식 생성



rendirng

```python
from flask import Flask, render_template
@app.route('/')
def hello():
    # return 'Hello World!'
    return render_template('index.html')
#app.py 와 같은 위치애 templates(폴더)안에 템플릿 생성
```



## 2.jionja2 활용

```jinja2
{% for user in users %}
```

{%   %}의 사이에는 유저에게 보이지않습니다.

```jinja2
<body>
    <!-- 본인 이름으로 값이오면 인사하고 아니면 누구세요 -->
    {% if html_name == '준호' %}
        <h2> {{html_name}} 왔니?</h2>
    {% else %}
        <h2>누구세요 ? ? ?</h2>
    {% endif %}
</body>
```

body에서 이름을 확인합니다.

jionja2에선 if 문이 끝난후 endif 의 선언을 해주어야합니다.

> for, if 등 역시 동일합니다.



```jinja2
{#  주석  #}

    <!-- {% if html_name == '준호' %}
        <h2> {{html_name}} 왔니?</h2>
    {% else %}
        <h2>누구세요 ? ? ?</h2>
    {% endif %} -->
```

주석을 사용할떄는 {# #}을 사용하게됩니다.

위의 상황일경우에는 vscode에서는 주석으로 처리되지만 jionja2에선 살아있기때문에 주석처리되지 않습니다.







## 3. Flask Rquest & Response

```html
<body>
    <form action="/pong">  #/pong?data=? 식으로 보내준다.
        <input type="text" name="data">
        <input type="submit" value="버튼">
    </form>
</body>
```

input type ="text"는 텍스트를 작성할수 있는 창을

input type ="submit"은 버튼을 작성합니다. value의 값은 버튼의 내용을 말합니다.  『버튼』



```python
@app.route('/pong')
def pong():
    name = request.args.get('data')  #안녕하세요
    return render_template('pong.html', name=name)


```



>HTML  <br>
>
>로 엔터가 가능합니다. 





##  4. 딕셔너리

`dict['key']`로 존재하지 않는 key 를 접근할 경우 key erro가 발생하지만, `dict.get('key')`로 존재하지 않는 key를 접근할 경우 None값을 넘겨준다.

```python
#딕셔너리 만들기 - 1
lunch = {
'중국집' : '02-123-1234'
}

#딕셔너리 만들기 - 2
dinner = dict(중국집='02',일식집='031')

#딕셔너리 내용 추가하기
lunch['분식집'] = '031-123-1234'

#딕셔너리 내용 가져오기
idol = {
    'bts':{
        '지민':25,
        'RM':24        
    }
}

#RM의 나이는?
#print(idol['exo'])   #에러남
#print(idol['bts']['RM']) #딕셔너리 출력-1

#print(idol.get('exo')) #None값을 준다.
#print(idol.get('bts').get('RM')) #딕셔너리 출력-2	
```



```python
#딕셔너리 만들기 - 1
lunch = {
'중국집' : '02-123-1234'
}

#딕셔너리 만들기 - 2
dinner = dict(중국집='02',일식집='031')

#딕셔너리 내용 추가하기
lunch['분식집'] = '031-123-1234'

#딕셔너리 내용 가져오기
idol = {
    'bts':{
        '지민':25,
        'RM':24        
    }
}

#RM의 나이는?
#print(idol['exo'])   #에러남
print(idol['bts']['RM']) #딕셔너리 출력-1

#print(idol.get('exo')) #None값을 준다.
print(idol.get('bts').get('RM')) #딕셔너리 출력-2



```

> 딕셔너리 출력-1 같은 경우 에러가 나면 서버가 멈추기 때문에 딕셔너리 출력 -2와 같은 형태를 더 많이 사용합니다.

```python
#딕셔너리 반복문 활용하기

lunch = {
'중국집' : '02-123-1234',
'분식집' : '031-123-1234',
'일식집' : '02-987-1254'
}

#기본 활용
for key in lunch:
    print(key)
    print(lunch[key])

# 둘다 가져오기 .items() 
for key, value in lunch.items():
    print(key,value)

# value만 가져오기 .values()
for value in lunch.values():
    print(value)

# key 만 가져오기 .key()
for key in lunch.keys():
    print(key)
```

리스트 명령어 참고자료

```python
max()   #리스트에서 가장 큰 값을 찾습니다.
min()   #리스트에서 가장 작은 값을 찾습니다.
sum()   #리스트의 모든값을 더합니다.
if a in b: #b의 리스트에서 a를 찾습니다. (True of Fals)
```

