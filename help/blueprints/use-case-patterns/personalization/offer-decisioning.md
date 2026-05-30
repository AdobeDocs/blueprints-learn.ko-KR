---
title: Offer Decisioning
description: 중앙 집중식 의사 결정 논리를 사용하여 여러 채널에서 프로필에 대한 차선책 오퍼 또는 콘텐츠를 선택하는 방법에 대해 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 8fd511b3-0200-41bf-aff1-e3f2a00a578e
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 5%

---

# Offer Decisioning

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) Decisioning과 [!DNL Adobe Real-Time Customer Data Platform]&#x200B;(RT-CDP)을 사용하여 여러 채널에서 각 고객 프로필에 대한 차선책을 결정하는 중앙 집중식 오퍼 선택 논리를 구현하는 Offer Decisioning 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

패턴은 &quot;표시할 위치&quot; 채널 논리에서 &quot;표시할 항목&quot; 결정을 분리하여 이메일, 웹, 모바일 앱 및 기타 모든 터치포인트에서 일관되고 최적화된 오퍼 선택을 활성화합니다. AJO Decisioning은 오퍼 생성 및 카탈로그 관리, 자격 규칙(각 오퍼를 볼 수 있는 사용자), 순위 전략(적격 오퍼 중에서 선택하는 방법), 배치(오퍼가 표시되는 위치) 및 의사 결정 정책(모든 것을 결합하는)과 같은 전체 오퍼 라이프사이클을 관리합니다.

## 사용 사례 패턴

이 섹션에서는 Offer Decisioning의 실행 계획 및 패턴 정의에 대해 설명합니다.

**Offer Decisioning**

중앙 집중식 의사 결정 논리를 사용하여 여러 채널에서 프로필에 대한 차선책 오퍼 또는 콘텐츠를 선택합니다.

**실행 계획:** 대상 평가 > 오퍼 자격 > 순위 전략 > 의사 결정 실행 > 게재 > 보고

## 사용 사례 개요

조직은 상호 작용 시 각 고객에게 가장 관련성이 높은 오퍼, 프로모션 또는 인센티브를 제공해야 하는 경우가 많습니다. 상호 작용이 이메일 여정, 웹 사이트 홈페이지, 모바일 앱 내에서 또는 여러 단계 캠페인의 결정 지점에서 발생하든지 상관없이, 당면 과제는 동일합니다. 고객이 누구이고, 고객이 무엇을 검증하고, 어떤 오퍼가 원하는 결과를 도출할 수 있는지에 따라 사용 가능한 옵션 카탈로그에서 최적 오퍼를 선택합니다.

Offer Decisioning은 AJO의 의사 결정 관리 엔진에서 모든 오퍼 선택 논리를 중앙 집중화하여 이를 해결합니다. 의사 결정 엔진은 오퍼 할당을 개별 캠페인이나 채널로 하드코딩하는 대신 각 프로필의 속성, 대상 멤버십 및 컨텍스트 신호를 평가하여 실시간으로 최상의 오퍼를 결정합니다. 이러한 중앙 집중화를 통해 동일한 고객이 어떤 채널을 통해 접속하는지에 관계없이 일관되고 최적화된 오퍼를 받을 수 있습니다.

이 패턴은 범위가 알려진 방문자 웹/앱 개인화와는 다릅니다. offer decisioning은 채널과 관계없고 중앙 집중화된 반면, 알려진 방문자 개인화는 디지털 표면 개인화에 중점을 둡니다. 이것은 카탈로그 모델의 행동 권장 사항과 다릅니다. 적격 항목 세트가 비즈니스 규칙, 자격 제한 또는 규제 요구 사항(프로모션, 금융 제품, 인센티브)에 의해 제어되는 경우 Offer Decisioning을 사용합니다. 항목 세트가 크고 지속적으로 변경되며 선택 사항이 행동 유사성 또는 선호도 신호(제품 카탈로그, 콘텐츠 라이브러리)에 의해 주도되는 경우 행동 권장 사항을 사용하십시오.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

**[개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.
**KPI:** 참여, 전환율, 고객 만족도(CSAT)

**[교차 판매 및 상향 판매 매출 촉진](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
행동 및 구매 내역을 기반으로 기존 고객에게 보완 및 프리미엄 제품 또는 서비스를 홍보합니다.
**KPI:** 상향 판매/교차 판매 %, 증분 수익, 고객 생애 가치

**[고객 충성도 및 라이프타임 값 증가](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
고객 관계를 심화하고 충성도 프로그램, 보상 및 개인화된 참여를 통해 장기적인 가치를 극대화합니다.
**KPI:** 고객 생애 가치, 유지, 상향 판매/교차 판매 %

## 예시 전술 사용 사례

다음 시나리오에서는 offer decisioning 을 실제로 적용하는 방법을 보여 줍니다.

- 이메일 캠페인의 다음 베스트 오퍼 — 전송 시 수신자별로 가장 관련성이 높은 프로모션을 선택합니다.
- 웹 사이트의 실시간 프로모션 배너 — 의사 결정은 방문자의 프로필을 기반으로 페이지 로드 시 오퍼를 선택합니다.
- 사용자의 라이프사이클 단계에 가장 좋은 인센티브를 제공하는 개인화된 인앱 카드
- 크로스 채널 오퍼 일관성 — 동일한 의사 결정 로직이 이메일, 웹 및 푸시를 제공하므로 고객은 통합된 오퍼 경험을 볼 수 있습니다.
- 고객 가치 계층에 따라 동적 쿠폰 또는 할인 선택(예: 고가치 고객은 프리미엄 오퍼를 받음)
- 현재 구독 수준에 따라 제품 업그레이드 또는 상향 판매 오퍼 선택
- 계층 및 활동 내역을 기반으로 한 충성도 보상 오퍼 개인화

## 주요 성과 지표

다음 KPI는 Offer Decisioning 구현의 효과를 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 오퍼 수락율 | 클릭, 상환 또는 전환을 초래하는 게재된 오퍼의 비율 | 오퍼 클릭 수 또는 상환 횟수/게재된 총 오퍼 수 |
| 오퍼 선택 배포 | 모든 의사 결정에서 선택한 각 오퍼의 비율 | 오퍼당 카운트 / 렌더링된 총 의사 결정 |
| 대체 비율 | 자격이 있는 개인화된 오퍼와 대체 항목이 제공된 의사 결정의 비율 | 대체 노출 횟수 / 총 결정 수 |
| 전환율 | 원하는 작업(구매, 등록, 상환)을 완료한 오퍼 수신자의 비율 | 전환/오퍼 노출 횟수 |
| 증분 수익 | 선택한 오퍼와 컨트롤 그룹 또는 대체 오퍼를 비교하여 발생하는 수익 | 개인화된 오퍼의 수익 - 대체/제어의 수익 |
| 크로스 채널 일관성 점수 | 정의된 기간 내의 여러 채널에서 동일한 오퍼를 받는 프로필의 비율 | 일관된 오퍼 / 총 멀티채널 노출 횟수 |
| 오퍼 클릭스루 비율 | 클릭을 발생시키는 오퍼 노출 비율입니다. | 오퍼 클릭수 / 오퍼 노출 횟수 |

## 애플리케이션

이 사용 사례 패턴에는 다음 Adobe 애플리케이션이 사용됩니다.

- **[!DNL Adobe Journey Optimizer] (AJO)** — 오퍼 만들기, 자격 규칙, 순위 전략, 배치 및 의사 결정 정책을 위한 의사 결정 관리 엔진, 오퍼 게재를 위한 채널 구성 및 메시지 작성, 캠페인 및 여정 실행
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — 오퍼 자격 세그먼트에 대한 대상 평가, 자격 및 순위에 사용되는 프로필 데이터 및 계산된 속성
- **[!DNL Adobe Experience Platform] (AEP)** - AJO과 RT-CDP를 모두 지원하는 통합 프로필 저장소, ID 확인 및 데이터 파운데이션

## 관련 설명서

다음 리소스는 이 사용 사례 패턴에 사용되는 구성 요소에 대한 추가 세부 정보를 제공합니다.

### 의사 결정 관리

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [결정 규칙 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [컬렉션 수식어 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 오퍼 게재

- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning API를 사용하여 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Decisioning API를 사용하여 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [이메일 표면 설정](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [SMS 채널 구성](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### 메시지 작성 및 개인화

- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 캠페인 및 여정

- [캠페인 시작하기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [여정 시작](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/journey)

### 콘텐츠 실험

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/edge-segmentation)

### 프로필 및 ID

- [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home)
- [병합 정책 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/merge-policies/overview)
- [계산된 속성 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/overview)
- [Customer AI 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/intelligent-services/customer-ai/overview)

### 데이터 모델링 및 수집

- [XDM 시스템 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/home)
- [웹 SDK 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/home)
- [데이터스트림 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/configure)

### 보고 및 분석

- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJA 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/home)

### 데이터 거버넌스 및 라이프사이클

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-lifecycle/home)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)

### 튜토리얼

- [의사 결정 관리 API 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
