---
layout: post
title: "SQL 데이터 조회와 필터링 : SELECT, ORDER BY 문"
description: >
    SELECT, ORDER BY 문
sitemap: false
categories:
  - sql
  - sqlgrammar 
---

* toc
{:toc .large-only}


>  이 학습은 패스트캠퍼스의 **올인원 패키지 : 모두를 위한 SQL/DB** 강의를 듣고 복습하는 내용입니다.

![img](/assets/md-images/image.png)





# SELECT 문

**:일반적으로 테이블에 저장된 데이터를 가져오는 데 쓰인다. SQL에서 가장 많이 쓰이는 문장이다.**







## SELECT 문법

***SELECT*** COLUMN_1, COLUMN_2, 중략...

***FROM*** TABLE_NAME ;



\>> 만약 모든 컬럼을 다 보고 싶다면 SELELCT *

\>> FROM 추출대상 테이블명

\>> 세미콜론으로 끝내야 함





#### ● SELECT 문 실습 - 전체 컬럼을 조회

```SQL
SELECT
	  *
  FROM
      CUSTOMER;
```

![img](/assets/md-images/image-16456048308942.png)

\>> 잘렸지만, 전체 컬럼이 조회되었다.





## SELECT 문 실습 - 지정한 컬럼을 조회

```SQL
SELECT
	  A.FIRST_NAME, A.LAST_NAME, A.EMAIL
  FROM
  	  CUSTOMER A;
```

![img](/assets/md-images/image-16456048392124.png)

\>> 지정한 컬럼명인 FIRST_NAME, LAST_NAME, EMAIL 컬럼만 가져왔다.

\>> 뒤에 붙은 a는 alias(별명)을 의미한다. alias를 사용하면 코드의 가독성이 좋아지고, sql 성능에도 도움을 준다.

\>> DBMS는 optimizer(최적화기)임으로 sql을 가장 빠르고, 가장 저비용으로 쓰는 것이 좋기에 alias 쓰는 것이 좋다.

---





# ORDER BY 문

 **SELECT문에서 가져온 데이터를 정렬하는데 사용한다. 업무 처리상 매우 중요한 기능이다.**





## ORDER BY 문법

***SELECT*** COLUMN1, COUMN2

***FROM*** TBL_NAME

***ORDER BY*** COLUMN _1 ***ASC***

​                  , COLUMN_2 ***DESC***

\>> SELECT 추출대상 컬럼

\>> FROM 추출 대상 테이블명

\>> COLUMN_1은 오름차순 정렬, COLUMN_2는 내림차순 정렬 (Default는 ASC)





## ORDER BY 실습 
#### ● ASC 정렬
```SQL
SELECT 
		FIRST_NAME
		, LAST_NAME 
	FROM 
		CUSTOMER 
	ORDER BY 
		FIRST_NAME ASC
```

![img](/assets/md-images/image-16456048427086.png)



>> FIRST_NAME이 A부터 오름차순으로 (같은 A이면 둘째자리, 둘째자리까지 같으면 셋째 ....) 나온 것 확인 가능하다.





#### ● DESC 정렬

```SQL
SELECT
		FIRST_NAME
		, LAST_NAME
	FROM
		CUSTOMER
	ORDER BY FIRST_NAME DESC
```

![img](/assets/md-images/image-16456048451928.png)



\>> FIRST_NAME이 Z부터 내림차순으로 나온 것 확인 가능하다.





#### ● ASC + DESC 정렬
  - 컬럼 명시하는 방법

```sql
SELECT
		FIRST_NAME -- ASC -- 오름차순 --순차적
		, LAST_NAME -- DESC -- 내림차순 -- 역순
	FROM
		CUSTOMER
	ORDER BY FIRST_NAME ASC
		   , LAST_NAME DESC 
```

![img](/assets/md-images/image-164560484779610.png)



\>> SQL 결과를 출력시 FIRST_NAME을 오름차순으로, LAST_NAME을 내림차순으로 정렬한다.

- 컬럼 명시 X 방법 (추천 X)

```SQL
SELECT -- 추천하지 않는 방법
		FIRST_NAME -- ASC -- 오름차순 --순차적
		, LAST_NAME -- DESC -- 내림차순 -- 역순
	FROM
		CUSTOMER
	ORDER BY 1 ASC
		   , 2 DESC 
```

![img](/assets/md-images/image-164560484992212.png)



\>> 컬럼 명시하는 방법과 결과가 같다. (ORDER BY 절에 정수를 넣어도 됨 - 1, 2)

