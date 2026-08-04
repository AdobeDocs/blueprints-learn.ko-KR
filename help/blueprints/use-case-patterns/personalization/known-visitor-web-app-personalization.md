---
title: 알려진 방문자 웹/앱 Personalization
description: 실시간 프로필 및 세그먼트 멤버십을 기반으로 식별된 방문자에게 개인화된 콘텐츠, 오퍼 또는 프로모션을 제공하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 585adc0e-f528-4a09-b931-ef6b45fa8ec8
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1819'
ht-degree: 4%

---

# 알려진 방문자 웹/앱 개인화

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) 및 [!DNL Adobe Real-Time Customer Data Platform]&#x200B;(RT-CDP)을 사용하여 디지털 표면에 걸쳐 식별된 방문자에게 개인화된 콘텐츠를 제공하는 알려진 방문자 웹/앱 개인화 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

알려진 방문자 웹/앱 개인화는 인증된 디지털 경험에 대한 기본 개인화 패턴입니다. 세션 내 동작 신호에만 의존하는 익명 방문자 개인화와 달리, 이 패턴은 이전 동작 데이터, 세그먼트 멤버십, 충성도 계층, 구매 기록, 라이프사이클 단계, 계산된 속성 및 성향 점수와 같은 전체 통합 프로필을 활용합니다. AJO 웹 채널을 통한 웹 페이지, 모바일 인앱 메시지 및 콘텐츠 카드 전반에서 개인화를 지원합니다.

## 사용 사례 패턴

이 섹션에서는 핵심 패턴과 해당 실행 계획에 대해 설명합니다.

**알려진 방문자 웹/앱 개인화**

웹, 모바일 인앱 및 콘텐츠 카드 표면 전반의 실시간 프로필 및 세그먼트 멤버십을 기반으로 식별된 방문자에게 개인화된 콘텐츠, 오퍼 또는 프로모션을 제공합니다.

**실행 계획:** 대상 평가 > Personalization Decisioning > 표면/채널 구성 > 콘텐츠 게재 > 노출 추적 > 보고

## 사용 사례 개요

전자 상거래 사이트, 뱅킹 포털, 구독 서비스, 로열티 프로그램, 모바일 앱과 같은 인증된 디지털 속성을 보유한 조직은 브랜드와 각 고객의 관계를 반영하는 개인화된 경험을 제공해야 합니다. 방문자가 로그인하거나 ID 확인을 통해 인식되면 플랫폼은 전체 통합 프로필에 액세스하여 특정 속성, 동작 및 환경 설정에 따른 콘텐츠를 제공할 수 있습니다.

이 패턴은 식별된 방문자가 웹 속성에 도달하거나 모바일 앱을 여는 시나리오를 해결하며, 시스템은 실시간 프로필 데이터 및 대상 멤버십을 기반으로 표시할 최적의 콘텐츠, 오퍼 또는 프로모션을 결정해야 합니다. 개인화 결정은 에지(밀리초)에서 발생하며 가시 지연 없이 초 미만의 콘텐츠 전달을 활성화합니다.

이 패턴은 결정론적 개인화(특정 콘텐츠가 특정 대상 세그먼트에 매핑되는 경우)와 동적 의사 결정(AJO Decisioning이 자격 규칙 및 등급 전략을 평가하여 프로필별로 최적의 콘텐츠를 선택하는 경우)을 모두 지원합니다. 웹 페이지, 모바일 인앱 메시지 및 컨텐츠 카드 등 여러 디지털 표면에 걸쳐 있으므로 고객의 디지털 여정 전반에 걸쳐 일관된 개인화가 가능합니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 개인화된 고객 경험 전달

콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다. 자세한 내용은 [개인화된 고객 경험 전달](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)을 참조하십시오.

**KPI:** 참여, 전환율, 고객 만족도(CSAT)

### 웹 사이트 참여 늘리기

관련 경험을 통해 사이트에서 보낸 시간, 세션당 페이지 수 및 웹 콘텐츠와의 상호 작용을 개선합니다. 자세한 내용은 [웹 사이트 참여 늘리기](../../business-objectives/acquisition-growth/increase-website-engagement.md)를 참조하십시오.

**KPI:** 웹 페이지 체류 시간, 참여, 전환율

### 모바일 앱 참여 늘리기

개인화된 인앱 경험을 통해 일일 활성 사용량, 기능 채택 및 인앱 전환을 유도합니다.

**KPI:** 참여, 유지, 전환율

## 예시 전술 사용 사례

다음은 이 패턴의 일반적인 전술적 구현입니다.

- 충성도 계층 또는 라이프사이클 단계에 의한 홈 페이지 영웅 개인화 - 고객이 신규 고객인지, 활성 고객인지, 위험 고객인지 또는 VIP 고객인지에 따라 다른 영웅 배너를 표시합니다
- 구매 내역을 기반으로 한 제품 추천 캐러셀 - 과거 구매 데이터 및 제품 선호도 점수를 사용하여 관련 제품 제안을 표시합니다
- 고객 세그먼트별로 개인화된 프로모션 배너 - 고가치, 위험 및 새로운 고객 세그먼트에 대한 다양한 프로모션 표시
- 기능 채택을 기반으로 하는 모바일 사용자를 위한 인앱 메시지 - 사용 패턴에 따라 활용도가 낮은 기능을 안내합니다
- 계정 대시보드에 개인화된 오퍼가 있는 컨텐츠 카드 - 고객의 프로필에 맞게 맞춤화된 영구적이고 판매 불가능한 오퍼
- 고객 계층을 기반으로 한 맞춤형 가격 또는 할인 표시 - 등급별 가격 또는 고객 충성도 프로그램 회원에 대한 단독 할인 표시
- 소유 제품 기반 교차 판매 추천 위젯 — 현재 포트폴리오를 기반으로 보완 제품 또는 서비스 제안
- 관심 영역을 기반으로 개인화된 탐색 또는 콘텐츠 정렬 — 표시된 환경 설정을 기반으로 콘텐츠 모듈 또는 탐색 요소 재정렬

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 효과를 측정하는 데 도움이 됩니다.

| KPI | 측정 접근 방식 | 벤치마크 지침 |
| --- | --- | --- |
| Personalization 참여율 | 노출에 따라 구분된 개인화된 콘텐츠 요소와의 클릭 및 상호 작용 | 개인화된 컨텐츠는 기본 컨텐츠보다 20~50% 더 뛰어난 성과를 보여야 합니다. |
| 전환율 상승도 | 맞춤형 경험 대 제어/기본 경험에 대한 전환율 | 개인화되지 않은 경험에 대해 10~30% 상승도를 Target으로 지정 |
| 클릭스루 비율(CTR) | 개인화된 CTA, 오퍼 및 권장 사항을 노출로 나눈 클릭 | 표면(웹, 인앱, 콘텐츠 카드) 및 세그먼트당 모니터링 |
| 방문당 매출 | 개인화된 경험이 있는 세션에 따른 매출 | 개인화된 방문자 집단과 개인화되지 않은 방문자 집단 비교 |
| 컨텐츠 카드 상호 작용률 | 노출 횟수에 따른 컨텐츠 카드 클릭 및 해제 | 카드 유형 및 대상 세그먼트당 추적 |
| 인앱 메시지 참여 | 노출 횟수에 따른 인앱 메시지 상호 작용(CTA 클릭, 해제) | 대상 세그먼트 및 메시지 유형 간 비교 |
| 페이지에서 시간 | 개인화된 콘텐츠가 있는 페이지에서 보낸 평균 시간과 기본값 | 개인화된 페이지에 체류 시간이 늘어남 |
| 오퍼 수락율 | 전환 이벤트를 발생시키는 의사 결정 선택 오퍼의 비율 | 오퍼당, 배치당 및 순위 전략당 추적 |

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Adobe Journey Optimizer] (AJO)** — 웹 채널 구성, 인앱 채널 구성, 콘텐츠 카드 채널 구성, 의사 결정(오퍼 선택 및 등급), 메시지 작성(개인화된 콘텐츠 만들기), 캠페인 실행, 콘텐츠 실험 및 보고
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — 대상 평가(에지, 스트리밍 및 일괄 처리), Edge Network을 통한 실시간 프로필 조회, 계산된 특성 및 성향 점수를 통한 프로필 보강
- **[!DNL Adobe Experience Platform] (AEP)** — 프로필 저장소, ID 서비스, Web SDK, Mobile SDK, 데이터스트림 구성, Edge Network Delivery

## 관련 설명서

다음 리소스는 이 안내서에서 참조하는 기술 및 구성에 대한 추가 세부 정보를 제공합니다.

### 웹 채널 개인화

- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [웹 경험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [웹 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)

### 인앱 및 콘텐츠 카드 채널

- [인앱 채널 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [인앱 채널 사전 요구 사항](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [인앱 메시지 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [콘텐츠 카드 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [콘텐츠 카드 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)
- [콘텐츠 카드 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### 의사 결정 관리

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Personalization 및 콘텐츠

- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### ID 및 프로필

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [아이덴티티 그래프 연결 규칙](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### 데이터 수집 및 SDK

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### 캠페인 및 실험

- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### 계산된 속성 및 데이터 보강

- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [계산된 속성 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Customer AI 개요](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### 보고 및 분석

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### 거버넌스 및 개인 정보 보호

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
