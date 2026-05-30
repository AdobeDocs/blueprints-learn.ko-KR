---
title: 일괄 아웃바운드 메시지 활성화
description: 대상자를 평가하고 예약된 아웃바운드 메시지를 단일 배치 실행으로 전달하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 192853ce-02ab-46e6-9092-3db5354bc19c
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 4%

---

# 일괄 아웃바운드 메시지 활성화

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) 및 [!DNL Adobe Real-Time Customer Data Platform]&#x200B;(RT-CDP)을 사용하여 예약된 아웃바운드 메시지를 정의된 대상 세그먼트에 전달하는 일괄 아웃바운드 메시지 활성화 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

일괄 아웃바운드 메시지 활성화는 일대다 아웃바운드 메시지의 기본 캠페인 패턴입니다. 대상 정의부터 메시지 전달 및 성능 분석에 이르기까지 전체 라이프사이클을 다룹니다.

## 사용 사례 패턴

**일괄 아웃바운드 메시지 활성화**

대상을 평가한 다음, 단일 배치 실행에서 모든 자격 있는 프로필에 예약된 아웃바운드 메시지(이메일, SMS, 푸시)를 전달합니다.

**실행 계획:** 대상 평가 > 메시지 작성 > 캠페인 실행 > 보고

## 사용 사례 개요

조직은 특정 시간에 또는 시스템 이벤트에 대한 응답으로 알려진 대상 세그먼트에 단일 메시지를 전달해야 하는 경우가 많습니다. 이 패턴은 [!DNL RT-CDP]의 대상 평가를 [!DNL Journey Optimizer]의 메시지 작성 및 캠페인 실행과 결합하여 해당 요구 사항을 해결합니다.

비즈니스 시나리오는 간단합니다. 메시지를 받을 사용자를 정의하고, 개인화로 메시지 콘텐츠를 만들고, 대상자와 메시지를 캠페인이나 여정에 바인딩하고, 일정에 따라, 대상자 자격을 통해 또는 시스템 트리거를 통해 전송을 실행합니다. 그 결과 게재, 참여 및 전환 지표에 대한 전체 보고가 포함된 메시지가 전달됩니다.

이 패턴은 한 번의 실행으로 알려진 대상자에게 단일 메시지를 전달하여 비즈니스 목표를 발전시킬 수 있을 때마다 적용됩니다. 실시간 행동 이벤트에 응답하는 이벤트 트리거 메시징과 시간이 지남에 따라 프로필을 여러 접점으로 안내하는 여러 단계 오케스트레이션된 여정과 다릅니다. 일괄 활성화 는 아웃바운드 메시지 사용 사례에 대한 가장 간단한 캠페인 패턴이며 가장 일반적인 시작점입니다.

## 주요 비즈니스 목표

이 섹션에서는 배치 아웃바운드 메시지 활성화가 지원하는 주요 비즈니스 목표를 식별합니다.

### 이메일 및 캠페인 참여 늘리기

**설명:** 최적화된 콘텐츠와 타깃팅을 통해 열람율, 클릭스루 비율 및 전체 캠페인 반응을 개선합니다.

**KPI:** 열람율, 참여, 전환율

### 매출 및 매출 증대

**설명:** 최적화된 디지털 채널, 캠페인 및 고객 여정을 통해 매출 성장을 촉진합니다.

**KPI:** 전환율, 증분 수익, 평균 주문 가격

**관련 비즈니스 목표:** [매출 및 판매 증가](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

### 캠페인 실행 간소화

**설명:** 템플릿, 자동화 및 표준화된 프로세스를 통해 캠페인 빌드 시간을 줄이고 멀티채널 캠페인 게재를 간소화합니다.

**KPI:** 출시 속도, 효율성, 정시 완료율 %

## 예시 전술 사용 사례

다음 시나리오는 배치 아웃바운드 메시지 활성화의 일반적인 응용 프로그램을 보여 줍니다.

- **판매 발표 또는 프로모션 이메일 발송** — 예정된 날짜에 적격 고객의 세그먼트에 프로모션 오퍼를 브로드캐스트합니다.
- **제품 출시 푸시 알림** - 관심 있는 고객에게 푸시를 통해 새로운 제품 사용 가능 여부를 알립니다.
- **뉴스레터 또는 다이제스트 이메일** - 정기적인 콘텐츠 조회 수를 구독자 대상자에게 전달합니다.
- **이벤트 등록 초대** — 자격을 갖춘 잠재 고객을 웨비나, 회의 또는 직접 이벤트에 초대합니다.
- **구독 갱신 미리 알림 이메일** — 갱신 날짜가 다가오고 있는 고객에게 조치를 취하도록 미리 알림
- **충성도 프로그램 마일스톤 알림** - 충성도 계층 또는 포인트 임계값에 도달한 구성원을 축하합니다.
- **특정 call-to-action 이메일** — 구매 완료, 환경 설정 업데이트 또는 프로그램 등록과 같은 타깃팅된 작업을 실행합니다.
- **플래시 판매 또는 시간 제한 오퍼에 대한 SMS 캠페인** — SMS를 통해 옵트인 대상자에게 긴급 제한 프로모션을 보냅니다.

## 주요 성과 지표

다음 표는 캠페인 효과를 측정하는 데 사용되는 KPI를 정의합니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 게재율 | 수신자에게 정상적으로 전달된 메시지 비율 | 게재됨 / 전송됨 x 100 |
| 열람률 | 수신자가 연 게재된 메시지 비율 | 고유 열람수 / 게재됨 x 100 |
| 클릭스루 비율(CTR) | 링크를 클릭한 게재된 메시지 비율 | 고유 클릭 수 / 게재됨 x 100 |
| 클릭투오픈율(CTOR) | 링크를 클릭한 열린 메시지의 백분율 | 고유 클릭수 / 고유 열람수 x 100 |
| 전환율 | 원하는 작업을 완료한 수신자 비율 | 전환 / 게재됨 x 100 |
| 구독 취소 비율 | 메시지를 받은 후 구독을 취소한 수신자 비율 | 구독 취소 / 제공 x 100 |
| 바운스 비율 | 게재할 수 없는 메시지 비율 | 바운스 수 / 전송된 x 100 |
| 보낸 이메일당 매출 | 캠페인으로 인한 수익(보낸 메시지로 나누기) | 총 수익 / 전송됨 |

## 애플리케이션

다음 응용 프로그램을 사용하여 이 패턴을 구현합니다.

- **[!DNL Adobe Journey Optimizer] (AJO)** — 메시지 작성, 채널 구성, 캠페인 실행, 여정 오케스트레이션, 콘텐츠 실험, 빈도 규칙 및 보고
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** - 대상 평가, 동의 및 거버넌스 적용
- **[!DNL Adobe Experience Platform] (AEP)** — 프로필 저장소, ID 서비스, 스키마, 데이터 세트, 데이터 수집

## 관련 설명서

이 단원에서는 항목별로 구성된 [!DNL Experience League] 설명서에 대한 포괄적인 링크를 제공합니다.

### 캠페인

- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [API 트리거된 캠페인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### 여정

- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [대상자 여정 읽기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

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
- [이메일 Designer 콘텐츠 구성 요소 사용](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [이메일 콘텐츠 가져오기 또는 코드 작성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/code-content)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### 콘텐츠 관리

- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [이메일 증명 보내기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [전자 메일 렌더링](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)

### 콘텐츠 실험

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [통계적 계산](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### 빈도 및 충돌 관리

- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [비즈니스 규칙 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [충돌 및 우선 순위 관리 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [여정 한도 및 중재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [대상자 구성](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### 보고

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### 데이터 거버넌스 및 동의

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### 데이터 모델링 및 ID

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### 튜토리얼 및 시작하기

- [Journey Optimizer 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started)
- [첫 캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [첫 여정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
