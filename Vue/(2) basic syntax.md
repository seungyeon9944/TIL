### Template Syntax
Vue는 DOM을 컴포넌트 인스턴스의 데이터에 **선언적으로 바인딩** (데이터 상태가 바뀌면 화면이 알아서 업데이트되는 것)할 수 있는, HTML 기반 **템플릿 구문**을 사용

### 1. Text Interpolation
이중 중괄호 구문으로 컴포넌트 인스턴스의 msg 속성값으로 대체.
`<p> Message: {{ msg }} </p>`

### 2. Raw HTML
실제 HTML을 출력하려면 v-html을 사용해야함
`<div v-html = "rawHtml"> </div>`

### 3. Attribute Bindings
v-bind를 사용.
HTML의 **id 속성 값**을 vue의 **dynamicId 속성과 동기화**되도록 함
`<div v-bind.id = "dynamicId"> </div>`

### 4. JavaScript Expressions
`{{ number + 1 }}`, `{{ message.split(' ').reverse().join('')}}`, `<div v-bind:id="`list-${id}`"></div>`
각 바인딩에는 하나의 단일 표현식만 포함될 수 있음. 표현식이 아닌 선언식에는 X

### Directive
'v-' 접두사가 있는 특수 속성
- 단일 JavaScript 표현식이어야 (v-for, v-on 제외)
- 표현식 값이 변경될 때 DOM에 반응적으로 업데이트 적응
- Directive 전체 구문
![Directive 전체 구문](https://velog.velcdn.com/images/bzeromo/post/877b18e6-af6d-421d-bbfb-bcf185e07a53/image.png)
- Directive: "Arguments"
`<a v-bind:href="myUrl">Link</a>`에서 href는 HTML `<a>`요소의 href 속성값을 바인딩하도록 하는 v-bind의 인자
- Directive: "Modifiers"
`<form v-on:submit.prevent="onSubmit">`에서 .prevent는 발생한 이벤트에서 event.preventDefault()를 호출하도록 v-on에 지시하는 modifier

### v-bind
하나 이상의 속성 또는 컴포넌트 데이터를 표현식에 동적으로 바인딩
- Attribute Bindings (속성 바인딩)
```
<img v-bind:src = "imageSrc">
<a v-bind:href = "myUrl">Move to url</a>
```

- v-bind shorthand (약어)
```
<img:src = "imageSrc">
<a:href = "myUrl">Move to url</a:href>
```

- Dynamic attribute name (동적 인자 이름)
대괄호로 감싸서 directive argument에 JavaScript 표현식 사용할 수 있음
```
<button :[key]="myValue"></button>
```

---

### Class and Style Bindings (클래스와 스타일 바인딩)
- class와 style은 모두 HTML 속성이므로 다른 속성과 마찬가지로 **v-bind** 사용하여 동적으로 할당
- **객체** 또는 **배열**을 활용하여 작성할 수 있도록 함

### 1.1 Binding HTML Classes: Binding to Objects
```
const isActive = ref(true)
<div :class="{ active: isActive }">Text</div>
```

### 1.2 Binding HTML Classes: Binding to Arrays
```
const activeClass = ref('active')
const infoClass = ref('text-primary')

<div :class="[activeClass, infoClass]">Text</div>
```

### 2.1 Binding Inline Styles: Binding to Objects
```
const activeColor = ref('crimson')
const fontSize = ref(50)

<div :style="{ color: activeColor, fontSize: fontSize + 'px' }">Text</div>
```

### 2.2 Binding Inline Styles: Binding to Arrays
```
const styleObj2 = ref({
  color: 'blue',
  border: '1px solid black'
})

<div :style="[styleObj, styleObj2]">Text</div>
```

### v-on
- DOM 요소에 이벤트 리스너를 연결 및 수신
`v-on:event="handler"`

- v-on shorthand (약어)
`@event="handler"`

1. Inline handlers
```
const count = ref(0)

<button @click="count++">Add 1</button>
<p>Count: {{ count }}</p>
```
`<button @click="warning('경고입니다',$event)">Warning</button>`처럼 **$event** 변수를 사용하여 메서드에 전달

2. Method Handlers
**@click="myFunc"**처럼 괄호 없이 메서드 이름만 연결하면 핸들러의 첫번째 인자로 DOM의 EVENT 객체가 자동으로 전달됨
```
const myFunc = function (event) {
  count.value += 1
}

<button @click="myFunc">Hello</button>
```

- Event Modifiers
stop, prevent, self 등 다양한 modifier로 코드를 메서드 안에 직접 작성할 필요가 없도록 함
`<form @submit.prevent="onSubmit">...</form>`

- Key Modifiers
```
<input @keyup.enter="onSubmit">
<textarea @keydown.ctrl.enter="submitComment"></textarea>
```

### Form Input Bindings (폼 입력 바인딩)
form을 처리할 때 사용자가 input에 입력하는 값을 실시간으로 JavaScript 상태에 동기화해야 하는 경우 (양방향 바인딩)

### v-model
form input 요소 또는 컴포넌트에서 양방향 바인딩을 만듦
- 사용자 입력 데이터와 반응형 변수를 실시간 동기화
```
const inputText2 = ref('')
<p>{{ inputText2 }}</p>
<input v-model="inputText2">
```
- Checkbox와 활용 `<input type="checkbox" id="checkbox" v-model="checked">`
- Select와 활용 
```
const selected = ref('')

<div>Selected: {{ selected }}</div>
<select v-model = "selected">
  <option disabled value="">Please select one</option>
  <option>A</option>
  <option>B</option>
  <option>C</option>
</select>
```

---

### computed( )
"계산된 속성"을 정의하는 함수
- 템플리 표현식을 단순하게, 불필요한 반복 연산 줄여줌
- 한번 계산된 값은 캐싱(임시 저장)되어 성능에 유리함
```
const { createApp, ref, computed } = Vue

const restOfTodos = computed(() => {
  return todos.value.length > 0 ? '아직 남았다'  : '퇴근!'
})
```
- 반환되는 값은 계산된 **ref (computed ref)**이며 계산된 결과를 .value로 참조 가능
- 의존된 반응형 데이터를 **자동으로 추적**, 결과를 캐시
- 의존하는 반응형 데이터가 **변경될 때만 재평가**

### 캐시 (Cache)
데이터나 결과를 일시적으로 저장해두는 임시 저장소
- 페이지 일부 데이터를 브라우저 캐시에 저장 후 같은 페이지에 다시 요청 시 모든 데이터를 다시 응답받는게 아닌 ! **일부 캐시 된 데이터 사용**하여 더 빠르게 웹 페이지 렌더링


#### computed VS method
| computed | method |
| ----- | ----- |
| 의존된 데이터가 변경되면 자동 업데이트 | 호출해야만 실행됨 |
| 동일 의존성 가진 여러 곳에서 계산 결과 캐싱하여 중복 계산 방지 | 데이터 의존여부 관계없이 항상 동일한 결과 반환 |

---

### v-if
표현식 값의 true/false를 기반으로 요소를 조건부로 렌더링
- 조건이 참이면 HTML 요소를 화면에 보여줌
- 조건이 거짓이면 해당 요소는 DOM에서 완전히 제거되어 안보임
```
const name = ref('Cathy')

<template v-if="name === 'Cathy'">
  <div>Cathy입니다</div>
  <div>나이는 30살입니다</div>
</template>
```

### v-show
표현식 값의 true/false를 기반으로 요소의 가시성을 전환
- v-if와 다르게 **CSS의 display 속성**을 none으로 바꿔 화면에서만 안 보이게 숨김
```
const isShow = ref(false)

<div v-show="isShow">v-show</div>
<div style="display: none;">v-show</div>
```

---

### v-for
**소스 데이터**를 기반으로 요소 또는 템플릿 블록을 반복 렌더링
- alias in expression 형식의 구문 사용
- 객체는 key-value 쌍으로 이루어져있음
- 각 요소를 key를 활용하여 고유한 값으로 식별
```
<div v-for="item in items" :key="item.id">
  {{ item.name }}
</div>
```

#### v-for와 v-if 
v-if가 더 높은 우선순위 가지므로 v-for 범위의 todo 데이터를 v-if에서 사용할 수 없음 ! 그리고 동일 요소에 v-for와 v-if를 함께 사용하면 안됨

  sol 1) **computed 활용**하여 이미 필터링 된 목록 반환하여 반복하도록 설정하여 해결
  ```
  const completeTodos = computed(() => {
    return todos.value.filter((todo) => !todo.isComplete)
  })

  <ul>
    <li v-for="todo in completeTodos" :key="todo.id">
      {{ todo.name }}
    </li>
  </ul>
  ```

  sol 2) v-for와 template 요소를 사용하여 **v-if 위치 이동**
  ```
  <ul>
    <template v-for="todo in todos" : key="todo.id">
      <li v-if="!todo.isComplete">
        {{ todo.name }}
      </li>
    </template>
  </ul>
  ```

---

### watch ( )
하나 이상의 반응형 데이터 감지하고, 감시하는 데이터(ref)가 변경되면 콜백 함수 호출

구조 : `watch(source, (newValue, oldValue) => { // sth })`

#### computed VS watch
| computed | watch |
| ----- | ----- |
| 의존하는 데이터 속성의 계산된값 반환 | 데이터 속성의 변화 감시, 작업 수행 |
| 계산 결과 캐싱하여 중복 계산 방지 | 데이터 변화에 따른 특정 작업 수행 |
| ex) 연산된 길이, 필터링된 목록 계산 | ex) DOM 변경, 다른 비동기 작업, 외부 API와 연동 |

---

### Lifecycle Hooks
Vue 컴포넌트가 생성되고, DOM에 마운트되고, 업데이트되고, 소멸되는 각 생애 주기 단계에서 실행되도록 제공되는 함수 
- onMounted
  Vue 컴포넌트 인스턴스가 **초기 렌더링 및 DOM 요소 생성이 완료된 후** 특정 로직 수행
- onUpdated
  반응형 데이터의 변경으로 인해 컴포넌트의 **DOM이 업데이트된 후** 특정 로직 수행

### Vue Style Guide
우선순위에 따라 4가지 범주 (A: 필수, B: 적극 권장, C: 권장, D: 주의 필요)로 나뉨