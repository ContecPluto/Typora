# 2019-11-18_-_Django&Vue_JS

django => API

Vue => Backend



## 1. JWT(Json Web Token)

정보를 안전하게 json 객체로 전송하기 위한 간결하고 독립적인 방법

> https://jwt.io/

- 세션/쿠키와 함께 모바일과 웹의 인증을 책임지는 대표 기술 중 하나. 세션/쿠기의 정보 전달 방식과 유사하게 사용자는 Aucess Token(JWT token)을 HTTP header 에 실어서 서버로 요청을 보냄.

- 세션/쿠키 방식과 가장 큰 차이점은 세션/쿠키는 세션 저장소에 유저의 정보를 넣지만, JWT 는 토큰안에 유저의 정보를 넣는다.

- Client의 입장에서는 HTTP header에 세션ID/ 토큰을 실어서 보낸다는 점은 동일하지만, Server의 입장에서는 인증을 위해 암호화 (JWT 방식)를 하냐 혹은 별도의 저장소(세션/쿠키 방식)를 이용하느냐의 차이.

- 주류 프로그래밍언어가 모두 지원한다.

  

- 사용처

  1.  Authoriztion (회원 인증)
     - 서버가 유저 정보에 기반한 토큰(JWT)을 발급해 유저에게 전달하고, 유저는 서버에 요청을 보낼때마다 JWT를 포함하여 전달.
     - 서버는 세션을 유지할 필요 없이 유저의 요청정보 안에 있는 JWT만 확인하면 된다. (서버 자원 아낄 수 있다.)
  2. Information Exchanges(정보 교환)
     - 정보가 서명되어 있기 때문에 정보를 보낸사람의 정보 혹은 정보가 조작여부 확인 등이 가능

- 구조

  - xxxx.yyyy.zzzz

  - Header.Payload.Signature

    1. Header :

       - token의 type과 사용 algorithm의명칭

    2. Payload :

       - 토큰에 담길 정보가있는 곳

       - 정보

         (1) registerd claim

         - 토큰에 대한 정보들을 담기 위해 이름이 이미 정해진 클레임들. 클레임의 사용은 모두 선택적이다.

         (2) publick claim

         - 공개 클레임은 충돌이 되지않는 이름을 가지고 있어야 한다. 보통 충돌을 방지하기 위해 key 값을 URI 형태로 만든다. (예: 'https://test.co.kr/jwt_token/: true')

         (3) private claim

         - 등록된 클레임도 아니고 공개 클레임도 아니다. 클라이언트와 서버간에 협의하에 사용되는 클레임들이다.
         - key 값이 중복되서 충돌이 될 수 있으니 유의해서 사용해야 한다.
         - 예) {"username" : "admin"}

    3. Signature(서명)
       - Header와 Payload의 값에 비밀키로 hashing
       - HEADER 의 인코딩 값과, PAYLOAD의 인코딩 값을 합친 후 주어진 비밀키로 해쉬를 생성한 값이다.

### 1.1 요약

- 두 객체에서 JSON 객체를 사용하여 가볍고 자가 수용적인(self-contained, 필요한 모든 정보를 자체적으로 지닌다.) 방식으로 정보를 안정성 있게 전달.
- 세션 상태를 저장하는 것이 아니라 필요한 정보를 JWT에 저장해서 사용자가 가지고 있게 하고, 해당 JWT를 증명서처럼 사용하는 방식



### 1.2 장점

1. 세션/쿠키처럼 별도의 저장소 관리가 필요 없고 발급한 이후에 검증만 하면 된다.
2. 토큰을 기반으로 한 다른 인증시스템에 접근이 용이하기 때문에 확장성이 뛰어나다.
3. 모바일 환경에 적합 (쿠키와 같은 데이터로 인증할 필요가 없기 때문)
4. Paython, JS, Ruby, Go 등 주류 프로그래밍 언어에서 대부분 지원이 된다.



### 1.3 단점

1. 이미 발급된 JWT는 유효기간이 완료될 때까지 계속 사용하기 떄문에 악용될 가능성이 있다. (한번 발급된 토큰은 값을 수정하거나 폐기할 수 없다.) 그래서 이 문제는 Access Token의 유효기간(expire time)을 짧게 하고 Refresh  Token 등 을 이용해서 중간중간 새로운 토큰을 재발행 해준다.
2. 세션/쿠키 방식에 비해 claim 데이터가 많아진다면 JWT 토큰의 길이가 길어지기 때문에 인증 요청이 많아 질수록 네트워크의 대역폭이 낭비될 수 있다.(API 호출 시 매 호출마다 헤더에 붙여서 전달하기 때문)



---



## 2. router

> vue ui를 이용해 창을 실행해 설치한다.

### 2.1 router-link

- router 지원 앱에서 사용자 네비게이션을 가능하게하는 컴포넌트
- 목표 위치는 `to` prop 으로 지정된다.
- 라우팅은 URI에 따라 해당하는 정적 파일을 내려주는 방식인데 이를 브라우저에서 구현하는것이 SPA개발의 핵심
- `router-link` 는 `a` 태그보다 선호되는데 이유는 HTML5 히스토리 모드에서 클릭 이벤트 자체를 차단하여 브라우저가 페이지를 다시 로드하지  않도록 한다.



### 2.2 router-view

- 라우팅이 경로에 맞는 컴포넌트를 제공하는 데 해당 경로에 맞는 컴포넌트를 렌더링 해주는 부분



## 3. CORS(Cross-Origin Resource Sharing)

### 3.1 정의

- 한 도메인에서 로드되어 다른 도메인에 있는 리소스와 상호 작용 하는 것
- 즉, 도메인이나 포트가 다른 서버의 자원을 요청하는 메커니즘.



### 3.2 문제상황

1. 요청을 할 때 cross-origin HTTP 에 의해 요청을 한다.
2. 하지만 CORS와 같은 상황이 발생하면 외부 서버에 의한 요청 데이터를 브라우저에서 차단하기 때문에 (보안 목적) 정상적으로 데이터를 받을 수 없다.
3. 예를 들어, http://locallhost:8080/ 에서 vue를 실행하고 http://locallhost:8000/에서 django를 실행할 경우 포트가 달라 다른 도메인으로인지하고 브라우저가 요청을 차단한다.



### 3.3 해결 방법

1. 서버(django)와 클라이언트(vue)가 같은 도메인과 포트를 사용하도록 한다.
2. 서버에서 cross-origin HTTP 요청을 허가한다. (우리가 해결할 방법)
   - 실제 API 서버들은 이러한 CORS 제한과 관련된 처리를 모두 해두어야한다.



---

사용 라이브러리 (파이썬)

- DRF
- DRF-jwt
  - https://github.com/jpadilla/django-rest-framework-jwt
- cors
  - https://github.com/adamchainz/django-cors-headers

 npm i vue-session

![image](https://user-images.githubusercontent.com/52685373/69108430-f7bef000-0ab7-11ea-8074-fb950db61d3b.png)

**this.$session.start()**

- session-id 초기화. 만약 세션이 없이 저장하려고 하면 vue-session 플러그인이 자동으로 새로운 세션을 시작

**this.$session.set(key,value)**

- session 에 해당 key 에 맞는 값을 저장

**this.$session.has(key)**

- key(JWT)가 존재하는지 여부를 확인

**this.$session.destroy()**

- 세션을 삭제



흐름

1. Django - 회원가입 
2. Vue => Django - 로그인 정보(credentials)를 django 서버로 보낸다. 
3. Django - Vue 에서 받은 유저정보에 해당하는 고유한 Web Token(JWT) 발급
4. Django => Vue - 해당 유저에 대한 토큰을 Vue로 보낸다.
5. Vue - Django에서 받은 토큰을 vue-session 을 통해 저장한다. ( 이 시점부터 vue 에서는 로그인 성공 상태)
6. Vue => Django || vue-session에 저장된 토큰을 가지고 django에 로그인 요청
7. Django || 최초로 보낸 토큰과 일치하는지 여부를 확인(세션에 저장된 토큰 == 요청자의 토큰)

.start() 를 통해 `session-id:sess+Date.now()`가 만들어진다.

.set() 을 통해 `jwt:jwt 값`이 만들어진다.

---

Vue - 라이프사이클

1. Vue instance 생성 (create)
2. DOM 에 부착(mounted)
3. 업데이트 (Update)
4. 사라짐(destroy)

---

**FormData**

- 기존 키에 새로운 값을 추가하거나 키가 없는 경우 새로운 키를 추가.(`FormData.append()`)
- `FormData.append(name, value)`
- name: value에 포함되는 데이터 필드 이름
- value는 필드 값

