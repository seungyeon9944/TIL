## Bootstrap Grid System
웹 페이지의 **레이아웃**을 조정하는 데 사용되는 **12개의 컬럼**으로 구성된 시스템

↓
## 반응형 웹 디자인 Responsive Web Design
디바이스 **종류에 관계없이 일관된** 레이아웃 및 사용자 경험을 제공

---

# Grid System
- Container
- Column : 실제 컨텐츠를 포함하는 부분
  (4 4 4 또는 2 8 2 이렇게해서 비율 일정하게)
- Gutter : 컬럼과 컬럼 사이의 여백 영역
- row : 1개의 row 안에 12개의 column 영역이 구성
```
<div class="container">
  <div class="row">
    <div class="col-4"></div>
    <div class="col-4"></div>
    <div class="col-4"></div>
  </div>
<div>
```

- 중첩 (Nesting)
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

- 상쇄 (Offset)
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
