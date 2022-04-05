---
layout: post
title: "LEFT JOIN 문제풀이"
description: >
    Infrean 데이터 분석을 위한 중급 SQL 강의 복습 정리
sitemap: false
tags:
  - [SQL, data_analytics, MySQL,Infrean, ReetCode]
categories:
  - sql
  - sqlpractice 

---


* toc
{:toc .large-only}


## 01. 183 - Customers Who Never Order

- 활용 테이블 (Customers, Orders)

![image-20220405145052953](/assets/md-images/image-20220405145052953.png)

- Write an SQL query to report all customers who never order anything.

  Return the result table in **any order**.

```sql
-- 내 문제 풀이(정답)
SELECT name as Customers
FROM Customers as C 
	 LEFT JOIN Orders as O ON C.id = O.customerId
WHERE ISNULL(O.id);

-- WHERE O.id IS NULL 도 된다.
```

