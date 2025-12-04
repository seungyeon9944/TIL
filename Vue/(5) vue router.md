### Routing
네트워크에서 경로를 선택하는 프로세스
- CSR에서 routing은 **클라이언트** 측(브라우저)에서 수행
- 클라이언트 측 자바스크립트가 새 데이터를 동적으로 가져와 전체 페이지를 다시 로드하지 않음
- SPA에서 Routing이 없다면
유저가 URL을 통한 페이지 변화 감지x, 페이지가 무엇을 렌더링 중인지 상태 x, 뒤로가기기능x

### Vue Router
SPA에서 페이지 이동 기능을 구현할 때 사용. `<router-link>`와 `<router-view>`라는 핵심 컴포넌트 제공

- 라우팅 기본 동작 순서
1. `index.js`에 **라우터 관련 설정** 작성
2. RouterLink에 **index에 정의한 주소 값** 작성 (ex. 'to' 속성으로 정의한 path 사용)
3. RouterLink 클릭 시 경로와 일치하는 컴포넌트가 **RouterView에서 렌더링**

- **Named Routes** : name 속성 값에 경로에 대한 이름 지정. 경로에 연결하려면 RouterLink에 **y-bind**를 사용해 'to' **props 객체**로 전달 가능
```
<RouterLink :to="{ name: 'home'}">Home</RouterLink>
<RouterLInk :to="{ name: 'about'}">About</RouterLink>
```

### Dynamic Route Matching
URL의 일부를 변수로 사용하여 경로를 동적으로 매칭. 패턴은 같지만 ID 값만 다른 여러 URL을 하나의 라우트 설정으로 처리 !
- views 폴더 내 UserView 컴포넌트 작성
- `router/index.js` 파일에 매개변수와 컴포넌트 라우터 등록
```
// index.js

const router = createRouter({
    routes : [
        {
            path: '/user/:id',
            name: 'user',
            component: UserView
        }
    ]
})
```
- 객체의 key 이름과 `index.js`에서 지정한 매개변수 이름이 같도록 UserView 컴포넌트로 이동하기 위한 RouterLInk 작성
```
<!-- App.vue -->

<RouterLink :to="{ name: 'user', params: {'id' :userId} }">User</RouterLink>
```
- 경로가 일치하면 라우트의 매개변수는 컴포넌트에서 `$route.params`로 참조 가능
- **userRoute()** 함수 사용하여 스크립트 내 반응형 변수에 할당 후 템플릿에 출력
```
<!-- UserView.vue -->

import { ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const userId = ref(route.params.id)

<template>
    <div>
        <h2>{{ userId }}번 User 페이지</h2>
    </div>
</template>
```

### Nested Routes
중첩된 라우팅
- **"children"** 옵션 사용하여 중첩된 라우터에 컴포넌트 등록
- 중첩된 Named Routes 다룰 때는 하위 경로에만 이름 지정
```
// index.js

{
    path: '/user/:id',
    component: UserView,
    children: [
        { path: '', name: 'user', component: UserProfile},
        { path: 'profile', name: 'userProfile', component: UserProfile},
        { path: 'posts', name: 'userPosts', component: UserPosts}
    ],
},
```

### Programmatic Navigation
`<RouterLink>`를 사용하는 대신, **JavaScript 코드를 사용**해 페이지를 이동시킴

router의 메서드
1. `router.push()`
- 다른 위치로 이동하기
- `<RouterLink :to="...">`

2. `router.replace()`
- 현재 위치 바꾸기
- push 메서드와 달리 history stack에 새로운 항목을 push하지 않고 다른 URL로 이동
- `<RouterLink :to="..." replace>`

---

### useRoute( )
- 현재 활성화된 "경로 정보(route)"를 담은 **route 객체** 반환
    - route 객체 : 현재 URL 상태를 보여주는 역할로 반응형이고 읽기 전용임
- 컴포넌트의 setup 함수나 `<script setup>` 최상단에서만 호출해야

### useRouter( )
- 라우터 인스턴스 router 객체를 반환
    - router 객체 : 애플리케이션 전체 라우팅 로직을 제어 + 페이지 이동이나 네이게이션 관련 메서드 제공 + **네이베이션 가드 등록**
- useRouter는 **페이지 이동** 등 액션용, useRoute는 경로 정보 읽기용으로 역할이 다름

---

### Navigation Guard
Vue router를 통해 특정 URL에 접근할 때 다른 URL로 redirect를 하거나 취소하여 내비게이션 보호
1. Globally (전역 가드)
- 애플리케이션 전역에서 동작, 작성위치 : **index.js**
- `beforeEach()`
- `beforeResolve()`
- `afterEach()`

2. Per-route (라우터 가드)
- 특정 route에서만 동작, 작성위치 : **index.js의 각 routes**
- `beforeEnter()`

3. In-component (컴포넌트 가드)
- 특저어 컴포넌트 내에서만 동작, 작성위치 : **각 컴포넌트의 script**
- `onBeforeRouteLeave()`
- `onBeforeRouteUpdate()`