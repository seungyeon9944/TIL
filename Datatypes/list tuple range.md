# Sequence 
시퀀스, 여러 데이터가 정해진 순서대로 일렬로 늘어선 자료 구조

**Types** : 여러 개의 값들을 순서대로 나열하여 저장하는 자료형. 


모든 칸에는 0번부터 시작하는 고유한 번호(인덱스)가 붙어 있음
공통 특징 : 
1) 순서(Order) 
2) 인덱싱(Indexing) 
3) 슬라이싱(Slicing) 
4) 길이(Length) 
5) 반복(Iteration)

### 오답노트
- 0이 250000개 있는 리스트 만들기 

ex. `many_zero_list = '0'*250000`

- **얕은복사의 오류**

`import copy`
`backup_catalog = copy.deepcopy(catalog)`
하면 backup_catalog은 catalog가 변해도 변하지않음
