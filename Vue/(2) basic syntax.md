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