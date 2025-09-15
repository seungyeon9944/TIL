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