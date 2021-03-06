---
layout: post
title: "SQL 데이터 조회와 필터링 : SELECT DISTINCT 문"
description: >
    SELECT DISTINCT 문
sitemap: false
categories:
  - sql
  - sqlgrammar 
---

* toc
{:toc .large-only}


>  이 학습은 패스트캠퍼스의 **올인원 패키지 : 모두를 위한 SQL/DB** 강의를 듣고 복습하는 내용입니다.


![img](/assets/md-images/image-16456048631391.png)

 



## SELECT DISTINCT 문법

![img](/assets/md-images/image-16456048830343.png)

\>> COLUMN_1의 값이 중복 값 존재 시 중복 값 제거

![img](/assets/md-images/image-16456048844635.png)



\>> COLUMN_1 + COLUUMN_2의 값이 중복 값 존재 시 중복 값을 제거

![img](/assets/md-images/image-16456048861017.png)

\>> COLUMN_1 + COLUUMN_2의 값이 중복 값 존재 시 중복 값을 제거

\>> 결과를 명확하게 하기 위해 ORDER BY 절 사용





## SELECT DISTINCT 실습





#### ● 테이블 생성 & INSERT

\- 쿼리문

```SQL
CREATE TABLE T1 ( ID SERIAL NOT NULL PRIMARY KEY, BCOLOR VARCHAR, FCOLOR VARCHAR );

INSERT
  INTO T1 (BCOLOR, FCOLOR)
VALUES
         ('red', 'red')
       , ('red', 'red')
       , ('red', NULL)
       , (NULL, 'red')
       , ('red', 'green')
       , ('red', 'blue')
       , ('green', 'red')
       , ('green', 'blue')
       , ('green', 'green')
       , ('blue', 'red')
       , ('blue', 'green')
       , ('blue', 'blue')
;

COMMIT; 
```

\>> COMMIT 은 나중에 배울 것인데, 이 테이블에 이 데이터를 집어넣을 거라는 의미!(INSERT문 한다음에 필요)

​     -> 하지만 위의 CREATE TABLE 에는 필요없는 이유는 테이블생성은 DDL로 치는 순간에 바로 적용되기 때문

\## 테이블을 날리고 싶으면 *DROP TABLE T1;* 하면 된다



-  *SELECT \* FROM T1* 의 결과

![img](/assets/md-images/image-16456048887429.png)





#### ● DISTINCT 사용 + 컬럼 1개



\- 쿼리문

```sql
SELECT
    DISTINCT BCOLOR
FROM
    T1
ORDER BY
    BCOLOR
```



\- 실행결과

![img](/assets/md-images/image-164560489079111.png)

\>> 중복이 제거된 BCOLOR 컬럼의 값이 출력되었다.

\>> ORDER BY BCOLOR 로 인해 BCOLOR값 기준으로 알파벳 순으로 정렬된 결과 (A가 가장먼저, NULL값은 가장 뒤)





#### ● DISTINCT 사용 + 컬럼 2개



\- 쿼리문

```sql
SELECT
    DISTINCT BCOLOR, FCOLOR
FROM
    T1
ORDER BY
    BCOLOR, FCOLOR;
```

\- 실행 결과

![img](/assets/md-images/image-164560489321613.png)

\>> [RED | RED] 만 사라졌다.





#### ● DISTINCT 사용 + 컬럼 2개 + ON 사용



\- 쿼리문

```sql
SELECT
      DISTINCT ON (BCOLOR) BCOLOR
   ,  FCOLOR
FROM
    T1
ORDER BY
    BCOLOR, FCOLOR;
```

\- 실행 결과

![img](/assets/md-images/image-164560489498815.png)

\>> DISTINCT ON (BCOLOR) 는 BCOLOR 기준으로 중복 제거되게 하겠다는 뜻이다.

​     -> 따라서, BCOLOR NULL값 하나, red값 중 하나, green값 중 하나, blue값 중 하나가 나온것이다.

\>> FCOLOR의 값이 NULL값 제외하고 blue인 이유는 ORDER BY로 오름차순 정렬했기 때문이다.

​     -> 아래 그림처럼 bcolor의 red/green/blue 값중 blue가 가장 앞쪽의 알파벳이다.

​          NULL은 FCOLOR가 red 밖에 없기 때문에 그대로 나온 것

![img](/assets/md-images/image-164560489643517.png)





#### ●DISTINCT 사용 + 컬럼 2개 + ON 사용 + DESC 정렬



\- 쿼리문

```sql
SELECT
      DISTINCT ON (BCOLOR) BCOLOR
   ,  FCOLOR
FROM
    T1
ORDER BY
    BCOLOR, FCOLOR DESC;
```

\- 실행 결과

![img](/assets/md-images/image-164560489813619.png)

\>> 마찬가지로 DISTINCT ON (BCOLOR)로 BCOLOR 기준으로 중복제거 되었다.

\>> 다른 점은 내림차순이기 때문에 FCOLOR값이 RED아니면 NULL이 나옴

​      -> 내림차순이면 NULL이 젤 먼저인데 NULL을 가진 BCOLOR는 red밖에 없음.





#### ● DISTINCT 사용 + 컬럼 2개 + ON 사용 + 두 컬럼 모두 DESC 정렬

DISTINCT ON 사용한 두 실습은 전부 *ORDER BY BCOLOR, FCOLOR desc;* 라서 BCOLOR는 오름차순이다.

하지만 아래처럼 바꾸면 둘 다 내림차순 가능.





\- 쿼리문

```sql
SELECT
      DISTINCT ON (BCOLOR) BCOLOR
   ,  FCOLOR
FROM
    T1
ORDER BY
    BCOLOR DESC, FCOLOR DESC;
```

\- 실행 결과

![img](/assets/md-images/image-164560490056121.png)

