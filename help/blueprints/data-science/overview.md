---
title: 프로파일 데이터 활용 청사진을 위한 맞춤형 데이터 과학
description: 이 블루프린트는 Adobe Experience Platform의 데이터 과학 작업 영역에서 Experience Platform 내의 데이터를 사용하여 모델을 트레이닝, 배포 및 점수로 지정하여 데이터를 통해 머신 러닝 인사이트를 제공하는 방법을 보여줍니다.
solution: Experience Platform, Data Collection
kt: 7203
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---


# 프로파일 데이터 활용 청사진을 위한 맞춤형 데이터 과학

이 블루프린트는 Adobe Experience Platform의 데이터를 머신 러닝 인사이트를 제공하기 위해 데이터 과학 작업 공간에서 모델을 트레이닝, 배포 및 평가하는 데 사용하는 방법을 보여줍니다. 이러한 모델은 실시간 고객 프로파일을 위해 활성화된 데이터 세트에 직접 출력할 수 있습니다. 머신 러닝 인사이트의 예로는 라이프타임 가치, 제품 및 카테고리 관련성, 전환율 성향 또는 이탈률 등이 있습니다.

## 사용 사례

* Experience Platform의 고객 데이터에서 인사이트를 추출하고 패턴을 발견합니다. 이 데이터에서 모델을 트레이닝하고 점수를 매길 수 있습니다.
* 보다 세분화된 개인화와 최적화된 여정 최적화를 위해 모델 기반의 통찰력과 속성을 통해 실시간 고객 프로파일을 강화할 수 있습니다.
* 고객 라이프타임 가치, 전환율 또는 이탈률, 제품 및 컨텐츠 친화성, 참여 점수 등 고객 인사이트를 도출할 수 있는 트레이닝 및 점수 모델을 제공합니다.

## 시나리오

| 시나리오 | 시나리오 설명 | Experience Cloud 애플리케이션 |
|---|---|---|
| 탐구적 데이터 과학 | <ul><li>신호와 완벽성, 데이터의 정확성 파악</li><li>데이터 과학 툴을 사용하여 새로운 인사이트 발견</li></ul> | <ul><li>Experience Platform 인텔리전스</li></ul> |
| AI/ML<br>로 프로파일 강화 - 일괄 처리 | <ul><li>모델을 검색, 저작, 트레이닝, 배포, 점수 및 운영</li><li>프로필 또는 데이터 레이크에 대한 푸시 모델 예측을 통해 일괄적으로 활성화할 수 있습니다.</li></ul> | <ul><li>Experience Platform 인텔리전스</li></ul> |

## 아키텍처

<img src="assets/datascience.svg" alt="프로파일 연계 데이터 청사진을 위한 참조구조" style="border:1px solid #4a4a4a" />

## 구현 단계

1. 스키마 및 데이터 세트를 만듭니다.
1. 데이터를 Experience Platform으로 인제스트
1. DSW 전자 필기장을 만듭니다.
1. 언어를 선택합니다. Python 및 PySpark가 지원됩니다.
1. 노트북의 작성자 모델.
1. 모델 트레이닝
1. 모델을 점수를 매겨 대상 데이터로 예측을 생성합니다.
1. 모델 결과를 실시간 고객 프로필에 푸시하는 경우 프로필에 대한 모델 결과 데이터 세트를 활성화합니다.

## 관련 설명서

* [Adobe Experience Platform Intelligence 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [데이터 과학 작업 공간 설명서](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=en)
* [데이터 과학 작업 공간 자습서](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-science-workspace/understanding-data-science-workspace.html)

## 관련 블로그 게시물

* [Adobe 플랫폼 경험으로 데이터 과학 라이프사이클 간소화](https://medium.com/adobetech/simplifying-the-data-science-lifecycle-with-adobe-platform-experience-8ea4f056d82f)
* [콘텐츠 및 상거래 AI:콘텐츠 인텔리전스를 통해 고객과의 인터랙션 개인화](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [데이터 과학 작업 영역을 사용하여 이탈에 대한 심도 있는 이해](https://medium.com/adobetech/gaining-a-deeper-understanding-of-churn-using-data-science-workspace-18a2190e0cf3)
* [Adobe Experience Platform의 데이터 과학 이해](https://medium.com/adobetech/understanding-data-science-in-adobe-experience-platform-5bce5a17b42)
* [Adobe Experience Platform에 대한 예비 데이터 분석 소개](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [머신 러닝을 통한 Adobe Experience 제품 개발, 사용자 경험 향상](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Adobe Experience Platform의 규모에 따른 데이터과학에 대한 XDM 데이터 모델링](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7)
* [세그멘테이션.AI:Adobe Experience Platform의 자동 고객 클러스터링-as-a-Service](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)
* [엔터프라이즈 규모의 Jupiter 노트북 재구성](https://medium.com/adobetech/reimagining-jupyter-notebooks-for-enterprise-scale-8bc6340d504a)
* [Adobe Experience Platform Data Science 작업 공간을 사용하여 지능적인 통찰력 향상](https://medium.com/adobetech/accelerate-intelligent-insights-with-adobe-experience-platform-data-science-workspace-89538bacbbea)
* [Adobe Experience Platform을 사용한 시계열 예측 미리 보기](https://medium.com/adobetech/preview-of-time-series-forecasting-with-adobe-experience-platform-38a2fc778e89)
* [머신 러닝을 통한 Adobe Experience 제품 개발, 사용자 경험 향상](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)


