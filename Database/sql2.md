## `CREATE TABLE`
- 테이블 생성
```
CREATE TABLE examples ( 
  ExamID INTEGER PRIMARY KEY AUTOINCREMENT,
  LastName VARCHAR(50) NOT NULL,
  FirstName VARCHAR(50) NOT NULL
);
```
### `AUTOINCREMENT`
- 필드의 자동 증가 기능
- 삭제된 값은 무시되며 재사용x
  
### SQLite 데이터 타입
- NULL
- INTEGER
- REAL (부동 소수점)
- TEXT
- BLOB (이미지, 동영상, 문서 등의 바이너리 데이터)

### 제약 조건
- PRIMARY KEY (해당 키를 기본 키로, INTEGER 타입에만 적용)
- NOT NULL
- FOREIGN KEY

## `ALTER TABLE`
- `ALTER TABLE ADD COLUMN` :
  SQLite는 단일 문 사용해서 한번에 여러 필드 추가x ! 따로따로 적어줘야함.
- `ALTER TABLE RENAME COLUMN` (필드 이름 변경)
- `ALTER TABLE DROP COLUMN`
- `ALTER TABLE RENAME TO` (테이블 이름 변경)

## `DROP TABLE`
테이블 삭제 !

## `INSERT`
```
INSERT INTO 
  articles (title, content, createdAt)
VALUES 
  ('hello', 'world','2000-01-01')
```

## `UPDATE`
```
UPDATE table_name
SET column_name = expression,
[WHERE
  condition];
```

## `DELETE`
```
DELETE FROM
  articles
WHERE
  id = 1;
```

## `INNER JOIN`
두 테이블에서 **값이 일치하는 레코드에 대해서만 결과 반환**
```
SELECT
  articles.title, users.name
FROM
  articles
INNER JOIN users
  ON articles.userId = users.id;
```

## `LEFT JOIN`
- 오른쪽 테이블의 일치하는 레코드와 함께 왼쪽 테이블의 모든 레코드 반환  
- 왼쪽 조건에 맞는 오른쪽 레코드가 없으면 NULL로 출력
```
SELECT * FROM articles
LEFT JOIN users
  On articles.userId = users.id;
```         