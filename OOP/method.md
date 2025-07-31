## 1. 인스턴스 메서드 instance method
인스턴스의 **상태**를 조작하거나 **동작을 수행**
⭐️ 반드시 ! 첫번째 인자로 **인스턴스 자신(self)**을 받음 ⭐️ 
self를 쓰는 이유 : `'hello'.upper()`를 실행했을 때 파이썬 내부에서는 `str.upper('hello')` 와 같이 진행됨 (단축형 호출)

ex. `def instance_method(self):`
        `self.count += 1`

## 1-1. 생성자 메서드 constructor method
인스턴스 객체가 생성될때 인스턴스 변수의 초기값 설정
ex. `def __init__(self, name, age):` 
        `self.name = name` **인스턴스 변수**(속성) name과 생성자 메서드의 매개변수 이름
        `self.age = age`


## 2. 클래스 메서드 class method
클래스의 변수를 조작하거나 클래스 레벨의 동작을 수행
데코레이터 `@classmethod`를 사용하여 정의
첫번째 인자로 **해당 메서드를 호출하는 클래스(cls)**가 전달
ex. `class MyClass:`
        `@classmethod`
        `def class_method(cls, arg1, ...):`
            `cls.population += 1`


## 3. 스대틱 메서드 static method
클래스, 인스턴스와 상관없이 독립적으로 동작하는 메서드
호출 시 자동으로 전달받는 인자가 없음
ex. `class MyClass:`
        `@staticmethod`
        `def static_method(arg1, ...):`
            `pass`



같은 클래스로 만든 인스턴스라도 서로 다른 이름 공간을 갖기때문에 서로 영향 X
속성 접근 시 인스턴스 -> 클래스 순서로 탐색
+ 매직 메서드 ..  __str__
+ 데코레이터 ..


---


### 오답노트
**인스턴스 메소드**

        class Plus_minus:
                def __init__(self, first, second):
                        self.first = first
                        self.second = second

                def plus(self):
                result = self.first + self.second
                return result

                def minus(self):
                result self.first - self.second
                return result

        a = Plus_minus(3,4)
        print(a.plus())
        print(a.minus())


**클래스 메소드**는 정적 메소드처럼 인스턴스 없이 호출할 수 있다는 점은 같습니다. 하지만 생성자 함수를 대체하여 인스턴스를 생성할 때 사용도 함. 

        class Shape :
                def __init__(self, width, height):
                        self.width = width
                        self.height = height

                def calculate_perimeter(self):
                        return 2*(self.width + self.height)
                        shape1 = Shape(5, 3)
        perimeter1 = shape1.calculate_perimeter()
        print(perimeter1)