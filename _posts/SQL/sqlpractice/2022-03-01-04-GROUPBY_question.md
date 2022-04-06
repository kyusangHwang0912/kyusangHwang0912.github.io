---
layout: post
title: "GROUP BY"

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

## GROUP BY

```sql
-- SupplierID, CategoryID 별 평균 가격대 + 가격대 내림차순
select SupplierID
     , Categoryid
     , AVG(price)
from Products
group by SupplierID, CategoryID;
order by AVG(Price) DESC;
```

![image-20220404195018634](/assets/md-images/image-20220404195018634.png)



## GROUP BY + HAVING

```sql
-- SupplierID, CategoryID 별 평균 가격대 + 평균 가격이 100 이상 (group by 결과물 중에서 $100 이상) + alias 사용
-- where 절을 사용하면 $100 이상인 것들을 가져와서 group by를 실행하기 때문에 다른 결과가 출력된다.

select SupplierID
     , Categoryid
     , AVG(price) as avg_price
from Products
group by SupplierID, CategoryID
having avg_price >= 100
```

![image-20220404195416270](/assets/md-images/image-20220404195416270.png)





## 문제풀이


- 사용 테이블 Employee

![image-20220404204755799](/assets/md-images/image-20220404204755799.png)





#### 01. Top Earners

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
