# 2019-11-04 XML httpRequest(XHR)

## 1. XML httpRequest

- 브라우저는 XML httpRequest 객체를 이용하여 Ajsx 요청을 생성하고 전송
- 서버가 브라우저의 요청에 대해 응답을 반환하면 같은 XHR 객체가 그 결과를 처리한다.

- 단 IE 5, 6 에서는 ActiveXobject 를 사용해야한다.

---

기존 redirect로 인해 index.html 로 페이지가 로딩 되는것이 아닌 JSON 형태로 응답 결과를 반환 받기로 변경

JSON 데이터에 liked 변수를 만들어서 template 에서 좋아요를 취소할지 추가할지를 판단할 수 있도록 한다.

그래서 True False 값을 통해 좋앙 버튼의 style 값을 변경한다.





## 2. ViewJS

### 2.1 SPA(Single Page Application)

- 전체 데이터를 갱신하지않고 부분 갱신합니다.(네이티브앱과 유사한 경험)
- UX 향상(속도는 부가적)
- 모바일 퍼스트 전략에 적합한 전략

- 단점은 초기구동속도가 느리다.

---



### 2.2 인스턴스 옵션

#### 2.2.1 el

- Vue 인스턴스와 DOM 을 연결(마운트, mount)하는 옵션
- View - View Model 을 연결 시킨다.
- HTML 의 id나 class와 마운트가 가능하다.
- 마운트 밖에서의 사용은 되지 않는다.

#### 2.2.2 data

- Vue 인스턴스의 데이터 객체, 인스턴스의 속성
- 데이터 객체는 반드시 기본 객체 `{}`여야 한다.
- 객체 내부의 아이템들은 value로써 모든 타입의 객체를 가질 수 있다.(object, string, integer, array ...)
- 정의된 속성은 인터폴레이션 (`{{  }}`) 을 통해 View에서 랜더링 가능
- data 에서도 이벤트리스너와 비슷한 이유로 화살표 함수를 작성해서는 안된다.



#### 2.2.3 methods

- Vue 인스턴스에 추가할 메소드들을 정의하는 곳
- (주의) 메소드를 정의하는데에 화살표 함수를 사용해선 안된다.

---



### 2.3 Vue directive(지시문)

- 디렉티브는 `v-` 접두사가 있는 특수 속성(attr)이며, 디렉티브 속성의 값은 단일 JS 표현식6

#### 2.3.1 v-for

```html
<li v-for="todo in todos">
    {{ todo }}      
</li>
```



#### 2.3.2 v-if

- 특정 조건을 만족할때만 보여지도록(렌더링되도록) 할 수 있다.
- `v-else`는 반드시 `v-if`엘리먼트 바로 뒤에 와야 인식 가능
- `v-else-if`도 존재.



#### 우선순위

- 동일한 노드에서는 for 가 if 보다 높은 우선순위를 가진다.
- 즉, v-if는 루프가 반복될때마다 실행!(일부 항목만 렌더링 할 때 유용)



#### 2.3.3 v-on

- JS에서 이벤트리스너와 비슷한 열할을 한다.

- 이벤트리스너는 HTML element를 querrySelector 로 가져와 이벤트를 붙여줬다면, Vue는 HTML element자체에 이벤트를 붙여준다.
- `v-on` : 뒤에 오는 친구를 `전달인자`라고 한다.
- `:`을 붙여 사용하는, 디렉티브 바로 뒤에 붙는 친구들을 지칭한다.

##### 사용법

1. inline

   - `v-on:click="todo.completed = true`

2. method 정의

   ```Vue
   <div id="app">
     <li v-for="todo in todos" v-if="!todo.completed" v-on:click="check(todo)">
       {{ todo.content }}      
     </li>
     <li v-else>[완료 !]</li>
   </div>
   
   methods: {
     check: function (todo) {
       todo.completed = true
     }
   }
   ```

   



#### 2.3.4 v-bind

- HTML element 을 변경할 때 사용

