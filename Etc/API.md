## ChatGPT의 3가지 특징
### 1. Generative AI
생성형 AI (새로운 콘텐츠 생성하는 인공지능 모델) 
ChatGPT는 GPT(**G**enerative **P**re-trained **T**ransformer) 모델을 기반으로 한 대화형 AI .. 앵무새

### 2. Pre-trained
**LLM**, Large Language Model : pre-trained되고 fine-tuning된 모델

### 3. Transformer 
Neural Network Architecture, 문장의 맥락을 효과적으로 이해하고 처리
GPT 모델은 특히 Transformer의 **디코더** 부분만을 사용

- **Self-Attention 메커니즘**
입력 데이터 간의 관계와 중요도를 계산
- **병렬 처리 가능**
RNN과 달리 순차 처리가 필요 없어 속도가 빠름
- **스케일링 가능**
대규모 데이터 및 파라미터로 확장 가능


---


참고_ **Attention 메커니즘**
입력 데이터의 각 요소가 출력에 얼마나 중요한지 **중요도(weight)**를 계산하는 기법
반대 개념으로는 Multi-Head Attention (다양한 관심사 즉 관점을 병렬로 계산하여 성능 향상)이 있음


---


## API
API (Application Programming Interface) 
두 소프트웨어 (또는 시스템)가 서로 통신할 수 있게 하는 메커니즘
즉 **약속된 방식의 인터페이스**


**Interface** : 시스템이 정보를 교환할 때 그 사이에 존재하는 접점. 
- ex. 키보드, 리모컨, 터치스크린
**User Interface, UI** : API는 응용소프트웨어를 만드는 데 사용되는 인터페이스다


웹의 동작 방식 : **클라이언트 - 서버 구조** 
- 클라이언트: 서비스 요청
- 서버: 요청 받아서 처리하고 결과 응답


## API Key
API에게 요청을 보내는 애플리케이션을 구별하기 위한 고유한 식별 문자열
for 보안 강화 + 데이터관리


**토큰** : 텍스트 데이터를 처리하고 이해하는 기본 단위
- 영어 문장 < 한글 문장 표현
- 각 LLM 모델마다 **최애 입력 토큰 제한**


### OPEN AI 주요 파라미터
- 필수 파라미터
    **model** : GPT 모델 이름
    **messages** : 대화 메시지 기록
- 응답 다양성 제어
    **temperature** : 다음 토큰(단어) 예측 다양성을 통해 응답의 **창의성**과 **다양성** 조정
    높을수록 확률 분포가 평탄해져 다양한 단어가 선택될 가능성 증가
    **top_p** : 선택할 토큰의 확률 범위를 제한 (0~1)해 응답의 범위 제한
    1.0일 경우 모든 단어를후보로 포함


---


## 요약
1. OpenAI **클라이언트를 초기화**하고 **API 키로 인증**
2. 대화의 기본 지침(시스템)과 사용자 질문을 **conversation_history에 추가**
3. OpenAI **API에 conversation_history를 전달**하여 **응답 생성**
4. 생성된 응답 **출력**