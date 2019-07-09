아프니까 청춘이다.

> 흐릿한 글자가된다 >를 쓰고 글자를쓰면
>
> 주석같은느낌



```python
##```typora 코딩 사용
import requests
from bs4 import BeautifulSoup

# 1. 원하는 주소로 요청을 보내 응답을 저장한다.
html = requests.get('https://finance.naver.com/sise/').text
# 2. 정보를 조작하기 편하게 바꾸고
soup = BeautifulSoup(html, 'html.parser')
# 3. 바꾼 정보 중 원하는 것만 뽑아서
kospi = soup.select_one('#KOSPI_now').text
# 4. 출력한다.
print(kospi)
```



# 외장 함수는 `import`로 가져와야한다.

[네이버](www.naver.com)

![](C:\Users\student\Pictures\1920x1080_3_수정.jpg)

* 12312 이건 *+탭으로 만든다

  * 213123

    * `

      * `13

        * `321

        * 2312312

          

          

          1.asdasda

  2. 21231 

     > 숫자도 자동으로 정렬된다

  3. 3231

  4. 12312

  5. 1231

  6. 2312

  7. 3

dfsdf

[TOC]

> [toc] 를 이용해 목차정리 

## 1. 파이선 기초

###   1.1 ㄴㅇㄹㄴㅇㄹ

----

###   1.2 헤드라인은----로 작성한다.