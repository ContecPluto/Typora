# 05_Day



int 

string

list

dict



set(집합 연산자) 합집합/  교집합/  차집합



## telegram bot

from decouple import config

<token>값을 숨기기위해  .env의 폴더를 만들어 gitignore를 사용합니다.

> 중요합니다. 



> BotFather검색 이후 new bot name

bot name : Gagle/Gagle_bot

> 봇으로 끝나야함.

반드시 https:// 로 작성되어야함.



get방식은 검색과같이 URL에 노출

POST방식은 로그인과 같이 URL에 노출되지않습니다.





https://api.telegram.org/bot<token>/METHOD_NAME

> 기본구조

id, <token>은 엄중하게 관리해야함.



특정사용자에게 메세지 보내기

sendMasege



ngrok (서버 개방)

방화벽을 뚫어서 서버를 개방해줍니다.

cmd -> ngrok http 5000



 webhook을 위해 넣어줍니다.

https://api.telegram.org/bot<token>/setWebhook?url=<ngrok-forwarding-http-url>

 ```python
print(request.get_json())   #내용물을 파악하기위해 사용합니다.
#딕셔너리형태의 데이터가 전송되는걸 볼수 있습니다. 이후 필요에 따라 사용합니다.

from_telegrem = request.get_json()
#ex test& id

chat_id = from_telegrem.get('message').get('from').get('id')
text = from_telegrem.get('message').get('text')
 ```





배포(deploy) - pythonanywhere  (ngrok 에서 pythonanywhere로 변경함.)

https://api.telegram.org/bot<token>/setWebhook?url=<pythonanywhere-url>