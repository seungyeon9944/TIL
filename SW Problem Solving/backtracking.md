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
    # 가지치기 : 같은 열ㅇ르 못 고르도록
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

