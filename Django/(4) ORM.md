# ORM (Object-Relational-Mapping)
객체 지향 프로그래밍 언어의 객체(Object)와 데이터베이스의 데이터를 매핑(Mapping), 즉 연결하는 기술

pb) Django는 Python 언어를 사용하지만 데이터베이스는 SQL 언어를 사용함

sol) ORM이 Django와 데이터베이스 사이에서 언어 번역자 역할
개발자를 위해 **QuerySet API**를 제공함

## QuerySet API
복잡한 SQL 쿼리문을 직관적인 Python 코드로 다룰 수 있게 해줌
`.filter()`, `.exclude()`, `.order_by()` 등 파이썬다운 메서드를 사용하여 가독성을 높이고 개발 생산성을 극대화

- 동작 방식 
1) Django → QuerySet API → DB: Django
2) DB: Django → Instance (단일) / QuerySet (다중) → Django

- 구조

  `Article.objects.all()`일 때

  각각 (Model class).(Manager).Queryset API

  - `Article` (**모델 클래스**) : 데이터베이스 테이블에 대한 Python 클래스 표현, 테이블의 스키마 (필드, 데이터 타입) 정의, ORM이 데이터베이스와 상호작용할 때 기본적인 구조체
  - `.objects` (**매니저, manager**) : 모든 모델에 objects라는 이름의 매니저를 자동으로 추가, 매니저를 통해 쿼리 메서드 호출
  - `.all` (**QuerySet API 쿼리 메서드**) : 특정 데이터베이스 작업 수행, 모델과 연결된 테이블의 모든 레코드 조회

### Query
데이터베이스에 특정한 데이터를 보여달라는 요청.
"쿼리문을 작성한다" → 원하는 데이터를 얻기 위해 데이터베이스에 요청 보낼 코드를 작성한다. 

### QuerySet
데이터베이스에서 전달받은 객체 목록(데이터 모음). 순회 가능한 데이터로 1개 이상 데이터를 불러와 사용 가능하고 Django에서만 볼 수 있음

---

## CRUD 
생성, 조회, 수정, 삭제를 묶어 이르는 말

### `Create`
1) 빈 객체 생성 후 값 할당 및 저장
```
article = Article() # Article(class)로부터 article(instance) 생성
article.title = 'first' # 변수 할당 
article.content = 'django!'

article.save() # save를 호출해야 객체가 데이베이스에 저장됨 (인스턴스 메서드)
```

2) 초기 값과 함께 객체 생성 및 저장
```
article = Article(title='second', content='django!')
article.save()
```

3) create() 메서드로 한번에 생성 및 저장
```
Article.objects.create(title ='third', content = 'django!')
```

### `Read`

### `all()`
전체 데이터 조회

### `filter()`
주어진 매개변수와 일치하는 객체를 포함하는 QuerySet 반환.
ex) `Article.objects.filter(title='first')`

### `get()`
주어진 매개변수와 일치하는 객체를 반환 (QuerySet을 반환하지않음 !, 고유성을 보장하는 조회에서만 사용).
ex) `Article.objects.get(pk=100)`

**primary key(pk)** : DB 테이블마다 각 행을 고유하게 식별할 수 있는 속성


### `Update`
수정 전에 조회해야 함 !
```
article = Article.objects.get(pk=1) # 수정할 인스턴스 조회
article.title = 'byebye' # 인스턴스 변수를 변경
article.save() # 저장
```

### `Delete`
삭제 전에 조회해야 함 !
```
article = Article.objects.get(pk=1) # 수정할 인스턴스 조회
article.delete() # delete 메서드 호출 (삭제 된 객체가 반환)
```

