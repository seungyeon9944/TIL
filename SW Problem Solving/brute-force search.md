A형 : 완전 탐색에서 경우의 수를 줄여가면서 가지치기를 먼저 할 것 ! -> 그 이후에 규칙 찾기 (Greedy) -> 동적 계획법 (DP)

# 완전 탐색
## 반복과 재귀
- 반복 : 수행하는 작업이 완료될 때까지 계속 반복 (**반복문은 코드를 n번 반복시킬 수 있음**)
- 재귀 : 주어진 문제의 해를 구하기 위해 동일하면서 더 작은 문제의 해를 이용 (**n중 반복문과 같은 효과**) 
  - 재귀호출 개수 == 가지의 개수
  - 종료조건에 따라 깊이가 달라짐 (if `x==2 : return` 설정해놓으면 `KFC(x+1) KFC(x+1) KFC(x+1)` 이렇게 트리형태의 높이가 3)


## 순열
```
path = []
visited = [0]*(N+1) # 고를 수 있는 수만큼 만들어줌

def recur(cnt):
  if cnt == 3:
    print(*path)
    return

  for num in range(1,7):
    if used[num]:
      continue

    used[num] = 1
    path.append(num)
    recur(cnt+1)
    path.pop
    used[num] = 0

  recur(0)
```

## 완전탐색 (=Brute-Force, 부르트 포스 알고리즘)
모든 가능한 경우를 모두 시도를 해보아 정답을 찾아내는 알고리즘
