---
layout: post
title: "UNION, UNION ALL"
description: >
    Infrean 데이터 분석을 위한 중급 SQL 강의 복습 정리
sitemap: false
tags:
  - [SQL, data_analytics, MySQL,Infrean, HACKERRANK]
categories:
  - sql
  - sqlpractice 
---

* toc
{:toc .large-only}


## UNION

- JOIN과 달리 데이터를 위아래로(행으로) 데이터를 붙이는 것 => SELECT와 달리 DISTINCT 옵션이 기본이라고 생각하면 된다.
- 중복 값들을 삭제



#### 예제 : Product 테이블에서 Price가 5이하 또는 200 이상인 상품들만 출력하세요.

```sql
-- OR 로 조건 2개 사용
SELECT *
FROM Products
WHERE Price <= 5 OR Price >= 200

-- UNION 사용
SELECT *
FROM Products
WHERE Price <= 5

UNION

SELECT *
FROM Products
WHERE Price >= 200

```

![image-20220405174626423](/assets/md-images/image-20220405174626423.png)



- MySQL에서 지원안하는  기능등을 활용하여 교집합, 차집합 등을 구할 수 있다.
  - 차집합 : EXCEPT, MINUS
  - 교집합 : INTERSECT





## UNION ALL

- UNION과 달리 중복 값들을 포함하며 전부(ALL) 데이터를 붙인다.



#### 예제 :  LEFT JOIN + RIGHT JOIN 섞어서 쓰는 방법

```sql
-- 그냥 LEFT JOIN (Customers 테이블에 정보가 없다면 출력되지 않는다.)
SELECT *
FROM Customers
	 LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
	 
-- Orders 테이블에는 데이터가 있지만 Customers 테이블에는 데이터가 없는 비회원 주문같은 경우도 같이 보고 싶을 때
-- FULL OUTER JOIN 이라고도 한다.
SELECT *
FROM Customers
	 LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
UNION ALL
SELECT *
FROM Customers
	 RIGHT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
```





## 문제풀이



#### 01. Symmetric Pairs

- 활용 테이블(Functions)

![image-20220405174948820](/assets/md-images/image-20220405174948820.png)



- Two pairs *(X1, Y1)* and *(X2, Y2)* are said to be *symmetric* *pairs* if *X1 = Y2* and *X2 = Y1*.

  Write a query to output all such *symmetric* *pairs* in ascending order by the value of *X*. List the rows such that *X1 ≤ Y1*.



```sql
-- 문제 풀이 실패
SELECT X, Y
FROM Functions
WHERE X = Y
GROUP BY X, Y
HAVING COUNT(*) = 2

UNION

SELECT f1.X, f1.Y
FROM Functions AS f1
     INNER JOIN Functions f2 ON f1.X = f2.Y AND f1.Y = f2.X
WHERE f1.X < f1.Y
ORDER BY X
```

- 같은 숫자 2번 있는 숫자만 출력하는 쿼리 + (UNION) +  pair가 되는 숫자만 출력하는 쿼리
  - 출력 결과가 몇 번 있는지 확인하려면 group by와 having을 이용해서 count(*)를 하자.
  - INNER JOIN의 ON 조건에서 AND를 통해 조건을 추가할 수 있다!
  - ORDER BY는 UNION 된 결과에서 실행된다. 따라서 위의 쿼리에는 ORDER BY 쓸 수 없음!

