### event
웹 페이지 상에서 '무언가 일어났다는 신호 또는 사건'

DOM에서 이벤트가 발생하면 브라우저는 해당 이벤트는 연결된 이벤트 처리기(**event handler**)에 의해 처리됨

### event handler
특정 이벤트가 발생했을 떄 실행되는 (콜백)함수

### `.addEventListener()`
특정 DOM 요소에, 지정한 이벤트가 발생했을 때 실행할 이벤트 핸들러를 **등록하는 메서드**
```
# 1. 요소 가져오기
const button = document.querySelector('button')

# 2. 이벤트 핸들러
const handleClick = function () {
  window.alert('버튼이 클릭 되었습니다!')
}

# 3. addEventListener 메서드를 이용해 이벤트 핸들러 등록
button.addEventListener('click', handleClick)
```
- DOM 요소.리스너(수신할 이벤트, 핸들러) 로 구성되어있음

### 버블링 (Bubbling)
- 한 요소에 이벤트 발생하면, 해당 요소의 핸들러로 동작한 후 이어서 부모 요소의 핸들러가 동작
- **가장 최상단의 조상 요소(document)** 만날 때까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작

이벤트가 정학히 어디서 발생했는지 접근할 수 있는 방법
### 1. `event.currentTarget`
'현재' 요소로 항상 이벤트 핸들러가 연결된 요소만을 참조, 'this'와 같음
```
const inputTag = document.querySelector("#text-input")
const h1Tag = document.querySelector("h1")

const inputHandler = function(event){
  h1Tag.textContent = event.currentTarget.value // input에 입력한 값을 h1 태그에 지정
}
inputTag.addEventListener("input", inputHandler)
```

### 2. `event.target`
이벤트가 발생한 가장 안쪽의 요소를 참조, 실제 이벤트가 시작된 요소로 버블링이 진행되어도 변하지x

---

### 캡쳐링 (capturing)
버블링과 반대로 이벤트가 하위로 전파되는 단계.
- table의 하위 요소 td를 클릭하면 이벤트는 먼저 **최상위 요소부터 아래로 전파** (캡처링)
- 실제 이벤트가 발생한 지점(event.target)에서 실행된 후 **다시 위로 전파** (버블링)

---

### `.preventDefault()`
해당 이벤트에 대한 기본 동작 실행하지 않도록 지정