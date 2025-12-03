### Props
**부모** 컴포넌트로부터 **자식** 컴포넌트로 데이터를 전달하는데 사용되는 사용자 지정 특성
- 반대는 불가능 (자식 컴포넌트 내부에서 props 변경하려고 시도해서도 x, 불가능)
- 모든 props는 **하향식 단방향 바인딩** 형성 (one-way-down binding)
- props 선언하는 법
1. vue 프로젝트 생성
2. 초기 생성된 컴포넌트 모두 삭제
3. src/assets 내부 파일 모두 삭제
4. main.js의 `import './assets/main.css'` 삭제
5. App > Parent > ParentChild 컴포넌트 관계 작성
- App.vue의 template 안의 div에는 `<Parent />`, script 안에는 `import Parent from '@/components/Parent.vue'`
- Parent.vue의 template 안의 div에는 `<Parentchild />`, script 안에는 `import ParentChild from '@/components/ParentChild.vue'`
6. 부모 컴포넌트 Parent에서 자식 컴포넌트 ParentChild에 보낼 props 작성 `<ParentChild my-msg="message" />`
7. Props 선언 (script setup 안에 `defineProps()`, 문자열 배열을 사용하거나 객체를 사용할 수 있음)

- 한단계 더 props 내려 보내기
ParentChild 컴포넌트에서 **Parent로부터 props인 myMsg**을 ParentGrandChild에게 전달 !

- Props Name Casing (Props 이름 컨벤션)
    - 부모 템플릿에서 전달 시 (HTML 속성) : kebab-case (`my-msg`)
    - 자식 스크립트에서 선언 시 (JavaScript) : camelCase (`myMsg`)
- Static Props와 Dynamic Props
v-bind를 사용하여 **동적으로 할당된 props** 사용 가능

---

### $ emit()
자식 컴포넌트가 이벤트를 발생시켜 부모 컴포넌트로 데이터를 전달하는 메서드 (props와 반대로 **올라가는** 이벤트 만듦)
- `$emit(event, _args)` 형태로 구성됨
- $emit을 사용하여 템플릿 표현식에서 직접 사용자 정의 이벤트 발신
- 부모 컴포넌트에서는 v-on (또는 @)을 사용하여 이벤트 수신

### defineEmits( )
`<script setup>` 내에서 이벤트 발신하기 위한 **emit 함수 반환**

**이벤트 인자 (Event Arguments)** : ParentChild에서 이벤트 발신하여 Parent로 추가 인자 전달, ParentChild에서 발신한 이벤트 Parent에서 수신.