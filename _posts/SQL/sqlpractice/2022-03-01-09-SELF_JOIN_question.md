---
layout: post
title: "SELF JOIN 문제풀이"
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


## 01. 181 - Employees Earning More Than Their Managers

- 활용 테이블 (Employee)

![image-20220405150952319](/assets/md-images/image-20220405150952319.png)

- Write an SQL query to find the employees who earn more than their managers.

  Return the result table in **any order**.

```sql
-- 내 문제 풀이(정답)
SELECT E1.name AS Employee
FROM Employee E1 
	 INNER JOIN Employee E2 ON E1.managerId = E2.id
WHERE E1.salary > E2.salary;

/*
## 아래와 같이 적절한 Alias 사용하면서 확인해가는 과정을 거치는 것이 좋다.
*/
SELECT Employee.name AS employee_name
     , Employee.Salary AS employee_salary
     , Manager.name AS manager_name
     , Manager.Salary AS manager_salary
FROM Employee INNER JOIN Employee as Manager ON Employee.managerid = Manager.id;
S
/*
## 결과
["employee_name", "employee_salary", "manager_name", "manager_salary"]
["Joe", 70000, "Sam", 60000]   -- 이 부분이 뽑아야 할 데이터(Joe)
["Henry", 80000, "Max", 90000]
*/
```





## 02. 197 - Rising Temperature

- 활용 테이블(Weather)

![image-20220405151817237](/assets/md-images/image-20220405151817237.png)



- Write an SQL query to find all dates' `Id` with higher temperatures compared to its previous dates (yesterday).

  Return the result table in **any order**.

```sql
-- 내 문제 풀이(오답 : DATETIME 계산 오류)
SELECT W1.id
FROM Weather W1 INNER JOIN Weather W2 ON W1.recordDate = W2.recordDate + 1
WHERE W1.temperature > W2.temperature;


/*
## 오답이유 : Datetime 값은 +1 로 데이트 더할 수 없다(아래 시간 더하기, 빼기 방식 사용해야(DATE_ADD, DATE_SUB))
## 또한, 1번과 마찬가지로 적절한 Alias 쓰는게 덜 헷갈리다!
*/

SELECT today.id as id
FROM Weather today 
     INNER JOIN Weather yesterday ON today.recordDate = DATE_ADD(yesterday.recordDate, INTERVAL 1 DAY)
WHERE today.temperature > yesterday.temperature;



```



#### MySQL 시간 더하기, 빼기

- DATE_ADD(기준날짜, INTERVAL)
  - SELECT DATE_ADD(NOW(), INTERVAL 1 SECOND)
  - SELECT DATE_ADD(NOW(), INTERVAL 1 MINUTE)
  - SELECT DATE_ADD(NOW(), INTERVAL 1 HOUR)
  - SELECT DATE_ADD(NOW(), INTERVAL 1 DAY)
  - SELECT DATE_ADD(NOW(), INTERVAL 1 MONTH)
  - SELECT DATE_ADD(NOW(), INTERVAL 1 YEAR)
  - SELECT DATE_ADD(NOW(), INTERVAL -1 YEAR) -- SUB 기능이 되는것

- DATE_SUB(기준날짜, INTERVAL)
  - SELECT DATE_SUB(NOW(), INTERVAL 1 SECOND)
