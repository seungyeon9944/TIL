### 오답노트

문제 : 다수의 유저를 등록하고자 한다. 주어진 유저 정보 리스트와 모든 유저를 등록하고, 반환된 유저 정보를 하나의 리스트에 담아 출력할 수 있도록 map 함수를 사용하여 코드를 작성하시오.

답안 :
`name = ['김시습', '허균', '남영로', '임제', '박지원']`

`age = [20, 16, 52, 36, 60]`

`address = ['서울', '강릉', '조선', '나주', '한성부']`

`def create_user(name, age, address):`
**매개변수에 name, age, address 입력**

`global person_info` **전역변수**

`person_info = {'name': name, 'age': age, 'address' : address} ` **map함수를 이용하기 때문에 인덱스할 필요 X**

`print(f"{name}님 환영합니다 !")`

`return person_info`

`result = list(map(create_user, name, age, address))` **map함수는 (함수,매개변수1,매개변수2,매개변수3) 해서 create_user에 있는 매개변수의 갯수만큼 스택이 쌓이고, 각 함수를 적용한 결과의 list를 도출**

`print(result)`
