# 7주차 summary

## Database

-   데이터베이스: 체계화된 데이터의 모임
-   몇 개의 자료 파일을 조직적으로 통합하여 자료 항목의 중복을 없애고 자료를 구조화하여 기억시켜 놓은 자료의 집합체 = 데이터베이스

## RDB

관계형 데이터베이스 (Relational Database)
: 서로 관련된 데이터를 저장하고 접근할 수 있는 데이터베이스 유형

키와 값들의 간단한 관계를 표의 형태로 정리한 데이터 베이스

### 스키마 (shema)

: 데이터베이스에서 자료의 구조, 표현방법, 관계 등 전반적인 명세를 기술한 것

### 테이블

:열(컬럼/필드)과 행(레코드/값)의 모델을 사용해 조직된 데이터 요소들의 집합

-   행 (row) : 실제 데이터가 저장되는 형태
-   열 (column) : 각 열에 고유한 데이터 형식 지정
-   기본키 (Primary Key): 각 행(레코드)의 고유 값
    -   반드시 설정해야 함, 데이터베이스 관리 및 관계 설정 시 주요하게 활용 됨

| id  | name   | address | age |
| --- | ------ | ------- | --- |
| 1   | 김지우 | 서울    | 20  |
| 2   | 이현지 | 대전    | 30  |
| 3   | 박은재 | 부산    | 40  |

## RDBMS

: 관계형 데이터베이스 관리 시스템

관계형 모델을 기반으로 하는 데이터베이스 관리시스템 (e.g. My SQL, SQLite, Oracle … ect)

### SQLite Data Type

-   NULL
-   INTEGER : 크기에 따라 0, 1, 2, 3, 4, 6 또는 8바이트에 저장된 부호가 있는 정수
-   REAL: 8바이트 부동 소수점 숫자로 저장된 부동 소수점 값
-   TEXT
-   BLOB : 입력된 그대로 저장된 데이터 (별다른 타입 없이 그대로 저장)

## SQL (Structured Query Language)

-   관계형 데이터베이스 관리시스템의 데이터 관리를 위해 특수 목적으로 설계된 프로그래밍 언어
-   데이터베이스 스키마 생성 및 수정
-   자료의 검색 및 관리
-   데이터베이스 객체 접근 조정 관리

DDL 데이터 정의 언어 (Data Definition Language)

: 관계형 데이터베이스 구조(테이블, 스키마)를 정의하기 위한 명령어

DML 데이터 조작 언어 (Data Manipulation Language)

: 데이터를 저장, 조회, 수정, 삭제 등을 하기 위한 명령어

DCL 데이터 제어 언어 (Data Control Language)

: 데이터베이스 사용자의 권한 제어를 위해 사용하는 명령어

### SQL Keywords (DML)

-   INSERT : 새로운 데이터 삽입(추가)
-   SELECT : 저장되어있는 데이터 조회
-   UPDATE : 저장되어있는 데이터 갱신
-   DELETE : 저장되어있는 데이터 삭제

### 테이블 생성 및 삭제 statement

-   CREATE TABLE : 데이터베이스에서 테이블 생성
-   DROP TABLE : 데이터베이스에서 테이블 제거

```bash
$ sqlite3 tutorial.sqlite3
sqlite> .database

sqlite> .mode csv
sqlite> .import hellodb.csv examples
sqlite> .tables
examples
```

```sql
CREATE TABLE classmates(
	name TEXT,
	age INT,
	address TEXT,
);

.schema classmate

INSERT INTO classmates VALUES ()
```

### 필드 제약 조건

-   NOT NULL : NULL 값 입력 금지
-   UNIQUE : 중복 값 입력 금지 (NULL 값은 중복 입력 가능)
-   PRIMARY KEY : 테이블에서 반드시 하나. NOT NULL + UNIQUE
-   FOREIGN KEY : 외래키, 다른 테이블의 KEY
-   CHECK : 조건으로 설정된 값만 입력 허용
-   DEFAULT : 기본 설정 값

## CRUD

INSERT : 테이블에 단일 행 삽입

`INSERT INTO 테이블이름 (컬럼1, 컬럼2) VALUES (값1, 값2);`

`INSERT INTO classmate (name, age) VALUES (’홍길동’, 23);`

rowid: SQLite 에서 primary key 없는 경우 자동으로 증가하는 pk column

## READ

SELECT : 테이블에서 데이터를 조회

`SELECT age FROM classmates;`

LIMIT : 쿼리에서 반환되는 행 수를 제한, 특정 행부터 시작해서 조회하기 위해 OFFSET 키워드와 함께 사용하기도 함

`SELECT age FROM classmates LIMIT 1;`

OFFSET : 처음부터 주어진 요소나 지점까지의 차이를 나타내는 정수형

`SELECT age FROM classmates LIMIT 1 OFFSET 2;`

WHERE : 쿼리에서 반환된 행에 대한 특정 검색 조건을 지정

`SELECT * FROM classmates WHERE address=’서울’;`

SELECT DISTINCT : 조회 결과에서 중복 행을 제거

`SELECT DISTINCT age FROM classmates;`

## WHERE

: 특정 조건으로 데이터 조회하기
`SELECT * FROM 테이블 이름 WHERE 조건;`

where 절에서 사용할 수 있는 연산자

-   비교 연산자 : =, >, ≥, <, ≤
-   논리 연산자: AND, OR, NOT

```sql
WHERE HEIGHT = 175 OR HEIGHT = 183 WHERE WEIGHT = 80
-- 키가 175 거나 키가 183 이면서 몸무게가 80인 사람
WHERE (HEIGHT = 175 OR HEIGHT = 183) WHERE WEIGHT = 80
-- 키가 175 또는 183인 사람 중에서 몸무게가 80인 사람
```

SQL에서 사용할 수 있는 연산자

-   BETWEEN 값1 AND 값2 : 값1과 값2 사이의 비교 (값1 ≤ 비교값 ≤ 값2)
-   IN (값1, 값2, …) : 목록 중 값이 하나라도 일치하면 OK
-   LIKE : 비교 문자열과 형태 일치 / 와일드카드 (%, \_)
-   IS NULL / IS NOT NULL : NULL 여부 확인할 때 사용
-   부정 연산자 : ≠, ^=, <>, NOT

연산자 우선순위

1. 괄호
2. NOT
3. 비교연산자, SQL
4. AND
5. OR

## SQLite Aggregate Functions

### Aggregate function (집계 함수)

: 값 집합에 대한 계산을 수행하고 단일 값 반환, 여러 행으로부터 하나의 결과값을 반환하는 함수
SELECT 구문에서만 사용됨

-   COUNT : 그룹의 항목 수
-   AVG : 모든 값의 평균 계산
-   MAX : 그룹 내 모든 최대값
-   MIN : 그룹 내 모든 최소값
-   SUM : 모든 값의 합을 계산

## LIKE

: 패턴 일치를 기반으로 데이터를 조회하는 방법

패탠 구성을 위해 SQLite에서 제공하는 wildcard

-   % : 0개 이상의 문자 - 해당 자리에 문자열이 있을 수도, 없을 수도 있음
-   \_ : 임의의 단일 문자 - 해당 자리에 반드시 한 개의 문자가 존재해야 함

`SELECT * FROM 테이블이름 WHERE 칼럼 LIKE ‘패턴’;`

| 패턴           | 의미                                         |
| -------------- | -------------------------------------------- |
| 2%             | 2로 시작하는 값                              |
| %2             | 2로 끝나는 값                                |
| %2%            | 2가 들어가는 값                              |
| \_2%           | 어떤 값이 하나 있고 두번째까 2로 시작하는 값 |
| 1\_\_\_\_      | 1로 시작하는 총 4자리의 값                   |
| 2*%*% / 2\_\_% | 2로 시작하고 적어도 3자리인 값               |

## ORDER BY

: 조회 결과 집합을 정렬

`SELECT * FROM 테이블이름 ORDER BY 칼럼 ASC;`

`SELECT * FROM 테이블이름 ORDER BY 칼럼 DESC;`

## 기본 함수와 연산

### 문자열 함수

-   SUBSTR(문자열, start, length) : 문자열 자르기 (시작 인덱스 1, 마지막 인덱스 -1)
-   TRIM(문자열), LTRIM(문자열), RTRIM(문자열) : 문자열 공백 제거
-   LENGTH(문자열) : 문자열 길이
-   REPLACE(문자열, 패턴, 변경값) : 패턴에 일치하는 부분 변경
-   UPPER(문자열), LOWER(문자열) : 대소문자 변경
-   || : 문자열 합치기

```sql
SELECT
	last_name || first_name 이름,
	age
FROM users
LIMIT 1;
-- 이름 age
-- --- ---
-- 이지윤 30
```

### 숫자 함수

-   ABS(숫자) : 절댓값
-   SIGN(숫자) : 부호
-   MOD(숫자1, 숫자2) : 숫자1을 숫자2로 나눈 나머지
-   CEIL(숫자), FLOOR(숫자), ROUND(숫자) : 올림, 내림, 반올림
-   POWER(숫자1, 숫자2) : 숫자1의 숫자2 제곱
-   SQRT(숫자) : 제곱근

+) 산술연산자

### ALIAS

: 칼럼명이나 테이블명이 너무 길거나 다른 명칭으로 확인하고 싶을 때는 ALIAS 활용

AS를 생략하여 공백으로 표현할 수 있음, 별칭에 공백 및 특수문자 있는 경우 따옴표로 따로 묶어 표기

```sql
SELECT last_name 성 FROM users;
SELECT last_nmae AS 성 FROM users;
SELECT last_name AS 성 FROM users WHERE 성='김';
```

### GROUP BY

: SELECT 문의 optional 절, 행 집합에서 요약 행 집합을 만듦 (선택된 행 그룹을 하나 이상의 열 값으로 요약 행으로 만듦)

-   지정된 컬럼의 값이 같은 행들로 묶임
-   집계함수와 활용하였을 때 의미가 있음
-   그룹화된 각각의 그룹이 하나의 집합으로 집계함수의 인수로 넘겨짐
-   GROUP BY 절에 명시하지 않은 컬럼은 별도로 지정 불가
    -   그룹마다 하나의 행을 출력하게 되므로 집계함수 등을 활용해야 함
-   GROUP BY의 절은 정렬되지 않음
    -   기존 순서와 바뀌는 경우도 존재
    -   원책적으로 관계형 DB에서는 ORDER BY 통해 정렬

**_문장에 WHERE 절이 포함된 경우 반드시 WHERE 절 뒤에 작성해야 함_**

`SELECT * FROM 테이블 이름 GROUP BY 칼럼1, 칼럼2;`

### HAVING

-   집계함수는 WHERE 절의 조건식에서는 사용 불가 (실행 순서에 의해 WHERE절이 앞에 있기 때문)
-   집계 결과에서 조건에 맞는 값을 따로 활용하기 위해 HAVING 활용

`SELECT * FROM 테이블이름 GROUP BY 칼럼1, 칼럼2 HAVING 그룹조건;`

SELECT 문장 실행 순서

> : FROM ⇒ WHERE ⇒ GROUP BY ⇒ HAVING ⇒ SELECT ⇒ ORDER BY ⇒ LIMIT / OFFSET

## ALTER TABLE

1. 테이블 이름 변경
2. 새로운 column 추가
3. column 이름 수정
4. column 삭제

```sql
ALTER TABLE table_name RENAME TO new_name;
--
ALTER TABLE table_name ADD COLUMN column_definition;
--
ALTER TABLE table_name RENAME COLUMN current_name TO new_name;
--
ALTER TABLE table_name DROP COLUMN column_name;
```

## Case

: 특정 상황에서 데이터를 변환하여 사용할 때 활용 (ELSE 생략할 경우 NULL 값이 지정됨)

```sql
SELECT
	id,
	smoking,
	CASE
		WHEN smoking = 1 THEN '비흡연자'
		WHEN smoking = 2 THEN '흡연자'
		WHEN smoking = 3 THEN '흡연자'
		ELSE '무응답'
	END
FROM healthcare
LIMIT 50;
```

## 서브쿼리

: 특정한 값을 메인 쿼리에 반환하여 활용하는 것으로 실제 테이블에 없는 기준을 이용한 검색이 가능

-   단일행 서브쿼리 : 서브쿼리의 결과가 0 또는 1개인 경우, 단일행 비교 연산자와 함께 사용

    ```sql
    SELECT COUNT(*) FROM users WHERE age = (SELECT MIN(age) FROM users);
    -- users 에서 가장 나이가 작은 사람의 수

    SELECT COUNT(*) FROM users WHERE balance > (SELECT AVG(balance) FROM users);
    -- users에서 평균보다 계좌 잔고가 높은 사람의 수

    SELECT
    	( SELECT COUNT(*) FROM users ) AS 총인원
    	( SELECT AVG(balance) FROM users ) AS 평균연봉
    	( SELECT AVG(age) FROM users ) AS 평균나이
    ;
    -- 전체 인원과 평균 연봉, 평균 나이 출력

    UPDATE users SET balance = (SELECT AVG(balance) FROM users);
    -- UPDATE에서 활용 가능
    ```

-   다중행 서브쿼리 : 서브쿼리의 결과가 2개 이상인 경우, 다중행 비교 연산자와 함께 사용(IN, EXSTS)
    ```sql
    SELECT COUNT(*) FROM users
    WHERE country IN (
    	SELECT country FROM users
    	WHERE first_name='은정' AND last_name = '이'
    );
    -- users에서 이은정과 같은 지역의 사는 사람의 수
    ```
-   다중컬럼 서브쿼리
    ```sql
    SELECT last_name, first_name, age FROM users
    WHERE (last_name, age) IN (
    	SELECT last_name, MIN(age) FROM users GROUP BY last_name)
    ORDER BY last_name;
    -- 특정 성씨에서 가장 어린 사람들의 이름과 나이
    ```
