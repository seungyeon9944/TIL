### 1. 원시 자료형 (Primitive type)
- **값 자체가 변수에 직접 저장**
- **불변(immutable)**이며, 변수 간 할당 시 값이 복사
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
- **가변(mutable)**이며, 변수 간 할당 시 주소가 복사
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
  - if 
    조건 표현식의 결과값을 boolean 타입으로 변환 후 참/거짓을 반환

  - 삼항 연산자
    ```
    const age = 20
    const message = (age >= 18) ? '성인' : '미성년자'
    console.log(message) // '성인'
    ```

