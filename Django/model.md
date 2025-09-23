# Model
데이터베이스와 Python 클래스(객체)로 추상화된 형태로 상호작용. 유지보수 및 확장성 증대

### Model 클래스
데이터베이스 테이블의 열(column)을 나타내는 중요한 구성 요소
```
# articles/models.py
class Article(models.Model):
  title = models.CharField(max_length = 10)
  content = models.TextField()
```
### Model Field
DB 테이블의 필드(열) 정의. 데이터 타입 및 제약 조건 명시
CharField랑 TextField는 필드 유형, max_length = 10은 필드 옵션

---
### Field types !
## `CharField()`
제한된 길이의 문자열을 저장

## `TextField()`
길이 제한이 없는 대용량 텍스트를 저장

그밖에도 숫자 필드 `IntegerField`, `FloatField`/
날짜 및 시간 필드 `DateField`, `TimeField`, `DateTimeField` / 파일 관련 필드 `FileField`, `ImageField`

---
### Field Options
필드의 **동작**과 **제약조건**을 정의

#### 제약 조건 (Constraint)
특정 규칙을 강제하기 위해 테이블의 열이나 행에 적용되는 규칙이나 제한사항

## `null`
데이터베이스에서 NULL 값을 허용할지 여부 (기본값 : `False`)

## `blank`
form에서 빈 값을 허용할지 여부 (기본값 : `False`)

## `default`
필드의 기본값

---
# Migrations
