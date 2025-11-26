### Client-side frameworks
클라이언트 측에서 UI와 상호작용을 개발하기 위해 사용되는 JavaScript 기반 프레임워크. ex) Vue, React, Angular
- 동적이고 반응적인 **웹 애플리케이션(web applications)** 개발
- 코드 재사용성 증가
- 개발 생산성 향상

### Single Page Application (SPA)
단일 페이지에서 동작하는 웹 애플리케이션

작동 원리
1. 최초 로드 시, 어플리케이션에 필요한 주요 **리소스 다운로드**
2. 페이지 갱신에 **필요한 데이터만**을 비동기적으로 전달받아 화면의 필요한 부분만 **동적으로 갱신**
3. JavaScript을 사용하여 **클라이언트 측**에서 동적으로 콘텐츠를 생성하고 업데이트 (**CSR 방식**)

### Client Side Rendering (CSR)
클라이언트 측에서 콘텐츠를 렌더링하는 방식

작동 원리
1. 사용자가 웹사이트에 요청을 보냄
2. 서버는 최소한의 HTML과 JavaScript 파일을 클라이언트에 전송
3. 클라이언트는 HTML과 JavaScript를 다운받음
4. 브라우저가 JavaScript를 실행하여 동적으로 콘텐츠 생성
5. 필요한 데이터는 API를 통해 서버로부터 비동기적으로 가져옴

CSR과 SPA의 장점
- 빠른 페이지 전환
- 사용자 경험
- Frontend와 Backend의 명확한 분리

CSR과 SPA의 단점
- 느린 초기 로드 속도
- SEO (검색 엔진 최적화) 문제

---

### Vue
사용자 인터페이스를 구축하기 위한 JavaScript 프레임워크
- 반응성이 가장 큰 특징
- 컴포넌트 기반 아키텍처
- 간결한 문법과 직관적인 API
- 유연한 스케일링