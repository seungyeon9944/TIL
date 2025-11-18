## Bootstrap Grid System
웹 페이지의 **레이아웃**을 조정하는 데 사용되는 **12개의 컬럼**으로 구성된 시스템

↓

반응형 웹 디자인 Responsive Web Design

---

# Grid System
- **Container**

- **Column** : 실제 컨텐츠를 포함하는 부분
  (4 4 4 또는 2 8 2 이렇게해서 비율 일정하게)

- **Gutter** : 컬럼과 컬럼 사이의 여백 영역

  -> **x축은 padding**으로 여백 생성
`<div class="row gx-0">` 이렇게

  -> **y축은 margin**으로 여백 생성
`<div class="row gy-5">` 이렇게

- **row** : 1개의 row 안에 12개의 column 영역이 구성
```
<div class="container">
  <div class="row">
    <div class="col-4"></div>
    <div class="col-4"></div>
    <div class="col-4"></div>
  </div>
<div>
```

- **중첩** (Nesting)
하나의 column에 또다른 row를 넣게되면 8개의 column이 다시 12개로 분리됨
```
<div class="col-8 box">
  <div class="row">

    <div class="col-6">
      <div class="box">col-6</div>
    </div>

    <div class="col-6">
      <div class="box">col-6</div>
    </div>

    <div class="col-6">
      <div class="box">col-6</div>
    </div>

    <div class="col-6">
      <div class="box">col-6</div>
    </div>

  </div>
<div>
```

- **상쇄** (Offset)
```
<div class="container">
  <div class="row">
    <div class="col-4">
      <div class="box">col-4</div>
    </div>
    <div class-"col-4 offset-4">
      <div class="box">col-4 offset-4</div>
  </div>
<div>
```
---

## 반응형 웹 디자인 Responsive Web Design
디바이스 **종류에 관계없이 일관된** 레이아웃 및 사용자 경험을 제공

12개의 column과 **6개의 breakpoints**를 사용하여 구현.
각 breakpoints마다 설정한 최대 너비 값 "이상으로" 화면이 커지면 grid system 동작이 변경됨
- xs: `.col-`
- sm : `.col-sm-`
- md : `.col-md-`
- lg : `.col-lg-`
- xl : `.col-xl-`
- xxl : `.col-xxl-`

---

### UX (User Experience)
제품이나 서비스를 사용하는 사람들이 느끼는 전체적인 경험과 만족도를 개선하고 최적화하기 위한 디자인과 개발 분야

### UI (User Interface)
서비스와 사용자 간의 상호작용을 가능하게 하는 디자인 요소들을 개발하고 구현하는 분야
