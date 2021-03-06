---
layout: post
title: "SQL과 데이터베이스 - 조인과 집계 데이터 : NATURAL JOIN"
description: >
    NATURAL JOIN
sitemap: false
categories:
  - sql
  - sqlgrammar 
---

* toc
{:toc .large-only}



> 이 학습은 패스트캠퍼스의 **올인원 패키지 : 모두를 위한 SQL/DB** 강의를 듣고 복습하는 내용입니다.

![image](https://user-images.githubusercontent.com/80219821/149906379-0630ea90-3c1c-4997-8890-78676ed11ea4.png)



## NATURAL JOIN 설명 및 특징

- 두 개의 테이블에서 같은 이름을 가진 컬럼 간의 INNER JOIN을 자동으로 출력해준다.(컬럼 따로 지정 X) 즉, SQL문 자체가 간소해 진다.
- 하지만 NATURAL JOIN은 실무에서 잘 쓰이지 않는다.
  - 자동으로 출력해준다고 하는 것은 에러가 발생할 가능성이 있다는 뜻이기 때문





## NATURAL JOIN 실습





- 실습 준비

```sql
CREATE TABLE CATEGORIES 
(
  CATEGORY_ID SERIAL PRIMARY KEY
, CATEGORY_NAME VARCHAR (255) NOT NULL
);

CREATE TABLE PRODUCTS 
(
  PRODUCT_ID SERIAL PRIMARY KEY
, PRODUCT_NAME VARCHAR (255) NOT NULL
, CATEGORY_ID INT NOT NULL
, FOREIGN KEY (CATEGORY_ID) 
  REFERENCES CATEGORIES (CATEGORY_ID) -- 참조한다. 즉 특정 제품은 특정 카테고리를 가지고 있어야 한다. 라는 참조 무결성 제약조건
);

INSERT INTO CATEGORIES 
(CATEGORY_NAME)
VALUES
  ('Smart Phone')
, ('Laptop')
, ('Tablet')
;
COMMIT;

INSERT INTO PRODUCTS 
(PRODUCT_NAME, CATEGORY_ID)
VALUES
  ('iPhone', 1)
, ('Samsung Galaxy', 1)
, ('HP Elite', 2)
, ('Lenovo Thinkpad', 2)
, ('iPad', 3)
, ('Kindle Fire', 3)
;
COMMIT;

SELECT * FROM CATEGORIES; -- CATEGORY TABLE
SELECT * FROM PRODUCTS;   -- PRODUCTS TABLE
```

![image](https://user-images.githubusercontent.com/80219821/149907758-d3d9d780-825b-4f52-b473-f811250605d9.png)

![image](https://user-images.githubusercontent.com/80219821/149907963-18561db7-8915-4331-84d1-ca5cd6184bb3.png)





- 실습 1 (NATURAL JOIN이 잘 되는 경우)

```sql
-- 1. NATURAL JOIN 이용
SELECT
	  *
  FROM
	  PRODUCTS A 
NATURAL JOIN 
	  CATEGORIES B
;

-- 2. INNER JOIN 이용
SELECT
	  A.CATEGORY_ID, A.PRODUCT_ID ,
	  A.PRODUCT_NAME, B.CATEGORY_NAME
  FROM
	  PRODUCTS A
  INNER JOIN CATEGORIES B 
  ON (A.CATEGORY_ID = B.CATEGORY_ID);

-- 3. WHERE 절 이용
SELECT
	  A.CATEGORY_ID, A.PRODUCT_ID ,
	  A.PRODUCT_NAME, B.CATEGORY_NAME
  FROM
	  PRODUCTS A, CATEGORIES B 
WHERE A.CATEGORY_ID = B.CATEGORY_ID;
```

![image](https://user-images.githubusercontent.com/80219821/149908324-7f568041-3579-4b6e-9dd3-6915573bb76e.png)

=> category_id 컬럼으로 inner join(natural join) 되었다.

=> 가급적 2,3번 같이 확실한 결과를 도출할 수 있는 JOIN 방법을 활용하는 것이 좋다.

​      (오류가 날 가능성이 조금이라고 있기 때문)





- 실습 2 (NATURAL JOIN이 생각처럼 되지 않는 경우)

```sql
-- 활용할 테이블
SELECT * FROM CITY;
SELECT * FROM COUNTRY;
```

  ![image](https://user-images.githubusercontent.com/80219821/149909029-34a0b420-ce02-4527-a8a1-f8bce358ea7c.png)

![image](https://user-images.githubusercontent.com/80219821/149909163-e8d36c45-259e-4091-83ec-1df701ddd883.png)





```sql
-- 1. NATURAL JOIN => 결과가 나오지 않음
SELECT
	  *
 FROM
 	  CITY A 
NATURAL JOIN COUNTRY B;

-- 2. INNER JOIN
SELECT
	  *
  FROM
	  CITY A
  INNER JOIN COUNTRY B 
  ON (A.COUNTRY_ID = B.COUNTRY_ID);
  
-- 3. WHERE 절 사용
SELECT 
	  *
  FROM 
      CITY A, COUNTRY B
WHERE A.COUNTRY_ID = B.COUNTRY_ID;

```

![image](https://user-images.githubusercontent.com/80219821/149909608-a534bf78-253d-4f3f-8aa3-7df5ff14645e.png)

=> NATURAL JOIN의 결과가 도출되지 않는 이유는 두 테이블은 country_id라는 컬럼 이외에도  last_update라는 중복된 컬럼이 존재하기 때문이다.

=> 위와 같이 NATURAL JOIN은 결과가 생각대로 도출되지 않을 가능성이 있기 때문에 잘 쓰지 않는다.



