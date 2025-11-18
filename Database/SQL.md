# SQL
'Structure Query Language'의 약자로, 테이블의 형태로 **구조화**된 관계형 데이터베이스에게 요청을 질의(**요청**)

`SELECT column_name FROM table_name;`처럼 대소문자 구분 X, 각 끝에는 세미콜론 필요

수행 목적에 따른 SQL Statements 4가지 유형
1. **DDL** - 데이터 정의 (기본 구조 및 형식 변경) ex. `CREATE, DROP, ALTER`
2. **DQL** - 데이터 검색 ex. `SELECT`
3. **DML** - 데이터 조작 ex. `INSERT, UPDATE, DELETE`
4. **DCL** - 데이터 및 작업에 대한 사용자 권한 제어 ex. `COMMIT, ROLLBACK, GRANT, REVOKE`

## `SELECT`
- 테이블의 데이터 **조회 및 반환**
- `'*'` (asterisk) 사용하여 모든 필드 선택

## `ORDER BY`
- FROM 절 뒤에 위치
- 결과를 **오름차순 (ASC, 기본 값) 혹은 내림차순 (DESC)** 으로 정렬
- `SELECT FirstName FROM employees ORDER BY FirstName DESC;`

## `DISTINCT`
- 조회 결과에서 **중복된 레코드 제거**
- `SELECT DISTINCT select_list FROM table_name;`

## `WHERE` ⭐
- 조회 시 **특정 검색 조건 지정**
- `SELECT select_list FROM table_name WHERE search_condition ORDER BY standard;`
- `SELECT LastName, FirstName, Company, Country FROM customers WHERE Company IS NULL AND Country IN ('Canada', 'USA');`

### SQL의 `NULL`
SQL은 논리 연산에 대해 `TRUE, FALSE, UNKNOWN` 이렇게 세 가지 값을 사용하기 때문에 `= NULL` 이라고 안쓰고 `IS NULL`이라고 써야함.

## `LIMIT`
- **조회**하는 레코드 수 **제한**
- `SELECT select_list FROM table_name LIMIT [offset,] row_count;`
- `LIMIT 2, 5;`면 2번 인덱스부터 5개
- `LIMIT 7;`이면 내림차순으로 상위 7개
- ORDER BY 뒤에 씀

## `BETWEEN`
- `WHERE Bytes BETWEEN 10000 AND 500000;`

## `LIKE`
- 값이 특정 패턴에 일치하는지 확인
1) `%` : **0개 이상의 문자열과 일치**하는지 확인 (`%son`이면 json, jason 다 가능)
2) `_` : **1개 문자**와 일치하는지 확인 (`_son`이면 무조건 1글자만 가능)
- `SELECT LastName, FirstName FROM customers WHERE LastName LIKE '%sun';`

## `GROUP BY`
- 레코드를 **그룹화하여 요약본** 생성 (기준은 '집계 함수'와 함께 사용)
  - 집계 함수 (Aggregation Functions) : `SUM, AVG, MAX, MIN, COUNT`
- `SELECT Country, COUNT(*) FROM customers GROUP BY Country ORDER BY AVG(Bytes) DESC;` : 그룹별로 묶은 총 수 반환

## `HAVING`
- 집계 항목에 대한 **세부 조건**
- `SELECT department, COUNT(*) AS num_employees FROM employees GROUP BY department HAVING num_employees > 5;`


| 비교 |    `WHERE`    |    `HAVING`   |
| --- | ----------- | ----------- |
| 목적 | 개별 행 조건 지정 | `GROUP BY`에 의해 그룹화 조건 지정 |
| 적용시점 | `GROUP BY` 이전에 | 그룹핑/집계 함수 적용 후에 |
| 예시 | 특정조건 만족하는 행 집계, 정렬 | 그룹별 집계 결과 조건걸어 특정그룹 선택 |


결론 ! SELECT statement 실행 순서
## `FROM` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` → `ORDER BY` → `LIMIT`


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