### 데이터 구조 
여러 데이터를 효과적으로 사용 관리하기 위한 구조 (str, list, dict 등)

### 자료 구조 
효율적인 저장, 관리를 위해 구조를 나눠놓은 것. 프로그램의 성능과 효율성, 유지보수성에 큰 영향을 미침

### 메서드 
각 데이터 구조의 메서드를 호출하여 다양한 기능 활용 
(**객체 Object에 속한 함수**, 클래스 내부에 정의되는 함수)
따라서 메서드는 어딘가 클래스에 속해 있는 함수이며 각 데이터 타입별로 다양한 기능을 가진 **메서드**가 존재한다.

- 메서드 호출 방법 : **데이터타입객체.메서드( )**
ex. ‘hello’.capitalize( )

---

# 객체와 참조
변수는 객체의 메모리 주소를 저장하기에 이미 메모리에 존재하는 객체를 변수에 할당할 때는 새로운 객체를 만들지 않고 해당 객체에 대한 주소만 참조함
- 가변/불변 메모리 관리 방식의 이유 
1) 성능 최적화 
2) 메모리 효율성

- **얕은복사** : 객체의 최상위 요소만 새로운 메모리에 복사하는 방법, 내부에 중첩된 객체가 있다면 그 객체의 참조만 복사됨 by 리스트 슬라이싱, `copy( )` 메서드, `list ( )`함수
- **깊은복사** : 객체의 모든 수준의 요소를 새로운 메모리에 복사, 중첩된 객체까지 모두 새로운 객체로 생성됨 - copy 모듈에서 제공하는 `deepcopy( )` 함수 사용 `copy.deepcopy(a)` 이렇게

## List Comprehension 
쉽게 생각하면 append 생략하는 것 !
`numbers = [1, 2, 3]`
`squared_numbers = [num**2 for num in numbers]`
`print(squared_numbers)`
+ 인접행렬

## 메서드 체이닝
`new_text = text.swapcase().replace(‘l’, ‘z’)`
하면 `swapcase` 먼저 그 이후로 `replace`
- 주의1
`result = numbers.copy().sort()`하면 **sort가 None을 반환**하기 때문에
`sorted_numbers = sorted(numbers.copy())`라고 적어야함 (이유: sorted는 내장함수)

- 주의2
`result = numbers.append(7).extend([8, 9])`하면 **append가 None을 반환**하기 때문에 에러뜸

+ 문자 유형 판별 메서드
`isdecimal( )`
`isdigit( )`
`isnumeric( )`

---
### 오답노트 📝💯
✏️ **break** : 앞의 조건이 True이면 코드를 중단시킴

✏️ **continue** : 앞의 조건이 True이면 코드를 실행하지 않고 처음으로 돌아가서 반복


