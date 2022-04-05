---
layout: post
title: "GROUP BY 문제풀이"

description: >
    Infrean 데이터 분석을 위한 중급 SQL 강의 복습 정리
sitemap: false
tags:
  - [SQL, data_analytics, MySQL,Infrean, Hackerrank]
categories:
  - sql
  - sqlpractice 

---



* toc
{:toc .large-only}

- 사용 테이블 Employee

![image-20220404204755799](/assets/md-images/image-20220404204755799.png)





## 01. Top Earners

- We define an employee's *total earnings* to be their monthly [salary * months] worked, and the *maximum total earnings* to be the maximum total earnings for any employee in the **Employee** table. Write a query to find the *maximum total earnings* for all employees as well as the total number of employees who have maximum total earnings. Then print these values as space-separated integers.

```sql
-- 내 문제 풀이
select months*salary as earnings
     , count(*)
from Employee
group by earnings
order by earnings desc
limit 1;

-- 정답

/*
풀이 step
1. salary * month = earnings
2. 각 earnings 별로 몇명이 그만큼 벌었는지 계산
3. earnins 중에 가장 큰 값을 가져온다.
*/
```
