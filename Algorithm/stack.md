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