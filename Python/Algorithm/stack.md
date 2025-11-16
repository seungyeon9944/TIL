# 스택
자료를 쌓아 올린 형태의 선형 자료구조

## 후입선출 (LIFO)
Last-In-First-Out 가장 마지막에 넣은 자료가 가장 먼저 나오는 것. 1 - 2 - 3 차례대로 넣으면 3 - 2 - 1 순서로 나옴

스택의 연산
- **Push** 삽입 (자료 저장)

        def my_push(item):
            s.append(item)

        size = 10
        stack = [0] * size
        top = -1

        my_push(10, size)
        top += 1
        stack[top] = 20

- **Pop** 삭제 (삽입자료의 역순으로 꺼냄)
    `return s.pop()` 이런 식으로

        def my_pop():
            global top
            if top == -1:
                print('underflow')
                return 0
            else:
                top -= 1
                return stack[top+1]
        print(pop())

- **isEmpty** (비어있으면 True, 아니면 False)
- **peek** (스택의 top에 있는 원소를 반환)

---

스택을 이용한 괄호 검사

        txt = input()
        top = -1
        stack = [0] * 100

        ans = 1
        for x in txt:
            if == '(':
                top += 1
                stack[top] =x

            elif x == ')':
                # 스택이 비어있으면 (여는 괄호가 없으면)
                if top == -1: 
                    ans = 0
                    break
                # 여는 괄호 하나 버림
                else:
                    top -= 1

        # 여는 괄호가 남아있으면
        if top != -1:
            ans = 0

        print(ans)

---
### 재귀호출
ex. 팩토리얼

---

### 후위 표기법
pb) 문자열 수식 계산 

sol) 
1) 스택을 이용해서 중위 표기법을 후위 표기법으로 변경 

    - 연산자의 경우, 스택이 비어 있거나 토큰 우선순위(icp와 isp ..)가 top보다 높으면 push
    - `icp = {'(': 3, '*': 2, '/': 2, '+': 1, '-' : 1}`이고
       `isp = {'(': 0, '*': 2, '/': 2, '+': 1, '-' : 1}`
    - 닫는 괄호 차례면 **여는 괄호를 만날 때까지 모두 pop해서 후위식에 추가**. 닫는 괄호와 해당 여는 괄호는 모두 버림
    - / 차례면 /보다 낮은 연산자를 만날때까지 pop(), 낮은 연산자일 경우 push()
    - 피연산자의 경우 출력
    - 수식이 끝났고 스택이 비었으면 종료 !


2) 후위 표기법의 수식을 스택으로 계산.
    - 연산자의 경우 스택에서 피연산자를 두번 pop()해서 꺼내고 계산결과 스택에 push
    - 피연산자의 경우 스택에 push()

---

## 부분집합
부분집합 구하는 Backtracking 알고리즘1

    def backtrack(a, k, n):
        c = [0] * MAXCANDIDATES

        if k == n:
            process_solution(a, k)
        else:
            ncandidates = construct_candidates(a, k, n, c)
            for i in range(ncandidates):
                a[k] = c[i]
                backtrack(a, k+1, n)

부분집합 구하는 Backtracking 알고리즘2

    def construct_candidates(a, k, n, c):
        c[0] = True
        c[1] = False
        return 2

    def process_solution(a, k):
        for i in range(k):
            if a[i]:
                print(num[i], end = ' ')
        print()

부분집합 구하는 Backtracking 알고리즘3

    MAXCANDIDATES = 3
    NMAX = 4
    a = [0] * NMAX
    num = [1,2,3,4]
    backtrack(a,0,3)

---
### 순열
Backtracking을 이용하여 순열 구하기2
(순열구하기1은 부분집합 구하는1과 유사함)

    def construct_candidates(a, k, n, c):
        in_perm = [False]*(NMAX+1)

        for i in range(k):
            in_perm[a[i]] = True

        ncandidates = 0
        for i in range(1, NMAX+1):
            if in_perm[i] == False:
                c[ncandidates] = i
                ncandidates += 1

        return ncandidates

---

### 가지치기
**부분집합의 합** : I원소의 포함 여부를 결정하면 i까지의 부분집합의 합 Si를 결정가능. Si-1이 찾고자하는 부분집합이 합보다 크면 남은원소 고려할필요가 x