### **MLP**
**MLP (Multi-Layer Perceptron)**, 즉 **다층 퍼셉트론**은 가장 기본적인 형태의 심층 신경망(Deep Neural Network)입니다. 이는 인공 신경망(Artificial Neural Network, ANN)의 한 종류로, **입력층(Input Layer)** 과 **출력층(Output Layer)** 사이에 **하나 이상의 은닉층(Hidden Layer)**을 가진 구조를 의미합니다.

- 추세선 y = ax + b에서 a, b를 어떻게 설정하는지 설명하시오.
  
  **MSE가 최소**가 되도록 하는 a, b를 찾는다. 최소제곱법 사용

- 경사하강법을 설명하시오.
  
  경사하강법이란 함수의 최솟값을 찾기 위해, **현재 위치의 기울기(경사)를 계산**하고 그 **반대 방향으로 이동**하는 것을 반복하는 최적화 알고리즘이다.

- 확률적 경사하강법을 설명하시오.
  
  확률적 경사하강법이란 전체 데이터 대신 **훈련 데이터 중 무작위로 하나의 샘플을 선택해** **가중치를 업데이트**하는 최적화 알고리즘이다.

- 비선형 MLP에서 곡선도 모사하는 방법을 설명하시오.

  y = ax + b 꼴의 **선형 함수의 중첩과 ReLU라는 활성화 함수**를 이용하면, 모사할 수 있다.

- MLP의 은닉층에서는 활성화 함수가 중요한 이유는 무엇인가? 
  
  은닉층에서 활성화 함수는 **비선형성**을 추가하여, 신경망이 복잡한 함수(비선형적 관계, 고차원 분포)를 학습할 수 있게 한다.

*✏️ 오답노트 : MLP의 학습 루프 순서*
```
# 학습 루프
for epoch in range(2000): 
    y_hat = model(X) # 모델 예측
    loss = criterion(y_hat, y) # 로스 계산

    optimizer.zero_grad() # 미분 계산 초기화 (미분 Ready)
    loss.backward() # 미분 계산 수행
    optimizer.step() # GD 점프 1회 (w, b 값이 업데이트 됩니다.)

    if epoch % 400 == 0:
        print(f"Epoch {epoch:4d} | Loss: {loss.item():.4f}")
```
    
---

### **데이터 생성 방법**
- 데이터 증강하는 방법 : 회전, 축소, 좌우 반전. 텍스트의 경우는 단어 치환, 삭제, 순서 섞기
- 데이터 증강이 필요한 이유 : 학습 **데이터가 적거나 불균형할 때, 과적합(overfitting) 방지**가 필요할 때.

---

### **토큰화와 임베딩**
- 토큰화와 임베딩에 대해 설명하시오.
  
토큰화란 텍스트를 각 의미 있는 단위, 즉 **토큰 단위로 글자를 자르는 것**을 의미하고,
임베딩이란 벡터 공간에서 **각각의 단어에 벡터값을 부여**하는 것을 의미한다.

- RAG 동작 원리에 대해 설명하시오. :

RAG란 Retrieval-Augmented Generation의 약자로, 검색을 통해 LLM의 한계를 보완하는 기술입니다. 

1. 외부 **데이터 생성** 단계에서 방대한 문서를 **청킹**하여 작은 단위로 나눔
2. 이렇게 청킹된 텍스트 청크들은 **임베딩 모델**을 거쳐 벡터로 **변환**
3. 벡터는 **Vector DB에 저장**
4. 사용자가 질문을 담은 **프롬프트를 입력**
5. 해당 질문이 **임베딩**되어 Vector DB의 **벡터들과 유사도 검색**
6. 검색 결과로 나온 문서가 원래 사용자 질문과 함께 **최종 프롬프트에 포함**, LLM에 전달
7. **LLM**이 답변 **생성**

---

### **EDA**
- 데이터셋에 포함된 총 샘플 수 구하기
```sql
sample_count = df.shape[0]
print('샘플 수: ', sample_count)
df.info() #null 값 및 정보
```

- 특성 수 구하기
```sql
feature_count = df.shape[1]
print('특성 수: ', feature_count)
```

---

### **선형 회귀**
```sql
# 모델 예시 (선형 회귀 모델)

# reg plot은 추세선을 그려주는 기능
# x="total_bill", y="tip" 이부분 외우기

sns.regplot(x="total_bill", y="tip", data=tips, ci=None, line_kws={"color": "red"})
print()
```

---

### **Linear Probing**
- 사전학습된 모델의 **가중치**(weight)을 **고정**하고, 단지 마지막 linear 계층만 학습 (FC Layer처럼 !)
- 반대되는 개념으로 **Fine-tuning:** 사전학습된 모든(또는 일부) 계층의 weight를 **전체 재학습**(gradient update)

```sql
# [핵심코드 1] 모든 파라미터 autograd off
for param in model.parameters():
param.requires_grad = False

# [핵심코드 2] 마지막 FC 변경 (새로 생성)
model.fc = nn.Linear(512, 2) # 입력 512개, 출력 2개, 이 부분만 autograd on
model = [model.to](http://model.to/)(device)
print('완료')
```