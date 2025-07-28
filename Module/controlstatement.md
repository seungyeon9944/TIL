# 제어문 Control Statement 
조건에 따라 코드 블록을 실행하거나 반복적으로 코드를 실행

## 1. 조건문 Conditional Statement
**if / elif / else** 이고 elif나 else 없이 if만 있어도 쓸 수 있음

if 조건1:
elif 조건2:
elif 조건3:
else:

---

## 2. 반복문
1) **for문**
반복가능(iterable)한 객체의 요소 반복. 
`student_list`에 객체가 3개 있으니까 3번 반복
`for` 변수 `in` 반복 가능한 객체 :
코드 블록         의 형태

`for` 변수 `in range`(범위) :
코드 블록         의 형태

`for` 변수 `in my_dict :`
`print(key)`
`print(my_dict[key])`

⭐⭐⭐ `for 변수 in range(len(numbers))` : <- 인덱스로 리스트 순회 ⭐⭐⭐
`numbers[i] = numbers[i] * 2 `

- 중첩된 반복문
`for outer in outers:`
    `for inner in inners:`
        `print(outer, inner)`

---

2) **while문** 
반복횟수가 정해지지 않은 경우, 조건에 따라. 반드시 종료 조건이 필요

while 조건식 :
   코드 블록

반복 제어
- continue 키워드는 만나면 다음 코드는 무시하고 다음 반복을 수행
- pass 키워드는 아무 동작도 수행하지 않거나 구조를 잡거나 빈 코드나 없으면 오류 발생 .. 등등
