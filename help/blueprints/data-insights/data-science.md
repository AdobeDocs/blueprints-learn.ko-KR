---
title: 사용자 정의 데이터 과학을 통한 프로필 강화 블루프린트
description: 데이터 과학 기반의 통찰력을  [!DNL Experience Platform] 에 수집하여 실시간 고객 프로필을 보강하는 방법을 알아봅니다.
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 63%

---

# 프로필 강화를 위한 맞춤형 데이터 과학 블루프린트

프로필 강화를 위한 사용자 지정 데이터 과학 블루프린트는 데이터를 사용하여 모델을 교육하고 배포하고 평가하여 데이터 과학 및 기계 학습 도구에서 [!DNL Experience Platform] 및 [!DNL Real-Time Customer Data Platform]에 기계 학습 통찰력을 제공하는 방법을 보여 줍니다.

모델링된 인사이트를 [!DNL Experience Platform]에 수집하여 실시간 고객 프로필을 보강할 수 있습니다. 머신 러닝 인사이트의 예로는 생애 가치 평가, 제품 및 카테고리 관심도, 전환 경향 또는 이탈 경향 등이 있습니다.

## 사용 사례

* 고객 데이터에서 인사이트를 끌어내고 패턴을 발견하며, 이 데이터로 모델을 교육하고 평가합니다.
* 모델 기반 인사이트와 특성으로 [!UICONTROL Real-time Customer Profile]을 강화하여 개인화를 개선하고 여정을 최적화합니다.
* 모델을 훈련 및 사용하여 고객 생애 가치, 전환 또는 이탈 경향, 제품과 콘텐츠 관련성 및 참여도 점수를 확인합니다.

## 아키텍처

<img src="assets/data_science.svg" alt="사용자 정의 데이터 과학을 통한 프로필 강화 블루프린트용 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" />

## 가드레일

* 데이터 과학 결과를 [!DNL Experience Platform]&#x200B;(으)로 수집하는 데 필요한 세부 보호 기능 및 종단 간 지연 시간을 알아보려면 실시간 고객 프로필에서 [배포 보호 기능 문서](../experience-platform/guardrails.md)에 참조된 데이터 수집 보호 기능 및 지연 시간 다이어그램을 참조하십시오.

## 구현 시 고려 사항

* 대부분의 경우 모델 결과는 경험 이벤트가 아니라 프로필 속성으로 수집해야 합니다. 모델 결과는 단순한 속성 문자열일 수 있습니다. 수집할 모델 결과가 여러 개 있는 경우 배열이나 맵 유형 필드를 사용하면 좋습니다.
* 통합 프로필 속성 데이터를 일 단위로 내보낸 일별 프로필 스냅샷 데이터 세트를 활용하여 프로필 속성 데이터에 대한 모델을 교육할 수 있습니다. 프로필 스냅샷 데이터 세트 설명서는 [여기](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=ko#profile-attribute-datasets)에서 확인할 수 있습니다.

## 관련 설명서

* [Adobe [!DNL Experience Platform] 인텔리전스 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe [!DNL Experience Platform] 쿼리 서비스](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ko)

## 관련 블로그 게시물

* [콘텐츠와 커머스 AI: 콘텐츠 인텔리전스로 고객과의 상호 작용 개인화하기](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [Adobe의 탐색적 데이터 분석에 대한 소개 보기 [!DNL Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [Adobe Experience 제품에 머신 러닝을 활용하여 사용자 경험 향상](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [Segmentation.AI: Adobe의 Automated Audience-Clustering-as-a-Service [!DNL Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)