# SQL
'Structure Query Language'의 약자로, 테이블의 형태로 **구조화**된 관계형 데이터베이스에게 요청을 질의(**요청**)

`SELECT column_name FROM table_name;`처럼 대소문자 구분 X, 각 끝에는 세미콜론 필요

수행 목적에 따른 SQL Statements 4가지 유형
1. DDL - 데이터 정의 (기본 구조 및 형식 변경) ex. `CREATE, DROP, ALTER`
2. DQL - 데이터 검색 ex. `SELECT`
3. DML - 데이터 조작 ex. `INSERT, UPDATE, DELETE`
4. DCL - 데이터 및 작업에 대한 사용자 권한 제어 ex. `COMMIT, ROLLBACK, GRANT, REVOKE`

## `SELECT`
- 테이블의 데이터 조회 및 반환
- `'*'` (asterisk) 사용하여 모든 필드 선택

## `ORDER BY`
- FROM 절 뒤에 위치
- 결과를 오름차순 (ASC, 기본 값) 혹은 내림차순 (DESC) 으로 정렬
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
- 조회하는 레코드 수 제한
- `SELECT select_list FROM table_name LIMIT [offset,] row_count;`
- `LIMIT 2, 5;`면 2번 인덱스부터 5개
- `LIMIT 7;`이면 내림차순으로 상위 7개
- ORDER BY 뒤에 씀

## `BETWEEN`
- `WHERE Bytes BETWEEN 10000 AND 500000;`
- 
## `IN`

## `LIKE`
- 값이 특정 패턴에 일치하는지 확인
1) `%` : 0개 이상의 문자열과 일치하는지 확인 (`%son`이면 json, jason 다 가능)
2) `_` : 1개 문자와 일치하는지 확인 (`_son`이면 무조건 1글자만 가능)
- `SELECT LastName, FirstName FROM customers WHERE LastName LIKE '%sun';`

## `GROUP BY`
- 레코드를 그룹화하여 요약본 생성 (기준은 '집계 함수'와 함께 사용)
  - 집계 함수 (Aggregation Functions) : `SUM, AVG, MAX, MIN, COUNT`
- `SELECT Country, COUNT(*) FROM customers GROUP BY Country ORDER BY AVG(Bytes) DESC;` : 그룹별로 묶은 총 수 반환

## `HAVING`
- 집계 항목에 대한 세부 조건
- `SELECT department, COUNT(*) AS num_employees FROM employees GROUP BY department HAVING num_employees > 5;`


SELECT statement 실행 순서
# `FROM` -> `WHERE` -> `GROUP BY` -> `HAVING` -> `SELECT` -> `ORDER BY` -> `LIMIT`