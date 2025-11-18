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

  ### null
  프로그래머가 의도적으로 '값이 없음'을 나타냄

  ### undefined
  '값이 할당되지 않음'

  ![javascript-null](javascript-null.png)

  ### Boolean
  참과 거짓을 나타내는 논리적인 자료형
  | 데이터타입 | true | false |
  | ----- | ----- | ----- |
  | undefined | X | 항상 false | 
  | null | X | 항상 false |
  | Number | 나머지 모든 경우 | 0, -0, NaN |
  | String | 나머지 모든 경우 | ' '(빈 문자열) |
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
  - 동등 연산자 (==) `console.log('1' == 1) // true`
  - 일치 연산자 (===) `console.log('1' === 1) // false`
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
  객체의 열거 가능한(enumerable) 속성(property)의 **키(key)**에 대해 반복
  ```
  const capitals = {
    korea : '서울',
    japan : '도쿄',
    china : '베이징',
  }
  for (const capital in capitals) {
    console.log(capital) // korea japan china
  }
  ```

  - ### for ... of
  반복 가능한(iterable) 객체(배열, 문자열 등)의 **값(value)**에 대해 반복
  ```
  const arr = ['a', 'b', 'c']
  for (const elem of arr) {
    console.log(elem) // a b c
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
- 선언식
  ```
  function funcName () {
    statements
  }
  ```
- 표현식
  ```
  const funcName = function () {
    statements
  }
  ```

- 호이스팅 되지않음
- 함수 이름이 없는 익명 함수 사용가능
- 예측 가능성 + 유연성 + 스코프 관리

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

### 화살표 함수 표현식
```
const arrow = name => `hello, &{name}`
```