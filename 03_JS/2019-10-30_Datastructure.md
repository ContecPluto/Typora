# 2019-10-30_Datastructure

## 1. Datastructure: Object 와 Array

```javascript
const numbers = [1, 2, 3, 4]

console.log(numbers[0])
console.log(numbers[-1]) // undefined : 정확한 양의 정수 index만 가능
console.log(numbers.length) // 4

// 원본 파괴
console.log(numbers.reverse())
console.log(numbers)
console.log(numbers.reverse())
console.log(numbers)

// push - 배열의 길이를 return
console.log(numbers.push('a'))  // 5
console.log(numbers)

// pop - 배열의 가장 마지막 요소 제거 후 return
console.log(numbers.pop())
console.log(numbers)

// unshift - 배열의 가장 앞에 요소를 추가하고 return 은 배열의 길이
console.log(numbers.unshift('a'))
console.log(numbers)

// shift  - 배열의 가장 앞에 요소를 제거 후 return
console.log(numbers.shift())
console.log(numbers)

//boolean return
console.log(numbers.includes(1))
console.log(numbers.includes(0))

// push, indexof - 요소를 추가하고 요소의 인덱스를 찾습니다.
console.log(numbers.push('a', 'a'))
console.log(numbers)
console.log(numbers.indexOf('a')) // 4 -> 중복이 존재한다면 처음 찾은 요소의 index를 return
console.log(numbers.indexOf('b')) // -1 -> 찾고자 하는 요소가 없으면 -1 을 return

// join - 배열의 요소를 join 함수의 인자를 기준으로 이어서 문자열로 return 한다.
console.log(numbers.join()) // 1,2,3,4,a,a -> 아무것도 넣지 않으면 , 를 기준으로 가져온다. 
console.log(numbers.join('')) // 1234aa
console.log(numbers.join('-')) // 1-2-3-4-a-a
console.log(numbers) // 원본은 변화하지 않는다.
```



## 2 JSON(JavaScript Object Notation, JS 객체 표기법)

- KEY-VALUE 형태의 자료구조를 JS 객체와 유사한 모습으로 표현하는 표기법
- 모습만 비슷할 뿐이고 실제로 Object 처럼 사용하려면 다른 언어들 처럼 JS 에서도 Parsing(구문 분석) 작업이 필요하다.

```javascript
const me = {
  name: 'ssafy', // key 가 한단어 일 때
  'phone number': '01012345678', // key 가 여러 단어 일 때
  appleProducts: {
    ipad: '2018pro',
    iphon: '7',
    macbook: '2019pro',
  }
}

console.log(me.name) // ssafy
console.log(me['name']) // ssafy
console.log(me['phone number']) // key가 여러 단어인 경우 반드시 []로 접근

console.log(me.appleProducts)
console.log(me.appleProducts.ipad)

// Object Literal(객체 표현법)
// ES5
var books = ['Learning JS', 'Eloquent Js']

var comics = {
  'DC': ['Joker', 'Aquaman'],
  'Marvel': ['Captain Marvel', 'Avergers'],
}

var megazines = null

var bookShop = {
  books: books,
  comics: comics,
  megazines: megazines,
}
console.log(typeof bookShop)
console.log(bookShop.books[0])

// ES6+
// object의 key 와 value 가 같다면, 마치 배열처럼 한번만 작성 가능
let bookShopTwo = {
  books,
  comics,
  megazines,
}
console.log(bookShopTwo)

////////////////////////////
// JSON(JavaScript Object Notation, JS 객체 표기법)
const jsonDate = JSON.stringify({ //JSON -> String
  coffe: 'Americano',
  iceCream: 'Mint Choco',
})
console.log(jsonDate) // {"coffe":"Americano","iceCream":"Mint Choco"}
console.log(typeof jsonDate)

const parseData = JSON.parse(jsonDate)
console.log(parseData)
console.log(typeof parseData)
```

### 2.1 정리

- object - JS 의 key - value 페어의 자료 구조
- JSON - 데이터를 표현하기 위한 **단순한 문자열**



## 3. Helper

- 자주 사용하는 로직을 재활용할 수 있게 만든 일종의 Library 다.