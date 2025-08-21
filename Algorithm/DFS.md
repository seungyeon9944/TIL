# 깊이 우선 탐색 DFS (Depth First Search)
다음분기로 넘어가기 전에 해당 분기를 완벽하게 탐색 - **스택**이나 재귀함수 사용


    # 0. 인접 행렬이나 인접 리스트 만들기 (README 참고)

    # 1. 재방문 방지를 위한 방문 배열
    visited = [0 for _ in range(n+1)]

    # 2. 출발 지점과 끝 지점 기록
    start, goal = map(int, input().split())
    visited[start] = 1

    # 3. (덤) 진행 경로를 저장할 리스트
    route = []

    # 4. 스택을 만들기
    stack = [start]

    # stack이 비어있지않은 동안 반복
    while stack:
        # 1) 이번 방문 지점을 가져옴
        now = stack.pop()

        # 2) (덤) 방문 순서를 기록 (문제마다 달라지는 부분)
        route.append(now)

        # 3) 다음 방문 가능 점들을 넣어줌
        for next_node in adj_lst[now]:
            # 연결되어있고 방문한 적 없으면 stack에 넣어주고 방문표시
            if visited[next_node] == 0:
                stack.append(next_node)
                visited[next_node] = 1

    print(route)
    print(visited[goal])