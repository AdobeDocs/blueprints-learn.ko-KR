---
user-guide-title: 디지털 경험 블루프린트
breadcrumb-title: 블루프린트
user-guide-description: 블루프린트는 기존 비즈니스 문제를 다루는 반복 가능한 구현으로 아키텍처 다이어그램, 기술적 고려 사항 및 관련 설명서 링크 등을 포함하고 있습니다.
product: adobe experience platform
mini-toc-levels: 3
role: Architect, Developer, User
source-git-commit: af390011dc068c4289f98d7fc0108ce48a5375c7
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 100%

---


# 디지털 경험 블루프린트 {#architecture}

+ [개요](/help/blueprints/overview.md)
+ 세로형 산업 블루프린트 {#vertical-blueprints}
   + [개요](/help/blueprints/vertical-blueprints/overview.md)
   + [의류](/help/blueprints/vertical-blueprints/apparel.md)
   + [소매](/help/blueprints/vertical-blueprints/retail.md)
   + [통신](/help/blueprints/vertical-blueprints/telecommunications.md)
   + [여행 및 서비스](/help/blueprints/vertical-blueprints/travel-hospitality.md)
+ 아키텍처 개요 {#architecture-overview}
   + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
   + [Experience Platform과 애플리케이션](/help/blueprints/experience-platform/platform-applications.md)
   + [Experience Platform 데이터 흐름](/help/blueprints/experience-platform/platform-data-flow.md)
   + 배포 {#deployment}
      + [Experience Platform Web SDK와 Edge Network](/help/blueprints/experience-platform/deployment/websdk.md)
      + [애플리케이션 SDK](/help/blueprints/experience-platform/deployment/appsdk.md)
      + [가드레일](/help/blueprints/experience-platform/deployment/guardrails.md)
+ 대상 및 프로필 활성화 {#audience-activation}
   + [개요](/help/blueprints/audience-activation/overview.md)
   + [익명 대상자 활성화       (AAM)](/help/blueprints/audience-activation/anonymous.md)
   + 알려진 고객 활성화(RTCDP) {#known-customer-audience-activation}
      + [개요](/help/blueprints/audience-activation/known.md)
      + 소셜 및 광고 채널에 대한 활성화 {#audience-activation}
         + [Facebook 맞춤 타겟 활성화](/help/blueprints/audience-activation/destinations/facebook.md)
         + [Google Customer Match 활성화](/help/blueprints/audience-activation/destinations/gcm.md)
      + [파일 및 엔터프라이즈 스트리밍 대상 활성화](/help/blueprints/audience-activation/enterprise-destinations.md)
      + [고객 활동 허브 ](/help/blueprints/audience-activation/customer-activity.md)
      + [Segment Match](/help/blueprints/audience-activation/segment-match.md)
   + [Experience Cloud 애플리케이션을 사용한 활성화](/help/blueprints/audience-activation/platform-and-applications.md)
+ B2B 활성화 및 마케팅 {#b2b-activation}
   + [개요](/help/blueprints/b2b/overview.md)
   + [B2B 활성화](/help/blueprints/b2b/b2bactivation.md)
   + Marketo와 Workfront를 사용하는 캠페인 공급망 {#optimize-campaign-supply-chain-with-marketo-and-workfront}
      + [개요](/help/blueprints/b2b/campaign-supply-chain/overview.md)
      + [가져오기 및 만들기](/help/blueprints/b2b/campaign-supply-chain/intake-and-create.md)
      + [고객 성공 사례](/help/blueprints/b2b/campaign-supply-chain/customer-success-stories.md)
+ Customer Journey Analytics {#customer-journey-analytics}
   + [개요](/help/blueprints/customer-journey-analytics/overview.md)
   + [CJA 대상자를 RTCDP에 공유](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
   + [CJA와 Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
+ 고객 여정 {#customer-journeys}
   + [개요](/help/blueprints/customer-journeys/overview.md)
   + Journey Optimizer {#journey-optimizer}
      + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer.md)
      + 의사 결정 관리 {#decision-management}
         + [개요](/help/blueprints/customer-journeys/decision_management/decision-management-overview.md)
         + [Edge의 의사 결정 관리](/help/blueprints/customer-journeys/decision_management/decision-management-edge.md)
         + [허브의 의사 결정 관리](/help/blueprints/customer-journeys/decision_management/decision-management-hub.md)
      + [Journey Optimizer와 Adobe Campaign](/help/blueprints/customer-journeys/ajo-and-campaign.md)
      + [서드파티 메시지](/help/blueprints/customer-journeys/3rd-party-messaging.md)
   + Campaign Standard {#campaign-standard}
      + [Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ko)
      + [Real-Time CDP와 Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=ko)
   + Campaign v8 {#campaign-v8}
      + [Campaign v8](/help/blueprints/customer-journeys/campaign-v8.md)
      + [Real-Time CDP와 Adobe Campaign v8](/help/blueprints/customer-journeys/rtcdp-and-campaign-v8.md)
      + [Journey Optimizer와 Adobe Campaign v8](/help/blueprints/customer-journeys/ajo-and-campaign-v8.md)
   + Campaign v7 {#campaign-v7}
      + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7.md)
      + [Real-Time CDP와 Adobe Campaign     v7](/help/blueprints/customer-journeys/rtcdp-and-campaign.md)
      + [Journey Optimizer와 Adobe Campaign v7](/help/blueprints/customer-journeys/ajo-and-campaign-v7.md)
+ 데이터 수집, 액세스, 내보내기 {#data-ingestion}
   + [개요](/help/blueprints/data-ingestion/overview.md)
   + [데이터 준비 및 수집 ](/help/blueprints/data-ingestion/ingestion.md)
   + [데이터 액세스 및 내보내기](/help/blueprints/data-ingestion/egress.md)
   + [이벤트 전송](/help/blueprints/data-ingestion/server-side-collection.md)
+ 데이터 분석, 인텔리전스 및 AI/ML {#data-exploration}
   + [개요](/help/blueprints/data-insights/overview.md)
   + [데이터 분석 및 인텔리전스](/help/blueprints/data-insights/analysis.md)
   + [사용자 정의 데이터 과학을 통한 프로필 강화 ](/help/blueprints/data-insights/data-science.md)
+ 웹 및 모바일 개인화 {#web-personalization}
   + [개요](/help/blueprints/web-personalization/overview.md)
   + [행동을 통한 개인화       - Target](/help/blueprints/web-personalization/behavioral.md)
   + [알려진 고객 개인화 - Target 및 RTCDP](/help/blueprints/web-personalization/known-personalization.md)
   + [의사 결정 관리](/help/blueprints/web-personalization/decision-management-edge.md)