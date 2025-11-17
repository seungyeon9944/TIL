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
- 예약어 (for, if, function 등) 사용X

### 식별자(변수명) Naming Convention
- 카멜 케이스 (camelCase) : 변수, 객체, 함수에 사용
- 파스칼 케이스 (PascalCase) : 클래스, 생성자에 사용
- 대문자 스네이크 케이스 (SNAKE_CASE) : **상수(constants)**에 사용

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
Document Object Model, 웹 페이지를 구조화된 객체로 제공하여 프로그래밍 언어가 페이지 구조에 접근할 수 있는 방법 제공