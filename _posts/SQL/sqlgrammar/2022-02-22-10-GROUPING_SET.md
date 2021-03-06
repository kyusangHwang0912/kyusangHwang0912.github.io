---
layout: post
title: "SQL과 데이터베이스 - 조인과 집계 데이터 : GROUPING SET 절"
description: >
    GROUPING SET 절
sitemap: false
categories:
  - sql
  - sqlgrammar 
---

* toc
{:toc .large-only}



> 이 학습은 패스트캠퍼스의 **올인원 패키지 : 모두를 위한 SQL/DB** 강의를 듣고 복습하는 내용입니다.

![image](https://user-images.githubusercontent.com/80219821/151759809-56256e05-32d6-49ed-be3d-35305839f4de.png)



## GROUPING SET 절 설명 및 특징

- 집계기준을 달리하여 집계값을 나타낼 수 있는 집계 절이다.
- GROUPING SET 절을 사용하여 여러 개의 UNION ALL을 이용한 SQL과 같은 결과를 도출할 수 있다.
  - UNION ALL을 활용하여 여러 SQL문을 붙이는 방식이 아니라 더 성능이 좋고 깔끔하게 문장을 만들 수 있다.





## GROUPING SET 절 실습 준비 - GROUP BY 절

```sql
-- 테이블 생성 및 값 INSERT
CREATE TABLE SALES 
(
BRAND VARCHAR NOT NULL,
SEGMENT VARCHAR NOT NULL,
QUANTITY INT NOT NULL,
PRIMARY KEY (BRAND, SEGMENT)
);

INSERT INTO SALES (BRAND, SEGMENT, QUANTITY)
VALUES
  ('ABC', 'Premium', 100)
, ('ABC', 'Basic', 200)
, ('XYZ', 'Premium', 100)
, ('XYZ', 'Basic', 300);

COMMIT;

SELECT * FROM sales; 
```

![image](https://user-images.githubusercontent.com/80219821/151760345-638e3214-37eb-4fa6-a26c-c364be828d38.png)





## GROUPING SET 절 학습 전 준비1 - GROUP BY 집계

- 2개 컬럼 GROUP BY 절

```sql
SELECT
	  BRAND,
	  SEGMENT,
	  SUM(QUANTITY)			-- GROUP BY 후 QUANTITIY 컬럼의 합계를 구한다.
  FROM
	  SALES					-- SALES 테이블을 조회한다.
GROUP BY BRAND, SEGMENT;	-- BRAND와 SEGMENT 컬럼 기준으로 GROUP BY 한다.
```

![image](https://user-images.githubusercontent.com/80219821/151760541-48e1e937-2548-49dd-b13f-be0b0d21e75e.png)





- 1개 컬럼 GROUP BY 절

```sql
SELECT
	  BRAND,
	  SUM(QUANTITY)		-- GROUP BY 후 QUANTITY 컬럼의 함계를 구한다.
  FROM
	  SALES				-- SALES 테이블을 조회한다.
GROUP BY BRAND;			-- BRAND 컬럼 기준으로 GROUP BY 한다.
```

![image](https://user-images.githubusercontent.com/80219821/151760885-b851d445-e69f-4e13-aac0-2a21ccfe3f8c.png)





- 전체 합계 구하기

```sql
SELECT
	  SUM(QUANTITY)		-- QUANTITY 컬럼의 합계를 구한다.
  FROM
	  SALES;			-- SALES 테이블을 조회한다.
```

![image](https://user-images.githubusercontent.com/80219821/151761001-58ee4cf9-eb0d-4efa-88d7-0eb57f5a66b0.png)





## GROUPING SET 절 학습 전 준비1 - UNION ALL 활용

- UNION ALL을 이용하여 [BRAND, SEGMENT 기준],[BRAND 기준], [SEGMENT기준], [전체 기준]으로 QUANTITY 합계를 값을 구할 수 있다.

```sql
SELECT BRAND, SEGMENT, SUM(QUANTITY)
FROM SALES
GROUP BY BRAND, SEGMENT
UNION ALL
SELECT BRAND, NULL, SUM(QUANTITY)
FROM SALES
GROUP BY BRAND
UNION ALL
SELECT NULL, SEGMENT, SUM(QUANTITY)
FROM SALES
GROUP BY SEGMENT
UNION ALL 
SELECT NULL, NULL, SUM(QUANTITY)
FROM SALES;

-- 동일한 테이블을 4번씩이나 일공 있다 => 성능저하 가능성이 존재
-- 너무 SQL문이 길어진다 -> 복잡 -> 유지보수 용이하지 않음!(최초 개발자 말고는 보고 분석하기 싶지 않음)
```

![image](https://user-images.githubusercontent.com/80219821/151761262-c7217786-ff49-4778-a159-794abf3bcfd7.png)







## GROUPING SET 절 문법

```sql
SELECT
	  C1,
	  C2,
	  집계함수(C3)
  FROM
	  TABLE_NAME
GROUP BY
GROUPING SETS 		-- GROUPING SET절을 이용하면 한번에 다양한 기준의 컬럼 조합으로 집계를 구할 수 있다.
(	(C1,C2),
	(C1),
	(C2),
	()
	);
```







## GROUPING SET 절 실습



- GROUPING SET절을 이용하여 [BRAND, SEGMENT 기준],[BRAND 기준], [SEGMENT기준], [전체 기준]으로 QUANTITY 합계를 값을 구할 수 있다.

```sql
-- GROUP BY의 결과 값 중에서 SUM(AMOUNT)가 200을 초과하는 행을 출력한다.

SELECT BRAND, SEGMENT, SUM(QUANTITY)
  FROM SALES
GROUP BY
GROUPING SETS 
(
	(BRAND, SEGMENT), 	-- BRAND,SEGMENT 기준
	(BRAND),			-- BRAND 기준	
	(SEGMENT),			-- SEGMENT 기준
	()					-- 전체 기준
);

-- UNION ALL과 순서는 좀 다르지만 같은 결과이다.(ORDER BY로 설정가능)
```

![image](https://user-images.githubusercontent.com/80219821/151761502-f2225846-b5fc-4876-aed1-9639efad3942.png)







- GROUPING 함수를 활용하여 집계기준이 무엇이냐를 직관적으로 보여줄 수 있다.

```sql
SELECT
	GROUPING(BRAND) GROUPING_BRAND,		-- 해당 컬럼이 집계에 사용되었으면 0, 그렇지 않으면 1을 리턴한다.
	GROUPING(SEGMENT) GROUPING_SEGMENT,
	BRAND,
	SEGMENT,
	SUM(QUANTITY)
FROM
	SALES
GROUP BY
GROUPING SETS 
(	(BRAND,SEGMENT),
	(BRAND),
	(SEGMENT),
	() )
ORDER BY BRAND,SEGMENT;
```

![image](https://user-images.githubusercontent.com/80219821/151761809-c3bca0e0-d2c3-4b21-9ff0-6776731ea94f.png)







- case when ~ then 절을 활용하여 데이터를 좀 더 예쁘게 뽑을 수 있다.

```sql
SELECT
		CASE WHEN GROUPING(BRAND) = 0 AND GROUPING(SEGMENT) = 0 THEN '브랜드별+등급별'
			 WHEN GROUPING(BRAND) = 0 AND GROUPING(SEGMENT) = 1 THEN '브랜드별'
		     WHEN GROUPING(BRAND) = 1 AND GROUPING(SEGMENT) = 0 THEN '등급별'
			 WHEN GROUPING(BRAND) = 1 AND GROUPING(SEGMENT) = 1 THEN '전체합계'
			 ELSE '' 
			 END AS "집계기준"	
     , BRAND
     , SEGMENT
     , SUM (QUANTITY)
 FROM
      SALES
GROUP BY
GROUPING SETS 
( 
  (BRAND, SEGMENT)
, (BRAND)
, (SEGMENT)
, () 
)
ORDER BY BRAND, SEGMENT;
```

![image](https://user-images.githubusercontent.com/80219821/151761981-1ee49fd4-b0b9-436a-b642-923eca99d116.png)

