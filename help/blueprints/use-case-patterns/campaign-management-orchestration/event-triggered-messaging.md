---
title: 이벤트 트리거된 메시징
description: 행동 또는 시스템 이벤트에 대한 응답으로 상황에 맞는 실시간 메시지를 전달하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 75137990-9848-40c0-abf3-adbd21d2de52
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1955'
ht-degree: 5%

---

# 이벤트 트리거된 메시징

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO), [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP) 및 [!DNL Adobe Experience Platform]&#x200B;(AEP)을 사용하여 동작 또는 시스템 이벤트에 대한 응답으로 상황에 맞는 실시간 메시지를 전달하는 이벤트로 트리거되는 메시징 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

이 패턴은 이벤트 수집 및 여정 생성에서부터 메시지 전달 및 성능 보고에 이르는 전체 라이프사이클을 다룹니다.

## 사용 사례 패턴

이 섹션에서는 이벤트가 트리거된 메시징을 구동하는 핵심 패턴 및 실행 계획에 대해 설명합니다.

**이벤트 트리거된 메시징**

실시간 행동 또는 시스템 이벤트를 수신한 다음 상황별 메시지를 트리거하는 프로필에 전달합니다.

**실행 계획:** 이벤트 수집 > 여정 항목 > 조건 평가 > 메시지 게재 > 보고

## 사용 사례 개요

이벤트 트리거 메시징은 실시간 행동 또는 시스템 이벤트에 대한 응답으로 컨텍스트 메시지를 제공합니다. 예약된 미리 평가된 대상자에게 보내는 배치 아웃바운드 메시지 활성화와 달리 이 패턴은 장바구니 포기, 찾아보기 세션, 양식 제출 또는 시스템 상태 변경과 같은 자격을 갖춘 이벤트를 수신하고 조건을 평가하고 메시지를 전달하는 여정에 즉시 트리거 프로필을 입력합니다.

이 패턴은 AEP(웹 SDK, 모바일 SDK 또는 서버측 API를 통해)로의 실시간 이벤트 스트리밍, AJO에 단일 이벤트 항목이 있는 여정 및 전송 여부와 내용을 결정하는 조건 평가 논리에 의존합니다. 메시지는 일반적으로 트리거 이벤트가 발생한 후 몇 분 내에 전송되므로 이 패턴은 시간에 민감하고 컨텍스트에 따라 적절한 통신에 이상적입니다.

조직은 이 패턴을 사용하여 고객 작업에 실시간으로 응답함으로써 관련성을 높이고 예약된 일괄 처리 통신에 비해 높은 참여도 및 전환율을 제공합니다. 일반적인 시나리오에는 포기한 장바구니 복구, 구매 후 후속 조치, 등록 후 환영 메시지, 결제 실패 또는 가격 하락 경고와 같은 시간에 민감한 알림이 포함됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

**[포기한 장바구니 및 여정 복구](../../business-objectives/customer-experience/recover-abandoned-carts-journeys.md)**

구매, 애플리케이션 또는 등록 중에 중단한 사용자를 적시에 개인화된 후속 조치와 함께 다시 참여시킵니다.

| KPI |
| --- |
| 전환율, 증분 수익, 참여 |

**[전환율 증가](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

구매, 등록 또는 양식 제출과 같은 원하는 작업을 완료하는 방문자 및 잠재 고객의 비율을 향상시킵니다.

| KPI |
| --- |
| 전환율, 가망 고객 전환, 가망 고객당 비용 |

**[개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.

| KPI |
| --- |
| 참여, 전환율, 고객 만족도(CSAT) |

**[고객 온보딩 개선](../../business-objectives/customer-experience/improve-customer-onboarding.md)**

능률적이고 개인화된 환영 경험과 활성화 여정을 통해 신규 고객의 가치 실현 시간을 단축합니다.

| KPI |
| --- |
| 참여, 유지, 전환율 |

## 예시 전술 사용 사례

다음 시나리오는 이벤트 트리거 메시징이 다양한 비즈니스 컨텍스트에 적용될 수 있는 방법을 보여줍니다.

- **장바구니 포기 전자 메일 또는 SMS** — 고객이 장바구니에 항목을 추가하지만 정의된 기간 내에 구매를 완료하지 않으면 알림 메시지를 보냅니다.
- **찾아보기 포기 후속 작업** - 제품이나 콘텐츠를 보았지만 전환 작업을 수행하지 않은 방문자를 다시 참여시킵니다.
- **구매 후 감사 또는 크로스셀** — 구매 이벤트 직후 확인 및 크로스셀 권장 사항을 제공합니다.
- **평가판 만료 알림** — 갱신 또는 전환 메시지를 통해 무료 평가판 종료에 가까워지는 사용자에게 알립니다.
- **등록 후 환영 메시지** — 새 사용자가 등록하거나 계정을 만들 때 즉시 온보딩 메시지를 보냅니다.
- **양식 제출 확인** — 상황별 확인을 통해 양식 제출(연락처 요청, 애플리케이션, 등록)을 확인합니다
- **결제 실패 알림** — 반복 결제가 실패하면 고객에게 경고하여 결제 정보를 업데이트하도록 합니다
- **앱 제거 win-back 푸시 알림** - 사용자가 모바일 응용 프로그램을 제거할 때 win-back 메시지를 트리거합니다.
- **예약 또는 약속 확인** — 예약, 예약 또는 약속이 예약된 후 즉시 확인을 보냅니다.
- **위시리스트 항목에 대한 가격 하락 경고** — 위시리스트에 있는 제품의 가격이 하락하면 고객에게 알립니다.

## 주요 성과 지표

다음 KPI는 이벤트가 트리거된 메시징 구현의 효과를 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 전환율 | 원하는 작업(구매, 등록, 갱신)을 완료하는 트리거된 메시지 수신자의 백분율 | 전환/게재된 메시지 * 100 |
| 증분 수익 | 전송 안 함 제어 그룹에 비해 이벤트가 트리거된 메시지로 인한 추가 매출 | 트리거된 전송에서의 수익 - 컨트롤 그룹 기준선 |
| 열람률 | 수신자가 연 게재된 메시지 비율 | 열기/게재됨 * 100 |
| 클릭스루 비율(CTR) | 최소 한 번의 클릭을 생성하는 게재된 메시지 비율 | 클릭 수 / 게재됨 * 100 |
| 전환 시간 | 메시지 게재와 전환 이벤트 사이의 평균 경과 시간 | 평균(전환 타임스탬프 - 게재 타임스탬프) |
| 여정 완료율 | 여정에 들어가서 메시지 게재 단계에 도달하는 프로필의 비율 (조건 또는 종료에 의해 삭제되지 않음) | 게재 중인 프로필 / 여정 중인 프로필 * 100 |
| 메시지 비표시 비율 | 빈도 제한, 동의 또는 상태 평가로 인해 제외된 적격 프로필의 비율 | 제외된 프로필 / 총 적격 프로필 * 100 |
| 바운스 비율 | 하드 바운스 또는 소프트 바운스로 인해 배달되지 못한 메시지 비율 | 바운스 수 / 전송됨 * 100 |

## 애플리케이션

이 사용 사례 패턴에는 다음 Adobe 애플리케이션이 사용됩니다.

- **[!DNL Adobe Journey Optimizer](AJO)** — 단일 이벤트 항목, 조건 평가, 대기 단계, 메시지 작성, 채널 구성, 빈도 거버넌스 및 게재 보고와 함께 여정 오케스트레이션
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** - 여정, 동의 및 거버넌스 적용, 프로필 강화 내에서의 조건 기반 필터링에 대한 대상 평가
- **[!DNL Adobe Experience Platform](AEP)** — 웹 SDK, Mobile SDK 또는 서버측 API를 통한 실시간 이벤트 수집, 데이터 모델링, ID 확인, Edge Network

## 관련 설명서

다음 리소스는 이 구현에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

### 여정 편성

- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [여정 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [일반 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [대상자 선별 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [조건 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [여정에 메시지 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [여정 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [이메일 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [제외 목록 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### 메시지 작성 및 개인화

- [이메일 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [SMS 메시지 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [푸시 알림 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### 빈도 및 비즈니스 규칙

- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [비즈니스 규칙 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [최대 가용량 API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces/capping)

### 충돌 및 우선 순위 관리

- [충돌 및 우선 순위 관리 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [여정 한도 및 중재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### 보고 및 성능

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### 데이터 수집 및 수집

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [스트리밍 수집 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### 데이터 모델링 및 스키마

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### ID 및 프로필

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [아이덴티티 그래프 연결 규칙](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### 세분화 및 대상자

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### 데이터 거버넌스 및 동의

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### 계산된 속성

- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [계산된 속성 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

### 모니터링 및 가시성

- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### 튜토리얼 및 안내서

- [여정 자습서 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
