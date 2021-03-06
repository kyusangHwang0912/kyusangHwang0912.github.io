---
layout: post
title: "상관 관계 분석"
subtitle:  분산형 차트, 데이터 설명, 매개 변수 적용
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




##  상관 관계 분석





### 01. 분산형 차트

- 측정값 간의 관계를 파악하기 위한 시각화 방식
- 열 선반과 행 선반에 각각 측정값을 배치하면 자동적으로 분산형 차트가 만들어진다.
- 열 선반과 행 선반에 올리는 필드를 고정적으로 배치가 가능하지만, 좀 더 자유도를 주기 위해서는 별도의 매개 변수를 만들어 매개 변수 안의 값에 따라서 분산형 차트를 다양하게 활용할 수 있다.



#### 01-1. 분산형 차트 예시

![image-20220414133957584](/assets/md-images/image-20220414133957584.png)



- 측정값

  - 수익

  - 할인율
    - 집계 : 평균
    - 백분율 : 소수점 첫째짜리까지

- 마크

  - 원
  - 색상
    - 불투명도 : 70%
    - 테두리 : 흰색으로 변경
    - 색상 범례 : 합계(수익)

- 분석패널

  - 추세선
    - 선형 추세







### 02. 데이터 설명

- AI의 힘을 활용하여 뷰 내의 특정 요소를 설명함으로써 기존에 찾지 못했던 왜(why)를 발견하도록 도와주는 기능
- 고객 통계 모델인 베이지안 방법론을 기반으로 통계적으로 의미 있는 설명 제공, 일반적인 추세에서 벗어나 막연한 질문에 대한 대답 대신 궁극적인 원인을 찾도록 도움을 줌





#### 02-1. 데이터 설명 예시



- 분산형 차트에서 떨어져 있는 데이터 클릭 후 데이터 설명 클릭

![image-20220414134517197](/assets/md-images/image-20220414134517197.png)





- 합계(수익) 설명에서 극한값이 있다는 설명 정보 확인 가능

  - 각 설명을 워크시트로 열 수 있다.

![image-20220414134915806](/assets/md-images/image-20220414134915806.png)

- 워크시트로 자세히 보기 결과(이 설명 외에도 다양한 설명 존재)

![image-20220414135017577](/assets/md-images/image-20220414135017577.png)









### 03. 매개 변수 적용

- 분산형 차트에 매개 변수를 적용하여 해당 값에 따라 기준을 충족한 마크만 별도의 색상으로 표시 가능
- 상수 값을 동적인 값으로 변경해주는 기능이 바로 매개 변수이다.
- 매개 변수는 혼자서 쓰일 수 없고, 반드시 계산된 필드, 필터 도는 참조선하고 엮일 대만 화면을 동적인 값으로 변경해주는 기능이다.
- 매개 변수를 잘 활용하면 태블로를 효율적으로 잘 활용할 수 있다.





#### 03-1. 매개 변수 적용 예시

![image-20220414140227057](/assets/md-images/image-20220414140227057.png)



##### 03-1-1. 과정

- 매개 변수 생성

![image-20220414135331846](/assets/md-images/image-20220414135331846.png)



- p. 할인율, p. 수익율에 관한 매개 변수 생성

  - 허용 가능한 값을 범위로 변경 -> 최소값, 최대값, 단계 크기 설정

![image-20220414135430143](/assets/md-images/image-20220414135430143.png)

![image-20220414135450611](/assets/md-images/image-20220414135450611.png)



3. 매개 변수 표시

![image-20220414135606012](/assets/md-images/image-20220414135606012.png)



4. 집합 생성 후 색상 마크에 넣기

![image-20220414135653108](/assets/md-images/image-20220414135653108.png)

![image-20220414135812552](/assets/md-images/image-20220414135812552.png)



5. 분석 패널의 참조선 추가(테이블) & 설정 변경 (가로축: p. 수익 매개변수, 세로축:p. 할인율 매개변수)

![image-20220414140039849](/assets/md-images/image-20220414140039849.png)

![image-20220414140122821](/assets/md-images/image-20220414140122821.png)



6. 결과 : 오른쪽 매개변수를 통해 범위 지정 가능

![image-20220414140208510](/assets/md-images/image-20220414140208510.png)
