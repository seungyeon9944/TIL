### 1. 원시 자료형 (Primitive type)
- **값 자체가 변수에 직접 저장**
- **불변**이며, 변수 간 할당 시 값이 복사
- Number, String, Boolean, null, undefined
```
const a = 'bar'
console.log(a) // bar

a.toUpperCase()
console.log(a) // bar 

const text = a.toUpperCase()
console.log(text) // BAR
```

  ### 1-1. Number
  - 정수 또는 실수형 숫자
  - 문자열과 + 연산 시, **숫자가 문자열로 자동 형변환**되어 연결
  - 정수와 실수 구분x, 모든 숫자를 단일 타입으로 처리

  ### 1-2. String
  - '+' 연산자를 사용해 문자열끼리 결합
  - 뺄셈, 곱셈, 나눗셈 x

  ### Template literals (템플릿 리터럴)
  - 백틱을 이용하여 표현식은 '$'와 중괄호({expression})으로 표현하여 **자바스크립트의 변수를 문자열 안에 바로 연결**
  ```
  const message = `홍길동은 ${age}세입니다.`
  ```

  ### 1-3. null
  프로그래머가 의도적으로 '값이 없음'을 나타냄

  ### 1-4. undefined
  '값이 할당되지 않음'

  ![javascript-null](javascript-null.png)

  ### 1-5. Boolean
  참과 거짓을 나타내는 논리적인 자료형
  | 데이터타입 | true | false |
  | ----- | ----- | ----- |
  | undefined | X | 항상 false | 
  | null | X | 항상 false |
  | Number | 나머지 모든 경우 | 0, -0, NaN |
  | String | 나머지 모든 경우 | ''(빈 문자열) |
  ```
  console.log(Boolean([])); // true
  console.log(Boolean({})); // true
  ```
---

### 2. 참조 자료형 (Reference type)
- 데이터가 저장된 **메모리의 주소가 변수에 저장**
- **가변**이며, 변수 간 할당 시 주소가 복사
- Objects(Object, Array, Function)
```
const obj1 = { name: 'Alice', age: 30 }
const obj2 = obj1

obj2.age = 40

console.log(obj1.age) // 40
console.log(obj2.age) // 40
```
---

### 연산자
  - 할당 연산자 (단축 연산자 지원) `let a = 10; a += 10;`
  - 증가 연산자 ('++')
    ```
    let x = 3
    const y = x++
    console.log(x, y) // 4 3

    let a = 3
    const b = ++a
    console.log(a, b) // 4 4
    ```
  - 감소 연산자 ('--')
  - 비교 연산자 `'Z' < 'a' // true`
  - 동등 연산자 (==, 값만 비교) `console.log('1' == 1) // true`
  - 일치 연산자 (===, **값+타입** 다 비교) `console.log('1' === 1) // false`
  - 논리 연산자 (&&, ||, !)
    ```
    1 & 0 // 0
    0 & 1 // 0
    4 & 7 // 7
    1 || 0 // 1
    0 || 1 // 1
    4 || 7 // 4
    ```

### 조건문
  - ### if 
  조건 표현식의 결과값을 boolean 타입으로 변환 후 참/거짓을 반환

  - ### 삼항 연산자
  ```
  const age = 20
  const message = (age >= 18) ? '성인' : '미성년자'
  console.log(message) // '성인'
  ```

### 반복문
  - ### while
  조건문이 참이면 문장을 계속해서 수행

  - ### for
  특정한 조건이 거짓으로 판별될 때까지 반복
  ```
  for ([초기문]; [조건문]; [증감문]) {
    // do something
  }

  <!-- loops-and-iteration.html -->
  for (let i = 0; i < 6; i++) { // 코드블록 실행 이후 i값 증가
    console.log(i)
  }
  ```

  - ### for ... in
  객체의 열거 가능한(enumerable) 속성(property)의 **키(key)** 에 대해 반복
  ```
  const capitals = {
    korea : '서울',
    japan : '도쿄',
    china : '베이징',
  }
  for (const capital in capitals) {
    console.log(capital) // korea japan china
  }

  const arr = ['a', 'b', 'c']
  for (const i in arr) {
    console.log(i) // 0, 1, 2
  }
  ```

  - ### for ... of
  반복 가능한(iterable) 객체(배열, 문자열 등)의 **값(value)** 에 대해 반복
  ```
  const arr = ['a', 'b', 'c']
  for (const elem of arr) {
    console.log(elem) // a, b, c
  }
  ```

---

### 함수
참조 자료형에 속하며 모든 함수는 Function Object
```
function name ([param[, param,[..., param]]]){
  statements
  return values
}
```
- 선언식 (호이스팅o, 구조+가독성)
  ```
  function funcName () {
    statements
  }
  ```

- 표현식 (호이스팅x, 익명함수o, 예측 가능성 + 유연성 + 스코프 관리)
  ```
  const funcName = function () {
    statements
  }
  ```

### 매개변수
- 기본 함수 매개변수
  ```
  const greeting = function (name = 'Anonymous') {
    return 'Hi ${name}'
  }

  greeting() // Hi Anonymous
  ```
- 나머지 매개변수
  ```
  const myFunc = function (param1, param2, ... restPrams){
    return [param1, param2, restPrams]
  }

  myFunc(1, 2, 3, 4, 5) // [1, 2, [3, 4, 5]]
  myFunc(1, 2) // [1, 2, []]
  ```
- 매개변수 > 인자 개수일 때 : 누락된 인자는 undefined로 할당
- 매개변수 개수 < 인자 개수일 때 : 초과 입력한 인자는 사용x

### Spread syntax '...'
배열이나 문자열처럼 반복가능한 항목들을 개별 요소로 펼침
- 인자 확장 (함수 호출 시)
```
function myFunc(x, y, z){
  return x + y + z
}
let numbers = [1, 2, 3]
console.log(myFunc(...numbers)) // 6
```

- 나머지 매개변수 (압축)
```
function myFunc2(x, y, ...restArgs) {
  return [x, y, restArgs]
}

console.log(myFunc(1, 2)) // [1, 2, []]
```

- 배열과의 활용

### 화살표 함수 표현식
```
const arrow = name => `hello, &{name}`
```

---

### 객체 구조
- 중괄호('{ }')를 이용해 작성
- 중괄호 안에는 key:value 쌍으로 구성된 속성 여러개 작성 가능
- key는 문자형만 허용

### 속성 참조
- 점('.') 표기법 또는 대괄호 ('[]') 표기법으로 속성에 접근
  ex. `console.log(user.name)` 또는
  `console.log(user['key with space'])`

### 'in' 연산자
- 속성이 객체에 존재하는지 여부 확인
- 객체의 키나 배열의 인덱스 존재 여부 확인

### 메서드 (Method)
- 객체 속성에 정의된 함수
- 메서드는 자신이 속한 객체의 다른 속성들에 접근할 수 있음 → this

### `this`
- 함수나 메서드를 호출한 객체를 가리키는 키워드
- 함수가 **호출될 때 동적으로 결정**
```
const person = {
  name: 'Alice',
  greeting: function() {
    return `Hello my name is ${this.name}`
  },
}

console.log(person.greeting()) 
```

- this는 함수를 **호출하는 방법**에 따라 가리키는 대상이 달라짐

| 호출 방법 | 대상 |
| ----- | ----- |
| 일반 함수에서의 단순호출 | 전역 객체 |
| 객체에서의 메서드 호출 | 메서드를 호출한 객체 |

```
const myObj = {
  data: 1,
  myFunc: function() {
    return this
  }
}

console.log(myObj.myFunc()) // myObj
```

- forEach의 인자로 전달된 콜백 함수는 일반 함수로 호출 → this는 전역 객체를 가리킴
```
const myObj2 = {
  numbers: [1, 2, 3],
  myFunc: function () {
    this.numbers.forEach(function (number) {
      console.log(this) // window
    })
  }
}

console.log(myObj2.myFunc())
```

- forEach 문제를 해결하기 위해 **화살표 함수** 이용 (**자신만의 this를 갖지않음**)
```
const myObj3 = {
  numbers: [1, 2, 3],
  myFunc: function () {
    this.numbers.forEach((number) =>
{
      console.log(this) // myObj3
    })
  }
}

console.log(myObj3.myFunc())
```

---

추가 객체 문법
### 1. 단축 속성 ⭐
키 이름과 값으로 쓰이는 변수이름이 같으면 단축 구문 사용가능
```
const name = 'Alice'
const age = 30
const user = {
  name,
  age,
} # {name: name, age: age}랑 같은 의미
```

### 2. 단축 메서드
메서드 선언 시 function 키워드 생략 가능

### 3. 계산된 속성 (computed property name)
키가 대괄호 ([])로 둘러싸여 있는 속성

### 4. 구조 분해 할당 (destructing assignment)
배열 또는 객체를 분해하여 객체 속성을 변수에 쉽게 할당할 수 있는 문법
`const firstName = userInfo.firstname`와 `const { firstName } = userInfo`

### 5. 객체와 전개 구문 (Spread Syntax, ...)
- "객체 복사"
- **얕은 복사**에 활용 가능

### 6. 유용한 객체 메서드
- `Object.keys()` : 키값들을 리스트로 변환
- `Object.values()` : Value값들을 리스트로 변환
- `Object.entries()` : 키와 Value값들을 한쌍으로 묶은 리스트로 변환

### 7. Optional chaining ('?.')
- 속성이 없는 중첩 객체에 접근하려고 할 때 에러 발생 없이 안전하게 접근
- 연결된 속성으로 접근할 때 더 짧고 간단하게 작성, 어떤 속성이 필요핮니에 대한 보증이 확실하지 않은경우 내용을 편리하게 탐색할 수 있음
```
console.log(user.address.street) // Uncaught TypeError
console.log(user.address?.street) // undefined
```

---

### JSON (JavaScript Object Notation)
Key-Value 형태로 이루어진 자료 표기법

### 배열
순서가 있는 데이터 집합 저장하는 자료구조
- `push( )` : **배열 끝**에 요소 추가
- `pop( )` : **배열 끝** 요소 제거
- `unshift( )` : **배열 앞**에 요소를 추가, 배열이 클수록 성능 저하
- `shift( )` : **배열 앞** 요소 제거, 제거한 요소 반환, 배열이 클수록 성능 저하

### Array Helper Methods
- 배열의 각 요소를 **순회**하며 각 요소에 대해 함수(**콜백함수**) 호출
- `forEach( )` : 파이썬의 map함수와 유사, 반환 값이 없음
- `map( )` : 배열의 모든요소에 콜백함수 호출, 함수 호출 결과를 모다 **새로운 배열 반환**
- `reduce( )`

### 콜백 함수 (Callback function)
- 다른 함수에 인자로 전달되는 함수
- 특정 작업이 완료된 후, 시스템에 의해 나중에 호출되는 함수

### `forEach()`
- 배열의 모든 요소 반복하며 콜백함수 호출
- `arr.forEach(callback(item[, index[, array]]))`
- item + index + arrary 3가지 매개변수로 구성됨
- 반환값 : undefined

### `map()`
- 배열 순회하며 각 객체의 name 속성 값 추출해서 **새로운 배열 반환**
- 새로운 배열 반환하므로 다른 메서드를 **체이닝**할 수 있음
- `const result2 = persons.map(function (person) {return person.name})`
```
const names = ['A', 'B', 'C']
const result1 = names.map(function (name) {
  return name.length
})
const result2 = names.map((name) => {
  return name.length
})
```
```
const numbers = [1, 2, 3]
const myCallbackFunc = function (number) {
  return number * 2
}
const doubleNumber = numbers.map(myCallbackFunc)
console.log(doubleNumber) // [2, 4, 6]
```

### `filter()`
콜백 함수의 반환 값이 참인 요소들만 모아서 새로운 배열 반환
```
const languages = ['python', 'javascript', 'html', 'java']
    const query = 'java'

    const language = languages.filter(value => value.includes(query))
    console.log(language) // ['javascript', 'java']
```

### `find()`
콜백 함수의 반환 값이 참이면 해당 요소를 반환
```
const accounts = [
      { name: 'sophia', balance: 1200 },
      { name: 'john', balance: 50000 },
      { name: 'tailer', balance: 24000 }
    ]

    const person = accounts.find(({balance}) => balance == 24000)
    console.log(person)
```

### `some()`
적어도 하나라도 콜백 함수 통과하면 true 반환 → 즉시 배열 순회 중지 / 모두 통과x하면 false 반환

### `every()`
모든 요소가 콜백 함수 통과하면 true 반환 / 하나라도 통과x하면 false 반환 → 즉시 배열 순회 중지