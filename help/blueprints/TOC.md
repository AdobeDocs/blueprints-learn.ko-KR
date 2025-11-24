---
user-guide-title: 디지털 경험 블루프린트
breadcrumb-title: 블루프린트
user-guide-description: 블루프린트는 기존 비즈니스 문제를 다루는 반복 가능한 구현으로 아키텍처 다이어그램, 기술적 고려 사항 및 관련 설명서 링크 등을 포함하고 있습니다.
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
source-git-commit: 3a3988e93dd9e92f4f564bfedfa314e8e2b5d9ba
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 41%

---


# 디지털 경험 블루프린트 {#architecture}

+ [Digital Experiences 블루프린트](/help/blueprints/overview.md)
+ 아키텍처 개요{#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform 및 애플리케이션](/help/blueprints/experience-platform/platform-applications.md)
   + [Experience Platform 데이터 흐름](/help/blueprints/experience-platform/platform-data-flow.md)
   + [Experience Platform 가드 레일](/help/blueprints/experience-platform/guardrails.md)
   + 배포{#deployment}
      + [Experience Platform Web SDK &amp; [!DNL Edge Network]](/help/blueprints/experience-platform/deployment/websdk.md)
      + [애플리케이션 SDK](/help/blueprints/experience-platform/deployment/appsdk.md)
+ 대상자 및 프로필 활성화{#audience-activation}
   + [Audience Manager](/help/blueprints/audience-activation/audience-manager.md)
   + Real-time Customer Data Platform (RTCDP) {#known-customer-audience-activation}
      + [소셜 및 광고 채널 활성화](/help/blueprints/audience-activation/advertising-activation.md)
      + [파일 및 엔터프라이즈 스트리밍 대상에 대한 활성화](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [고객 활동 허브](/help/blueprints/audience-activation/customer-activity.md)
      + [세그먼트 일치](/help/blueprints/audience-activation/segment-match.md)
      + [Target 및 RTCDP](/help/blueprints/audience-activation/rtcdp-target.md)
+ B2B 활성화 및 마케팅{#b2b-activation}
   + [개요](/help/blueprints/b2b/overview.md)
   + [B2B 활성화](/help/blueprints/b2b/b2bactivation.md)
   + [B2B 계정 활성화](/help/blueprints/b2b/b2b-account-activation.md)
   + [구매 그룹 기반 마케팅 및 여정 관리](/help/blueprints/b2b/b2b-buying-group-journeys.md)
   + [Marketo 데이터를 사용하는 B2B 여정](/help/blueprints/b2b/b2b-journeys-with-marketo.md)
   + Marketo Engage 및 Workfront 통합 블루프린트{#marketo-engage-and-workfront-integration-blueprint}
      + [개요](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
      + [접수 및 만들기](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
      + [검토 및 승인](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
      + [고객 성공 사례](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
+ Content &amp; Commerce{#content-commerce}
   + [Adobe Commerce 및 RTCDP](/help/blueprints/content-commerce/commerce/commerce-rtcdp.md)
+ Customer Journey Analytics     {#customer-journey-analytics}
   + [개요](/help/blueprints/customer-journey-analytics/overview.md)
   + [RTCDP에 CJA 대상 공유](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA와 Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ 고객 여정{#customer-journeys}
   + [개요](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer   {#journey-optimizer}
      + [Journey Optimizer   &#x200B;](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md)
      + [AJO 여정](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md)
      + [AJO 캠페인](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md)
      + [서드파티 메시징](/help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md)
   + 의사 결정 관리{#decision-management}
      + [개요](/help/blueprints/customer-journeys/decision-management/decision-management-overview.md)
      + [Edge에서 의사 결정 관리](/help/blueprints/customer-journeys/decision-management/decision-management-edge.md)
      + [허브에서 의사 결정 관리](/help/blueprints/customer-journeys/decision-management/decision-management-hub.md)
   + Campaign v8{#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md)
      + [Adobe이 포함된 Real-Time CDP [!DNL Campaign] v8](/help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer와 Adobe Campaign v8](/help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md)
   + 더 이상 사용되지 않는 블루프린트{#deprecated-blueprints}
      + Campaign Standard{#campaign-standard}
         + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/ko/docs/campaign-standard){target="_blank"}
         + [Adobe이 포함된 Real-Time CDP [!DNL Campaign Standard]](https://experienceleague.adobe.com/ko/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/get-started-sources-destinations)
      + Campaign v7{#campaign-v7}
         + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md)
+ 데이터 분석, 인텔리전스, AI/ML {#data-exploration}
   + [데이터 분석 및 인텔리전스](/help/blueprints/data-insights/analysis.md)
   + [프로필 강화를 위한 맞춤형 데이터 과학](/help/blueprints/data-insights/data-science.md)
