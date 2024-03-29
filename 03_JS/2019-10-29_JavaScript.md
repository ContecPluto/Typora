# 2019-10-29_JavaScript

## 1. 변수

### 1.1 let

- 값을 재할당 할 수 있는 변수를 선언
- 단, 각 변수는 **한번만 선언** 할 수 있다.(할당은 여러번 가능x=1 -> 할당, let x=1 -> 선언   )
- 블록 유효 범위(block scope) (중괄호 내부)

### 1.2 count

- 값이 변하지 않는 상수를 선언하는 키워드
- 담긴 값이 불변임을 뜻하는게 아니다.
- 단지 상수의 값은 재할당 할 수 없고 재선언도 안된다.
- 블록 유효 범위(block scope)

### 1.3 var(변수)

- ES6 이전의 feature 로 예기치 않은 문제를 많이 발생시키는 키워드로 절대 사용하지 않는다.
- var로 선언된 변수의 범위는 현재 실행 문맥인데, 그 문맥이 함수 혹은 함수 외부의 전역으로도 갈 수 있다.

---

- 어디에 쓸지 결정하는건 프로그래머의 몫
- `PI`, `DAYS_IN_JUNE`과 같은 경우는 상수가 적절하다.
- `WEATHER_TEMP` 처럼 모호한 경우(각자가 생각하는 좋아하는 기온은 다를 수 있으니까) 이런 경우는 변수가 적절하다.

---

일단 모든 선언에서 가능한한 상수(const)를 사용해야 한다.

먼저 상수를 생각하고 값이 바뀌는 것이 더 자연스러운 상황이라면, 그때 변수로 바꿔서 사용하는 것을 권장.

---

var : 할당 및 선언 자유/ 함수 스코프

let : 할당 자유 / 선언은 한번만/ 블록 스코프

const : 할당 및 선언 모두 한번만 / 블록 스코프

## 2. 식별자(identifier)

- 변수명은 식별자라고 불리며 특정 규칙을 따른다.

1. 반드시 문자, 달러($), 또는 밑줄로 시작해야 한다. 이후는 숫자도 가능.
2. 대소문자를 구별하며 클래스명을 제외하고는 대문자로 시작하지 않는것이 좋다.
3. 예약어는 사용 불가능(class, super, const, case, function, ....)

 ```javascript
// 식별자 작성 스타일
// 1. 카멜 케이스(camelCase) - 객체, 변수, 함수(=lower-camel-case)
let dog
let variableName

// 배열은 복수형 변수명을 사용
const dogs = []

// 정규 표현식은 'r' 로 시작
const rDecs = /.*/

// 함수
function getPropertyName() {
  return 1
}

// boolean 을 반환하는 변수나 함수 - 'is' 로 시작
let isAvilable = false

// 2. 파스칼 케이스(PascalCase) - 클래스, 생성자 (=== upper-camel-case)
class User{
  constructor(options) {
    this.name = option.name
  }
}

// 3. 대문자 스네이크 메이스(SNAKE_CASE) - 상수
// 이 표현은 변수와 변수의 속성이 변하지 않는다는 것을 프로그래머에게 알려준다.
const API_KEY = 'aasdasdacvsvsadv3r1qwqwr2#!@#!2r2'
 ```





## 3. 호이스팅(hoisthing)

- 이 개념은 JS변수, 함수나 표현이 최상단으로 올려지는 것을 말한다.
- 끌어 올려진 변수는 `undefined`값을 반환한다.
- 변수와 함수를 위한 메모리 공간을 확보하는 과정

```javascript
console.log(a) // undefined
var a = 10
console.log(a)

// JS 가 이해한 코드
var a // (선언과 초기화)
console.log(a) // undefined
a = 10 // (할당)
console.log(a)

// let 은 안된다. ReferenceError
// console.log(b)
// let b = 10
// console.log(b)

// 마찬가지로 아래와 같은 가정을 거친다.
let b // 선언 + TDZ
console.log(b)
b = 10 // 할당 불가 (초기화가 아직 안됨)
console.log(b)


if (x !== 1) {
  console.log(y) // undefined
  var y = 3
  if (y === 3) {
    var x = 1
  }
  console.log(y) // 3
}

if (x === 1) {
  console.log(y) // 3
}

// JS 가 이해한 코드
var x
var y

if (x !== 1) {
  console.log(y) // undefined
  var y = 3
  if (y === 3) {
    var x = 1
  }
  console.log(y) // 3
}

if (x === 1) {
  console.log(y) // 3
}
```



---

### 3.1 var 할당 과정

1. 선언 + 초기화
2. 할당

### 3.2 let 할당 과정

1. 선언
2. TDZ(임시적 사각지대)
3. 초기화
4. 할당

---

let, const의 정의가 평가되기까지 초기화되지 않는다는 의미이지, 호이스팅이 되지않아 정의가 되지 않는다는 의미와는 다르다.

---

Babel 로 ES6+ 문법을 그보다 아래 버전의 JS로 변경해서 사용하기도 한다.



## 4. 타입과 연산자

### 4.1 타입

#### 4.1.1 Primitive

- 불변하다는 특징을 띄고 있다.

1. Number
   - `infinity` : 양의 무한대와 음의 문한대로 나뉨
   - `NaN` : Not a Number, 표현할 수 없는 값, 자기 자신과 일치하지 않는 유일한 값을 표현
     - ex) 0/0, "문자" *10, Math.sqrt(-9)
   
2. Strings

   ```javascript
   // 문자열
   const sentence1 = 'sentence'
   const sentence2 = "sentence"
   const sentence3 = `sentence`
   const sentence4 = `sentence`
   
   // backtick `
   // const word = "안녕 
   // 하세요"
   // console.log(word)
   
   const word1 = "안녕 \n하세요"
   console.log(word1)
   
   const word2 = `안녕
   하세요`
   console.log(word2)
   
   // Template Literal
   // JS 에서 문자열을 입력하는 방식
   const age = 10
   const message = `홍길동은 ${age}
   세 입니다.`
   console.log(message)
   
   const happy = 'hello'
   const hacking = 'world!' + 'lol' + '!!!'
   console.log(happy, hacking)
   ```

3. Bollean
   - true
   - false

4. Empty Value

##### 4.1.1.1 Literal

- 값을 프로그램 안에서 직접 지정한다는 의미
- 값을 만드는 방법
- JS는 우리가 제공한 리터럴 값을 받아 데이터를 만듦

```javascript
// room 변수를 가리키는 식별자/ 'conference_room' 은 리터럴
let room = 'conference_room'

let hotelRoom = room

// 에러, conference_room 식별자는 존재하지 않는다.
hotelRoom = conference_room
```

- JS는 따음표를 통해 리터럴과 식별자를 구분한다.
- 식별자는 숫자로 시작할 수 없으므로 숫자에는 따음표가 필요없다. (숫자형 리터럴)

##### 4.1.1.2 `null` // `undefined`

- 동일한 역할을 하는 이 2개의 키워드가 존재하는 이유는 단순한 JS 의 설계 실수
- 큰 차이를 두지말고 interchangeable 하게 사용할 수 있도록 권장.

---

1. `undefined`

   - 값이 없을 경우 JS가 자동으로 할당 해주는 값

   ```javascript
   let first_name // 선언만 하고 할당하지 않음. undefined
   console.log(first_name)
   ```

2. `null`

   - 값이 없음을 우리가 표현하기 위해서 인위적으로 사용하는 값

     ```javascript
     let last_name = null
     console.log(last_name) // null - 의도적으로 값이 없음을 표현
     ```


#### 4.1.2 Reference

##### 4.1.2.1 할당연산자

```javascript
let c = 0
undefined
c += 10
10
console.log(c)
10
c -= 3
7
c *= 10
70

c++
71

c --
70
```

`false ? 1 : 2` false를 찾음

```javascript
const result = Math.PI > 4 ? 'YES!' : 'no!!'
undefined
```



## 5. if, switch

### 5.1 if

`const userName = prompt('Hello! who r u??')` 를 통해 

```javascript
if (userName === '1q2w3e4r') {
    message = '<h1>This is admin page</h1>'
} else if (userName === 'ssafy') {
    message = '<h1>You r from ssafy</h1>'
} else {
    message = `<h1>hello ${userName}</h1>`
}
```



### 5.2 switch

````javascript
switch (userName) {
  case '1q2w3e4r': {
    message = '<h1>This is admin</h1>'
    console.log(message)
  }
  case 'ssafy': {
    message = '<h1>you r from ssafy</h1>'
    console.log(message)
  }
  default: {
    message = `<h1>hello ${userName}</h1>`
    console.log(message)
  }
}
````

```javascript
switch (userName) {
  case '1q2w3e4r': {
    message = '<h1>This is admin</h1>'
    break
  }
  case 'ssafy': {
    message = '<h1>you r from ssafy</h1>'
    break
  }
  default: {
    message = `<h1>hello ${userName}</h1>`
  }
}
```

switch문은 break 가 없으면 멈추지않고 디폴트까지 가서 최종적으로 디폴트가 출력이된다.



## 6. 반복문

### 6.1 while

```javascript
let i = 0

while (i < 6) {
  console.log(i)
  i++
}
```



### 6.2 for

```javascript
for (let j = 0; j < 6; j++) {
  console.log(j)
}

console.log()
const numbers = [0, 1, 2, 3, 4, 5, ]

for (let number of numbers) {
  console.log(number)
}

for (let number of [0, 1, 2, 3, 4, 5, ]) {
  console.log(number)
}

for (const number of [0, 1, 2, 3, 4, 5, ]) {
  console.log(number)
}
// let과 const 는 선택
```



## 7. function




