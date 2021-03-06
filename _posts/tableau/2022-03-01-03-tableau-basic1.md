---
layout: post
title: "태블로 기본 컨셉 이해(1)"
subtitle: 측정값과 차원, 막대차트
description: >
    edwith [데이터 시각화를 위한 태블로] 강의를 참고했습니다.
sitemap: false
categories:
  - tableau
tags:
  - [Tableau, data_visualization, edwith강의]
---

* toc
{:toc .large-only}




## 태블로 기본 컨셉 이해(1)





### 측정값과 차원

- 측정값
  - 숫자 형식
  - 액션(drag-drop 또는 double-click)을 통해
  - 설정된 **집계**에 따라
  - 차트를 만들게 된다.
- 차원
  - 숫자들로 만들어진 차트를
  - 어떻게 나눠서 볼 것인가를 결정한다.





### 막대차트





- 막대차트 만드는 이유?
  - 만들기 쉽다.
  - 항목별로 나눠서 보는데 적합
  - 카테고리(범주), 순위, 추세를 보는데 유용하다.





- 막대차트 만드는 방식
  - 태블로 에서는 측정값에 있는 데이터 원본 필드 중 초록색 연속형 필드(지리적 역할인 위도, 경도는 제외)를 더블 클릭하면 기본적으로 막대 차트가 만들어진다.
  - 기본적으로는 집계방식(합계,평균 등)을 통해 우선 차트를 만들고 이것을 분할해서 보는 기준은 차원의 값으로 결정되는데, 그 출발은 막대 차트부터 시작하게 된다.





#### 막대차트 만들기

![image-20220327203411776](/assets/md-images/image-20220327203411776.png)





- 행 = 합계(매출), 열=제품 중분류

  ![image-20220327202557031](/assets/md-images/image-20220327202557031.png)

  - 만약 평균 매출을 보고 싶다면 매출 마우스 우측클릭 -> 기본속성 -> 집계 -> 평균 click

  ![image-20220327203613566](/assets/md-images/image-20220327203613566.png)





- 마크 레이블 표시 설정

![image-20220327202736081](/assets/md-images/image-20220327202736081.png)





- 보기 설정 = 전체보기

![image-20220327202839522](/assets/md-images/image-20220327202839522.png)





- 매출 내림차순 정렬

![image-20220327204229610](/assets/md-images/image-20220327204229610.png)





- 계산된 필드 만들기 => 평균 이상 미만 구분
  - 데이터 빈공간 마우스 우클릭 -> 계산된 필드 만들기 click -> 수식 작성 -> 만들어진 계산된 필드를 [마크]의 [색상]탭에 drag&drop

![image-20220327203017790](/assets/md-images/image-20220327203017790.png)





- 평균 라인 추가

  - 분석 탭으로 가서 평균라인을 drag -> 테이블로 drop

  ![image-20220327203224180](/assets/md-images/image-20220327203224180.png)

  ![image-20220327203239265](/assets/md-images/image-20220327203239265.png)

  