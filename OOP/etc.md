## 버그 bug
소프트웨어에서 발생하는 오류 또는 결함
프로그램의 예상된 동작과 실제 동작 사이의 불일치

## 디버깅 debugging
버그를 찾아내 수정, 프로그램의 오작동 원인을 식별하여 수정
by print 함수 활용, breakpoint나 변수 조회 등, python tutor 활용, 눈 디버깅 등등 ..

## 에러 error
프로그램 실행 중에 발생하는 예외 상황
1) **문법 에러** syntax error
2) **예외** exception
- 내장 예외 Built-in Exceptions : 예외 상황을 나타내는 예외 클래스들 (ex. 0으로 나눌 때)
- 예외 처리 Exception Handling 
by try, except, else, finally

### try-except 구조
`try:`
    예외가 발생할 수 있는 코드
`except 예외:`
    예외 처리 코드

ex.
`try:`
    `result = 10/0`
`except ZeroDivisionError:`
    `print('0으로 나눌 수 없습니다.')`

### else & finally 코드
- else는 예외가 없을 때
- finally는 예외 발생 여부와 관계없이 항상 실행됨


+ `except Exception:` 하면 Exception이 내장 예외의 모든 상속이기 때문에 그 하위에 있는 코드에 도달 X

### as 키워드
`except IndexError as error:`
`print(f'{error}가 발생했습니다.')`

### EAFP 
예외처리를 중심으로 코드 작성 (try - except)
### LBYL 
값 검사를 중심으로 코드 작성 (if - else)