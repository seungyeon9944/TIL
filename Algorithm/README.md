# DFS와 BFS
| DFS (깊이우선탐색) | BFS (너비우선탐색) |
| ------------ | ------------ |
| 다음분기로 넘어가기 전에 해당 분기를 완벽하게 탐색 | 루트 노드에서 시작해서 인접한 노드를 먼저 탐색 |
| **스택** 또는 재귀함수 | **큐** |
| 경로의 특징을 저장해야 할 때 | 두 노드 사이의 최단 경로 구할 때 |
| 검색 대상 그래프가 짱크다면 | 검색대상 규모가 크지 않다면 |

### 백트래킹 Backtracking
더이상 해가 될 수 없다고 판단하면 되돌아가서(backtrack) 다른 경로를 시도 - 최적화문제와 결정문제에 적용 

(ex. N-Queens 문제, 미로 찾기, 순열/조합 생성, 부분집합 탐색 등). 

DFS와 비슷하나 Prunning(가지치기)하고 조기 경로 차단. node가 유망한가 점검하고 유망하지 않으면 해당 node의 부모 node로 돌아감

---

### 인접 행렬

    # 2차원 배열(arr)을 만들고
    # arr[i][j]가 True라면 i->j로 통하는 길이 있음을 나타내도록
    # 값을 채움

    # 1. 일단 전체 배열을 만듬
    # n개의 점이 있다면 최소 n*n의 2차원 배열이 필요
    adj_mat = [
        [0] * (n+1) for _ in range(n+1)
    ]

    # 2. 각 간선을 살펴보면서, adj_mat을 채움
    for edge in edges:
        # edge[0]에서 edge[1]까지는 길이 존재함을 의미하므로
        adj_mat[edge[0]][edge[1]] = 1

        # 양방향이라면
        # edge[1]에서 edge[01]까지의 길도 존재한다는 뜻
        adj_mat[edge[1]][edge[0]] = 1 추가해주기

    for row in adj_mat:
        print(row)

### 인접 리스트

    # 2차원 배열을 만들고
    # arr[i]에 리스트(또는 다른자료형)을 할당한 다음,
    # i에 저장된 리스트에 연결된 정점들을 넣어줌

    # 1. 각 i와 연결된 점들 보관을 위한 리스트만 만듬
    adj_lst = [
        [] for _ in range(n+1)
    ]

    # 2. 각 간선을 살펴보면서 adj_list 갱신
    for edge in edges:
        # edge[0]에서 edge[1]이 도달 가능함을 의미함으로
        adj_lst[edge[0]].append(edge[1])

    for row in adj_lst:
        print(row)

---

### 오답노트
그래프 탐색할 때 방문할 수 있는 정점이 여러 개여서 정점 번호가 작은 것 ! 을 먼저 방문하려면
- DFS는 **stack**이어서 LIFO니까 내림차순으로 정리
`for next_node in sorted(adj_list[now], reverse=True):`
- BFS는 **queue**여서 FIFO니까 오름차순으로 정리
`for next_node in sorted(adj_list[now]):`
