---
layout: post
title: "집계함수"
description: >
    Infrean 데이터 분석을 위한 중급 SQL 강의 복습 정리
sitemap: false
tags:
  - [SQL, data_analytics, MySQL,Infrean]
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

