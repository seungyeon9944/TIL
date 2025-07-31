# 상속 inheritance
한 클래스(부모)의 속성과 메서드를 다른 클래스(자식)가 물려받는것
for 코드 재사용 + 계층구조 + 유지보수의 용이성

ex.
`class Person:`
    `def __init__(self, name, age):`
        `self.name = name`
        `self.age = age`
    `def talk(self):`
        `print(f'반갑습니다. {self.name}입니다.')`
    
`class Professor(Person):`
    `def __init__(self, name, age, department):`
        `self.name = name`
        `self.age = age`
        `self.department = department`

`class Student(Person):`
    `def __init__(self, name, age, gpa):`
        `self.name = name`
        `self.age = age`
        `self.gpa = gpa`

`p1 = Professor('박교수', 49, '컴퓨터공학과')`
`s1 = Student('김학생', 20, 3.5)`

`p1.talk()`
`s1.talk()`

---

## 메서드 오버라이딩 Method Overrriding
부모 클래스의 메서드를 같은 이름, 같은 파라미터 구조로 **재정의**
부모 클래스의 메서드대로 구현 X

---

# 다중 상속
둘 이상의 상위 클래스로부터 상속, 중복된 속성이나 메서드가 있는 경우 **상속 순서에 의해 결정됨**
**MRO**(Method Resolution Order) 알고리즘 사용 - 각 부모를 오직 한버만 호출, 단조적 구조 형성
기본적으로 **왼쪽에서 오른쪽**, 계층 구조에서 중복되는 클래스는 한번만 확인
ex. 
`class Firstchild(Dad, Mom):` 의 작성 순서이고
`baby = FirstChild('아가')`
`print(baby1.gene)` 이면 Dad가 Mom보다 먼저 적혀있어서 Dad class으로부터 상속됨


## super()
MRO에 따라서 현재 클래스에 부모(상위) 클래스의 메서드나 속성에 접근할 수 있게 해주는 *내장 함수*
직접 부모 클래스 이름을 적지 않아도 됨 !
다중 상속에서 잘 쓰임. 부모 클래스가 아니어도 호출가능

1) 단일 상속 구조
중복된 부분을 `super().__init__ (name, age, number, email)`로 대체가능

2) 다중 상속 구조
(코드 추가 예정)