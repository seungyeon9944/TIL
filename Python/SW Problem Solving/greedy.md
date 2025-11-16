## 부분집합 (powerset)
어떤 집합의 **공집합**과 **자기자신**을 포함한 모든 부분 - 집합의 원소 개수가 n개일 경우 부분집합의 수는 2^n개이다.
1) 완전 탐색 방법 
2) Binary Counting
<< 이렇게 2가지로 부분 집합을 찾아낼 수 있음

### 1. 완전탐색
부분집합으로 표현하면

```
arr = ['O', 'X']
name = ['MIN', 'CO', 'TIM']
path = []

def recur(cnt):
  # 종료조건 (3명을 모두 고려)
  if cnt == 3:
    return

  # 재귀호출 파트
  # 1. 부분집합에 포함되는 경우 (0을 추가)
  path.append(arr[0])
  recur(cnt+1)
  path.pop()

  # 2. 포함되지 않는 경우 (X를 추가)
  path.append(arr[1])
  recur(cnt+1)
  path.pop()

recur(0) # 0명을 고려한 상태로 시작
```

사람 이름으로 표현하면 (더 자주 쓰는 코드)
```
name = ['MIN', 'CO', 'TIM']

# 두번째 선택에서는 'MIN'이라는 친구가 포함된 상태를 저장하면서
def recur(cnt, subset):
  if cnt == 3:
    print(*subset)
    return

  # 1. 부분집합에 포함시키는 경우
  recur(cnt + 1, subset + [name[cnt]])

  # 2. 포함시키지 않는 경우
  recur(cnt + 1, subset)

recur(0, [])
```

---

### 2. 바이너리 카운팅 (Binary Counting)
```
arr = [1,2,3,4]
n = len(arr)

# 검사하고자하는 비트를 오른쪽으로 하나씩 shift하면서 체크
def get_sub(tar):
  print(f'target={tar}', end=' / ')
  for i in range(len(arr)):
    if tar & 0x1:
      print(arr[i], end=' ')
    tar >>= 1

for target in range(1 << n):
  get_sub(target)
  print()
```

---
## 조합 (combination)
서로 다른 n개의 원소 중 r개를 **순서 없이** 골라낸 것

---
# 탐욕 알고리즘 (Greedy)
결정이 필요할 때 현재 기준으로 가장 좋아보이는 선택지로 결정 -> 이게 진짜 되나?? ..
1) **탐욕적 선택 조건 (Greedy Choice Property)** : 
각 단계의 최적해 선택이 이후 단계 선택에 영향 X. 즉 각 단계 규칙이 변경되면 X.

2) **최적 부분 구조 (Optimal Substructure)** :
각 단계의 최적해 선택을 합하면, 전체 문제의 해결책이 되어야함. -> 증명을 통해 해결 ..