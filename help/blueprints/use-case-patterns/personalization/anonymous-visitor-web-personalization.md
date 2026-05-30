---
title: 익명 방문자 웹 Personalization
description: 세션 내 행동 신호를 기반으로 미확인된 방문자에게 개인화된 웹 콘텐츠를 전달하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: e2446801-ffce-40e6-bfe9-abec623c9201
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 4%

---

# 익명 방문자 웹 개인화

이 안내서에서는 세션 내 동작 신호를 기반으로 익명(미확인) 방문자에게 개인화된 웹 콘텐츠를 전달하기 위해 [!DNL Adobe Journey Optimizer]&#x200B;(AJO), [!DNL Adobe Real-Time Customer Data Platform]&#x200B;(RT-CDP) 및 [!DNL Adobe Experience Platform]&#x200B;(AEP)을 사용하는 익명 방문자 웹 개인화 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

패턴은 제한된 데이터로 작동합니다. 즉, 동일한 장치나 쿠키를 사용한 이전 방문에서 누적된 익명 에지 프로필과 현재 세션에서 관찰할 수 있는 항목만 해당됩니다. 이렇게 하면 방문자가 계정이 없거나 인증되지 않은 funnel의 최상위 개인화에 적합합니다.

## 사용 사례 패턴

다음은 이 사용 사례에 대한 핵심 패턴 및 실행 계획에 대해 설명합니다.

**익명 방문자 웹 Personalization**

AJO 웹 채널을 통해 미확인된 방문자에 대한 세션 내 행동 신호를 기반으로 개인화된 콘텐츠를 제공합니다.

**실행 계획:** 웹 표면 구성 > 행동 규칙 평가 > 콘텐츠 게재 > 노출 추적 > 보고

## 사용 사례 개요

익명 방문자 웹 Personalization은 아직 식별되지 않음(로그인하지 않음, 알려진 ID가 없음, 통합 고객 프로필로 해결할 수 없음)인 웹 사이트 방문자에게 관련성 있고 개인화된 콘텐츠를 제공해야 하는 비즈니스 요구를 해결합니다. 이러한 제한에도 불구하고 페이지 보기, 사이트에서 보낸 시간, 스크롤 깊이, 참조 소스, 지리적 위치, 장치 유형 및 UTM 캠페인 매개변수와 같은 세션 내 동작 신호를 사용하여 의미 있는 개인화를 달성할 수 있습니다.

이 패턴은 AJO의 웹 채널 표면과 코드 기반 경험을 사용하여 페이지 콘텐츠를 실시간으로 수정합니다. 방문자가 사이트를 탐색할 때 1초 미만의 지연 시간으로 결정을 내려야 하므로 Edge 세그먼테이션은 기본 평가 방법입니다. [!DNL Web SDK]은(는) 동작 신호를 수집하여 [!DNL AEP Edge Network]&#x200B;(으)로 보냅니다. 여기서 에지 평가 대상 규칙은 전달할 콘텐츠 변형을 결정합니다.

전체 통합 프로필 및 세그먼트 멤버십을 활용하는 알려진 방문자 웹/앱 개인화와 달리, 이 패턴은 현재 세션에서 관찰할 수 있는 데이터와 방문자의 ECID([!DNL Experience Cloud ID])와 연결된 모든 익명 에지 프로필로 제한됩니다. 이러한 구분은 구현 계획에 중요합니다. 개인화에 사용할 수 있는 동작 신호는 [!DNL Web SDK]이(가) 캡처하는 내용과 쿠키 기반 ECID를 통해 세션 간 Edge 프로필 저장소에서 지속되는 것으로 제한됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

**[웹 사이트 참여 늘리기](../../business-objectives/acquisition-growth/increase-website-engagement.md)**

익명 방문자 신호에 맞춘 적절한 경험을 통해 사이트에서 보낸 시간, 세션당 페이지 수 및 웹 콘텐츠와의 상호 작용을 개선합니다.

| KPI |
| --- |
| Time On (웹) 페이지 |
| 참여 |
| 전환율 |

**[개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

아직 자신을 식별하지 않은 방문자에게도 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 콘텐츠, 오퍼 및 메시지를 맞춤화할 수 있습니다.

| KPI |
| --- |
| 참여 |
| 전환율 |
| 고객 만족도(CSAT) |

**[전환율 증가](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

행동 컨텍스트에 따라 가장 관련성이 높은 콘텐츠를 제시하여 구매, 등록 또는 양식 제출과 같은 원하는 작업을 완료하는 방문자 및 잠재 고객의 비율을 향상시킵니다.

| KPI |
| --- |
| 전환율 |
| 잠재 고객 전환 |
| 잠재 고객당 비용 |

## 예시 전술 사용 사례

다음 예제는 이 패턴을 적용할 수 있는 특정 시나리오를 보여 줍니다.

- **조회 소스에 기반한 랜딩 페이지 헤드라인 A/B 테스트** - Google, 소셜 미디어 또는 직접 트래픽에서 도착하는 방문자에 대해 다양한 헤드라인을 테스트하여 획득 채널별 참여를 최적화합니다.
- **찾아보기 동작에 따른 카테고리 친화성 권장 사항** - 검색 및 전환을 늘리기 위해 현재 세션에서 표시된 페이지에 따라 제품 또는 콘텐츠 권장 사항을 표시합니다.
- **떠나려는 방문자를 위한 종료 의도 오퍼** - 동작 신호가 방문자가 사이트를 포기하려는 것으로 표시되면 프로모션 오퍼나 리드 캡처 양식을 제공합니다.
- **지리적 타겟팅 프로모션 배너** - 방문자의 지리적 위치를 기반으로 위치별 프로모션, 스토어 로케이터 콘텐츠 또는 지역 오퍼를 표시합니다
- **장치별 콘텐츠 레이아웃 최적화** - 방문자가 데스크톱, 태블릿 또는 모바일에 있는지 여부에 따라 콘텐츠 레이아웃, 이미지 크기 및 CTA 배치를 조정합니다
- **신규 방문자와 재방문자 환영 메시지 비교** - 세션 간 ECID 지속성을 사용하여 최초 방문자와 재방문자 경험을 구별합니다.
- **현재 세션에서 본 페이지를 기반으로 한 콘텐츠 권장 사항** - 방문자가 이미 본 페이지를 기반으로 관련 문서, 제품 또는 리소스를 동적으로 표시합니다
- **UTM 캠페인 매개 변수를 기반으로 한 동적 영웅 배너** — 추천 캠페인의 메시지 또는 크리에이티브와 일치하도록 영웅 배너를 개인화합니다

## 주요 성과 지표

다음 KPI를 사용하여 이 사용 사례 패턴의 효과를 측정합니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| Personalization 노출률 | 개인화된 콘텐츠가 게재된 적격한 페이지 조회수의 비율 | AJO 캠페인 보고서: 노출 횟수 / 총 페이지 보기 수 |
| 클릭스루 비율(CTR) | 클릭으로 이어지는 개인화된 콘텐츠 노출 비율입니다. | AJO 캠페인 보고서: 클릭수 / 노출수 |
| 참여 상승도 | 페이지, 세션당 페이지 수 또는 스크롤 깊이가 개인화된 컨텐츠와 기본 컨텐츠의 시간 증가 | CJA 작업 공간 비교: 개인화된 집단 대 제어 |
| 전환율 | 원하는 작업을 완료한 개인화된 콘텐츠에 노출된 방문자의 비율 | CJA funnel 분석: 노출 > 상호 작용 > 전환 |
| 바운스 비율 감소 | 개인화된 콘텐츠를 수신한 방문자의 단일 페이지 세션 수 감소 | CJA 세션 분석: 개인화된 횟수와 기본값에 대한 바운스 비율 델타 |
| 실험 성공률 | 통계적으로 유의한 승자를 생성하는 A/B 테스트의 백분율 | AJO 실험 보고서: 신뢰 임계값에 도달하는 실험 |

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Adobe Journey Optimizer] (AJO)** — 웹 채널 표면 구성, 콘텐츠 작성(웹 및 코드 기반 경험), 캠페인 실행, 콘텐츠 실험(A/B 테스트), 의사 결정(동적 콘텐츠 선택) 및 보고
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** - 세션 내 동작 신호를 기반으로 실시간 대상 평가를 위한 Edge 세그멘테이션, 익명 Edge 프로필 관리
- **[!DNL Adobe Experience Platform] (AEP)** — 동작 신호 수집의 경우 [!DNL Web SDK], 실시간 데이터 라우팅 및 개인화 전달의 경우 [!DNL Edge Network], 데이터스트림 구성

## 아키텍처

다음 참조 아키텍처는 익명의 방문자 신호가 에지에서 수집되고, 대상 규칙에 대해 평가되며, 개인화된 콘텐츠를 전달하는 데 사용되는 방식을 보여 줍니다.

![익명 대상자 활성화 및 개인화를 위한 참조 아키텍처](/help/blueprints/audience-activation/assets/anonymous_activation.png)

## 관련 설명서

다음 Experience League 리소스는 이 사용 사례 패턴에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

**웹 채널 및 코드 기반 경험**

- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [웹 경험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [코드 기반 경험 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [코드 기반 경험 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

**대상 및 세분화**

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

**Personalization 및 컨텐츠**

- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

**콘텐츠 실험**

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [통계적 계산](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

**의사 결정 관리**

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

**캠페인**

- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

**[!DNL Web SDK]및 데이터 수집**

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [태그 개요](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

**ID 및 프로필**

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

**데이터 모델링**

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

**보고 및 분석**

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

**데이터 거버넌스 및 개인 정보 보호**

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

**보호 기능**

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
