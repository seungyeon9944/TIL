# 너비 우선 탐색 BFS (Breadth First Search)
탐색 시작점의 **인접한 정점을 모두 차례로 방문한 후**에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문 -> 선입선출 형태의 **큐** 활용

    def bfs(G, v):
        # n은 정점의 개수
        visited = [0]*(n+1)
        queue = []
        # 탐색 시작점 v를 큐에 삽입
        queue.append(v)

        # 큐가 비어있지않은 경우
        while queue :
            # 큐의 첫번째 원소 반환
            t = queue.pop(0)

            # 방문하지않았던 곳이라면
            if not visited[t] :
                # 방문한 것으로 표시하고 방문
                visited[t] = True
                visit(t)

                # t와 연결된 모든 정점에 대해
                for i in G[t] :
                    # 방문하지않았던 곳이라면
                    if not visited[i]:
                        # 큐에 넣기
                        queue.append(i)

---

    # 0. 인접 행렬이나 인접 리스트 인접 만들기 (README 참고)
    
    # 1. 재방문 방지를 위한 방문 배열
    visited = [0 for _ in range(n+1)]

    # 2. 출발 지점과 끝 지점 기록
    start, goal = map(int, input().split())
    visited[start] = 1

    # 3. (덤) 진행 경로를 저장할 리스트
    route = []

    # 4. 큐 만들기
    queue = [start]

    # queue가 비어있지않은 동안 반복
    while queue:
        # 1) 이번 방문 지점을 가져옴
        now = queue.pop(0)

        # 2) (덤) 방문 순서를 기록 (문제마다 달라지는 부분)
        route.append(now)

        # 3) 다음 방문 가능 점들을 넣어줌
        for next_node in adj_lst[now]:
            # 연결되어있고 방문한 적 없으면 stack에 넣어주고 방문표시
            if visited[next_node] == 0:
                queue.append(next_node)
                visited[next_node] = 1

    print(route)
    print(visited[goal])

        