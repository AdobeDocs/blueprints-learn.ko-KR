---
user-guide-title: Customer Experience Orchestration 블루프린트
breadcrumb-title: 블루프린트
user-guide-description: 블루프린트는 기존 비즈니스 문제를 다루는 반복 가능한 구현으로 아키텍처 다이어그램, 기술적 고려 사항 및 관련 설명서 링크 등을 포함하고 있습니다.
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
source-git-commit: 021e6b48e09ce2d3da80ffe7ca1b7f4ce4a4a3a4
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 17%

---


# Customer experience orchestration 블루프린트 {#architecture}

+ [Customer experience orchestration 블루프린트](/help/blueprints/overview.md)
+ AEP 및 앱의 주요 비즈니스 목표{#business-objectives}
   + [개요](/help/blueprints/business-objectives/overview.md)
   + 고객 확보 및 성장{#acquisition-growth}
      + [신규 고객 확보](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)
      + [리드 생성 늘리기](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)
      + [웹 사이트 참여 증가](/help/blueprints/business-objectives/acquisition-growth/increase-website-engagement.md)
   + 수익 및 수익 창출{#revenue-monetization}
      + [전환율 향상](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)
      + [매출 및 판매 증대](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)
      + [교차 판매 및 상향 판매 매출 촉진](/help/blueprints/business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)
      + [고객 충성도 및 라이프타임 가치 향상](/help/blueprints/business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)
   + 비용 및 효율성{#cost-efficiency}
      + [고객 확보 비용 절감](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)
      + [마케팅 지출 및 ROI 최적화](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)
      + [데이터 품질 및 거버넌스 개선](/help/blueprints/business-objectives/cost-efficiency/improve-data-quality-governance.md)
      + [마케팅 기술 통합 및 현대화](/help/blueprints/business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)
   + 고객 경험{#customer-experience-objectives}
      + [개인화된 고객 경험 제공](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)
      + [고객 유지 기능 향상](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)
      + [고객 온보딩 개선](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)
      + [포기한 장바구니 및 여정 복구](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)
   + Analytics 및 Insights{#analytics-insights}
      + [분석 및 보고 개선](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)
      + [데이터 중심의 의사 결정 활성화](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)
      + [마케팅 기여도 개선](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md)
   + 자격 및 판매(B2B){#qualification-sales-b2b}
      + [리드 자격 및 전환 개선](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)
      + [고객 참여 개선](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)
+ 사용 사례 패턴{#use-case-patterns}
   + [개요](/help/blueprints/use-case-patterns/overview.md)
   + 대상 구축 및 활성화{#audience-building-activation}
      + [대상으로 Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md)
      + [세그먼트가 일치하는 Audience Collaboration](/help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md)
      + [이벤트 전달](/help/blueprints/use-case-patterns/audience-building-activation/event-forwarding.md)
      + [B2B Audience Activation](/help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md)
   + 개인화{#personalization-patterns}
      + [익명 방문자 웹 Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
      + [알려진 방문자 웹/앱 Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
      + [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
      + [행동 추천](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
   + 캠페인 관리 및 오케스트레이션{#campaign-orchestration-patterns}
      + [일괄 아웃바운드 메시지 활성화](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
      + [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
      + [여러 단계로 조정된 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
      + [Decisioning을 사용한 크로스 채널 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
      + [구매 그룹 기반 마케팅 및 여정 관리](/help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md)
   + Analysis{#analysis-patterns}
      + [Customer Analytics &amp; Insight 세대](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
      + [B2B 분석](/help/blueprints/use-case-patterns/analysis/b2b-analytics.md)
   + 대화 경험{#conversational-experience-patterns}
      + [Brand Concierge 대화 경험](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md)
+ 업계 사용 사례 예{#industry-use-cases}
   + [개요](/help/blueprints/industry-use-cases/overview.md)
   + [자동차](/help/blueprints/industry-use-cases/automotive/automotive-overview.md)
   + [B2B](/help/blueprints/industry-use-cases/b2b/b2b-overview.md)
   + [금융 서비스](/help/blueprints/industry-use-cases/financial-services/financial-services-overview.md)
   + [건강 관리](/help/blueprints/industry-use-cases/healthcare/healthcare-overview.md)
   + [보험](/help/blueprints/industry-use-cases/insurance/insurance-overview.md)
   + [미디어 및 엔터테인먼트](/help/blueprints/industry-use-cases/media-entertainment/media-entertainment-overview.md)
   + [리테일](/help/blueprints/industry-use-cases/retail/retail-overview.md)
   + [전기 통신](/help/blueprints/industry-use-cases/telecommunications/telecommunications-overview.md)
   + [여행 및 접대](/help/blueprints/industry-use-cases/travel-hospitality/travel-hospitality-overview.md)
+ 아키텍처 다이어그램 및 블루프린트{#architecture-diagrams}
   + 아키텍처 개요{#architecture-overview}
      + [Experience Cloud](/help/blueprints/experience-platform/experience-cloud.md)
      + [Experience Platform 및 애플리케이션](/help/blueprints/experience-platform/platform-applications.md)
      + [Experience Platform 데이터 흐름](/help/blueprints/experience-platform/platform-data-flow.md)
      + [Experience Platform 보호 기능](/help/blueprints/experience-platform/guardrails.md)
      + 배포{#deployment}
         + [Experience Platform Web SDK &amp; [!DNL Edge Network]](/help/blueprints/experience-platform/deployment/websdk.md)
         + [애플리케이션 SDK](/help/blueprints/experience-platform/deployment/appsdk.md)
   + 대상자 및 프로필 활성화{#audience-activation}
      + [장치 기반 - Audience Manager을 사용한 익명 대상 타깃팅](/help/blueprints/audience-activation/audience-manager.md)
      + Real-Time Customer Data Platform(RTCDP) {#known-customer-audience-activation}
         + [소셜 및 광고 대상에 대한 대상자 활성화](/help/blueprints/audience-activation/advertising-activation.md)
         + [엔터프라이즈 대상에 대한 대상자 및 프로필 활성화 블루프린트](/help/blueprints/audience-activation/enterprise-destinations.md)
         + [지원 및 판매 시나리오를 위한 실시간 프로필 액세스](/help/blueprints/audience-activation/customer-activity.md)
         + [웹 및 모바일 개인화를 위한 실시간 에지 프로필 액세스](/help/blueprints/audience-activation/real-time-lookup.md)
         + [세그먼트 일치로 대상자 공동 작업](/help/blueprints/audience-activation/segment-match.md)
         + [Target을 사용한 알려진 고객 개인화](/help/blueprints/audience-activation/rtcdp-target.md)
         + [프로필 강화를 위한 맞춤형 데이터 과학](/help/blueprints/audience-activation/data-science.md)
   + B2B 활성화 및 마케팅{#b2b-activation}
      + [개요](/help/blueprints/b2b/overview.md)
      + [B2B 활성화](/help/blueprints/b2b/b2bactivation.md)
      + [B2B 계정 활성화](/help/blueprints/b2b/b2b-account-activation.md)
      + [구매 그룹 기반 마케팅 및 여정 관리](/help/blueprints/b2b/b2b-buying-group-journeys.md)
      + [Marketo 데이터를 사용하는 B2B 여정](/help/blueprints/b2b/b2b-journeys-with-marketo.md)
      + [B2B 유료 미디어 컨트롤러](/help/blueprints/b2b/ajo-b2b-paid-media-controller.md)
      + Marketo Engage 및 Workfront 통합 블루프린트{#marketo-engage-and-workfront-integration-blueprint}
         + [개요](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md)
         + [접수 및 만들기](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md)
         + [검토 및 승인](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md)
         + [고객 성공 사례](/help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md)
   + Customer Journey Analytics{#customer-journey-analytics}
      + [개요](/help/blueprints/customer-journey-analytics/overview.md)
      + [B2B Customer Journey Analytics](/help/blueprints/customer-journey-analytics/b2b-cja.md)
      + [RTCDP에 CJA 대상 공유](/help/blueprints/customer-journey-analytics/cja-rtcdp.md)
      + [CJA와 Journey Optimizer](/help/blueprints/customer-journey-analytics/cja-ajo.md)
      + [데이터 분석 및 인텔리전스](/help/blueprints/customer-journey-analytics/analysis.md)
   + 고객 여정{#customer-journeys}
      + [개요](/help/blueprints/customer-journeys/overview.md)
      + Journey Optimizer{#journey-optimizer}
         + [Journey Optimizer](/help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md)
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
            + [Adobe [!DNL Campaign Standard]이(가) 있는 Real-Time CDP](https://experienceleague.adobe.com/ko/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/get-started-sources-destinations)
         + Campaign v7{#campaign-v7}
            + [Campaign v7](/help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md)
