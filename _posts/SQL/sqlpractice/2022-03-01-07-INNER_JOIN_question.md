---
layout: post
title: "INNER JOIN 문제풀이"
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

- 01-03 사용 테이블(CITY, COUNTRY)

![image-20220405142819781](/assets/md-images/image-20220405142819781.png)

![image-20220405142830650](/assets/md-images/image-20220405142830650.png)





## 01. African Cities

- Given the **CITY** and **COUNTRY** tables, query the names of all cities where the *CONTINENT* is *'Africa'*.

  **Note:** *CITY.CountryCode* and *COUNTRY.Code* are matching key columns.

```sql
-- 내 문제 풀이(정답)
SELECT CITY.NAME
FROM CITY 
	 INNER JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE
WHERE CONTINENT = 'Africa';
```





## 02. Population Census

- Given the **CITY** and **COUNTRY** tables, query the sum of the populations of all cities where the *CONTINENT* is *'Asia'*.

  **Note:** *CITY.CountryCode* and *COUNTRY.Code* are matching key columns.

```sql
-- 내 문제 풀이(정답)
SELECT SUM(CITY.POPULATION)
FROM CITY 
	 INNER JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE
WHERE CONTINENT = 'Asia'



```





## 03. Average Population of Each Continent

- Given the **CITY** and **COUNTRY** tables, query the names of all the continents (*COUNTRY.Continent*) and their respective average city populations (*CITY.Population*) rounded *down* to the nearest integer.

  **Note:** *CITY.CountryCode* and *COUNTRY.Code* are matching key columns.

```sql
-- 내 문제 풀이(정답)
SELECT COUNTRY.CONTINENT
	 , FLOOR(AVG(CITY.POPULATION))
FROM CITY 
	 INNER JOIN COUNTRY ON CITY.COUNTRYCODE = COUNTRY.CODE
GROUP BY COUNTRY.CONTINENT;
```
