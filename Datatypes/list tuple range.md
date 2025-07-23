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


### 1. assignment 할당
`a_list = [1,2,3]`

`b_list = a_list`

이때 `b_list`의 결과는 `[1,2,3]`

---

### 2. shallow copy 얕은복사
`a_list = [1,2,3]`

`b_list = a_list[:]` slicing은 연산자여서 list에 있는 데이터를 갖고와서 넣어주는거라 a_list가 변화해도 변하지않음 (반영x )

`a_list[0] = 100 ` 새로운 데이터 주소를 가리키기 때문, 별도의 리스트가 됨

`print(b_list[0])` 의 결과는 `1`

---

## shallow copy problem 얕은복사의 문제점
`a_list = [
    [1,2],
    [3,4],
]`

`b_list = a_list[:]`


`a_list[0] = [5,6]`

`a_list[1][0] = 7`

`print(b_list[0])`의 결과는 `1,2`

`print(b_list[1][0])`의 결과는 `7`

![얕은복사의오류](https://github.com/seungyeon9944/TIL/issues/1#issue-3255305427)
