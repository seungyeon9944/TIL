# Model
데이터베이스와 Python 클래스(객체)로 추상화된 형태로 상호작용. 유지보수 및 확장성 증대

### Model Class
데이터베이스 테이블을 **정의**하고 열(column)을 나타내는 중요한 구성 요소
```
# articles/models.py
class Article(models.Model): # django.db.models 모듈의 Model이라는 부모 클래스를 상속받음
  title = models.CharField(max_length = 10)
  content = models.TextField()
```

### 클래스 변수명 
테이블의 각 필드(열) 이름. 위 예시에서는 title과 content에 해당.

## Model Field
DB 테이블의 필드(열) 정의. **데이터 타입** 및 **제약 조건** 명시. 위 예시에서 등호 우측에 해당.
CharField랑 TextField는 필드 유형, max_length = 10은 필드 옵션

### 1. Field Types 
### `CharField()`
제한된 길이의 문자열을 저장

### `TextField()`
길이 제한이 없는 대용량 텍스트를 저장 (무한대는 아님)

그밖에도 숫자 필드 `IntegerField`, `FloatField`/
날짜 및 시간 필드 `DateField`, `TimeField`, `DateTimeField` / 파일 관련 필드 `FileField`, `ImageField`

---
### 2. Field Options
필드의 **동작**과 **제약조건**을 정의

#### 제약 조건 (Constraint)
특정 규칙을 강제하기 위해 테이블의 열이나 행에 적용되는 규칙이나 제한사항

### `null`
데이터베이스에서 NULL 값을 허용할지 여부 (기본값 : `False`)

### `blank`
form에서 빈 값을 허용할지 여부 (기본값 : `False`)

### `default`
필드의 기본값

---

# Migrations
model 클래스의 변경사항 (**필드 생성, 수정 삭제** 등)을 DB에 최종 반영하는 방법.

### model class (설계도 초안) 에 변경사항이 생기면 (model class 생성/수정) 반드시 새로운 설계도를 생성하고 (`makemigrations`) → (migration 파일, 최종 설계도) 이를 DB에 반영해야 한다. ( `migrate` ) → db.sqlite3 (DB)

- `migrate` 명령어는 마이그레이션 파일의 Python 코드를 SQL 문으로 자동 변환 (파이썬 코드 → 번역 → SQL 쿼리문 → 데이터베이스 실행)
- `$ python manage.py makemigrations` : model class를 기반으로 최종 설계도(migration)을 작성
- `$ python manage.py migrate` : 최종 설계도를 DB에 전달하여 반영, 경고 메시지 뜰 때 실행

추가 모델 필드 작성
1) 새로운 필드 작성 - 모델 클래스 수정
```
# articles/models.py
class Article(models.Model):
  title = models.CharField(max_length=10)
  content = models.TextField()
  created_at = models.DateTimeField(auto_now_add=True) # 데이터가 처음 생성될때만 자동으로 현재 날짜시간 저장
  updated_at = models.DateTimeField(auto_now=True) # 데이터가 저장될 때마다 자동으로 현재 날짜시간 저장
```

2) 새로운 필드 추가 후 `makemigrations` 명령어 입력
```
$ python manage.py makemigrations
```

3) Django가 제안하는 기본 값 사용 .. 엔터 누르면 됨
4) migrations 과정 종료 후 2번째 migration 파일이 생성됨
5) migrate 후 테이블 필드 변화 확인

---
# 관리자 인터페이스 (Automatic admin interface)
Django가 추가 설치 및 설정 없이 자동으로 제공하는 관리자 인터페이스. 
- 데이터베이스 모델의 **CRUD(생성, 읽기, 업데이트, 삭제)** 작업을 간편하게 할 수 있음
- 빠른 프로토타이핑, 비개발자 데이터 관리, 내부 시스템 구축에 이상적

1) Django admin 계정 생성 - 터미널 열기, 관리자 계정 생성 명령어 입력 (`$ python manage.py createsuperuser`), 정보 입력
2) DB에 생성된 admin 계정 확인
3) 관리자 인터페이스 페이지 .. 웹 브라우저 열고 `http://127.0.0.1:8000/admin`로 이동
4) 관리자 인터페이스 접속 확인 (아무것도 안 보이는게 맞음)
5) Admin site 모델 클래스 등록 및 확인 .. admin.py에 작성한 모델 클래스 등록해야만 확인 가능
이때 admin.py는
  ```
  # articles/admin.py
  from django.contrib import admin
  from .models import Article

  admin.site.register(Article)
  ```

6) 데이터 생성, 수정, 삭제 테스트. Articles 앱에서 article에 대한 **CRUD(생성, 읽기, 업데이트, 삭제)**를 위한 페이지로 이동


+)

- `$ python manage.py showmigrations` : migration 파일들이 migrate됐는지 여부를 확인. [X] 표시가 있으면 migrate가 완료된 것
- `$ python manage.py sqlmigrate articles 0001` : migration 파일들이 SQL 언어로 어떻게 번역되어 DB에 전달되는지 확인.

### SQLite
데이터베이스 관리 시스템 중 하나, Django의 기본 데이터베이스로 사용됨. 설치/설정 없이 **간편하게 복사/이동/백업** 가능함. Git과 같은 버전 관리 시스템에서 관리하지 않는 게 원칙이며 .gitignore 파일에 추가해두어야함