# 모듈 Module 
한 파일로 묶인, 만들어 둔 변수와 함수의 묶음으로 검증된 파일 (파이썬파일 .py) 
내장되어 있기 때문에 바로 import
ex.
`import math`
`print(math.pi)` 처럼 모듈명. 변수명의 형태, 점의 왼쪽 객체에서 점의 오른쪽 이름을 찾기

## from 절 
- 장점: 코드가 짧고 간결
- 단점 : 사용자가 선언한 변수에서 정의한 동작이 이루어지지 않을수도
ex. 실수형 대신 문자열이 나옴

## as 키워드 : 이름 충돌 해결
`from math import sqrt`
`from my_math import sqrt as my_sqrt`
`sqrt(4)`
`my_sqrt(4)`

+ 파이썬 표준 라이브러리
### 패키지 
연관된 모듈들을 하나의 디렉토리에 모아 둔 것, 코드 꾸러미
내부 패키지(PSL, Python Standard Library)와 외부 패키지
패키지 설치 `$ pip install ~~`
ex. `requests` 패키지 (웹에 요청을 보내고 응답을 받음)
`requests.get(url).json( )`에서 `get`은 url 요청
