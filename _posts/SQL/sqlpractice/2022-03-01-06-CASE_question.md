---
layout: post
title: "CASE"

description: >
    Infrean 데이터 분석을 위한 중급 SQL 강의 복습 정리
sitemap: false
tags:
  - [SQL, data_analytics, MySQL,Infrean, Hackerrank, LeetCode]
categories:
  - sql
  - sqlpractice 

---



* toc
{:toc .large-only}
## 01. 조건 1개

```sql
SELECT CASE
			WHEN categoryid = 1 THEN '음료'
            WHEN categoryid = 2 THEN '조미료'
            ELSE '기타'
       END as category_name, categoryid
FROM Products;
```

![image-20220404213850609](/assets/md-images/image-20220404213850609.png)



## 02. 조건 2개 이상

- and로 조건 묶으면 된다.

```sql
SELECT CASE
			WHEN categoryid = 1 AND Supplierid = 1 THEN '음료'
            WHEN categoryid = 2 THEN '조미료'
            ELSE '기타'
       END as category_name, categoryid, supplierid
FROM Products;
```

![image-20220404214530534](/assets/md-images/image-20220404214530534.png)






## 03. 조건 컬럼 GROUP BY

```sql
SELECT CASE
			WHEN categoryid = 1 THEN '음료'
            WHEN categoryid = 2 THEN '소스'
            ELSE '이외'
       END AS new_category
     , AVG(price)
FROM Products
GROUP BY new_category;
```

![image-20220404214509610](/assets/md-images/image-20220404214509610.png)



## 04. CASE 테이블 피봇

- 기본 개념

```sql
SELECT CASE WHEN categoryid = 1 THEN price ELSE NULL END AS category1_price, categoryid, price
FROM Products;
```

![image-20220405004544007](/assets/md-images/image-20220405004544007.png)



- 테이블 피봇

```sql
SELECT AVG(CASE WHEN categoryid = 1 THEN price ELSE NULL END) AS category1_price
	 , AVG(CASE WHEN categoryid = 2 THEN price ELSE NULL END) AS category2_price
     , AVG(CASE WHEN categoryid = 3 THEN price ELSE NULL END) AS category3_price
FROM Products;
```

![image-20220405004737850](/assets/md-images/image-20220405004737850.png)



## 05. 문제풀이



#### 01. Type of Triangle(해커랭크)

- 활용 테이블(TRIANGLES)

![image-20220404215847494](/assets/md-images/image-20220404215847494.png)

- Write a query identifying the *type* of each record in the **TRIANGLES** table using its three side lengths. Output one of the following statements for each record in the table:
  - **Equilateral**: It's a triangle with 3 sides of equal length.
  - **Isosceles**: It's a triangle with 2 sides of equal length.
  - **Scalene**: It's a triangle with 3 sides of differing lengths.
  - **Not A Triangle**: The given values of *A*, *B*, and *C* don't form a triangle. (the combined value of 2 sides is not larger than that of other 1 side .)

```sql
-- 내 문제 풀이
SELECT CASE
            WHEN (A+B <= C) OR (B+C <= A) OR (A+C <= B) THEN 'Not A Triangle'
            WHEN A!=B AND B!=C AND A!=C THEN 'Scalene'
            WHEN A=B AND B=C THEN 'Equilateral'
            WHEN A=B OR B=C OR A=C THEN 'Isosceles'   
       END
FROM TRIANGLES;

-- 정답!
-- tip : 조건문 작성할 때는 select 문에 다른 컬럼들 추가해서 확인하면서 잘 작성했는지 확인하는 것이 좋다.
-- 조건문을 작성할 때는 순서가 중요하다!(맨 위의 조건을 만족하면 아래조건으로 넘어가지 않는다!)
-- equilateral, not a triangle, isosceles 순으로 먼저 작성 후 else 로 scalene 하는 방법도 정답.
```



#### 02. 1179 - Reformat Department Table(리트코드)

- 활용 테이블(Department)

![image-20220405005127345](/assets/md-images/image-20220405005127345.png)

- Write an SQL query to reformat the table such that there is a department id column and a revenue column **for each month**.

- Return the result table in **any order**.

```sql
-- 내 문제 풀이(오답)
SELECT id
     , (CASE WHEN month = 'Jan' THEN revenue ELSE NULL END) AS Jan_Revenue
     , (CASE WHEN month = 'Feb' THEN revenue ELSE NULL END) AS Feb_Revenue
     , (CASE WHEN month = 'Mar' THEN revenue ELSE NULL END) AS Mar_Revenue
     , (CASE WHEN month = 'Apr' THEN revenue ELSE NULL END) AS Apr_Revenue
     , (CASE WHEN month = 'May' THEN revenue ELSE NULL END) AS May_Revenue
     , (CASE WHEN month = 'Jun' THEN revenue ELSE NULL END) AS Jun_Revenue
     , (CASE WHEN month = 'Jul' THEN revenue ELSE NULL END) AS Jul_Revenue
     , (CASE WHEN month = 'Aug' THEN revenue ELSE NULL END) AS Aug_Revenue
     , (CASE WHEN month = 'Sep' THEN revenue ELSE NULL END) AS Sep_Revenue
     , (CASE WHEN month = 'Oct' THEN revenue ELSE NULL END) AS Oct_Revenue
     , (CASE WHEN month = 'Nov' THEN revenue ELSE NULL END) AS Nov_Revenue
     , (CASE WHEN month = 'Dec' THEN revenue ELSE NULL END) AS Dec_Revenue
FROM Department
group by id

-- 정답 : SUM으로 각 그룹 별 revenue를 합해주면 된다!
SELECT id
     , SUM(CASE WHEN month = 'Jan' THEN revenue ELSE NULL END) AS Jan_Revenue
     , SUM(CASE WHEN month = 'Feb' THEN revenue ELSE NULL END) AS Feb_Revenue
     , SUM(CASE WHEN month = 'Mar' THEN revenue ELSE NULL END) AS Mar_Revenue
     , SUM(CASE WHEN month = 'Apr' THEN revenue ELSE NULL END) AS Apr_Revenue
     , SUM(CASE WHEN month = 'May' THEN revenue ELSE NULL END) AS May_Revenue
     , SUM(CASE WHEN month = 'Jun' THEN revenue ELSE NULL END) AS Jun_Revenue
     , SUM(CASE WHEN month = 'Jul' THEN revenue ELSE NULL END) AS Jul_Revenue
     , SUM(CASE WHEN month = 'Aug' THEN revenue ELSE NULL END) AS Aug_Revenue
     , SUM(CASE WHEN month = 'Sep' THEN revenue ELSE NULL END) AS Sep_Revenue
     , SUM(CASE WHEN month = 'Oct' THEN revenue ELSE NULL END) AS Oct_Revenue
     , SUM(CASE WHEN month = 'Nov' THEN revenue ELSE NULL END) AS Nov_Revenue
     , SUM(CASE WHEN month = 'Dec' THEN revenue ELSE NULL END) AS Dec_Revenue
FROM Department
group by id
```

