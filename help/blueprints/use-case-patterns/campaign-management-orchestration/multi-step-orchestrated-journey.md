---
title: 여러 단계로 조정된 여정
description: 대기, 조건 및 시간 경과에 따른 여러 메시지 작업을 사용하는 분기, 다중 터치 여정을 통해 프로필을 안내하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 5667b188-1b20-4a85-aebb-74efd5f771a1
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1798'
ht-degree: 5%

---

# 여러 단계로 조정된 여정

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) 및 [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP)을 사용하여 시간에 따라 여러 메시지를 전달하는 분기, 다중 터치 고객 여정을 오케스트레이션하는 여러 단계 오케스트레이션된 여정 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

## 사용 사례 패턴

**여러 단계로 조정된 여정**

대기, 조건 및 시간 경과에 따른 여러 메시지 작업을 사용하는 분기, 다중 터치 여정을 통해 프로필을 안내합니다.

**실행 계획:** 대상 평가 > 여정 실행(다중 노드) > 조건 분기 > 메시지 배달(xN) > 종료 기준 > 보고

## 사용 사례 개요

여러 단계로 구성된 통합 여정은 단일 메시지로 원하는 고객 성과를 달성하기에 충분하지 않은 비즈니스 시나리오를 처리합니다. 여정은 일회성 전송 대신 프로필 속성, 동작 신호 또는 이벤트 데이터를 기반으로 경로를 조정하는 분기 논리를 사용하여 며칠 또는 몇 주 동안 간격을 두고 이메일, SMS 메시지, 푸시 알림 또는 인앱 메시지 등 일련의 터치포인트를 통해 각 프로필을 안내합니다.

이러한 여정은 AJO에서 가장 복잡한 캠페인 패턴입니다. 대상 기반 또는 이벤트 기반 항목을 작업 노드(메시지), 조건 노드(분기 논리), 대기 노드(시간 지연) 및 종료 기준(전환 이벤트 또는 시간 초과)의 캔버스와 결합합니다. 각 프로필은 각 단계에서 컨텍스트에 맞는 콘텐츠를 제공받으며 자체 속도로 독립적으로 여정을 통해 진행됩니다.

이 패턴은 단일 전송 캠페인에 대한 일괄 아웃바운드 메시지 활성화와 단일 이벤트 응답에 대한 이벤트 트리거 메시징과 같은 더 간단한 패턴을 대체합니다. 사용 사례에서 시간에 따른 여러 상호 작용을 통해 프로필을 양성해야 하는 경우 이 패턴을 사용합니다.

>[!NOTE]
>여정에서 개별 의사 결정 지점에서 최적의 오퍼, 콘텐츠 또는 채널을 동적으로 선택해야 하는 경우 [의사 결정을 사용한 크로스 채널 여정](cross-channel-journey-with-decisioning.md)을 참조하세요. 이 패턴은 AJO Decisioning 통합으로 이 패턴을 확장합니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 고객 유지 능력 향상

가치 중심의 경험과 지속적인 관계 관리를 통해 기존 고객의 참여와 갱신을 유지합니다.

**KPI:** 유지, 고객 생애 가치, 참여

[고객 유지 관리 향상에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### 고객 온보딩 개선

능률적이고 개인화된 환영 경험과 활성화 여정을 통해 신규 고객의 가치 실현 시간을 단축합니다.

**KPI:** 참여, 유지, 전환율

[고객 온보딩 향상에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)

### 휴면 상태 고객 재참여

행동 신호를 기반으로 타겟팅된 재활성화 캠페인을 통해 비활성 상태이거나 종료된 고객을 다시 확보할 수 있습니다.

**KPI:** 참여, 유지, 전환율

[고객 유지 관리 향상에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### 포기한 장바구니 및 여정 복구

구매, 애플리케이션 또는 등록 중에 중단한 사용자를 적시에 개인화된 후속 조치와 함께 다시 참여시킵니다.

**KPI:** 전환율, 증분 매출, 참여

[포기한 장바구니 및 여정 복구에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)

## 예시 전술 사용 사례

다음 시나리오는 여러 단계로 조정된 여정 패턴의 일반적인 애플리케이션을 보여 줍니다.

- **고객 온보딩 시리즈** — 환영 전자 메일, 기능 교육, 등록 후 처음 14일 동안의 활성화 메시지 표시
- **재참여 드립 캠페인** - 미리 알림 이메일, 인센티브 제공, 3주 이상 경과된 고객에 대한 최종 공지
- **충성도 마일스톤 여정** — 계층 업그레이드 알림, 전용 제공, 멤버십 갱신일이 다가오면 갱신 미리 알림
- **되찾기 시퀀스** — &quot;보고싶다&quot;는 이메일을 보낸 다음 이메일을 통해 할인 오퍼를 받은 다음, 소멸된 구매자를 위한 최종 SMS 미리 알림을 보냅니다.
- **제품 채택 여정** — 평가판 시작, 사용 팁, 평가판 기간 진행 시 업그레이드 안내
- **구독 갱신 시퀀스** — 30일 알림, 7일 미리 알림, 예정된 구독 갱신에 대한 만료일 메시지
- **구매 후 양육** - 구매 후 30일 동안 감사 이메일, 사용 방법 안내서, 교차 판매 권장 사항, 검토 요청

## 주요 성과 지표

다음 KPI를 사용하여 여러 단계로 조정된 여정 구현의 효과를 측정합니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 여정 완료율 | 조기 종료 없이 전체 여정을 완료하는 프로필의 비율 | 여정 보고서: 종료됨(완료됨) / 입력됨 |
| 단계 전환율 | 한 단계에서 다음 단계로 진행되는 프로필의 백분율 | 여정 보고서의 노드당 지표 |
| 채널 참여 비율 | 각 터치포인트에서의 오픈율, 클릭스루 비율 및 응답 비율 | 메시지당 게재 및 참여 지표 |
| 종료 기준 전환율 | 여정 시간 초과 전에 종료 이벤트(예: 구매, 등록)를 트리거하는 프로필의 비율 | 종료 기준 히트 수/총 입력 |
| 전환 시간 | 여정 시작부터 종료 기준 이벤트까지의 평균 기간 | 여정 분석: 항목 타임스탬프에서 전환 이벤트 타임스탬프로의 전환 |
| 여정 드롭오프율 | 각 단계에서 관여를 중단하는 프로필의 비율(폴아웃 분석) | 여정 단계 간 CJA 폴아웃 시각화 |
| 유지/재참여 비율 | 활성 상태로 돌아가는 타겟팅된 프로필의 비율 | CJA의 여정 후 행동 분석 |

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Adobe Journey Optimizer] (AJO)** — 여정 오케스트레이션 엔진, 메시지 작성, 채널 구성, 콘텐츠 실험, 빈도 및 충돌 관리, 보고
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — 여정 항목 대상에 대한 대상 평가 및 정의, 개인화를 위한 프로필 데이터 및 조건 분기
- **[!DNL Adobe Experience Platform] (AEP)** — 프로필 저장소, ID 서비스, 이벤트 데이터 수집 및 기본 데이터 인프라

## 관련 설명서

다음 리소스는 이 구현에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

### 여정

- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [여정 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [여정 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)

### 여정 활동

- [대상자 활동 읽기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [일반 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [대상자 선별 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [조건 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [여정에 메시지 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [종료 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [사용자 정의 액션 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)

### 시작 및 종료 관리

- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [채널 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 메시지 작성 및 개인화

- [이메일 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [이메일 Designer 콘텐츠 구성 요소 사용](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 콘텐츠 실험

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [통계적 계산](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### 빈도, 충돌 및 우선 순위

- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [비즈니스 규칙 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [충돌 및 우선 순위 관리 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [여정 한도 및 중재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/edge-segmentation)

### 보고 및 분석

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

### 동의 및 거버넌스

- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [제외 목록 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### 데이터 기반

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
