---
title: 사용 사례 패턴
description: 주요 비즈니스 목표를 달성하기 위한 Adobe Experience Platform 및 애플리케이션 구현 사용 사례 패턴에 대해 알아봅니다.
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
doc-type: overview-page
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 사용 사례 패턴

사용 사례 패턴은 Adobe Experience Platform 및 애플리케이션에 대한 반복 가능한 구현 접근 방식을 정의합니다. 각 패턴은 특정 기능, 기능을 제공하는 기능 체인, 관련 애플리케이션 및 지원하는 [주요 비즈니스 목표](/help/blueprints/business-objectives/overview.md)를 설명합니다.

아래 표를 사용하여 구현 요구 사항과 일치하는 패턴을 찾은 다음 옵션, 단계, 의사 결정 지침 및 Experience League 설명서를 포함한 전체 구현 참조에 대한 링크를 따르십시오.

## 대상자 구축 및 활성화

다음 패턴은 채널 및 대상 전반에서 대상 세그먼트를 만들고, 평가하고, 활성화하는 데 도움이 됩니다.

| 패턴 | 기본 기능 | 핵심 솔루션 |
| --- | --- | --- |
| 대상에 대한 [Audience Activation](audience-building-activation/audience-activation-to-destinations.md) | 타깃팅 또는 제외를 위해 대상 세그먼트를 평가하고 외부 대상에 게시합니다. | [!DNL Real-Time CDP] |
| [세그먼트가 일치하는 Audience Collaboration](audience-building-activation/audience-collaboration-segment-match.md) | 세그먼트 일치를 사용하여 샌드박스 또는 조직에서 대상 세그먼트 공유 및 일치 | [!DNL Real-Time CDP], [!DNL Experience Platform] |
| [이벤트 전달](audience-building-activation/event-forwarding.md) | Edge Network을 통해 수집된 실시간 이벤트 데이터를 Adobe이 아닌 대상으로 전달 | [!DNL Experience Platform]&#x200B;(Edge Network, 이벤트 전달) |
| [B2B 대상자 활성화](audience-building-activation/b2b-audience-activation.md) | 웹, 이메일 및 광고 채널에서 계정 기반 B2B 대상 활성화 | [!DNL Real-Time CDP] B2B edition |

## 개인화

다음 패턴은 웹 및 앱 표면 전반에 걸쳐 알려진 방문자와 알 수 없는 방문자에게 맞춤 경험을 제공합니다.

| 패턴 | 기본 기능 | 핵심 솔루션 |
| --- | --- | --- |
| [익명 방문자 웹 Personalization](personalization/anonymous-visitor-web-personalization.md) | 미확인된 방문자에 대한 세션 내 행동 신호를 기반으로 개인화된 콘텐츠 전달 | [!DNL Journey Optimizer]&#x200B;(웹 채널), [!DNL Real-Time CDP] |
| [알려진 방문자 웹/앱 Personalization](personalization/known-visitor-web-app-personalization.md) | 실시간 프로필 및 세그먼트 멤버십을 기반으로 식별된 방문자에게 개인화된 콘텐츠, 오퍼 또는 프로모션을 제공합니다 | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Offer Decisioning](personalization/offer-decisioning.md) | 중앙 집중식 의사 결정 논리를 사용하여 여러 채널에서 프로필에 대한 차선책 오퍼 또는 콘텐츠를 선택합니다 | [!DNL Journey Optimizer]&#x200B;(Decisioning), [!DNL Real-Time CDP] |
| [동작 권장 사항](personalization/behavioral-recommendation.md) | 선택 전략 및 등급 모델을 사용하여 항목 및 컨텐츠 권장 사항 생성 | [!DNL Journey Optimizer]&#x200B;(Decisioning), [!DNL Real-Time CDP] |

## 캠페인 관리 및 오케스트레이션

다음 패턴에서는 채널 간 예약, 트리거 및 여러 단계 메시지 전달을 다룹니다.

| 패턴 | 기본 기능 | 핵심 솔루션 |
| --- | --- | --- |
| [아웃바운드 메시지 일괄 활성화](campaign-management-orchestration/batch-outbound-message-activation.md) | 대상자를 평가한 다음 예약된 아웃바운드 메시지를 단일 배치 실행으로 전달 | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [이벤트 트리거된 메시징](campaign-management-orchestration/event-triggered-messaging.md) | 실시간 행동 또는 시스템 이벤트를 수신한 다음 상황별 메시지를 트리거하는 프로필에 전달합니다 | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [여러 단계로 조정된 여정](campaign-management-orchestration/multi-step-orchestrated-journey.md) | 대기, 조건 및 여러 메시지 작업을 사용하는 분기, 다중 터치 여정을 통해 프로필 안내 | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [Decisioning을 사용한 크로스 채널 여정](campaign-management-orchestration/cross-channel-journey-with-decisioning.md) | 최적의 채널, 컨텐츠 또는 오퍼를 선택하기 위한 실시간 의사 결정을 통합하는 여러 단계 여정 오케스트레이션 | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
| [그룹 기반 마케팅 및 여정 관리 구매](campaign-management-orchestration/buying-group-based-marketing.md) | 잠재 고객을 구매 그룹으로 분류하여 B2B 마케팅 효과를 향상시키는 계정 수준 여정을 개발합니다. | [!DNL Journey Optimizer] B2B edition, [!DNL Real-Time CDP] B2B edition |

## Analysis

다음 패턴은 크로스 채널 행동 및 성능 분석을 지원합니다.

| 패턴 | 기본 기능 | 핵심 솔루션 |
| --- | --- | --- |
| [Customer Analytics 및 Insight 생성](analysis/customer-analytics-insight-generation.md) | 비헤이비어 및 성능 분석을 위한 크로스 채널 분석 작업 공간, 계산된 지표 및 대시보드 구축 | [!DNL Customer Journey Analytics], [!DNL Experience Platform] |
| [B2B 분석](analysis/b2b-analytics.md) | 크로스 채널 고객 여정 분석에 B2B 계정 수준 정보 포함 | [!DNL Customer Journey Analytics] B2B edition, [!DNL Real-Time CDP] B2B edition |

## 대화 경험

다음 패턴은 디지털 속성에서 AI 기반의 브랜드 안전한 대화 상호 작용을 가능하게 합니다.

| 패턴 | 기본 기능 | 핵심 솔루션 |
| --- | --- | --- |
| [Brand Concierge 대화 경험](conversational-experience/brand-concierge-conversational-experience.md) | 디지털 속성을 고객 검색을 안내하는 AI 기반의 브랜드 안전 대화 환경으로 전환 | [!DNL Brand Concierge], [!DNL Experience Platform], [!DNL Real-Time CDP] |
