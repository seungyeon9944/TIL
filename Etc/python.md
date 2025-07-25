**프로그램** : 문제를 해결하기 위한 **명령어들의 집합** 

**프로그래밍** : 새 연산을 정의하고 조합해 유용한 작업을 수행하는 것 (명령어 묶음을 만드는 과정)

**프로그래밍 언어** : 컴퓨터에게 **작업을 지시**하고 **문제를 해결**하는 도구

## 파이썬을 배우는 이유 
1) 쉽고 간결한 문법
2) 파이썬 커뮤니티의 지원
3) 광범위한 응용 분야 (프로그래밍과 인공지능에서 기본 언어로 가장 많이 사용되는 언어) -> TensorFlow (구글), Pytorch (페이스북) 


파이썬 인터프리터 : 
터미널을 켜고 python -i 입력
or 
확장자가 .py인 파일에 작성된 Python 프로그램 실행


---


**표현식** : 하나의 ‘값’으로 평가될 수 있는 모든 코드
**불리언** : 컴퓨터에서 참과 거짓을 나타내는 숫자 1과 0만을 이용하는 방식

**변수** : 값을 나중에 다시 사용하기 위해 (**재사용성**), 그 값에 붙여주는 고유한 이름
- 변수 할당 : 표현식이 만들어 낸 값에 이름을 붙이는 과정(연결) -> 할당문
- 변수명 규칙 : 영문 알파벳, 언더스코어, 숫자로 구성 + 숫자로 시작할 수 없음 + 대소문자 구분 + 파이썬의 내부 예약어로 사용할 수 없는 것들이 있음


메모리의 모든 위치에는 그 위치를 고유하게 식별하는 **메모리주소** 가 존재


- 고유한 ID (메모리 주소) : 제품의 바코드
- 타입 (Type) : 제품의 종류
- 값 (Value) : 제품의 실제 사용물

값 + 타입 + 주소 정보를 묶은 것을 **객체** **Object**라고 부름

(파이썬 -> 객체지향프로그램)



변수는 특정 개체를 가리키는 이름표 (참조)로, 메모리 주소를 가지지는 않음 (X contain X)
**재할당** : 이미 할당된 변수에 새로운 값 다시 할당

| 용어 | 핵심 정의 | 비유 (주소록) |
| --- | --- | --- |
| 객체 (Object) | 데이터(값, 타입, 행동)의 실체 | '김철수'라는 실제 사람
| 메모리 주소 | 객체가 저장된 고유한 위치 | 김철수의 실제 집 주소
| 변수 (Variable) | 객체를 가리키는 이름표 | 주소록에 저장된 '내 친구 철수'라는 이름
