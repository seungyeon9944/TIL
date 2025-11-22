### URL
특정 웹페이지나 파일을 찾기 위해 고유한 경로 주소

### HTTP
웹 브라우저와 서버가 데이터를 주고받기 위한 통신 규약

### www
World Wide Web, 전 세계적인 정보 공유 시스템

---

웹의 기술적 발전과 **웹 표준의 중요성** 

→ 크롬의 **V8 자바스크립트 엔진** (기존 인터프리터 → JIT로 속도 증진)

### ECMAScript
**표준화**된 스크립트 프로그래밍 언어 명세, JavaScript의 표준

---

### 식별자(변수명) 작성 규칙
- 반드시 문자, 달러('$'), 밑줄('_')로 시작
- 대소문자 구분
- 예약어 (for, if, function 등)를 변수명으로 사용X

### 식별자(변수명) Naming Convention
- 카멜 케이스 (camelCase) : 변수, 객체, 함수에 사용
- 파스칼 케이스 (PascalCase) : 클래스, 생성자에 사용
- 대문자 스네이크 케이스 (SNAKE_CASE) : **상수**에 사용

### 변수 선언 키워드 3가지
### `let`
- **재할당 가능**
  ```
  let number = 10
  number = 20
  ```
- 재선언 불가능
  ```
  let number = 10
  let number = 20 # 불가능
  ```

### `const`
- 재할당 불가능
  ```
  const number = 10
  number = 20 # 불가능
  ```
- 재선언 불가능
  ```
  const number = 10
  const number = 20 # 불가능
  ```
- 코드 의미 명확화 + 버그 예방으로 const를 기본으로 사용 !

### 블록 스코프 (block scope)
- if, for, 함수 등의 **중괄호({}) 내부** 가리킴
- 블록 스코프 갖는 변수는 블록 바깥에서 접근 불가능
```
let x = 1
if (x === 1) {
  let x = 2
  console.log(x) // 2
}
console.log(x) // 1
```

---


웹 브라우저에서의 JavaScript
- 웹 페이지에서의 동적인 기능을 담당
- HTML script 태그, js 확장자 파일, 브라우저 Console
  
### DOM
- Document Object Model, 웹 페이지를 구조화된 객체로 제공하여 프로그래밍 언어가 페이지 구조에 접근할 수 있는 방법 제공
- **DOM tree** : HTML 태그를 나타내는 elements의 node는 문서의 구조를 결정
- 즉 **문서의 요소들을 객체로 제공**하여 다른 프로그래밍 언어에서 **접근하고 조작할 수 있는 방법을 제공**하는 API 
- **웹 페이지를 동적으로 만들기 == 웹 페이지를 조작하기** by 조작하고자 하는 요소 **선택** → 속성 **조작** 

---

### 선택 메서드
### `document.querySelector(selector)`
제공된 선택자(selector)와 일치하는 첫번째 요소 한 개 선택하여 반환 (없으면 null 반환)
- `document.querySelector('.content')` // 클래스 선택자
- `document.querySelector('#id')` // 아이디 선택자
- `document.querySelector('ul > li')` // li 태그선택자

### `document.querySelectorAll(selector)`
제공된 선택자(selector)와 일치하는 여러 element 선택하여 NodeList 반환

---

### DOM 조작
1. 속성 (attribute) 조작 
  - 1.1 클래스 속성 조작 ⭐
  
    `'classList' property` : 요소의 클래스 목록을 유사 배열 형태로 변환
    ### `element.classList.add()`
    지정한 클래스 값 추가
    ### `element.classList.remove()`
    지정한 클래스 값 제거
    ### `element.classList.toggle()`
    클래스가 존재한다면 제거 + false 반환 / 존재하지않으면 클래스 추가 + true 반환
    
  - 1.2 일반 속성 조작
    ### `Element.getAttribute()`
    해당 요소에 지정된 값 반환 (조회)
    ### `Element.setAttribute(name, value)`
    지정된 요소의 속성 값 설정, 속성 이미 있으면 기존 값 갱신
    ### `Element.removeAttribute()`
    요소에서 지정된 이름 가진 속성 제거

2. HTML 콘텐츠 조작 ⭐
   
   `'textContent' property` : 요소의 텍스트 컨텐츠를 표현. ex) `<p> lorem <p>`

3. DOM 요소 조작
   ### `document.createElement(tagName)`
   작성한 tagName의 HTML 요소를 생성하여 반환
   ### `Node.appendChild()`
   한 Node를 특정 부모 Node의 자식 NodeList 중 마지막 자식으로 삽입, 추가된 Node 객체 반환
   ### `Node.removeChild()`
   DOM에서 자식 Node를 제거, 제거된 Node 반환

4. 스타일 조작
   ### `'style' property`

---

### Node
DOM의 기본 구성 단위

### NodeList
DOM 메서드를 사용해 선택한 Node의 목록

### Element
DOM 트리에서 HTML 요소를 나타내는 특별한 유형의 Node

### Parsing
브라우저가 문자열을 해석하여 DOM Tree로 만드는 과정 (구문 분석, 해석)

### 호이스팅 (hoisting)
변수 **선언문이 코드의 최상단으로 끌어올려지는 듯한** 현상
```
console.log(name) // undefined
var name = '홍길동' // 선언 및 할당
```