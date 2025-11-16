# set 세트
- **고유한** 항목들의 **정렬되지 않은** 컬렉션 
- **순서 X**, 계속 재정렬됨
- **해시 테이블**을 사용하여 저장 - 추가, 삭제, 존재여부가 빠름
- 집합연산에 특화

+ 리스트 중복 제거하는 문제 순서가 유지되어야할 경우 set로 변환하면 안됨 !!

### `s.add(x)`
세트에 x를 추가


### `s.update(iterable)`
세트에 다른 iterable 요소(ex. 리스트) 추가


### `s.clear()`
세트의 모든 항목 제거


### `s.remove(x)`
세트에서 항목 x를 **제거**, 항목 x가 **없을 경우 keyError**


### `s.pop()`
세트에서 **임의의** 요소를 제거하고 **반환**


### `s.discard(x)`
세트 s에서 항목 x를 제거. 항목 없어도 에러 없음

---

# set집합
|  메서드  | 연산자 |
| -------- | ---- |
|`set1.difference(set2)`| `set1 - set2` |
|`set1.intersection(set2)`| `set1 & set2` | 
|`set1.issubset(set2)`| `set1 <= set2` |
|`set1.issuperset(set2)`| `set1 >= set2` |
|`set1.union(set2)`| `set1 합집합 set2` |

---

## 해시 테이블 hash table
'키'와 '값'을 짝지어 저장하는 구조

## 해시 hash
- 임의의 크기를 가진 데이터를 고정된 크기의 고유한 값으로 변환하는 것
- 불변 타입만 가능 (가변형 객체 list dict set는 안됨 !!)

## 해시 함수
임의 길이 데이터를 입력받아 고정길이(**정수**)로 변환해주는 함수. 이 '정수'가 해시 값

---

## BNF (Backus-Naur Form)