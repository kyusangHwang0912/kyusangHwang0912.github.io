---
layout: post
title: "SQL과 데이터베이스 - 조인과 집계 데이터 : FULL OUTER JOIN"
description: >
    FULL OUTER JOIN
sitemap: false
categories:
  - sql
  - sqlgrammar 
---

* toc
{:toc .large-only}



> 이 학습은 패스트캠퍼스의 **올인원 패키지 : 모두를 위한 SQL/DB** 강의를 듣고 복습하는 내용입니다.



![image](https://user-images.githubusercontent.com/80219821/125222876-c71f7000-e305-11eb-945b-6aa89e6023eb.png)

**: 두 테이블 간 출력가능한 모든 데이터를 포함한 집합을 출력한다.**

**(INNER 조인, LEFT OUTER 조인, RIGHT OUTER 조인 모두 포함).**





---





## FULL OUTER 조인 실습





#### ● 기본 실습

: 아래그림과 같이 만들었던 BASKET_A, BASKET_B 테이블 이용

![image](https://user-images.githubusercontent.com/80219821/125156314-cf5d9b00-e19f-11eb-99a6-2e0f8cb688b7.png)



![image](https://user-images.githubusercontent.com/80219821/125156316-d1275e80-e19f-11eb-9e65-5721bd12345f.png)







```sql
SELECT
	  A.ID ID_A,
	  A.FRUIT FRUIT_A,
	  B.ID ID_B,
	  B.FRUIT FRUIT_B
FROM  BASKET_A A
FULL OUTER JOIN BASKET_B B 
ON A.FRUIT = B.FRUIT;
```

![image](https://user-images.githubusercontent.com/80219821/125223107-28dfda00-e306-11eb-9faa-f0ff1e5f520f.png)

-> 모든 집합이 출력되었다.

![image](https://user-images.githubusercontent.com/80219821/125223819-5d07ca80-e307-11eb-985a-ce9542b3943b.png)







---





#### ● ONLY OUTER 조인

```sql
SELECT
	  A.ID ID_A,
	  A.FRUIT FRUIT_A,
	  B.ID ID_B,
	  B.FRUIT FRUIT_B
FROM  BASKET_A A
FULL OUTER JOIN BASKET_B B 
ON A.FRUIT = B.FRUIT
WHERE A.ID IS NULL          -- right outer
   OR B.ID IS NULL;         -- left outer
```

![image](https://user-images.githubusercontent.com/80219821/125223769-48c3cd80-e307-11eb-9f87-c6b7d3cb8525.png)

-> FULL OUTER JOIN에서 A.ID가 NULL 혹은 B.ID가 널인 값들만 추출한다.

![image](https://user-images.githubusercontent.com/80219821/125223849-6db84080-e307-11eb-904b-949f4644ddb9.png)





---





## 추가 실습

#### ● 테이블 생성



```sql
CREATE TABLE
IF NOT EXISTS DEPARTMENTS 
(
  DEPARTMENT_ID SERIAL PRIMARY KEY
, DEPARTMENT_NAME VARCHAR (255) NOT NULL
);

CREATE TABLE
IF NOT EXISTS EMPLOYEES 
(
  EMPLOYEE_ID SERIAL PRIMARY KEY
, EMPLOYEE_NAME VARCHAR (255)
, DEPARTMENT_ID INTEGER
);

INSERT INTO DEPARTMENTS (DEPARTMENT_NAME)
VALUES
  ('Sales')
, ('Marketing')
, ('HR')
, ('IT')
, ('Production');

COMMIT;

INSERT INTO EMPLOYEES (
  EMPLOYEE_NAME
, DEPARTMENT_ID
)
VALUES
('Bette Nicholson', 1),
('Christian Gable', 1),
('Joe Swank', 2),
('Fred Costner', 3),
('Sandra Kilmer', 4),
('Julia Mcqueen', NULL);

COMMIT; 
```

```sql
SELECT * FROM DEPARTMENTS; 
```

![image](https://user-images.githubusercontent.com/80219821/125224075-d2739b00-e307-11eb-976d-7d300ae91c75.png)

``` sql
SELECT  * FROM EMPLOYEES; 
```

![image](https://user-images.githubusercontent.com/80219821/125224103-e6b79800-e307-11eb-99d4-4b249a8b5269.png)





---





#### ●  FULL OUTER 조인 실습

```sql
SELECT
       E.EMPLOYEE_NAME
     , D.DEPARTMENT_NAME
  FROM
      EMPLOYEES E
FULL OUTER JOIN DEPARTMENTS D 
ON D.DEPARTMENT_ID = E.DEPARTMENT_ID;
```

![image](https://user-images.githubusercontent.com/80219821/125224222-267e7f80-e308-11eb-9c16-48daa4a5865b.png)

-> 모든 집합이 출력되었다.

-> 소속된 부서가 없는 직원, 소속한 직원이 없는 부서 둘다 출력





---





#### ● RIGHT ONLY

``` sql
SELECT
       E.EMPLOYEE_NAME
     , D.DEPARTMENT_NAME
  FROM
      EMPLOYEES E
FULL OUTER JOIN DEPARTMENTS D 
ON D.DEPARTMENT_ID = E.DEPARTMENT_ID
WHERE E.EMPLOYEE_NAME IS NULL;  -- 소속된 직원이 없는 부서
```

![image](https://user-images.githubusercontent.com/80219821/125224530-c6d4a400-e308-11eb-9a7d-23731ed0df31.png)

-> 소속된 직원이 없는 부서만 출력

-> *FULL OUTER JOIN*을 *RIGHT JOIN* 으로 바꾸어도 같은 결과가 나온다.





---





#### ● LEFT ONLY

```sql
SELECT
       E.EMPLOYEE_NAME
     , D.DEPARTMENT_NAME
  FROM
      EMPLOYEES E
FULL OUTER JOIN DEPARTMENTS D 
ON D.DEPARTMENT_ID = E.DEPARTMENT_ID
WHERE D.DEPARTMENT_NAME IS NULL; -- 소속한 부서가 없는 직원
```

![image](https://user-images.githubusercontent.com/80219821/125224677-03080480-e309-11eb-954e-5bedad5fd464.png)

-> 소속한 부서가 없는 직원만 출력

-> *FULL OUTER JOIN*을 *LEFT JOIN*으로 바꾸어도 같은 결과가 나온다.







