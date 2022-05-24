---
title: 사용자 정의 데이터 과학을 통한 프로필 강화 블루프린트
description: 이 블루프린트에서는 Adobe Experience Platform의 Data Science Workspace에서 Experience Platform 내 데이터를 사용해 머신 러닝 인사이트를 제공할 수 있는 모델을 훈련, 배포 및 사용하는 방법을 보여 줍니다.
solution: Data Collection
kt: 7203
exl-id: e5ec6886-4fa4-4c9b-a2d8-e843d7758669,f0efaf3c-6c4f-47c3-ab8a-e8e146dd071c
source-git-commit: 56ed25f8ed954126c3291559b7f67f04565c01d4
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 48%

---

# 사용자 정의 데이터 과학을 통한 프로필 강화 블루프린트

프로필 데이터 보강 블루프린트를 위한 사용자 지정 데이터 과학을 통해 데이터 과학 및 시스템 학습 도구에서 Adobe Experience Platform의 데이터를 사용하여 Experience Platform 및 Real-time Customer Data Platform에 대한 기계 학습 인사이트를 제공하고, 모델을 교육, 배포 및 점수 책정 하는 방법을 보여줍니다. 모델링된 인사이트를 Experience Platform에 수집하여 실시간 고객 프로필을 보강할 수 있습니다. 머신 러닝 인사이트의 예로는 생애 가치 평가, 제품 및 카테고리 관심도, 전환 경향 또는 이탈 경향 등이 있습니다.

## 사용 사례

* 이 데이터에서 고객 데이터, 교육 및 점수 모델에서 인사이트를 추출하고 패턴을 발견합니다.
* 모델 기반 인사이트와 특성으로 [!UICONTROL Real-time Customer Profile]을 강화하여 개인화를 개선하고 여정을 최적화합니다.
* 모델을 훈련 및 사용하여 고객 생애 가치, 전환 또는 이탈 경향, 제품과 콘텐츠 관련성 및 참여도 점수를 확인합니다.

## 아키텍처

<img src="assets/data_science.svg" alt="사용자 정의 데이터 과학을 통한 프로필 강화 블루프린트용 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" />

## 구현 단계

1. 수집할 데이터를 위한 [스키마를 만듭니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 데이터를 Experience Platform으로 [수집합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)

실시간 고객 프로필에 수집할 모델 결과를 알려면 데이터를 수집하기 전에 다음을 수행해야 합니다.

1. 수집한 데이터를 통합 프로필로 결합할 수 있도록 스키마에 [올바른 ID와 ID 네임스페이스를 구성합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).

## 구현 시 고려 사항

* 대부분의 경우 모델 결과를 경험 이벤트가 아니라 프로필 속성으로 수집해야 합니다. 모델 결과는 단순 속성 문자열일 수 있습니다. 수집할 모델 결과가 여러 개 있는 경우 배열이나 맵 유형 필드를 사용하는 것이 좋습니다.
* 통합 프로필 속성 데이터의 일별 내보내기인 일별 프로필 스냅샷 데이터 세트를 활용하여 프로필 속성 데이터에 대한 모델을 교육할 수 있습니다. 프로필 스냅샷 데이터 세트 설명서에 액세스할 수 있습니다 [여기](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets).
* Experience Platform에서 데이터를 추출하기 위해 다음 방법을 사용할 수 있습니다
   * 데이터 액세스 SDK
      * 데이터는 원시 파일 양식에 있습니다
      * 프로필 경험 이벤트 데이터는 통합 해제된 원시 상태로 유지됩니다.
   * RTCDP 대상
      * 프로필 속성 및 세그먼트 멤버십만 세그먼트화할 수 있습니다.
   * 쿼리 서비스
      * 많은 양의 원시 데이터에 액세스하면 10분 제한 시 쿼리가 시간 초과될 수 있습니다. 데이터를 점진적으로 쿼리하는 것이 좋습니다.


## 관련 설명서

* [Adobe Experience Platform Intelligence 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [Adobe Experience Platform 쿼리 서비스](https://experienceleague.adobe.com/docs/experience-platform/query/home.html)

## 관련 블로그 게시물

* [[!DNL Content and Commerce AI: Personalizing Your Interactions with Customers Through Content Intelligence]](https://medium.com/adobetech/content-and-commerce-ai-personalizing-your-interactions-with-customers-through-content-intelligence-dc182601deab)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a)
* [[!DNL Cutting Across Adobe Experience Products with Machine Learning to Elevated User Experience]](https://medium.com/adobetech/cutting-across-adobe-experience-products-with-machine-learning-to-elevated-user-experience-7c85000510d1)
* [[!DNL Segmentation.AI: Automated Audience-Clustering-as-a-Service in Adobe Experience Platform]](https://medium.com/adobetech/segmentation-ai-automated-audience-clustering-as-a-service-in-adobe-experience-platform-261f4099462c)