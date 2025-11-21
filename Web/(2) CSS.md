# CSS (Cascading Style Sheet)
웹 페이지의 디자인과 레이아웃을 구성하는 언어

1. **인라인(Inline) 스타일** : HTML 요소 안에 style 속성값. 가독성과 유지보수성 때문에 거의 안씀

```
<body>
  <h1 style="color: blue; background-color: yellow;" Hello  World! </h1>
```

2. **내부(Internal) 스타일** : head 태그 안에 style 태그에 작성

```
<style>
  h1 {
    color : blue;
    background-color: yellow;
  }
</style>
```

3. **외부(External) 스타일** : 별도의 CSS 파일 생성 후 HTML link 태그 사용해 불러옴

`<link rel= "stylesheet" href="style.css">`

---

- 선택자(Selector) : 누구를 꾸밀지. `h1`
- 선언(Declaration) : 어떻게 꾸밀지. `{ 속성: 값; 속성: 값; }`
- 속성(Property) `color, font-size`
- 값(Value) `red, 30px`

## CSS Selectors (CSS 선택자)
### 기본 선택자
1. **전체 선택자 (*)** : HTML 모든요소 선택
2. **요소 선택자** / 태그 선택자
3. **클래스 선택자 ('.')** : 주어진 클래스 속성을 가진 모든 요소 (✅재사용성 + ✅명시도 신경쓸필요 X)
4. **아이디 선택자('#')** : 주어진 아이디 속성을 가진 요소 선택 .. ✅문서에 해당 아이디 가진 요소가 1개만 있어야함'
5. **속성 선택자('[]')** : 주어진 속성이나 속성값을 가진 모든 요소 선택. ex) `p[class^="y"]` 면 class명이 "y"로 시작하는 p요소를 뜻함

### CSS 결합자 (Combinators) ⭐⭐⭐
1. **자손 결합자(" ")** : **모든 자손 요소들** 선택. `p span`은 `<p>` 안에 있는 모든 `<span>`를 선택 (하위 레벨 상관 없이). 뒤쪽 선택자의 요소의 조상에 앞쪽 선택자 요소가 존재할 경우.
```
.blue p {
}
```

2. **자식 결합자 (">")** : **직계 자식만** 선택. 
`ul > li`은 `<ul>` 안에 있는 모든 `<li>`를 선택 (한단계 아래 자식들만). 뒤쪽 선택자의 요소가 앞쪽 선택자의 요소의 바로 밑에 위치할 때만.
```
.red > p {
}
```

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
3. 선택자 (✅ id 선택자 > class 선택자 > 요소 선택자)
4. 소스 코드 선언 순서

---

## 상속
부모 요소의 속성을 자식에게 상속
✅ 상속되는 속성 : Text 관련 요소 (font, color, text-align), opacity, visibility 등

---

## CSS Box Model
모든 HTML 요소를 감싸는 사각형 상자 모델
- **Margin** : 외부 간격
- **Border** : content와 padding 감싸는 테두리
- **Padding** : content와 border 사이의 내부 여백
- **Content** : 실제 내용의 영역

**shorthand 속성** : 속성을 한번에 지정할 수 있는 속성 ⭐⭐

4 - **상우하좌** 
`margin: 10px 20px 20px 30px;`

3 - **상 / 좌우 / 하**
`margin: 10px 20px 30px;`

2 - 상하 / 좌우
### 오답노트
그래서 박스 안에 content 가운데 정렬하려면 `margin: 0 auto;` 하면 됨

1 - 공통

---

CSS는 border box가 아닌 **content box의 크기를 width로 설정**

`{box-sizing: content-box;}`

근데 편하게하려고 `{box-sizing: border-box}`로 변경함

---

###  Block 타입
하나의 독립된 덩어리처럼 동작. 웹 페이지의 큰 구조와 단락을 만듦. 다른 요소를 상자로부터 밀어낼 수 있음. width 속성을 지정하지 않으면 ✅ **inline 방향으로 사용가능한 공간을 모두 차지함** -> 줄바꿈이 일어남
- `div` : 다양한 섹션을 구조화하는데 많이 쓰임

그외에도 `h1~6`, `p`, `ul`, `li`

### Inline 타입 
문장 안의 단어처럼 흐름에 따라 자연스럽게 배치됨. 줄을 바꾸지않고 텍스트의 일부만 다른 스타일을 적용할 때 사용. ✅ **콘텐츠의 크기만큼만 영역을 차지, width와 height 속성을 사용 X.** padding, margin, border 적용되는데 상하 방향으로 다른 요소를 밀어내지는 못하지만 좌우로는 다른 요소를 밀어낼 수 있음
- `span` : `<span style="color: blue;">`

그외에도 `a`, `img`, `strong`

---

### Normal flow
강제로 속성이나 레이아웃을 바꾸지않았을 때 웹 페이지 요소가 배치되는 방식
가로 : Inline Direction, 세로 (엔터 눌러 문단을 나눔) : Block Direction

---

기타 display 속성
### inline-block 타입 
두 가지 특징을 모두가짐. 줄바꿈없이 크기 지정 가능. width height 속성 사용가능, 다른 요소가 상자로부터 밀려남
`display: inline-block;`

### none 타입
요소를 화면에 표시하지않고 공간조차 없음 !
`<div class="box none"></div>`

---

## CSS Position
- CSS Layout: 요소의 위치와 크기 조정. `display(block, inline, flex, grid, ...)`
- CSS Position: Normal Flow에서 제거하여 다른 위치로 배치. `position(static, relative, absolute, fixed, sticky, ...)`


Position 이동방향 : top, bottom, left, right, z axis (모니터로부터 수직방향)


Position 유형
1)  **static** : Normal Flow에 따라 배치
2)  **relative** : 자신의 원래 기준(static)을 기준으로 이동. 이동할 때 요소가 차지하는 공간은 static때랑 같음 (빈 공간에 다른 요소가 못들어가서 다른 요소의 레이아웃에 영향 X)
3) **absolute** : 요소를 Normal Flow에서 제거. 가장 가까운 relative 부모 요소를 기준으로 이동. 겹치기 가능
4) **fixed** : 요소를 Normal Flow에서 제거. 현재 화면영역(viewport) 기준으로 이동
5) **sticky** : 임계점에 도달하면 화면에 고정, 도달하기 전까지는 relative처럼 동작

### z-index
요소의 쌓임 순서를 정의
- ✅정수값으로 **값이 클수록 위에** 쌓이게됨
- static이 아닌 요소에만 적용되고 기본값이 auto이고 상속됨
- 같은 부모내에서 z-index가 같으면 HTML 문서 순서대로
- ✅ 자식의 z-index가 부모의 z-index보다 위로 올라갈 수 X

---

## CSS Flexbox
Inner Display 타입 -> 박스 *내부의 요소들*이 어떻게 배치될지
요소를 행과 열 행태로 배치하는 1차원 레이아웃 방식

- **main axis** : 기본 축, 가로
- **cross axis** : 세로
- **flex container** (부모 역할)
  - `display : flex` 하면 Flex Container로 지정 
  - `flex-direction: column`하면 세로 방향으로 나열됨
  - `flex-wrap: wrap`하면 한 행에 안들어갔을 때 다른 행에 배치
  - `justify-content` : 주축 여러 줄
  - `align-content` : 교차 축 여러 줄
  - `align-items` : 교차 축 1줄

### 오답노트
  박스 가운데정렬하려면 `display: flex;`하고 `justify-content: center;` `align-content: center;` 하면 됨 !

- **flex item** (자식 요소)
  - `align-self` : 교차 축 1줄
  - `flex-grow` : 남는 행 여백을 비율에 따라 각 flex item에 분배
  - `flex-basis` : flex-item의 초기 크기값
  - `order`

---

### CSS animation
JS를 사용하지 않고도 복잡한 움직임을 구현할 수 있게 해주는 CSS의 기능
- 시작부터 끝까지 애니메이션의 전반적인 규칙 정의
- animation-name
- animation-duration
- animation-timing-function (속도 변화 - 느리게, 시작/끝 등)