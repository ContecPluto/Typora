[TOC]



# 2일차 start camp



.select_one('경로')

> select_one은 하나만 선택되어 출력됩니다.



.select('경로') 

> select는 리스트로 출력됨



## 1. git 깃

### 	1.1 git?

 분산 버전 관리 시스템

코드의  History를 관리하는 도구

개발된 과정과 역사를 볼 수 있으며,

프로젝트의 이전 버전을 복원하고 변경 사항을 비교, 분석 및 병합도 가능

> *git과 GitHub은 전혀 다른것이다.

> git은 ver1과 ver2의 차이가 무엇이고 수정 이유를 log로 남길 수 있다.
>
> 현재 파일들을 안전한 상태로 과거 모습 그대로 복원 가능(반대도 가능하다.)

### 	1.2 git의 작업 흐름

​		add 커밋할 목록에 추가

​		commit 커밋(create a snapshot) 만들기

​		push 현재까지의 역사 (commits)가 기록되어 있는 곳에 새로 생성한 커밋들 반영하기



> 작업 (수정)한 파일(working directory) -add -> 커밋할 목록(index커밋의 기준) -commit-> 쌓인커밋 (head) --push--> github 저장

 

> https://github.com/edujunho-hphk 
>
> https://github.com/ss-02-djpy2 코드풀이



### 	1.3 git의 commit 순서

git config --user.name "Gagle637"

git config --user.email gagle637@gmail.com

> 처음 TIL로 들어가서 (가장최상위폴더)에서만 git init 사용한다. 이후 오류의 원인 

> 위의 과정은 처음에만 사용하면됩니다. 이후 컴퓨터에 저장되어 사용됩니다.

![1562641290223](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562641290223.png)

git status

> 00_startcamp폴더가 현재 인식하지못한다 표시가됩니다.

![1562641187120](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562641187120.png)

git add 00_startcamp

>  00_startcamp의 폴더가 index로 이동합니다

git status

>  현재의 git 상태를 봅니다

![1562641215732](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562641215732.png)

git commit -m "first commit" 

> first commit 의 메시지와 함께 커밋이 쌓이게됩니다.

git status 

> 다시 현재의 git 상태를 확인해봅니다.  그동안 작업햇던 4개의 파일이 커밋됫습니다.

![1562641141144](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562641141144.png)

git remote add origin https://github.com/Gagle637/TIL.git

> https://github.com/Gagle637/TIL.git의 주소와 깃을 연결합니다. 

![1562642264022](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562642264022.png)

git remote -v 

> 현재 연결된 주소를 확인합니다.

git push -u origin master

> 깃헙으로 commit된 파일로 보냅니다.  
>
> 처음에만 사용합니다.   -u origin master 등록하며 푸쉬합니다. 이후에는 git push를 사용합니다.(-u가 그역할을 합니다. -u가 없다면 origin master를 이후에도 작성해야합니다.)

![1562642284674](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562642284674.png)

second commit 부터는 일련의 행동을 반복하되 복잡한 경로에 있을경우 git add . 을 이용하여 간단하게 추가가 가능합니다.

![1562642346914](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562642346914.png)

> 항상 git status를 이용하여 제대로 작동하엿는지등을 확인해야합니다.

git log에서 second commit이 추가된 모습이 확인이 가능합니다.

![1562642447878](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562642447878.png)



앞서 설명하엿든 이후에는 git push만으로 push가 가능합니다.

![1562642497955](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562642497955.png)





github에 second commit은 first commit과의 변화의 확인이 가능합니다.

![1562646015671](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562646015671.png)

#### 1.4 github Clone and Pull 





git clone [https://github.com/Gagle637/TIL.git]

![1562647088715](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562647088715.png)

![1562647197569](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562647197569.png)

다음과 같은 방법으로  어디서나 TIL프로젝트를 이어받고 어디서나 할수있다.



> 클론이후에는 pull을 사용하여 버전을 업데이트 해야한다. 

> 집과 교육장에서 계속 pull을 사용하며 버전을 업데이트  (clone, pull) 
>
> push를 이용하여 github로 보낸다.
>
> git clone url(https://github.com/Gagle637/game.git)를 사용 (처음 환경을 다운받을때 사용한다.)
>
> git pull  (이후 업데이트를 위해 사용한다. 달라진 버전을 땡겨온다.) -> 수정 -> git status ->(생략) -> git push

![1562650784213](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562650784213.png)

 Settings -> collaborators (user name 입력) -> 이메일 발송 -> 수락

의 과정으로 팀원에게 권한을 부여해 수정권한을 준다. 이후 push 가능해짐.





 gitignore

> (모든 파일을 올릴필요는 없다. 개인정보같은것 push전에 사용합니다.)

> 플랫폼 사용한다. 구글에 gitignore 검색하면 python측에서 만들어둔 ,gitignore가 있다.
>
> https://github.com/github/gitignore/blob/master/Python.gitignore
>
> 아니면 https://gitignore.io/ 을 사용한다 (python + vs code 등 여러가지 사용가능)



## 2. String 문자열

> terminal here 사용 shortcuts 검색 preferences open keyboard shortcuts -> ctrl+`검색 
>
>  -> 삭제 이후 terminal here ctrl+` 에 사용

1.과거

```paython
		'%s %s' % ('one', 'two')`
```

2 pyformat( ~3.5)

```
'{} {}'. format('one','two')
```

3 f-string(new in 3.6)

``` python
 a = one
 b = two
 
 print(f'{a},{b}')
```

> f-string {}안에는 함수가 사용 가능하다





\#필요하면 이렇게도 해보자

```python
name = '홍길동'

print('안녕하세요, '+ name + '입니다.')
```

> 문자열끼린 더해진다.





imports os

파일명 바꾸기

1. os를 import 한다.

   import os

2. 해당 폴더로 들어간다.

   os.chdir('C:\Users\student\Desktop\TIL\00_startcamp\02_day\change_filenames')폴더 안에 모든 파일을 돌면서 이름을 바꾼다.

   os.chdir(r'C:\Users\student\Desktop\TIL\00_startcamp\02_day\change_filenames') 윈도우에선 r이 필요하다. 



> 안녕하세요 "김준호"입니다. 에서 ""를 쓰고싶을떄 \\" 김준호\\" 입니다로 사용. 



3. 현재 폴더 안에 모든 파일 이름을 수집

   filenames = os.listdir('.')

   > '.'은 현재위치

4. 각각의 파일명을 돌면서 수정한다.

for filename in filenames

​    os.rename(이전파일명, 바꿀파일명)





5. 각각의 파일명을 돌면서 수정한다.

for filename in filenames:

​    os.rename(filename, f'SAMSUNG_{filename}')



6. SAMSUNG의 이름을 SSAFY로 변경한다

for filename in filenames:

​    os.rename(filename, filename.replace('SAMSUNG_','SSAFY_'))