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

        def bfs(G, v, n):
            visited = [0]*(n+1)
            queue = []
            queue.append(v)
            # 인큐와 동시에 방문 예정
            visited[v] = 1

            while queue :
                t = queue.pop(0)
                visit(t)
                for i in G[t] :
                    if not visited[i]:
                        queue.append(i)
                        # 거리 정보 (간선 수 확인을 위한)
                        visited[i] = visited[t] + 1