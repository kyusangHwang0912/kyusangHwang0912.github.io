---
layout: post
title: "SQL 데이터 조회와 필터링 실습"
description: >
    SQL 데이터 조회와 필터링 실습
sitemap: false
categories:
  - sql
  - sqlgrammar
related_posts:
  - _posts/sql/sqlgrammar/2022-02-21-01-SELECT,ORDER_BY.md  
---

* toc
{:toc .large-only}

> 이 학습은 패스트캠퍼스의 **올인원 패키지 : 모두를 위한 SQL/DB** 강의를 듣고 복습하는 내용입니다.

![img](/assets/md-images/image-16456063228991.png)

## 실습 1

#### ● 문제 : PAYMENT 테이블에서 단일 거래의 AMOUNT의 액수가 가장 많은 고객들의 CUSTOMER_ID를 추출하라.

​          단, CUSTOMER_ID의 값은 유일해야 한다.





1) 가장 큰 AMOUNT 값 추출





\- 쿼리문

```sql
SELECT 
	  K.AMOUNT 
  FROM 
	  PAYMENT K
ORDER BY K.AMOUNT DESC
LIMIT 1
```

\- 실행 결과

![img](/assets/md-images/image-16456063343973.png)





2) 1번의 결과를 IN으로 넣어서 CUSTOMER_ID 유일하게 추출



\- 쿼리문

```sql
SELECT 
	   DISTINCT CUSTOMER_ID 
  FROM PAYMENT 
 WHERE AMOUNT = 
				(
				  SELECT 
					     AMOUNT 
				    FROM PAYMENT 
				ORDER BY AMOUNT DESC
				   LIMIT 1
				)
;
```



\- 실행 결과

![img](/assets/md-images/image-16456063439175.png)

\>> ***AMOUNT IN*** 이 아닌 ***AMOUNT =*** 으로 서브쿼리를 작성해도 된다.





3) ALIAS 지정해준다. (가독성!)

```sql
SELECT 
	   DISTINCT A.CUSTOMER_ID 
  FROM PAYMENT A
 WHERE A.AMOUNT = 
				(
				  SELECT 
					     K.AMOUNT 
				    FROM PAYMENT K
				ORDER BY K.AMOUNT DESC
				   LIMIT 1 --LIMIT절
				)
```



\>> 결과는 위에 결과와 같으나, AMOUNT가 여러개 나옴으로 헷갈릴 수가 있다.

​     따라서, 가독성을 위해 ALIAS를 지정해주는 것이 좋다!





---





## 실습 2

#### ● 문제 : 고객들에게 단체 이메일을 전송 하고자 한다.

​          CUSTOMER 테이블에서 고객의 EMAIL 주소를 추출하고, 이메일 형식에 맞지 않는 이메일 주소 제외시켜라.

​          이메일 형식을 '@'가 존재해야 하고, '@'로 시작하지 말아야 하고 '@'로 끝나지 말아야 한다.





\# LIKE 연산자 사용하여 해결

```sql
SELECT
	  EMAIL
  FROM
	  CUSTOMER
 WHERE
	  EMAIL LIKE '%@%'
  AND EMAIL NOT LIKE '@%'
  AND EMAIL NOT LIKE '%@' ;
```

![img](/assets/md-images/image-16456063548247.png)

