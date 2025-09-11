## 백트래킹
여러 가지 선택지들이 존재하는 상황에서 한 가지 선택, 선택하면 새로운 선택지들의 집합이 생성되는 이 선택이 반복됨.

**Pruning(가지치기)** - 경로가 해결책으로 이어질 것 같지 않으면 더 이상 경로를 따라가지 않음으로서 시도의 횟수를 줄여 불필요한 경로 조기에 차단

```
def check(row, col):
  # 1. 같은 열에 놓은 적이 있는가 ?
  for i in range(row):
    if visited[i][col]:
      return False

  # 2. 좌상단 대각선에 놓은 적이 있는가 ?
  i, j = row-1, col-1
  while i >= 0 and j >= 0:
    if visited[i][j]:
      return False

    i -= 1
    j -= 1

  # 3. 우상단 대각선에 놓은 적이 있는가 ?
  i, j = row-1, col+1
  while i >= 0 and j < N:
    if visited[i][j] :
      return False

    i -= 1
    j += 1

def recur(now):
  global answer
  if row == N:
    answer += 1
    return

  for col in range(N):
    # 가지치기 : 같은 열을 못 고르도록
    # --> 유망하지 않은 케이스를 모두 삭제 (세로, 대각선)
    visited[row] = col # 현재 row의 col에 놓았다 라고 가정하고
    if not check(row): # 세로와 대각선을 체크해준다
      continue
    
    # col을 선택했다
    visited[col] = 1
    recur(row+1)
    visited[col] = 0

N = 4
answer 0
visited = [[0] * N for _ in range(N)]
recur(0)
```

## 트리
*(( 연결 리스트 코드 ))*

### 이진탐색트리 삭제
i. 자식이 하나인 경우 : 자식을 부모와 연결시켜줌

ii. 자식이 둘인 경우 : 왼쪽에서 가장 큰 수를 넣거나, 오른쪽에서 가장 작은 수를 넣어줌

### 이진탐색트리의 성능
- 탐색, 삽입, 삭제 시간은 트리의 높이만큼 시간이 걸림. `O(h), h` : BST의 깊이 (height)
- 평균의 경우 : 균형적으로 생성되어있음. `O(log n)`
- 최악의 경우 : 한쪽으로 치우친 경사 이진트리. `O(n)`

---

## 힙
**최대 힙** (부모노드의 키 값 > 자식 노드의 키 값)과 **최소 힙** 
(부모노드의 키 값 < 자식 노드의 키 값)

1) 가장 앞 데이터만 쓴다 (큐 !)
2) max or min이면 .. 우선순위 !
3) 우리가 찾는 건 루트 노드

힙은 완전 이진 트리 형태여야함. 그리고 규칙이 있음. 시간복잡도 : `O(n log n)` 만에 삽입, 삭제 가능해서 sort 대신 사용 !
그리고 `import heapq` 사용해서
```
min_heap = []
for num in arr:
  heapq.heappush(min_heap, num)
print(min_heap)
```

```
max_heap = []
for num in arr:
  heapq.heappush(max_heap, -min)

while max_heap:
  pop_num = heapq.heappop(max_heap)
  print(-pop_num, end = ' ')
```