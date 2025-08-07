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
2개 이상의 자료를 **키**(특정 기준)에 의해 재배열하는 알고리즘
sorted(list, key = 키) 이런식으로

## **버블 정렬** ⭐️⭐️⭐️
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

    좀 더 자세히 풀어쓰면,

        nums = [55,7,78,12,42]
        n = 5

        # 한번의 패스를 구현해보자
        # n개의 데이터가 있을 때 두개씩 찍지어 비교하자면
        # 총 n-1번 비교를 하게 된다
        # n-1번 반복하는 반복문을 만들어 보자.

        for i in range(n-1):

            # i = 0 ~ (n-2)까지 순회
            # 만약 i번째 숫자와 i+1번재 숫자를 비교했을 때
            # i번째 숫자가 i+1번째 숫자보다 클 경우 교환
            if nums[i] > nums[i+1]:

                # 둘의 위치를 바꾼다
                nums[i], nums[i+1] = nums[i+1], nums[i]

        # 이제 nums의 마지막 원소는 무엇일까?
        print(nums[-1]) # 78

        # 두번째 패스는 n-1개의 데이터를 갖고 두개씩 짝지어 비교해본다면 총 n-2번 비교를 하게된다

        for i in range(n-2):
            if nums[i] > nums[i+1]:
                nums[i], nums[i+1] = nums[i+1], nums[i]

        # 이런 식으로 range안의 범위를 바꿔주는것 !

        # 결론
        # i가 0부터 커지기 때문에, n-1-i를 해주면 패스마다 반복횟수가 줄어든다
        for i in range(n-1):
            for j in range(n-1-i):
                if nums[j] > nums[j+1]:
                    nums[j], nums[j+1] = nums[j+1], nums[j]

        # 함수로 나타내면
        def bubble_sort(data):
            n = len(data)
            for i in range(n-1):
                for j in range(n-1-i):
                if nums[j] > nums[j+1]:
                    nums[j], nums[j+1] = nums[j+1], nums[j]

---

## **카운팅 정렬**
항목의 순서 결정 위해 집합에 *각 항목이 몇 개씩 있는지* 세는 작업, 누적합을 이용해서 어느정도 정렬을 해준 뒤 값을 인덱스로 바꾸어 새 정렬리스트를 짜는 방식.


**정수**나 정수를 표현할 수 있는 자료만 가능 + 공간 할당을 위해 집합 내의 가장 큰 정수를 알아야됨 !시간복잡도 : O(n+k)

- `COUNTS[0] = 0`의 발생횟수(1번) = 1이 저장되는 COUNTS배열
- `COUNTS[i] = COUNTS[i-1]+COUNTS[i]`이용해서 누적합

        def counting_sort(DATA, TEMP, k):
            COUNTS = [0] * (k+1)
            for i in range(len(DATA)):
                COUNTS[DATA[i]] += 1
            for i in range(1,k+1):
                COUNTS[i] += COUNTS[i-1]

            # 마지막으로 등장한 다음 칸이 기록이 되어있으므로 
            # COUNTS에서 1을 빼주고, 빼준 값의 COUNTS값에 해당하는 TEMP에 해당 COUNTS의 인덱스를 넣어줌
            for i in range(len(DATA)-1, -1, -1):
                COUNTS[DATA[i]] -= 1
                TEMP[COUNTS[DATA[i]]] = DATA[i]


ex. `DATA = [4, 7, 9, 3, 5, 2, 3, 4]`일 때

| index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |9|
|----|----|----|----|----|----|----|----|----|---|---|
|DATA|4|7|9|3|5|2|3|4|
|COUNT|0|0|1|2|2|1|0|1|0|1
|누적합|0|0|1|3|5|6|6|7|6|8|
|최종|2|3|3|4|4|5|7|9|

- 4 -> 5 -> 4
- 7 -> 7 -> 6
- 9 -> 8 -> 7
- 3 -> 3 -> 2
- 5 -> 6 -> 5
- 2 -> 1 -> 0
- 3 -> 3 -> 2인데 중복 -> 1
- 4 -> 5 -> 4인데 중복 -> 3

---

## **선택 정렬**
리스트의 최솟값을 찾아 리스트의 맨 앞에 위치한 값과 교환

    def selection_sort(a,N):
        for i in range(N-1):
            min_idx = i
            for j in range(i+1, N):
                if a[min_idx] > a[j]:
                    min_idx = j
            a[i], a[min_idx] = a[min_idx], a[i]
---

그밖에도 ..
- 퀵 정렬 (O(nlogn)으로 빠름)
- 삽입 정렬
- 병합 정렬 (O(nlogn)으로 빠름)


---


## 완전검색
문제의 해법으로 생각할 수 있는 모든 경우의 수 나열, 확인
ex. Baby-gin 접근, 순열 nPr

---

## 탐욕 알고리즘
여러 경우 중 하나를 선택할 때 최적이라고 생각하는 것을 선택해 최적화.
1. 해 선택 2. 실행 가능성 검사 3. 해 검사


---

## 2차원 배열
        
        N = int(input)
        arr = [list(map(int, input().split())) for _ in range(N)]


### 배열 순회
i행의 좌표, j열의 좌표일 때

        for i in range(n):
            for j in range(m):
                f(array[i][j])

### 지그재그 순회
i행의 좌표, j열의 좌표일 때

        for i in range(n):
            for j in range(m):
                f(array[i][j + (m-1-2*j) * (i%2)])

## 델타를 활용한 2차원 배열 탐색 ⭐️
기준좌표의 인덱스가 `(i,j)` 일 때

|  | 좌 | 우 | 위 | 아래 |
|----|----|----|----|----|
| di | 0 | 0 | -1 | 1 |
| dj | -1 | 1 | 0 | 0 |

리스트 형태로 정리하면

    행 di[] <- [0,1,0,-1]
    열 dj[] <- [1,0,-1,0]

    for i in range(N): 
        for j in range(N):
            for d in range(4):

                # ni <- i + di[d]이고 nj <- j + dj[d]이기 때문에
                for di, dj in [[0,1],[1,0],[0,-1],[-1,0]]:
                    ni, nj = i+di, j+dj

                    # 유효한 인덱스인지 확인
                    if 0<= ni <N and 0<= nj <N :
                        f(arr[ni][nj])


---

## 부분집합 합 (멱집합)

    bit = [0,0,0]
    for i in range(2):
        bit[0] = i
        for j in range(2):
            bit[1] = j
            for k in range(2):
                bit[2] = k
                print_subset(bit)

- **비트연산자** 
    - `&` : 비트 단위로 AND
    - `|` : 비트 단위로 OR
    - `>>` : 피연산자의 비트 열을 오른쪽으로.
    - `<<` : 피연산자의 비트 열을 왼쪽으로 이동
    `1 << n : 2^n`는 원소가 n개인 경우 모든 부분집합의 수,
    `i & (1<<j)`하면 i의 j번째 비트가 1인지 아닌지 검사

## 비트연산자를 이용한 부분집합

    arr = [1,2,3]
    n = len(arr)

    # n개의 원소를 가진 집합의 부분집합의 수만큼 반복한다
    # 그걸 비트로 표현하면 000부터 111까지 표현이 된다
    for i in range(1 << n):

        # j번째 원소를 포함할지 말지를 결정하는 반복문
        for j in range(n):

            # 1 << j는 1을 j칸 움직인다
            # 0001, 0010, 0100, 1000
            # 이 숫자와 i의 비트가 겹치는지 판단한다
            if i & (1 << j):

                # j번째 자리가 1이었는지 아닌지를 말하는것이 된다.
                # j번째 원소를 포함시키자.
                print(arr[j], end =", ")

        # n번째 반복이 끝나면 하나의 부분집합이 완성된다.
        print()

    # 멱집합 완성 !
    print()

---

## 순차검색
- 정렬되어있지않은 경우

        for i in range(n):
            if key == arr[i]:
                return i
            else:
                return -1

- 정렬되어있는 경우
검색 실패를 반환하는 경우에도 평균 비교 회수가 반으로 줄어듬. (n+1)/2

---

## 이진검색
자료가 **정렬된 상태**에서 사용
ex. 9을 찾는다고할 때, 1 3 5 7 9 11 13 -> 9 11 13 -> 9 

    def binarySearch(a, N, key):
        start = 0
        end = N -1
        while start <= end :
            middle = (start + end)//2
            if a[middle] == key:
                return middle
            elif a[middle] > key:
                end = middle - 1
            else:
                start = middle + 1
        return -1
---

+) 셀렉션 알고리즘 ..           