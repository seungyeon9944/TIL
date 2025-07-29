# Dictionary 딕셔너리
- 해시 테이블을 사용하여 **키**와 **값**을 짝지어 저장하는 자료구조
- 삽입 삭제 검색이 매우 빠름
- 키는 hashable한 고유한 값 / 값은 중복 가능, 어떤 자료형도 저장가능


### `D.get(k)` 혹은 `D.get(k, v)`
`.get(key[,default])` 형태로, 키에 연결된 값 (키가 없는경우 None 또는 기본값) 반환
없는 key를 입력해도 에러가 안나서 확장성 


### `D.keys()` 와 `D.values()`
딕셔너리 키를 모은 객체를 반환 / 딕셔너리 값을 모은 객체를 반환
ex.
`person = {'key1': 'value1', 'key2': 'value2'}`
`print(person(person.keys())` 하면 `dict_keys(['key1', 'key2'])`
**`for item in person.keys() :`**
    `print(item)`
하면
`name`
`age`
나옴


### `D.items()`
딕셔너리 키/값 쌍을 모은 객체 반환
`print`했을 때 `dict_items([('name','Alice'), ('age', 25)])`가 나오기 때문에
**`for key, value in person.items():`**
해서 `print(key, value)`해줌


### `D.pop(k)` 또는 `D.pop(k, v)`
키를 제거하고 값을 반환 (없으면 에러나 default 반환)
ex. `print(person.pop('country', None))`하면 없을때 `None` 반환

---

### `D.clear()`
딕셔너리의 모든 키/값 쌍 제거해서 빈 딕셔너리 {}가 됨


### `D.setdefault(k)` 또는 `D.setdefault(k, v)`
`.setdefault(key[,default])`의 형태
키와 연결된 값 반환 + 키가 없으면 **default와 연결한 키를 딕셔너리에 추가**하고 default 반환


### `D.update([other])`
other가 제공하는 키/값 쌍으로 딕셔너리를 갱신하고 기존 키는 덮어씀
ex. `A = {'name': 'Alice', 'age' : 25}`이고 `B = {'name': 'Mark', 'country': 'Canada'}`일 때
`A.update(B)`이면 'name'에는 'Mark' 쌍이 연결됨
ex. 혹은 `A.update(age = 27, address='Vancouver')` 이렇게도 가능