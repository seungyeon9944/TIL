# 알고리즘 Algorithm
문제를 해결하기 위한 절차나 방법
의사코드(슈도코드) + 순서도
    1) 정확성 2) 작업량 3) 메모리사용량 4) 단순성 5) 최적성

## 알고리즘의 시간 복잡도(Time Complexity)
알고리즘의 작업량 표현, 실행되는 명령문 개수 계산
by 빅-오 표기법 (가장 큰 영향력을 주는 n에 대한 항만 표시, 계수는 생략)

        ex. O(3n+2) = O(3n) 최고차항 3n만 선택 = O(n)
        ex. O(2n^2 + 10n + 100) = O(n^2), O(4) = O(1)

---

# 배열 Array
일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조.
다수의 변수로는 하기 힘든 작업을 쉽게 할 수 있음


        arr = list()
        arr = []
        arr = [0] * 10  # 크기가 정해진 리스트
        arr = [1,2,3]

- 입력 받은 정수를 1차원배열에 저장

        N = int(input())
        arr = list(map(int, input().split()))

- 배열 원소의 합 계산

        s = 0
        for i in range(N):
            s += arr[i]

- 배열 원소의 최대값 찾기

        max_v = arr[0]  # 첫 원소를 최대로 가정
        for i in range(1,N):
            if max_v < arr[i]:
                max_v = arr[i]  # arr[i]가 더크면 max_v 갱신

- 배열 원소의 최댓값의 인덱스 찾기
        
        max_idx = 0
        for i in range(1,N):
            if arr[max_idx] < arr[i]: # 최대값이 여러개일때 마지막 인덱스를 찾으려면 부등호대신 '<='
                max_idx = i

- 찾는값이 배열에 있으면 인덱스, 없으면 -1을 idx에 넣기

        N, V = map(int, input().split())
        arr = list(map(int, input().split()))
        idx = -1  # 찾는 값이 없다고 가정
        for i in range(N):
            if arr[i] == V:
                idx = i
                break

---

# 정렬 Sort
2개 이상의 자료를 **키**에 의해 재배열하는 알고리즘

- **버블 정렬**
인접한 두개의 원소를 비교해서 자리 계속교환.
시간복잡도 : O(n^2)

        BubbleSort(a, N)
            for i : N-1 -> 1  # 정렬할 구간의 끝이 하나씩 줄어들음
                for j : 0 -> i-1 # 인접원소의 왼쪽 인덱스를 기준으로 삼아서 인덱스의 끝이 i-1
                    if a[j] > a[j+1]
                        a[j] <-> a[j+1]  # 교환
    슈도코드를 코드로 구현하면 아래와 같다

        def bubble_sort(a, N):
            for i in range(N-1, 0, -1):
                for j in range(i):
                    if a[j] > a[j+1]:
                        a[j], a[j+1] = a[j+1], a[j]

- **카운팅 정렬**
- 선택 정렬
- 퀵 정렬
- 삽입 정렬
- 병합 정렬