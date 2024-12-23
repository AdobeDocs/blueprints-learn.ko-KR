---
user-guide-title: 디지털 경험 블루프린트
breadcrumb-title: 블루프린트
user-guide-description: 블루프린트는 기존 비즈니스 문제를 다루는 반복 가능한 구현으로 아키텍처 다이어그램, 기술적 고려 사항 및 관련 설명서 링크 등을 포함하고 있습니다.
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: 6a13de73d7f61295092faccfc21172f5e188331d
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 54%

---


# 디지털 경험 블루프린트 {#architecture}

+ [Digital Experiences 블루프린트](/help/blueprints/overview.md)
+ 수직 산업 블루프린트{#vertical-blueprints}
   + [개요](/help/blueprints/vertical-blueprints/overview.md)
   + [의류](/help/blueprints/vertical-blueprints/apparel.md)
   + [소매](/help/blueprints/vertical-blueprints/retail.md)
   + [통신](/help/blueprints/vertical-blueprints/telecommunications.md)
   + [여행 및 접대](/help/blueprints/vertical-blueprints/travel-hospitality.md)
+ 아키텍처 개요 {#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform 및 애플리케이션](/help/blueprints/experience-platform/platform-applications.md)
   + [Experience Platform 데이터 흐름](/help/blueprints/experience-platform/platform-data-flow.md)
   + 배포 {#deployment}
      + [웹 SDK 및  [!DNL Edge Network] Experience Platform](/help/blueprints/experience-platform/deployment/websdk.md)
      + [애플리케이션 SDK](/help/blueprints/experience-platform/deployment/appsdk.md)
      + [가드레일](/help/blueprints/experience-platform/deployment/guardrails.md)
+ 대상 및 프로필 활성화 {#audience-activation}
   + [개요](/help/blueprints/audience-activation/overview.md)
   + [익명 대상자 활성화 ](/help/blueprints/audience-activation/anonymous.md)
   + 알려진 고객 활성화(RTCDP) {#known-customer-audience-activation}
      + [개요](/help/blueprints/audience-activation/known.md)
      + [소셜 및 광고 채널 활성화](/help/blueprints/audience-activation/advertising-activation.md)
      + [파일 및 엔터프라이즈 스트리밍 대상에 대한 활성화](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [고객 활동 허브](/help/blueprints/audience-activation/customer-activity.md)
      + [세그먼트 일치](/help/blueprints/audience-activation/segment-match.md)
   + [Experience Cloud 애플리케이션으로 활성화](/help/blueprints/audience-activation/platform-and-applications.md)
   + 웹 및 모바일 개인화 {#web-personalization}
      + [개요](/help/blueprints/audience-activation/web-personalization/overview.md)
      + [행동 개인화 - Target](/help/blueprints//audience-activation/web-personalization/behavioral.md)
      + [알려진 고객 개인화 - Target 및 RTCDP](/help/blueprints/audience-activation/web-personalization/known-personalization.md)
      + [의사 결정 관리](/help/blueprints/audience-activation/web-personalization/decision-management-edge.md)
+ B2B 활성화 및 마케팅 {#b2b-activation}
   + [개요](/help/blueprints/b2b/overview.md)
   + [B2B 활성화](/help/blueprints/b2b/b2bactivation.md)
   + [B2B 계정 활성화](/help/blueprints/b2b/b2b-account-activation.md)
   + [구매 그룹 기반 마케팅 및 여정 관리](/help/blueprints/b2b/b2b-buying-group-journeys.md)
   + Marketo Engage 및 Workfront 통합 블루프린트{#marketo-engage-and-workfront-integration-blueprint}
      + [개요](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
      + [접수 및 만들기](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
      + [검토 및 승인](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
      + [고객 성공 사례](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
+ 컨텐츠 및 Commerce{#content-commerce}
   + [Adobe Commerce 및 RTCDP](/help/blueprints/content-commerce/commerce/commerce-rtcdp.md)
+ Customer Journey Analytics {#customer-journey-analytics}
   + [개요](/help/blueprints/customer-journey-analytics/overview.md)
   + [RTCDP에 CJA 대상 공유](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA와 Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ 고객 여정 {#customer-journeys}
   + [개요](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer {#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer.md)
      + 의사 결정 관리 {#decision-management}
         + [개요](/help/blueprints/customer-journeys/decision_management/decision-management-overview.md)
         + [Edge의 의사 결정 관리](/help/blueprints/customer-journeys/decision_management/decision-management-edge.md)
         + [허브의 의사 결정 관리](/help/blueprints/customer-journeys/decision_management/decision-management-hub.md)
      + [Journey Optimizer와 Adobe Campaign  ](/help/blueprints/customer-journeys/ajo-and-campaign.md)
      + [서드파티 메시징](/help/blueprints/customer-journeys/3rd-party-messaging.md)
   + Campaign Standard {#campaign-standard}
      + [[!DNL Campaign Standard]](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ko){target="_blank"}
      + [Adobe이 있는 Real-Time CDP [!DNL Campaign Standard]](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=ko){target="_blank"}
   + Campaign v8 {#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Adobe  [!DNL Campaign] v8이(가) 있는 Real-Time CDP](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer와 Adobe Campaign v8](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7 {#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Adobe  [!DNL Campaign] v7이(가) 있는 Real-Time CDP](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Adobe  [!DNL Campaign] v7이(가) 있는 Journey Optimizer](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ 데이터 수집, 액세스, 내보내기 {#data-ingestion}
   + [개요](/help/blueprints/data-ingestion/overview.md)
   + [다중 샌드박스 이벤트 전달 데이터 수집](/help/blueprints/data-ingestion/multi-sandbox-event-forwarding.md)
   + [데이터 준비 및 수집](/help/blueprints/data-ingestion/ingestion.md)
   + [데이터 액세스 및 내보내기](/help/blueprints/data-ingestion/egress.md)
   + [이벤트 전달](/help/blueprints/data-ingestion/server-side-collection.md)
+ 데이터 분석, 인텔리전스 및 AI/ML {#data-exploration}
   + [개요](/help/blueprints/data-insights/overview.md)
   + [데이터 분석 및 인텔리전스](/help/blueprints/data-insights/analysis.md)
   + [프로필 강화를 위한 맞춤형 데이터 과학](/help/blueprints/data-insights/data-science.md)
