# 그래프
아이템(사물 또는 추상적 개념)들과 이들 사이의 연결관계를 표현.  N:N 관계 (다:다 관계)를 가지는 원소들을 표현하기 용이
- |V|개의 정점을 가지는 그래프는 **최대 |E| = |V|*(|V|-1)/2 개의 간선**을 가질 수 있음

## **인접 행렬**
|V| * |V| 크기의 2차원 배열을 이용해서 간선 정보 저장, 두 정점을 연결하는 간선의 유무를 행렬로 표현 (0과 1로)
```
graph = [[0] * (V+1) for _ in range(V+1)]
for _ in range(E):
  start, end = map(int, input().split())
  graph[start][end] = 1 # 여기까지만 쓰면 단방향
  graph[end][start] = 1 # 여기까지 쓰면 양방향
````
## **인접 리스트**
각 정점마다 해당 정점과 인접한 정점 정보 저장 (연결 안된 정보는 다 버림 !)
```
graph = [[] * (V+1) for _ in range(V+1)]
for _ in range(E):
  start, end = map(int, input().split())
  graph[start].append(end) # 여기까지만 쓰면 단방향
  graph[end].append(start) # 여기까지 쓰면 양방향
```

## DFS (깊이 우선 탐색)
1 ) stack 2 ) 재귀호출 방식 (코테용으로 쓸것 !)

----

# Union-Find (Disjoint set)
- 트리에서는 루트 노드가 대표자가 됨 ! 
- 연산할 때에도 Union(d, f) 해도 각각의 대표자인 c와 e가 연산됨
- 그래프의 사이클 탐지 때 사용

```
def find_set(x):
  # 자신 == 부모 -> 해당 집합의 대표자
  if x == parents[x]:
    return x

  # x의 부모노드를 기준으로 다시 부모를 검색
  return find_set(parents[x])
```

**경로압축**하면 한번에 대표자 찾음 !
```
def find_set(x):
  # 자신 == 부모 -> 해당 집합의 대표자
  if x == parents[x]:
    return x

  # 경로압축 (path compression)
  parents[x] = find_set(parents[x])
  # x의 부모노드를 기준으로 다시 부모를 검색
  return find_set(parents[x])
```

---

# 최소 신장 트리 (MST, Mininum Spanning Tree)
신장 트리를 구성하는 **간선들의 가중치 합이 최소**인 신장 트리
`[(도착지점, 가중치)]` 형태로 적어줌

## 1 ) Prim 알고리즘
BFS처럼 접근 - **인접한 정점들** 중에 최소 비용의 간선이 존재하는 정점 선택.
가중치가 적은 노드를 먼저 꺼내니까 우선순위 .. heapq 사용
```
from heapq import heappush, heappop

V, E = map(int, input().split())
graph = [[0]* V for _ in range(V)] # 인접행렬

# 특정 정점 기준으로 시작
# 갈 수 있는 노드들 중 가중치가 가장 작은 노드부터 간다
# 작은 노드를 먼저 꺼내기위해 우선순위큐(heapq)를 활용
def prim(start_mode):
  pq = [(0, start_node)] # (가중치, 노드) 형태
  MST = [0] * V # visited와 동일
  min_weight = 0 # 최소 비용

  while pq:
    weight, node = heappop(pq) # 가장 작은 가중치

    # 이미 방문한 노드라면 continue
    if MST[node]:
      continue

    for next_node in range(V):
      # 갈 수 없으면 continue
      if graph[node][next_node] == 0:
        continue

      # 이미 방문했으면 continue
      if MST[next_node]:
        continue

      MST[node] = 1 # node로 가는 최소 비용이 선택되었다
      min_weight += weight # 누적합 추가

      heappush(pq, (graph[node][next_node], next_node))

  return min_weight

for _ in range(E):
  start, end, weight = map(int, input().split())
  graph[start][end] = weight
  graph[end][start] = weight # 양방향

result = prim(0) # 출발정점과 함께 시작
```

## 2 ) Kruskal 알고리즘
가중치 기준으로 **간선들을 정렬**하고 사이클 발생 시 선택 X <- 서로소 집합
```
def find_set(x):
  if x == parents[x]:
    return x

  # 경로 압축
  parents[x] = find_set(parents[x]) # 대표자가 return
  return parents[x]

def union(x, y):
  rx = find_set(x)
  ry = find_set(y)

  if rx == ry: # 사이클 발생
    return
  if rx < ry:
    parents[ry] = rx
  else:
    parents[rx] = ry

V, E = map(int, input().split())

# 1. 간선들을 가중치 기준으로 정렬
edges = []
for _ in range(E):
  start, end, weight = map(int, input().split())
  edges.append((start, end, weight))

# 가중치 기준 오름차순 정렬
edges.sort(key = lambda x: x[2])

# 2. 가중치가 작은 간선부터 순서대로 선택하자
# 사이클이 발생하면 고르지 말자 !
# 언제까지 ? MST가 완성될때까지 (= V-1개를 선택할 때까지)
cnt = 0 # 현재까지 선택한 간선의 수
result = 0 # 가중치의 합

parents = [i for i in range(V)] # make_set

for u, v, w in edges:
  # 사이클이 아니라면
  # 연결 (같은 집합으로 만든다)
  # cnt += 1
  # cnt가 V-1이라면 종료
  if find_set(u) != find_set(v):
    union(u, v)
    cnt += 1
    result += w

    if cnt == V-1:
      break
```
---

## 최단 경로
간선의 가중치가 있는 그래프에서 두 정점 사이의 경로들 중에서 간선의 가중치의 합이 최소인 경로

# 다익스트라 (dijkstra) 알고리즘
시작 정점에서 **누적거리가 최소**인 정점을 선택해 나가면서 최단 경로를 구하는 방식. 큐에서 꺼내는 순간 최단거리 확정.
```
from heapq import heappop, heappush

def dijkstra(start_node):
  pq = [(0, start_node)] # (누적거리, 노드번호)
  dists = [INF] * V # 각 정점까지의 최단거리를 저장할 리스트
  dists[start_node] = 0 # 시작노드 최단거리는 0

  while pq:
    dist, node = heappop(pq)

    # 이미 더 작은 값으로 온 적이 있으면 버린다
    if dists[node] < dist:
      continue

    for next_dist, next_node in graph[node]:
      # 다음 노드로 가기 위한 누적거리
      # 누적 거리 = 현재까지의 거리 + 다음 거리
      new_dist = dist + new_dist

      # 이미 크거나 같은 가중치로 온 적이 있다면 continue
      if dists[next_node] <= new_dist:
        continue

      # 누적거리, 새로운 노드를 pq에 저장 + dists에 갱신
      dists[next_node] = new_dist
      heappush(pq, (new_dist, next_node))
    
  return dists

INF = int(21e8) # 무한대를 가정 (문제의 최대) 

V, E = map(int, input().split())
start_node = 0 # 시작점
graph = [[] for _ in range(V)] # 인접 리스트로 구현

for _ in range(E):
  start, end, weight = map(int, input().split())
  graph[start].append((weight, end)) # [주의] 단방향
  
# 출발지로부터 모든 최단거리
result = dijkstra(0)

```