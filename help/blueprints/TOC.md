---
user-guide-title: Customer Experience Orchestration 비즈니스 목표, 사용 사례, 아키텍처 다이어그램 및 블루프린트
breadcrumb-title: 사용 사례 및 블루프린트
user-guide-description: Adobe Experience Platform 및 애플리케이션에 대한 주요 비즈니스 목표, 사용 사례 패턴 및 업계 사용 사례를 살펴봅니다. 시각적 아키텍처 다이어그램 및 블루프린트는 비즈니스 가치를 구현에 연결하는 시스템 통합, 데이터 흐름 및 솔루션 설계에 대한 기술 참조를 제공합니다.
product: adobe experience platform
mini-toc-levels: 3
role: Developer, User
nudge: orange
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 15%

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
    + [지원 및 판매를 위한 실시간 프로필 조회](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md)
    + [프로필 강화를 위한 맞춤형 데이터 과학](/help/blueprints/use-case-patterns/audience-building-activation/data-science-profile-enrichment.md)
  + 개인화{#personalization-patterns}
    + [익명 방문자 웹 Personalization](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)
    + [알려진 방문자 웹/앱 Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md)
    + [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md)
    + [행동 추천](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md)
    + [웹/모바일 Personalization용 Edge 프로필 액세스](/help/blueprints/use-case-patterns/personalization/edge-profile-access.md)
    + [Adobe Target과 공유하는 대상](/help/blueprints/use-case-patterns/personalization/audience-sharing-with-target.md)
  + 캠페인 관리 및 오케스트레이션{#campaign-orchestration-patterns}
    + [일괄 아웃바운드 메시지 활성화](/help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md)
    + [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md)
    + [여러 단계로 조정된 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md)
    + [Decisioning을 사용한 크로스 채널 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md)
    + [Campaign v8 일괄 오케스트레이션 및 트랜잭션 메시지](/help/blueprints/use-case-patterns/campaign-management-orchestration/campaign-v8-orchestration.md)
    + [Journey Optimizer과 서드파티 메시징 통합](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md)
  + Analysis{#analysis-patterns}
    + [Customer Analytics &amp; Insight 세대](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md)
  + B2B 활성화 및 마케팅{#b2b-patterns}
    + [B2B Audience Activation](/help/blueprints/use-case-patterns/b2b/account-audience-activation.md)
    + [구매 그룹 기반 마케팅 및 여정 관리](/help/blueprints/use-case-patterns/b2b/buying-group-marketing.md)
    + [B2B 분석](/help/blueprints/use-case-patterns/b2b/account-analytics.md)
    + [Marketo 데이터를 사용하는 B2B 여정](/help/blueprints/use-case-patterns/b2b/marketo-data-journeys.md)
    + [AJO B2B 유료 미디어 컨트롤러](/help/blueprints/use-case-patterns/b2b/paid-media-orchestration.md)
    + [Marketo 및 Workfront Intake 및 Create](/help/blueprints/use-case-patterns/b2b/campaign-intake-and-creation.md)
    + [Marketo 및 Workfront 검토 및 승인](/help/blueprints/use-case-patterns/b2b/campaign-review-and-approval.md)
  + 대화 경험{#conversational-experience-patterns}
    + [Brand Concierge 대화 경험](/help/blueprints/use-case-patterns/conversational-experience/brand-concierge-conversational-experience.md)
+ 업계 사용 사례 예{#industry-use-cases}
  + [사용 사례 카탈로그](/help/blueprints/industry-use-cases/use-case-catalog.md)
  + [자동차](/help/blueprints/industry-use-cases/automotive/automotive-overview.md)
  + [B2B](/help/blueprints/industry-use-cases/b2b/b2b-overview.md)
  + [금융 서비스](/help/blueprints/industry-use-cases/financial-services/financial-services-overview.md)
  + [건강 관리](/help/blueprints/industry-use-cases/healthcare/healthcare-overview.md)
  + [보험](/help/blueprints/industry-use-cases/insurance/insurance-overview.md)
  + [미디어 및 엔터테인먼트](/help/blueprints/industry-use-cases/media-entertainment/media-entertainment-overview.md)
  + [리테일](/help/blueprints/industry-use-cases/retail/retail-overview.md)
  + [전기 통신](/help/blueprints/industry-use-cases/telecommunications/telecommunications-overview.md)
  + [기술](/help/blueprints/industry-use-cases/technology/technology-overview.md)
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

+ {hide-from-toc}실습 랩{#labs}
  + [실습형 Labs 개요](/help/blueprints/labs/overview.md)
  + 실습형 워크숍{#workshops}
    + AEP 재단{#aep-foundations}
      + [개요](/help/blueprints/labs/aep-foundations/overview.md)
      + [설정](/help/blueprints/labs/aep-foundations/setup.md)
      + 샌드박스 설정{#aep-sandbox}
        + [Developer Console 설정](/help/blueprints/labs/aep-foundations/sandbox-setup/developer-console-setup.md)
        + [배포 지침](/help/blueprints/labs/aep-foundations/sandbox-setup/deployment-instructions.md)
      + Postman 설정{#aep-postman}
        + [Postman 설치](/help/blueprints/labs/aep-foundations/postman-setup/postman-installation.md)
        + [환경 파일](/help/blueprints/labs/aep-foundations/postman-setup/environment-file.md)
        + [API 컬렉션](/help/blueprints/labs/aep-foundations/postman-setup/api-collection.md)
        + [샌드박스 액세스](/help/blueprints/labs/aep-foundations/postman-setup/sandbox-access.md)
        + [액세스 토큰](/help/blueprints/labs/aep-foundations/postman-setup/access-token.md)
      + 실시간 고객 프로필{#aep-rtcp}
        + [강의](/help/blueprints/labs/aep-foundations/real-time-customer-profile/lectures.md)
        + 프로필 검사{#aep-rtcp-inspect}
          + [개요](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/overview.md)
          + [프로필 기본 사항](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/profile-basics.md)
          + [병합 정책](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/merge-policies.md)
          + [프로필 및 ID API](/help/blueprints/labs/aep-foundations/real-time-customer-profile/inspecting-the-profile/profile-and-identity-apis.md)
      + LID 방식{#aep-lid}
        + [필요 조건](/help/blueprints/labs/aep-foundations/lid-methodology/prerequisites.md)
        + [레이블](/help/blueprints/labs/aep-foundations/lid-methodology/label.md)
        + 식별{#aep-lid-identify}
          + [개요](/help/blueprints/labs/aep-foundations/lid-methodology/identify/overview.md)
          + [1부 - 나머지 테이블 유형](/help/blueprints/labs/aep-foundations/lid-methodology/identify/part-1-remaining-table-types.md)
          + [2부 - 주요 필드](/help/blueprints/labs/aep-foundations/lid-methodology/identify/part-2-key-fields.md)
        + [비정규화](/help/blueprints/labs/aep-foundations/lid-methodology/denormalize.md)
      + XDM 모델링{#aep-xdm}
        + [강의](/help/blueprints/labs/aep-foundations/xdm-modeling/lectures.md)
        + UI 모델링{#aep-xdm-ui}
          + [개요](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/overview.md)
          + [로그인 및 찾아보기](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/login-and-browse.md)
          + [모델 표준 개체](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/model-standard-objects.md)
          + [모델 사용자 지정 개체](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/model-custom-objects.md)
          + [프로필에 대한 구성](/help/blueprints/labs/aep-foundations/xdm-modeling/ui-modeling/configure-for-profile.md)
        + API 모델링{#aep-xdm-api}
          + [개요](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/overview.md)
          + 스키마 작성{#aep-xdm-api-build}
            + [개요](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/overview.md)
            + [표준 필드 그룹 가져오기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/get-standard-field-groups.md)
            + [사용자 정의 필드 그룹 만들기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/create-custom-field-groups.md)
            + [프로필 클래스 가져오기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/get-profile-class.md)
            + [스키마 만들기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/create-schema.md)
            + [스키마 보기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/view-schema.md)
            + [스키마 수정 - JSON 패치](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/build-schema/modify-schema-json-patch.md)
          + ID 필드 표시{#aep-xdm-api-identity}
            + [개요](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/overview.md)
            + [기본 ID 만들기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/create-primary-identity.md)
            + [다른 ID 만들기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/create-other-identities.md)
            + [스키마 보기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/mark-identity-fields/view-schema.md)
          + 관계 정의{#aep-xdm-api-relationships}
            + [개요](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/overview.md)
            + [계획 스키마 ID 가져오기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/get-plan-schema-id.md)
            + [스키마 관계 만들기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/create-schema-relationship.md)
            + [계획 참조 ID 만들기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/create-plan-reference-identity.md)
            + [스키마 보기](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/define-relationships/view-schema.md)
          + [요약](/help/blueprints/labs/aep-foundations/xdm-modeling/api-modeling/recap.md)
        + 보너스 랩{#aep-xdm-bonus}
          + [개요](/help/blueprints/labs/aep-foundations/xdm-modeling/bonus-labs/overview.md)
          + [API를 사용한 자동화](/help/blueprints/labs/aep-foundations/xdm-modeling/bonus-labs/automate-with-apis.md)
      + 데이터 수집{#aep-ingestion}
        + [강의](/help/blueprints/labs/aep-foundations/data-ingestion/lectures.md)
        + [랩 개요](/help/blueprints/labs/aep-foundations/data-ingestion/lab-overview.md)
        + [샘플 파일](/help/blueprints/labs/aep-foundations/data-ingestion/sample-files.md)
        + 일괄 처리 수집{#aep-ingestion-batch}
          + [개요](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/overview.md)
          + [데이터 흐름 만들기](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/create-dataflow.md)
          + 데이터 매핑{#aep-ingestion-batch-mapping}
            + [개요](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/overview.md)
            + [통과 매핑 수정](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/fix-passthrough-mappings.md)
            + [계산된 필드](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/calculated-fields.md)
            + [최종 매핑 세트 확인](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/mapping-data/check-final-mapping-set.md)
          + [데이터 흐름 실행](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/run-dataflow.md)
          + [디버깅 오류](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/debugging-errors.md)
          + [새 데이터 흐름 만들기](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/create-a-new-dataflow.md)
          + [오류 해결](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/fixing-errors.md)
          + [확인 및 유효성 검사](/help/blueprints/labs/aep-foundations/data-ingestion/batch-ingestion/verification-and-validation.md)
        + 스트림 수집{#aep-ingestion-stream}
          + [개요](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/overview.md)
          + [Source 설정](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/setup-source.md)
          + [매핑 구성](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/configure-mapping.md)
          + [최종 매핑 세트 확인](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/check-final-mapping-set.md)
          + [프로필 스트리밍](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/stream-a-profile.md)
          + [수집된 프로필 확인](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/verify-ingested-profile.md)
          + [오류 모니터링 및 디버깅](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/monitoring-and-debugging-errors.md)
          + [확인 및 유효성 검사](/help/blueprints/labs/aep-foundations/data-ingestion/stream-ingestion/verification-and-validation.md)
        + 보너스 랩{#aep-ingestion-bonus}
          + [개요](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/overview.md)
          + [CreateDate에 대한 MAPPER 오류 수정](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/fix-mapper-errors-for-createdate.md)
          + [주문 이벤트 스트리밍](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/stream-an-order-event.md)
          + 데이터 랜딩 영역 사용{#aep-ingestion-dlz}
            + [개요](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/overview.md)
            + [Source 설정](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/setup-source.md)
            + [매핑 만들기](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/create-mappings.md)
            + [데이터 흐름 예약](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/schedule-dataflow.md)
            + [실패한 데이터 흐름 다시 시도](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/retry-a-failed-dataflow.md)
            + 주문 로드{#aep-ingestion-dlz-orders}
              + [개요](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/overview.md)
              + [Source 설정](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/setup-source.md)
              + [초기 매핑](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/initial-mappings.md)
              + [개체 복사 매핑](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/object-copy-mappings.md)
              + [데이터 흐름 확인 및 예약](/help/blueprints/labs/aep-foundations/data-ingestion/bonus-labs/using-data-landing-zone/load-orders/verify-and-schedule-dataflow.md)
      + 세분화 및 활성화{#aep-segmentation}
        + [강의](/help/blueprints/labs/aep-foundations/segmentation-and-activation/lecture.md)
        + Edge 활성화{#aep-segmentation-edge}
          + [개요](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/overview.md)
          + [Edge 대상 만들기](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/create-edge-audience.md)
          + [Edge 이벤트 보내기](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/send-an-edge-event.md)
          + 이벤트 전달 설정{#aep-segmentation-edge-ef}
            + [개요](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/overview.md)
            + [속성 만들기](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/create-property.md)
            + [데이터 스트림 만들기](/help/blueprints/labs/aep-foundations/segmentation-and-activation/edge-activation/setup-event-forwarding/create-datastream.md)
      + 대상자 작성{#aep-audiences}
        + 사용 사례 1 - 획득{#aep-uc1}
          + [개요](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/overview.md)
          + 대상 구성{#aep-uc1-destinations}
            + [사용자 지정 Personalization 대상 설정](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/configure-destinations/setup-custom-personalization-destination.md)
            + [스트리밍 대상 설정](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/configure-destinations/setup-streaming-destination.md)
          + [대상 1 작성](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-1.md)
          + [대상 2 작성](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-2.md)
          + [대상 작성 3](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/build-audience-3.md)
          + [Edge 이벤트 보내기](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/send-an-edge-event.md)
          + [비판적 사고 검토](/help/blueprints/labs/aep-foundations/audience-building/use-case-1-acquisition/critical-thinking-review.md)
        + 사용 사례 2 - 업셀{#aep-uc2}
          + [개요](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/overview.md)
          + [사전 작업](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/pre-work.md)
          + [옵션 1 - 대상을 사용하여 집계](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/option-1-using-audiences-to-aggregate.md)
          + [옵션 2 - 사전 집계 사용](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/option-2-use-pre-aggregates.md)
          + [비판적 사고 검토](/help/blueprints/labs/aep-foundations/audience-building/use-case-2-upsell/critical-thinking-review.md)
        + 사용 사례 3 - 지원{#aep-uc3}
          + [개요](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/overview.md)
          + [빌드 사용 사례 3](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/build-use-case-3.md)
          + [비판적 사고 검토](/help/blueprints/labs/aep-foundations/audience-building/use-case-3-outreach/critical-thinking-review.md)
        + 보너스 랩{#aep-audiences-bonus}
          + [개요](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/overview.md)
          + [허브로 주문 이벤트 보내기](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/send-order-event-to-hub.md)
          + [허브로 웹 이벤트 보내기](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/send-web-event-to-hub.md)
          + [이벤트 모니터링](/help/blueprints/labs/aep-foundations/audience-building/bonus-labs/monitor-your-event.md)
    + AJO 재단{#ajo-foundations}
      + [개요](/help/blueprints/labs/ajo-foundations/overview.md)
      + [설정](/help/blueprints/labs/ajo-foundations/setup.md)
      + 샌드박스 설정{#ajo-sandbox}
        + [Developer Console 설정](/help/blueprints/labs/ajo-foundations/sandbox-setup/developer-console-setup.md)
        + [배포 지침](/help/blueprints/labs/ajo-foundations/sandbox-setup/deployment-instructions.md)
      + Postman 설정{#ajo-postman}
        + [Postman 설치](/help/blueprints/labs/ajo-foundations/postman-setup/postman-installation.md)
        + [환경 파일 가져오기](/help/blueprints/labs/ajo-foundations/postman-setup/import-environment-file.md)
        + [API 컬렉션 가져오기](/help/blueprints/labs/ajo-foundations/postman-setup/import-api-collection.md)
      + 아키텍처 빌딩 블록{#ajo-architecture}
        + [강의](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/lecture.md)
        + 아키텍처에 사용 사례 매핑{#ajo-architecture-mapping}
          + [개요](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/overview.md)
          + [랩 소개](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-introduction.md)
          + [실습](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-exercise.md)
          + [랩 리뷰](/help/blueprints/labs/ajo-foundations/architecture-building-blocks/mapping-use-cases-to-architecture/lab-review.md)
      + 데이터 저장소{#ajo-data-stores}
        + [실시간 고객 프로필 강의](/help/blueprints/labs/ajo-foundations/data-stores/real-time-customer-profile-lecture.md)
        + 실행 중인 프로필{#ajo-profile}
          + [개요](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/overview.md)
          + [로그인 및 찾아보기](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/login-and-browse.md)
          + [데이터 스트림 만들기](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/create-datastream.md)
          + [Edge 웹 이벤트 보내기](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/send-an-edge-web-event.md)
          + [허브에서 프로필 유효성 검사](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-on-hub.md)
          + [Edge에서 프로필 유효성 검사](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-on-edge.md)
          + [데이터 레이크에서 이벤트 유효성 검사](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-event-on-data-lake.md)
          + [프로필 스냅숏 유효성 검사](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/validate-profile-snapshot.md)
          + [요약](/help/blueprints/labs/ajo-foundations/data-stores/profile-in-action/summary.md)
        + [Relational Store 강의](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-lecture.md)
        + 관계형 작업 저장소{#ajo-relational}
          + [개요](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/overview.md)
          + [스키마 찾아보기](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/browse-schemas.md)
          + [프로필 대상 Dimension](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/profile-target-dimension.md)
          + [대상자 읽기](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/read-an-audience.md)
          + [요약](/help/blueprints/labs/ajo-foundations/data-stores/relational-store-in-action/summary.md)
        + 이메일 채널 구성{#ajo-email}
          + [개요](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/overview.md)
          + [프로필에 대한 구성](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/configure-for-profile.md)
          + [관계형 구성](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/configure-for-relational.md)
          + [활성 상태 대기 중](/help/blueprints/labs/ajo-foundations/data-stores/configure-email-channels/waiting-for-active-status.md)
      + 오케스트레이션된 캠페인{#ajo-campaigns}
        + [메시지 게재 강의](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-lecture.md)
        + 작동 중인 메시지 게재{#ajo-campaigns-delivery}
          + [개요](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/overview.md)
          + [캠페인 만들기](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/create-a-campaign.md)
          + [대상자 작성](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/build-an-audience.md)
          + [포크 활동 추가](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/add-fork-activity.md)
          + [이메일 활동 추가](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/add-email-activities.md)
          + [캠페인 테스트](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/test-the-campaign.md)
          + [요약](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/message-delivery-in-action/summary.md)
        + [워크플로우 빌딩 블록 강의](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/workflow-building-blocks-lecture.md)
        + 플래그십 폰 출시{#ajo-campaigns-flagship}
          + [개요](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/overview.md)
          + [SMS 채널 구성](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/configure-sms-channel.md)
          + [오케스트레이션된 캠페인 만들기](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/create-an-orchestrated-campaign.md)
          + [대상자 작성](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/build-an-audience.md)
          + [결과 포크](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/fork-the-result.md)
          + [대상자 저장](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/save-the-audience.md)
          + [라인 필터링](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/filter-the-lines.md)
          + [SMS 구성](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/compose-the-sms.md)
          + [워크플로우 실행](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/run-the-workflow.md)
          + [요약](/help/blueprints/labs/ajo-foundations/orchestrated-campaigns/flagship-phone-launch/summary.md)
      + 여정{#ajo-journeys}
        + [강의](/help/blueprints/labs/ajo-foundations/journeys/lecture.md)
        + 구매 후 흥분{#ajo-journeys-post-purchase}
          + [개요](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/overview.md)
          + [이벤트 구성](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/configure-event.md)
          + [사용자 지정 작업 구성](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/configure-custom-action.md)
          + [여정 작성](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/build-journey.md)
          + [테스트 여정](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/test-journey.md)
          + [이벤트 보내기](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/send-an-event.md)
          + [수집된 이벤트 유효성 확인](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/validate-event-ingested.md)
          + [여정 확인](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/validate-journey.md)
          + [요약](/help/blueprints/labs/ajo-foundations/journeys/post-purchase-excitement/summary.md)
      + 결정{#ajo-decisioning}
        + [Experience Edge](/help/blueprints/labs/ajo-foundations/decisioning/experience-edge.md)
        + 의사 결정 설명{#ajo-decisioning-explained}
          + [개요](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/overview.md)
          + [소개](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/introduction.md)
          + [결정 항목 XDM](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-item-xdm.md)
          + [의사 결정 항목 만들기](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-item-creation.md)
          + [컬렉션](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/collections.md)
          + [등급 수식](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/ranking-formulas.md)
          + [선택 전략](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/selection-strategies.md)
          + [의사 결정 정책](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/decision-policies.md)
          + [가드레일, AI 모델이 미래를 결정함](/help/blueprints/labs/ajo-foundations/decisioning/decisioning-explained/guardrails-ai-models-decisioning-future.md)
        + 포기한 찾아보기{#ajo-decisioning-abandoned}
          + [개요](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/overview.md)
          + [의사 결정 규칙 만들기](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-decision-rule.md)
          + [오퍼 속성 만들기](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-attributes.md)
          + [오퍼 항목 만들기](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-items.md)
          + [오퍼 컬렉션 만들기](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-offer-collection.md)
          + [등급 수식 만들기](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-ranking-formula.md)
          + [선택 전략 만들기](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-selection-strategy.md)
          + [코드 기반 경험 채널 만들기](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-code-based-experience-channel.md)
          + [여정 만들기](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/create-the-journey.md)
          + [의사 결정 및 CBE 활용](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/decisioning-and-cbes-in-action.md)
          + [요약](/help/blueprints/labs/ajo-foundations/decisioning/abandoned-browse/summary.md)
      + AI를 사용한 콘텐츠 작성{#ajo-content-ai}
        + [강의](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/lecture.md)
        + [개요](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/overview.md)
        + [브랜드 관리](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/brand-management.md)
        + [컨텐츠 조각 작성](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/building-content-fragments.md)
        + [컨텐츠 템플릿 작성 중](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/building-content-template.md)
        + [이메일 만들기](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/creating-the-email.md)
        + [AI Assistant 및 Content Personalization](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/ai-assistant-and-content-personalization.md)
        + [Personalization 및 콘텐츠 실험](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/personalization-and-content-experimentation.md)
        + [콘텐츠 시뮬레이션](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/content-simulation.md)
        + [브랜드 정렬](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/brand-alignment.md)
        + [이메일 테스트](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/test-the-email.md)
        + [요약](/help/blueprints/labs/ajo-foundations/content-authoring-with-ai/summary.md)
