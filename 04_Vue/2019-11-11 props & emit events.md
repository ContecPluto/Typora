# 2019-11-11 props & emit events

## 흐름

사용자가 검색어 입력(SearchBar)  ==> 검색 결과를 App.vue로 올려줌

|             | main.js   |           |
| ----------- | --------- | --------- |
|             | app       |           |
| videoDetail | SearchBar | Videolist |
|             |           |           |

### 단방향 데이터 흐름의 이점

1. vue app 의 데이터 흐름을 쉽게 파악할 수 있음
2. 부모 컴포넌트에서 업데이트가 일어나면 자식 컴포넌트는 자동 업데이트(즉, 자식 컴포넌트의 상태를 관리하지 않아도 된다.)
3. 하위 컴포넌트가 실수로 부모의 상태를 변경하려 app 데이터의 흐름을 추론하기 어렵게 만드는것을 방지할 수 있다.



- 상위로 데이터를 올려 보낼 때는 Event 를 발생시키는 방법을 사용한다.(`emit`)

- `props`는 배열, 객체, 함수 등 무엇이든 내려보내는 속성(properties)이고, `emit event`는 자식에서 부모로 **이벤트를 발생** 시키는 것



App => searchbar : props

SearchBar => App : emit



### SearchBar => App

1. 트리거 : input 값 변경(@input)
   - 인자 : event
   - 실행 함수 : onInput
2. 트리거 : input 내 $emit(inputChange)
   - 인자 : 변경된 값
   - 실행 함수 : onInputChange



## SearchBar

1. 사용자가 input에 값을 입력하면 onInput 함수가 실행
2. inputChange 이벤트와 사용자가 입력한 value가 함께 상위 컴포넌트인 App.vue 로 event 와 input value 가 emit 된다.



## App

3. SearchBar에서 넘어온  이벤트 inputChange로 인해 onInputChange 함수가 실행된다.
4. oninputChange 함수는 유튜브 api에 요청을 보내고 비디오 리스트를 응답받는다.

---

5. 넘겨 받은 비디오 리스트를 videos라는 배열에 저장한다.

6. `data object`가 (videos 배열이 있는 곳) 업데이트 되면, 해당 컴포넌트 (App.vue가 템플릿을 다시 렌더링 한다.)
7. 그리고 바로 자식 컴포넌트들도 모두 다시 렌더링 된다.
8. `videoList` 컴포넌트가 비디오 배열을 받아 화면에보여주게 된다.



> Vue component 에서는 반드시 Object를 return 하는 함수로 작성.