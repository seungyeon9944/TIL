# 함수 (Function) 
특정 작업을 수행하기 위한 
1) 재사용 가능한 코드 묶음 
2) 코드의 가독성과 유지보수성 향상 
정의 - 호출 로 이루어짐. 
function_name(argments)의 형태. 
def 다음줄부터 들여쓰기

input x 
->
(docstring (함수의설명서, 선택적으로 작성) + return value (반환값) =) function 
-> 
output (그림 삽입)

**def <함수 이름> (매개변수1, 매개변수2)** :
*return 문이 없다면 None이 반환됨*

print( ) = 개발자에게 출력해준 것 
*그래서 print 함수는 반환 (코드 내에서 등장)값이 없음*

---

## 매개변수 
함수를 정의할 때, 함수가 받을 값을 나타내는 변수
- 인자 : 함수를 호출할 때, 실제로 전달되는 값
1)	위치 인자

2)	기본 인자 값 
`def greet(name, age = 30):` 일 때 
`greet(‘Bob’)`만 가능 `greet(‘Charlie’, 40)`도 가능

3)	키워드 인자
`def greet(name, age) :`
`greet(age=35, name=’Dave’)`도 가능. 
인자의 이름과 함께 전달. 인자의 순서는 중요x

4)	임의의 인자 목록
정해지지 않은 개수의 인자 처리 by 매개변수 앞에 '*' 사용
여러 개의 인자를 `tuple`(시퀀스, 변경불가 -> 내부 동작 때 씀)로 처리
`def calculate_sum(*args) :`
   `print(args)`
   `print(type(args))`

5)	임의의 키워드 인자 목록
정해지지 않은 개수의 인자 처리 by 매개변수 앞에 '**' 사용
여러 개의 인자를 dictionary로 묶어 처리
`def print_info(**kwargs) :`
   `print(kwargs)`
`print_info(name= ‘Eve’, age = 30)`

---

## 재귀함수 
함수 내부에서 자기 자신을 호출하는 함수 (끝없이 호출하지 않도록 종료시점 설정하는 것이 중요, 예로 if n ==0: return 1로 종료), 
- **스택 오버플로우** : 작업 고간에 일이 너무 많이 쌓임 에러 발생할 수도 있음
ex. 팩토리얼

---

## 내장함수 
파이썬이 기본적으로 제공하는 함수 (별도의 import 없이 바로 사용 가능) 
파이썬 공식 문서 속 [자습서], [라이브러리 레퍼런스], [언어 레퍼런스]

---

### Python의 범위 
local scope와 global scope

**local scope에서 존재하는 건 global scope에서 사용할 수 없음**

`def func( ):`
   `num = 20`
   `print(‘local’, num)`
`func( )`
`print(‘global’, num)`이면 `# NameError : name ‘num’ is not defined`가 뜸 이는 수명주기와 연관이 있음


### 변수 수명주기
1.	built-in scope (파이썬이 실행된 이후로 영원히)
2.	global scope (모듈이 호출된 시점 이후 혹은 인터프리터까지 끝날때까지)
3.	local scope (함수가 호출될 때 생성 ~ 함수가 종료될 때까지)

### 이름 검색 규칙 : LEGB Rule (Local -> Enclosed -> Global -> Built-in)
함수 내에서는 바깥 Scope의 변수에 접근 가능하나 수정은 할 수 없음
del sum 쓰면 sum 변수 객체 삭제 가능

ex.
`x = 'G'`
`y = 'G'`
`def outer_func():`
   `x = 'E'`
   `y = 'E'`

   `def inner_func(y):`
   `z = 'L'`
   `print(x, y, z)` # E P L 
   x는 L없음 -> E찾음
   y는 L에서 파라미터 y존재 -> 전달받은 'P' (이부분이 좀 어려운듯)
   z는 L찾음 -> L

`inner_func('P')`
`print(x, y)` # E E
outer function에서 E 찾음 

`outer_func()`
`print(x, y)` # G G
global 영역에서 G 찾음

- global 키워드 주의사항
1.	global 키워드 선언 전엔 참조 불가
2.	매개변수에는 global 키워드 사용 불가

### 단일 책임 원칙
모든 객체는 하나의 명확한 목적과 책임을 가져야 함
- 함수 설계 원칙 : 1) 명확한 목적 2) 책임 분리 3) 유지보수성 

패킹 Packing과 언패킹 Unpacking 

| 구분 | 상황 | * 연산자 | ** 연산자 |
| ---- | ------ | -------- | -------- |
| **패킹** | 함수 **정의** 시 | 여러 위치 인자를 하나의 **튜플**로 받음 | 여러 키워드 인자를 하나의 딕셔너리로 받음 |
| **언패킹** | 함수 **호출** 시 | 리스트/튜플을 개별 **위치 인자**로 전달 | 딕셔너리를 개별 키워드 인자로 전달 |

