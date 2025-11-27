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


