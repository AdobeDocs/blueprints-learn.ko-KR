---
title: 행동 추천
description: 선택 전략 및 순위 모델을 사용하여 항목 및 콘텐츠 권장 사항을 생성하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: db16e773-e0da-46c4-9fa5-d16f04feb46b
source-git-commit: 9ea30e48ec0fade2f9a97b185e35fbfa93f49c43
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 5%

---

# 행동 추천

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) Decisioning, [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP) 및 [!DNL Adobe Experience Platform]&#x200B;(AEP)을 사용하여 웹, 모바일 앱 및 이메일 채널 전반에 개인화된 권장 사항 경험을 제공하는 행동 권장 사항 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

행동 권장 사항은 AJO Decisioning 선택 전략 및 등급 모델과 결합된 행동 신호(제품 보기, 구매, 콘텐츠 상호 작용, 검색 쿼리)를 사용하여 항목 수준 또는 콘텐츠 수준 권장 사항을 생성합니다. 자격 규칙 및 비즈니스 제한을 사용하여 제한된 오퍼, 프로모션 또는 인센티브 세트를 제어하는 Offer Decisioning과 달리, 이 패턴은 통제 대상 자격이 아닌 행동 친화성 신호에 의해 선택이 유도되는 크고 지속적으로 변경되는 항목 카탈로그(제품, 문서, 비디오)에서 작동합니다.

## 사용 사례 패턴

**동작 권장 사항**

행동 신호를 기반으로 AJO Decisioning 선택 전략 및 등급 모델을 사용하여 컨텍스트 기반의 콘텐츠를 제공하는 항목 수준 또는 콘텐츠 수준 권장 사항을 생성합니다.

**실행 계획:** 동작 신호 수집 > 의사 결정 전략 평가 > 권장 사항 게재 > 보고

## 사용 사례 개요

제품 카탈로그, 콘텐츠 라이브러리 또는 미디어 라이브러리가 있는 조직은 행동 기록 및 세션 내 활동을 기반으로 각 방문자에게 가장 관련성이 높은 항목을 표시해야 합니다. 홈페이지의 &quot;권장&quot; 캐러셀, 제품 세부 사항 페이지의 교차 판매 위젯 또는 이메일 캠페인에 포함된 제품 권장 사항이든 기본 문제는 동일합니다. 각 방문자의 행동 프로필을 카탈로그의 가장 관련 있는 항목에 일치시킨 다음 적절한 시점에 적절한 채널에서 이러한 권장 사항을 제공합니다.

이 패턴은 [!DNL Web SDK] 또는 [!DNL Mobile SDK]을(를) 통해 동작 신호를 실시간으로 수집하고, 항목 특성을 동작 컨텍스트와 결합하는 AJO Decisioning 선택 전략을 통해 처리하고, 웹, 인앱 또는 이메일 채널을 통해 권장 항목을 제공함으로써 이러한 문제를 해결합니다. 순위 모델은 공식 기반(예: 카테고리 친화성 점수별로 정렬) 또는 AI 등급(예: 개인화된 추천 모델)일 수 있습니다. 이 패턴은 폴백 권장 사항을 구성하여 동작 기록이 없는 새 방문자에 대한 콜드 스타트 시나리오도 처리합니다.

이 패턴의 타겟 대상에는 전자 상거래 머천다이징 팀, 콘텐츠 개인화 팀 및 실제 사용자 행동을 통해 제공되는 개인화된 추천을 통해 참여, 전환 및 평균 주문 가치를 개선하려는 디지털 경험 팀이 포함됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 교차 판매 및 상향 판매 매출 촉진

[교차 판매 및 상향 판매 매출 촉진](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

행동 및 구매 내역을 기반으로 기존 고객에게 보완 및 프리미엄 제품 또는 서비스를 홍보합니다.

**KPI:** 상향 판매/교차 판매 %, 증분 수익, 고객 생애 가치

### 전환율 향상

[전환율 향상](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

구매, 등록 또는 양식 제출과 같은 원하는 작업을 완료하는 방문자 및 잠재 고객의 비율을 향상시킵니다.

**KPI:** 전환율, 잠재 고객 전환, 잠재 고객당 비용

### 개인화된 고객 경험 전달

[개인화된 고객 경험 전달](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.

**KPI:** 참여, 전환율, 고객 만족도(CSAT)

## 예시 전술 사용 사례

다음은 이 패턴의 일반적인 전술적 구현입니다.

- 제품 세부 사항 페이지의 제품 교차 판매 위젯(&quot;고객이 구매함&quot;)
- 찾아보기 기록을 기반으로 한 홈 페이지 캐러셀 &quot;추천 항목&quot;
- 읽기 동작을 기반으로 한 미디어 사이트의 콘텐츠 권장 사항
- 유사한 항목 위젯과 결합된 &quot;최근에 본 항목&quot;
- 구매 후 보완 제품 권장 사항
- 행동 친화성을 기반으로 한 이메일 제품 권장 사항
- 세션 내 검색 동작을 기반으로 하는 카테고리별 권장 사항
- 동작 신호를 기반으로 검색 결과 재순위 지정

## 주요 성과 지표

다음 KPI는 행동 추천 구현의 효과를 측정하는 데 도움이 됩니다.

| KPI | 측정 접근 방식 |
| --- | --- |
| 권장 사항 클릭스루 비율(CTR) | 추천 항목을 추천 노출로 나눈 클릭 수 |
| 추천 전환율 | 추천 클릭을 총 추천 클릭으로 나눈 구매 또는 원하는 작업 |
| 권장 사항의 영향을 받는 매출 | 최소 한 개 이상의 추천 기반 제품이 포함된 주문의 총 수익 |
| AOV(평균 주문 가격) 상승도 | 권장 사항과 관련된 세션과 그렇지 않은 세션의 AOV 증가 |
| 주문당 항목 수 | 권장 사항 참여 세션의 주문당 항목 수 |
| 권장 사항 범위 | 개인화된(대체 아님) 권장 사항을 받은 적합한 페이지 보기 또는 세션의 비율 |
| 콜드-스타트 대체 비율 | 동작 기록 부족으로 인해 대체 로직에서 제공하는 추천 요청의 비율 |

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Adobe Journey Optimizer] (AJO) Decisioning** — 선택 전략, 순위 모델, 항목 카탈로그 및 동작 신호를 평가하고 각 방문자에 대해 가장 관련성이 높은 항목을 반환하는 결정 정책
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — 행동 프로필 데이터 누적, 추천 범위에 대한 대상 평가 및 행동 선호도 점수에 대한 계산된 특성
- **[!DNL Adobe Experience Platform] (AEP)** — [!DNL Web SDK] 및 [!DNL Mobile SDK]을(를) 통한 동작 이벤트 수집, [!DNL Edge Network] 처리, 이벤트 및 카탈로그 데이터에 대한 XDM 스키마 관리

## 관련 설명서

다음 리소스는 이 패턴에 사용되는 기술 및 기능에 대한 추가 세부 정보를 제공합니다.

### 의사 결정 관리

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [컬렉션 수식어 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning API를 사용하여 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### 데이터 수집 및 웹/모바일 SDK

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### XDM 및 데이터 모델링

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [데이터 세트 만들기](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create)
- [두 스키마 간의 관계 정의](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### ID 및 프로필

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### 계산된 속성 및 프로필 보강

- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [계산된 속성 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Customer AI 개요](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [채널 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### 메시지 작성 및 개인화

- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### 보고 및 분석

- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [계산된 지표 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### 데이터 거버넌스 및 라이프사이클

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [데이터 세트 만료](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### 모니터링 및 가시성

- [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)

### 튜토리얼 및 안내서

- [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [태그 개요](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
