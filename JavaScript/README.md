FrontEnd 과목평가 대비 ! ✏️ 헷갈리는 것들 정리

### 1. DOM 조작 및 제어

- img 요소의 대체 텍스트(alt)를 자바스크립트로 동적으로 변경할 때 사용하는 속성이나 메서드를 선택하세요.

```jsx
imgElement.alt = 'A sample image'
```

- 클래스 제어

```jsx
const h1 = document.querySelector('h1');
h1.className = 'main'; // h1 요소의 class attribute가 'main'으로 초기화
h1.classList.add('big');
```
<br/>
---
<br/>

### 2. 자바스크립트 기초 문법

- 원시 자료형 : number, string, boolean, null, undefined
- 참조 자료형 : Objects (object, array, function)
- const로 선언한 변수는 **객체인 경우 내부 속성은 변경 가능**
- 논리 연산자의 **단축 평가**

```jsx
// && 연산은 False 나올 때까지
console.log(1 && 0); // 0
console.log(0 && 1); // 0
console.log(4 && 7); // 7

// || 연산은 True 나올 때까지
console.log(1 || 0); // 1
console.log(0 || 1); // 1
console.log(4 || 7); // 4
```

- 수학적으로 정의되지않는 값 (0/0 같은거)은 NaN 출력
- null과 undefined과 boolean

```jsx
let x = null
console.log(type of x) // object
console.log(10 + x) // 10

let y = undefined
console.log(type of y) // undefined
console.log(10 + y) // NaN

let z = true
console.log(type of z) // boolean
```

- key 이름에 띄어쓰기 같은 구분자가 있으면 대괄호 접근만 가능

```jsx
console.log(user.name) // Alice
console.log(user['key with space']) // true
```

- forEach의 인자로 작성된 함수는 일반적인 함수 호출이어서 전역 객체 (window) 가리킴 → **화살표 함수는 자신만의 this를 가지지 않음** → 따라서 화살표 함수 사용 !
- this는 메서드를 호출한 객체를 가리킴 !

<br/>
---
<br/>

### 3. 배열과 객체

- forEach는 **반환값 없이** 배열 모든 요소에 대해 반복 수행
- **구조 분해 할당**

```jsx
const user = { name: 'Hong', email: 'hong@email.com', age: 30 };
const { email } = user; // user 객체의 email 속성값이 email 변수값에 할당됨
```

- **shift( )** : 배열의 첫번째 요소 제거, 그 제거된 값 반환
- **unshift ( )** : 요소를 맨 앞에 추가
- **Object.entries(obj)** : [키, 값] 쌍의 배열 반환
- **Object.hasOwnProperty** : **** 특정 속성 존재 여부를 판별
- **JSON.stringify( )** : 객체 → 문자열로 반환
- **JSON.parse( )** : 문자열 → 객체로 반환
- **new** : 클래스로부터 새로운 객체 인스턴스를 생성할 때 사용
- **map**(callback(**item, index, array**))

<br/>
---
<br/>

### 4. 함수와 제어문

- JavaScript의 반복문과 객체에 대한 설명으로 알맞은 것을 고르시오

```jsx
var user = { name: 'Alice', age: 30 };
for (var key of user) { // for ... of은 값 / for ... in은 키
console.log(key)
}
```

**for … of 반복문은 배열이나 iterable에만 사용할 수 있음**. (배열이면 가능)

일반객체는 기본적으로 iterable하지 않음 → TypeError

- 콜백함수 : 다른 함수에 인자로 전달되는 함수 (map은 새로운 배열 반환)

<br/>
---
<br/>

### 5. 이벤트

- 이벤트 버블링에서 **이벤트는 가장 안쪽(자식)속성에서 시작해 바깥(부모) 요소로** 순차적으로 전파
- **event.target**은 실제 클릭된 요소인 ‘child’, **event.currentTarget**은 이벤트 리스너가 걸려있는 ‘parent’