# CSS (Cascading Style Sheet)
웹 페이지의 디자인과 레이아웃을 구성하는 언어

1. **인라인(Inline) 스타일** : HTML 요소 안에 style 속성값. 가독성과 유지보수성 때문에 거의 안씀

`<body>`

    `<h1 style="color: blue; background-color: yellow;"Hello World! </h1>`
2. **내부(Internal) 스타일** : head 태그 안에 style 태그에 작성

  `<style>`

    `h1 {`
      `color : blue;`
      `background-color: yellow;`
    `}`
`</style>`

3. **외부(External) 스타일** : 별도의 CSS 파일 생성 후 HTML link 태그 사용해 불러옴

`<link rel= "stylesheet" href="style.css">`

---

- 선택자(Selector) : 누구를 꾸밀지. `h1`
- 선언(Declaration) : 어떻게 꾸밀지. `{ 속성: 값; 속성: 값; }`
- 속성(Property) `color, font-size`
- 값(Value) `red, 30px`

## CSS Selectors (CSS 선택자)
기본 선택자
1. **전체 선택자 (*)** : HTML 모든요소 선택
2. **요소 선택자** / 태그 선택자
3. **클래스 선택자 ('.')** : 주어진 클래스 속성을 가진 모든 요소 (재사용성 + 명시도 신경쓸필요 X)
4. **아이디 선택자('#')** : 주어진 아이디 속성을 가진 요소 선택 .. 문서에 해당 아이디 가진 요소가 1개만 있어야함'
5. **속성 선택자('[]')** 

CSS 결합자
1. **자손 결합자(" ")** : 모든 자손 요소들 선택
2. **자식 결합자 (">")** : 직계 자식만 선택

## CSS Declaration (CSS 선언)
선택된 요소에 적용할 스타일을 구체적으로 명시
`{ 속성: 값; 속성: 값; }`으로 속성에는 font-size, background-color, width, margin, padding 등이 있음


값의 단위 ?
- 절대 단위 : `px`, `pt`, `cm` 등
- 상대 단위 : `%`, `em` (부모요소의 폰트사이즈를 기준으로 크기가 결정), `rem`(최상위 요소인 `<html>`의 폰트사이즈를 기준으로 크기가 결정, 일관성 + 유지보수성 + 접근성), `vw`, `vh` 등

---

## 명시도 Specificity
CSS 선언을 결정하기 위한 알고리즘. 여러 개의 CSS 규칙이 있을 때 가장 높은 명시도를 가진 Selector가 승리.
Cascade의 경우에 동일한 가중치이면 계단식이라 마지막에 나오는 선언이 사용됨

명시도가 높은 순:
1. Importance (`!important`) -> 사용 X
2. Inline 스타일
3. 선택자 (id 선택자 > class 선택자 > 요소 선택자)
4. 소스 코드 선언 순서

---

## 상속
부모 요소의 속성을 자식에게 상속
상속되는 속성 : Text 관련 요소 (font, color, text-align), opacity, visibility 등

---

## CSS Box Model
모든 HTML 요소를 감싸는 사각형 상자 모델
- Margin : 외부 간격
- Content : 실제 내용의 영역
- Border : content와 padding 감싸는 테두리
- Padding : content와 border 사이의 내부 여백