### 동기 (Synchronous)
하나의 작업이 완료된 후에 다음 작업이 실행되는 방식

### 비동기 (Asynchronous)
한 작업의 완료 여부를 기다리지 않고 **다른 작업을 동시에 수행할 수 있는 방식**
- 병렬적 수행
- 당장 처리완료 안되는 작업들은 백그라운드에서 실행, 빨리 완료되는 작업부터
- 장점 : 효율성 증가, 사용자 경험 향상
- 단점 : 코드의 복잡성 증가
```
const asyncTask = function (callBack) {
  setTimeout(() => {
    callBack('작업완료')
  }, 3000)
}
```

### Ajax (Asynchronous JavaScript and XML)
비동기적이 웹 애플리케이션 개발을 위한 기술
- **XMLHttpRequest** 기술 사용
- 현재는 더 가볍고 JavaScript에서 다루기 쉬운 JSON 형식 주로 사용
- 목적 : 비동기 통신 + 부분 업데이트 + 서버 부하 감소

### Axios
브라우저와 Node.js 환경에서 모두 사용할 수 있는, Promise 기반의 HTTP 클라이언트 라이브러리
- 브라우저를 위한 **XHR** 객체 생성
- 간편한 API를 제공하며, **Promise** 기반의 비동기 요청 처리

Ajax를 활용한 클라이언트 서버 간 동작 :

**XHR 객체 생성 및 요청 -> 응답 데이터 생성 -> JSON 데이터 응답 -> Promise 객체를 활용해 DOM 조작**

### 비동기 콜백
연쇄적으로 발생하는 비동기 작업을 순차적으로 동작할 수 있게 함
```
const asyncTask = function (callback) {
  setTimeout(function () {
    console.log('비동기 작업 완료')
    callback() // 작업 완료 후 콜백 호출
  }, 2000) // 1초 후에 작업 완료
}

// 비동기 작업 수행 후 콜백 실행
asyncTask(function () {
  console.log('작업 완료 후 콜백 실행')
})
```

### Promise
- 콜백 지옥 문제 해결. 
- Promise 기반의 HTTP 클라이언트 라이브러리가 바로 Axios
- then 메서드를 통해 여러 비동기 작업을 연결하는 **체이닝 (Chaining)** 하여 순차적으로 연결
```
axios({}) // Promise 객체 return
  .then (성공하면 수행할 1번 콜백함수)
  .then (1번 콜백함수가 성공하면 수행할 2번 콜백함수)
  .then (2번 콜백함수가 성공하면 수행할 3번 콜백함수)
  ...
  .catch (실패하면 수행할 콜백함수)
```