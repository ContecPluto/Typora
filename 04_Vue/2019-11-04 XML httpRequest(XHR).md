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

##### 2.3.2.1 v-if/ v-show

- v-if : 조건에 맞지 않으면 렌더링 자체를 하지 않는다
- v-show : 조건과 관계없이 일단 렌더링 후에, 조건에 맞지않으면 css display 속성을 토글해서 숨겨버린다.



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

shory

#### 2.3.4 v-model

- input tag의 value - View <----> v-model <----> data(**VM**)



#### 2.3.5 computed

- 미리 계산된 값을 반환.
- 종속 대상을 따라 저장(캐싱)되는 특성이 있다.
- 연산이 많이 필요한 경우 템플릿 안에서 연산 표현식을 사용하는 것보다 computed를 사용하는 것을 권장한다.
- `{{ newTodo.split("").reverse().join() }}`

```vue
computed: {
  reversedNewTodo: function() {
    return this.newTodo.split("").reverse().join()
  }
}
```

#### 숏컷

`v-bind:` -> `:`

`v-on:` -> `@`







### 2.4 View - VM - M(localstorage)



### 2.5 watch 

- Vue 인스턴스의 data변경을 관찰하고 이에 반응한다.
- 데이터 벼경에 대한 응답으로 비동기 또는 시간이 많이 소요되는 조작을 수행하려는 경우에 적합하다.
- 특정 데이터가 변경되었을 때 정의한 함수를 실행한다.

```vue
      watch: {
        todos: {
          // handler 특정 데이터가 변경 되었을 떄 실행할 함수
          handler: function (todos) {
            todoStorage.save(todos)
          },
          // 객체의 nested item 들도 관찰할지 유무를 설정한다. true 인경우 내부요소들도 감시하도록 한다.
          deep: true,
        }
      },

```

#### 2.5.1 computed vs watch

computed : 계산해야 하는 `목표 데이터를 정의하는 방식`(선언형 프로그래밍)

watch : 감시할 데이터를 지정하고 `그 데이터가 바뀌면 특정 함수를 실행하라는 방식`(명령형 프로그래밍)



### 2.6 mounted

```vue
      //새로고침 될 때 실행 되는 것
      mounted: function () {
        this.todos =todoStorage.fetch()
      }
    })
```



---

### 2.7 컴포넌트

"소프트웨어 개발에서 독립적인 단위 모듈"

- 대체로 컴포넌트는 특정 기능이나 관련된 기능의 조합으로 구성되는데 프로그래밍 설계에서 시스템은 모듈로 구성된 컴포넌트로 나뉜다. 
- Vue - "기본 HTML 엘리먼트를 확장하여 재사용 가능한 코드로 캡슐화 하는 것"

#### 2.7.1 컴포넌트 naming convention

- 컴포넌트의 첫 번째 인자는 태그이름, 두번째 인자는 속성들을 넣어준다

1. kebab-case - `todo-list`
   - 호출 할 때 : `<todo-list></todo-list>` 케밥케이스 태그로만 호출 가능
2. paskalCase - `TodoList`
   - 호출 할 때 :  `<todo-list></todo-list>`  / `<TodoList>` 둘다 호출 가능.
   - 단, DOM에 직접 작성할 때는 케밥케이스만 가능

- 그래서 Vue는 모두 소문자여야하고 하이픈을 포함하는 규칙을 따르는 것을 권장한다.



#### 2.7.1.1 props

- 컴포넌트를 재생산 할 떄 컴포넌트에서 사용할 변수를 부모에서 내려주게 되는데 이를 `props`라고 한다.
- 반복되는 컴포넌트에 서로다른 정보가 들어가야 할 때 사용
- 하위(자식)에서 상위(부모)로 데이터를 직접 찹조해선 안되고 실제로도 안된다.
- `props` 옵션을 통해 부모 -> 자식으로 데이터를 전달

- 전달하려고 하는 **데이터의 이름을 태그 내의 속성**으로, **내용을 속성 값**으로 넣어준다.