---
title: Decisioning을 사용한 크로스 채널 여정
description: 최적의 채널, 컨텐츠 또는 오퍼를 선택하기 위한 실시간 의사 결정을 통합하는 여러 단계 여정을 오케스트레이션하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: eabdd91f-bb7d-4de3-adb5-5940d3ca4a78
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 5%

---

# 의사 결정을 통한 크로스 채널 여정

이 안내서에서는 [!DNL Adobe Journey Optimizer] 및 [!DNL Adobe Real-Time Customer Data Platform]을(를) 사용하여 하나 이상의 여정 노드에서 실시간 의사 결정을 통합하는 다단계 다중 채널 여정을 오케스트레이션하는 의사 결정 사용 사례 패턴을 사용하는 크로스 채널 여정에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

의사 결정을 사용한 크로스 채널 여정은 [!DNL Adobe Experience Platform] 에코시스템에서 가장 정교한 캠페인 오케스트레이션 패턴입니다. 실시간 의사 결정을 통합하여 여러 단계로 오케스트레이션된 여정을 확장합니다. [!DNL AJO] 의사 결정을 사용하여 프로필의 현재 컨텍스트를 평가하고 여정 캔버스 내 하나 이상의 의사 결정 지점에서 최적의 채널, 콘텐츠 또는 오퍼를 동적으로 선택합니다.

## 사용 사례 패턴

**의사 결정 포함 크로스 채널 여정**

하나 이상의 노드에서 실시간 의사 결정을 통합하는 다단계 멀티채널 여정을 오케스트레이션하여 최적의 채널, 컨텐츠 또는 오퍼를 선택합니다.

**실행 계획:** 대상 평가 > 여정 실행 > 의사 결정 노드 > 채널 선택 > 메시지 게재 > 보고

## 사용 사례 개요

조직은 고정된 사전 결정된 시퀀스를 따르는 대신 각 개인의 실시간 컨텍스트에 동적으로 반응하는 개인화된 적응형 고객 여정을 제공해야 하는 경우가 점점 늘어나고 있습니다. 고객이 선호하는 채널, 참여 내역, 충성도 계층, 예측된 라이프타임 값 및 현재 제품 관심사는 모두 각 접점에서 다음 작업이 되어야 하는 요소에 영향을 줍니다.

의사 결정이 있는 크로스 채널 여정은 두 가지 강력한 [!DNL AJO] 기능인 여정 오케스트레이션(여러 단계 흐름, 타이밍, 조건 및 채널 전달을 관리)과 의사 결정(자격 규칙을 평가하고 등급 전략을 적용하고 각 의사 결정 지점에서 최적 오퍼 또는 콘텐츠 변형을 선택)을 결합하여 이 문제를 해결합니다.

이 패턴은 다음과 같은 경우에 적합합니다.

- 여정은 고정된 채널 또는 컨텐츠 시퀀스를 따르는 것이 아니라 각 프로필의 실시간 상태에 동적으로 적응해야 합니다
- 여러 오퍼, 콘텐츠 변형 또는 채널은 하나 이상의 여정 노드에서 후보이며 프로필 컨텍스트를 기반으로 최상의 옵션을 선택해야 합니다
- 여정 전반에서 오퍼 선택을 최적화하려면 AI 지원 또는 수식 기반 순위가 필요합니다
- 이 조직은 복잡한 분기 로직을 유지하는 대신 채널 선택 논리와 오퍼 관리를 중앙 집중식 의사 결정 프레임워크로 통합하고자 합니다

타겟 대상에는 라이프사이클 프로그램, 충성도 여정, 윈백 시퀀스 및 온보딩 플로우를 관리하는 마케터가 포함됩니다. 이 경우 규모에 맞게 개인화하려면 각 접점에서 자동화된 의사 결정이 필요합니다.

>[!NOTE]
>여정에 개별 노드에서 동적 의사 결정(예: 고정 시퀀스 육성 또는 온보딩 프로그램)이 필요하지 않은 경우 [여러 단계로 구성된 오케스트레이션된 여정](multi-step-orchestrated-journey.md)을 참조하십시오. 이 패턴은 구성이 더 간단하며 AJO Decisioning이 필요하지 않습니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

**[개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.
**KPI:** 참여, 전환율, 고객 만족도(CSAT)

**[고객 충성도 및 라이프타임 값 증가](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
고객 관계를 심화하고 충성도 프로그램, 보상 및 개인화된 참여를 통해 장기적인 가치를 극대화합니다.
**KPI:** 고객 생애 가치, 유지, 상향 판매/교차 판매 %

**[고객 유지 개선](../../business-objectives/customer-experience/improve-customer-retention.md)**
가치 중심의 경험과 지속적인 관계 관리를 통해 기존 고객의 참여와 갱신을 유지합니다.
**KPI:** 유지, 고객 생애 가치, 참여

**[교차 판매 및 상향 판매 매출 촉진](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
행동 및 구매 내역을 기반으로 기존 고객에게 보완 및 프리미엄 제품 또는 서비스를 홍보합니다.
**KPI:** 상향 판매/교차 판매 %, 증분 수익, 고객 생애 가치

## 예시 전술 사용 사례

다음 시나리오는 의사 결정을 통해 크로스 채널 여정을 실제로 적용하는 방법을 보여줍니다.

- **적응형 되먹임 여정** — 의사 결정에서 각 프로필의 참여 기록을 기반으로 채널(이메일, 푸시 또는 SMS)을 선택하고 예측된 라이프타임 값을 기반으로 최고의 인센티브 오퍼를 동적으로 선택하는 다단계 여정
- **다음 단계 라이프사이클 여정** — 의사 결정은 고객 라이프사이클의 각 단계에서 전달할 내용을 결정하며 온보딩 콘텐츠, 교차 판매 오퍼, 충성도 보상 또는 유지 인센티브에서 선택합니다
- **다이내믹 콘텐츠 선택을 통해 개인화된 온보딩** — 각 터치포인트가 의사 결정을 사용하여 가장 관련성이 높은 제품 교육 콘텐츠, 팁 또는 활성화 오퍼를 선택하는 새로운 고객 온보딩 여정
- **개인화된 보상을 포함하는 크로스 채널 충성도 프로그램 여정** — 충성도 멤버는 의사 결정에서 계층, 구매 내역 및 카테고리 관심도에 따라 개인화된 보상 오퍼를 선택하는 여정을 통해 진행됩니다.
- **채널 및 인센티브 최적화를 통한 동적 재참여** - 응답 확률을 극대화하기 위해 도달 채널과 인센티브가 모두 동적으로 선택되는 휴면 상태 고객 재참여
- **AI 등급 콘텐츠 추천을 통한 고객 라이프사이클 육성** — 각 접점에서 AI 등급 결정이 가장 관련성이 높은 콘텐츠 또는 제품 추천을 선택하는 지속적인 육성 여정

## 주요 성과 지표

다음 KPI를 사용하여 이 사용 사례 패턴의 효과를 측정합니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 여정 완료율 | 전체 여정을 완료하는 프로필 비율 | 여정 보고서: 완료/입력됨 |
| 오퍼 수락율 | 참여(클릭, 상환)한 의사 결정 선택 오퍼의 비율 | Decisioning 보고서: 오퍼 클릭수 / 오퍼 노출 횟수 |
| 채널 참여 비율 | 여정에 사용된 각 채널 간 열람율 및 클릭률 | 여정 보고서의 채널당 게재 지표 |
| 전환율 | 타겟 전환 작업을 완료하는 여정 참가자의 백분율 | 여정 종료 이벤트 추적 또는 CJA funnel 분석 |
| 대체 오퍼 비율 | 개인화된 오퍼 대신 대체 오퍼를 반환하는 의사 결정 요청의 비율 | 의사 결정 보고서: 대체 선택 항목 / 총 선택 항목 |
| 고객 생애 가치 영향 | 여정 참여자와 컨트롤 그룹의 CLV 변경 | 홀드아웃 비교가 포함된 CJA 집단 분석 |
| 교차 판매/상향 판매 수익 | 의사 결정 선택 오퍼로 인한 증분 매출 | 오퍼 기반 전환에 대한 CJA 속성 분석 |
| 의사 결정 순위 효율성 | AI 등급 오퍼와 무작위/우선 순위 기반 선택 간의 성능 차이 | 순위 전략을 비교하는 A/B 실험 |

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Adobe Journey Optimizer] ([!DNL AJO])** — 여정 오케스트레이션(다단계 캔버스 디자인, 시작 조건, 대기, 조건, 종료 기준), 채널 간 메시지 작성, 채널 표면 구성, 충돌 및 우선 순위 관리
- **[!DNL Adobe Journey Optimizer]의사 결정** — 오퍼 및 콘텐츠 항목 관리, 자격 규칙, 순위 전략(우선 순위, 공식, AI), 의사 결정 정책, 배치, 대체 오퍼
- **[!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP])** — 여정 입력 및 오퍼 자격 세그먼트에 대한 대상 평가, 계산된 특성 및 성향 점수를 통한 프로필 강화, 동의 및 거버넌스 적용
- **[!DNL Adobe Experience Platform] ([!DNL AEP])** — 실시간 고객 프로필 스토어, 크로스 채널 해결을 위한 ID 서비스, 데이터 모델링 및 수집 인프라

## 관련 설명서

다음 리소스는 이 사용 사례 패턴에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

### 여정 편성

- [여정 시작](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [여정 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [대상자 활동 읽기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [일반 이벤트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [대상자 선별 이벤트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [조건 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [여정에 메시지 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [여정 테스트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

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
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [이메일 표면 설정](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS 채널 구성](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 메시지 작성 및 개인화

- [이메일 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/create-email)
- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 충돌, 우선순위 및 빈도 관리

- [충돌 및 우선 순위 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [우선 순위 점수](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [여정 한도 및 중재](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/edge-segmentation)
- [대상자 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language 참조](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/pql/overview)

### 보고 및 분석

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [CJA 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/home)

### 프로필 및 ID

- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/home)
- [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home)
- [병합 정책 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/merge-policies/overview)
- [계산된 속성 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/overview)
- [Customer AI 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/intelligent-services/customer-ai/overview)

### 데이터 거버넌스 및 동의

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [제외 목록 관리](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/guardrails)
