[TOC]

# 03 Days

## 	1. Text

### 	1.1 Open & Close

open과 close 함수를 사용

```python
# 1. 변수에 만들고 싶은 파일을 open() 해야 한다.
# open() 할때 r : 일기 / w : 쓰기(+덮어쓰기) / a : 추가
#f = open('만들 파일 명', '행동')

f = open('ssafy.txt', 'w')

# 1~10까지 입력 

for i in range(10):
    f.write(f'This is line {i+1}.\n')
f.close()

#  \n은 Enter의 역할을 한다. (open은 항상 close가 필요)
```

### 	1.2 with 구문

```python
# with 구문(context manager)
with open('with_ssafy.txt','w') as f:
    for i in range(10):
        f.write(f'This is line {i+1}.\n')
```

> \# 이스케이프 문자
>
> \# \n : 개행문자(다음줄이동)
>
> \# \t : Tab 문자
>
> \# \\ : \(백슬래쉬)문자 사용
>
> \# \' : 따음표 사용
>
> \# \" : 쌍따음표 사용됨
>
> \# 첫번째 \는 출력되지않는다

> ```python
> ># writslines() : list를 넣어주면, 요소 하나당 한 줄씩 작성한다.
> >
> > with open('ssafy.txt','w') as f:
> >
> >     f.writelines(['0\n','1\n','2\n','3\n'])
> 
> 
> ```

### 	1.3 read 구문

```python
#read()
with open('with_ssafy.txt', 'r') as f:
    all_text = f.read()
    print(all_text)

#readlines() : 파일의 모든 라인을 읽어서 각각의 줄을 요소로 갖는 list 로 만들어냄
with open('with_ssafy.txt', 'r') as f:
    lines = f.readlines()
    for line in lines:
        print(line)
        
# '문자열'.strip() : 공백을 지워준다.
#  print(line.strip())

# print(dir(line)) : 함수검색
```

### 	1.4 DOCstring

```python
"""
이 함수는 블라블라
누가 만들었고 
어떻게 사용하고
이런 함수입니다.
"""
```

> """를 사용하여 사용



```python

ranks = soup.select('#PM_ID_ct > div.header > div.section_navbar > div.area_hotkeyword.PM_CL_realtimeKeyword_base > div.ah_roll.PM_CL_realtimeKeyword_rolling_base > div > ul > li > a > span.ah_r')
searchs = soup.select('#PM_ID_ct > div.header > div.section_navbar > div.area_hotkeyword.PM_CL_realtimeKeyword_base > div.ah_roll.PM_CL_realtimeKeyword_rolling_base > div > ul > li > a > span.ah_k')
#랭크와 서치 따로따로

searchings = soup.select('#PM_ID_ct > div.header > div.section_navbar > div.area_hotkeyword.PM_CL_realtimeKeyword_base > div.ah_roll.PM_CL_realtimeKeyword_rolling_base > div > ul > li > a')

rank = searching.select_one('span.ah_r').text
keyword = searching.select_one('span.ah_k').text
#랭크와 서치 같이
```



```python
import bs4
from bs4 import Butifulsoup

#1의경우
soup = bs4.Butifulsoup(!@#!@#)
#2의 경우
soup = Butifulsoup(!@#!@#)
```

## 	2.HTML

### 2.1 html & CSS

```python
<!DOCTYPE html> #html을 사용하며 필수적으로 처음 써줘야한다.
<html>#html의 시작과끝
<head> #head와 body로 나눈다. head는 보이지않는정보 이며 body는 보이는 정보이다.
    <meta charset="utf-8">#utf-8 유니코드이다. 글자의 세팅
    <title>여기는 네이버입니다.</title>  #title 크롬의 탭 네임같은걸을 보여준다.
    <link rel="stylesheet" href="style.css"> 
    #style.css 와 연결한다. 연결된 css는 글자를 키우거나 색깔을 변경하는등의 활동이 가능하다.

</head>  #head가 끝났다.


<body>  #body의 시작이다. 보이는 정보들을 보여준다.
    <h1>H1 태그입니다. </h1>  #h1태그 크게 가로지르는 큰 제목이다.
    <h2>HTML & CSS 맛보기</h2> #h2~ h6까지 있는듯하다.
    <p>문단을 구분하는 p태그 </p> 
    안녕하세요    #P태그는 html의 엔터이다. 옆의 엔터는 안녕하세요 반갑스니다. 와 같이 출력되어
    반갑습니다.   # p태그를 이용하여 엔터를 친다.(한줄사용함)
    <p></p>

    안녕하세요
    <p>  </p>  #비교를 위해 적어둿다.
    반갑습니다.

    <ol>   #1. 2. 3. 과 같이 순서가있는 태그이다.
        <li>이건 순서가 있는 태그</li>    #1. 이건 순서가 있는 태그
        <li>이것도 순서가 있는 태그</li>  #2. 이것도 순서가 있는 태그
    </ol>                             #와 같이 출력된다.
    <ul> #순서가 없는 태그이다 ●와 같이 순서가없는 태그이다.
        <li>이건 순서가 없는 태그</li>   # ● 이건 순서가 없는 태그
        <li>이것도 순서가 없엉</li>     # ● 이것도 순서가 없엉 
    </ul>                             # 와 같이 출력이된다.
  </body>  #body의 끝을 알린다.
</html> #html의 끝을 알린다.


```



head 안보이는 정도 (title : 탭의 이름, 유니코드) 

body 보이는 정보 (h1, h2 (~ h6 까지있음) 등 처리)

> 둘다 반드시 html 안에서 처리

 생성시 두개가 생김

> <html></html>

#### 	CSS

```python
h1 {
    color: cornflowerblue; #h1의 컬러를 지정한다.
}


h2{
    color: blue;
}

p{
    font-size: 60px  # p태그의 사이즈를 60px(픽셀)로 한다.
}

li{
    text-align: center;  #li들을 모두 가운데 정렬한다.
}
```

Html의 설정 (글자색, 크기, 정렬 등)을 하는대 사용된다.







## 		2.2 Flask (마이크로 프레임워크)

```python
FLASK_APP=hello.py flask run
```

~/.bash_profile 이 필요함 flask run만 사용하며 디버그모드등의 설정변경을위해

```python
export FLASK_APP=hello.py
export FLASK_ENV=development
```

> 주의 export 이후 공백이 있으면안됨

> source ~/.bash_profile 을 이용해 설정을 저장시킴

```python
@app.route('/ssafy/') #원하는주소
def hello():  
    return 'This is SSAFY!'     
```

> route의 '/' /뒤에 주소를 덧붙이면 주소가 추가됩니다.
>
> 두개이상일경우 def hello와같은 두개의 함수가 존재하면 오류가 납니다. 

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello(): #함수 만드는거 def는 함수실행 return은 값실행 
    return 'This is SSAFY!'  
    
@app.route('/ssafy/') #  /추가주소/  의 방식으로 주소를 바꿈
def hllo():  #겹치면 오류남
    return 'This is SSAFY!'

```

