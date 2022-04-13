---
layout: post
title: "집계함수"

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
## COUNT

추출되는 행의 개수

- COUNT(*)
  - NULL 포함

- COUNT(COLUMN_NAME)
  - NULL 제외

- COUNT(DISTINCT COLUMN_NAME)
  - NULL 제외 + 중복값 제외




## SUM, AVG

SUM:합계, AVG:평균

- AVG(COLUMN_NAME)
  - NULL 제외해서 평균
- SUM(COLUMN_NAME)/COUNT(*)
  - NULL 포함해서 평균(NULL을 0으로 본다)



## MIN, MAX

MIN: 최소값, MAX:최대값





## 문제풀이





- 01~04 사용 테이블 CITY

![image-20220404202121078](/assets/md-images/image-20220404202121078.png)





#### 01. Revising Aggregations - Averages

- Query the average population of all cities in **CITY** where *District* is **California**

```sql
-- 내 문제 풀이
SELECT AVG(POPULATION)
FROM CITY
WHERE DISTRICT = 'California';

-- 정답
```



#### 02. Revising Aggregations - The Sum Function

- Query the total population of all cities in **CITY** where *District* is **California**.

```sql
-- 내 문제 풀이
SELECT SUM(POPULATION)
FROM CITY
WHERE DISTRICT = 'California';

-- 정답
```



#### 03. Revising Aggregations - The Count Function

- Query a *count* of the number of cities in **CITY** having a *Population* larger than 100,000.

```sql
-- 내 문제 풀이
SELECT COUNT(*)
FROM CITY
WHERE POPULATION > 100000;

-- 정답
-- COUNT(ID) 라고 해도 상관없다.
```



#### 04. Average Population

- Query the average population for all cities in **CITY**, rounded *down* to the nearest integer.

```sql
-- 내 문제 풀이
SELECT ROUND(AVG(POPULATION),0)
FROM CITY;

-- 정답
-- 버림 써도 된다.
CEIL(숫자) -- 올림
FLOOR(숫자) -- 내림
ROUND(숫자, 표현할 자리 수) -- 반올림
```



#### 05. Population Density Difference

- Query the difference between the maximum and minimum populations in **CITY**.

```sql
-- 내 문제 풀이
SELECT MAX(POPULATION) - MIN(POPULATION)
FROM CITY;

-- 정답
```



#### 06. Weather Observation Station 4

![image-20220404202715583](/assets/md-images/image-20220404202715583.png)

- Find the difference between the total number of **CITY** entries in the table and the number of distinct **CITY** entries in the table.

```sql
-- 내 문제 풀이
SELECT COUNT(*) - COUNT(DISTINCT CITY)
FROM STATION;

-- 정답
-- 하지만 CITY 수를 세라고 했으므로 COUNT(CITY) 해주는게 더 정확하다.
```



