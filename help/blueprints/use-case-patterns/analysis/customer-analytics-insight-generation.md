---
title: Customer Analytics & Insight 세대
description: 비헤이비어 및 성능 분석을 위한 크로스 채널 분석 작업 공간, 계산된 지표 및 대시보드를 작성하는 방법에 대해 알아봅니다.
solution: Customer Journey Analytics, Experience Platform
exl-id: 235a4eb0-91ae-4030-b90e-7eda08c67ae1
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 3%

---

# Customer analytics &amp; insight 세대

이 안내서에서는 [!DNL Adobe Experience Platform]개의 데이터 세트를 [!DNL Customer Journey Analytics]에 연결하여 데이터 보기, 자유 형식 분석 작업 공간, 계산된 지표, 대시보드 및 모바일 스코어카드를 작성하고 선택적으로 활성화를 위해 CJA 정의 대상을 [!DNL Adobe Experience Platform]에 다시 게시하는 Customer Analytics 및 insight 생성 사용 사례 패턴에 대해 설명합니다.

이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

활성화 및 참여(메시지 보내기, 콘텐츠 개인화, 대상자 활성화)에 중점을 두는 분류법의 다른 패턴과는 달리, 이 패턴은 고객 행동을 이해 - 분석, 캠페인 성과 측정, 트렌드 식별 및 전략 및 최적화 결정을 알리는 통찰력 생성에 중점을 둡니다.

## 사용 사례 패턴

**고객 분석 및 insight 생성**

크로스 채널 분석 작업 공간, 계산된 지표 및 대시보드를 작성하여 고객 행동 및 캠페인 성과를 파악합니다.

**실행 계획:** 데이터 연결 > 데이터 보기 구성 > Workspace 분석 > 대시보드 게시

## 사용 사례 개요

조직에서는 고객이 채널 간에 어떻게 행동하고, 캠페인이 어떻게 수행되는지, 고객이 여정에서 드롭오프하는 위치, 반향을 일으키는 컨텐츠, 시간이 지남에 따라 서로 다른 세그먼트가 어떻게 유지되는지 이해해야 합니다. Customer Analytics 및 insight 세대는 분석가가 자유 형식 작업 공간을 구축하고, 사용자 지정 지표를 만들고, 속성 모델을 구성하고, 관련자 소비를 위해 대시보드를 게시할 수 있는 [!DNL Adobe Experience Platform]의 풍부한 크로스 채널 데이터를 [!DNL Customer Journey Analytics]에 연결하여 이러한 요구를 해결합니다.

이 패턴은 딥 탐색적 분석이 필요한 마케팅 분석가, 성과 대시보드가 필요한 캠페인 관리자, 참여 및 유지 통찰력이 필요한 제품 관리자, 한눈에 KPI 스코어카드가 필요한 경영진 등 여러 대상자에게 제공됩니다. 구현 접근 방식은 캠페인 성과 측정, 크로스 채널 여정 분석, 분석 기반 대상 활성화 또는 안내식 제품 통찰력과 같은 기본 분석 포커스에 따라 달라집니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

**분석 및 보고 개선**

통합 대시보드 및 셀프서비스 도구를 통해 보다 빠르고 실행 가능한 마케팅 통찰력을 위해 보고 기능을 향상시킵니다.

- **KPI:** 효율성, 생산성

이 비즈니스 목표에 대한 자세한 내용은 [분석 및 보고 개선](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)을 참조하십시오.

**데이터 기반 의사 결정 사용**

셀프서비스 분석, 실시간 고객 인사이트 및 AI 기반 예측을 통해 팀에 권한을 부여하여 전략을 안내합니다.

- **KPI:** 효율성, 생산성

이 비즈니스 목표에 대한 자세한 내용은 [데이터 기반 의사 결정 사용](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)을 참조하십시오.

**마케팅 속성 개선**

마케팅 접점, 채널 및 캠페인이 전환 및 매출 결과에 미치는 영향을 정확하게 측정합니다.

- **KPI:** 효율성, 수익 증가

이 비즈니스 목표에 대한 자세한 내용은 [마케팅 속성 개선](/help/blueprints/business-objectives/analytics-insights/improve-marketing-attribution.md)을 참조하십시오.

**마케팅 지출 및 ROI 최적화**

가장 높은 수익을 제공하는 채널과 캠페인을 파악하여 마케팅 예산 할당을 최적화합니다.

- **KPI:** 효율성, 수익 증가

이 비즈니스 목표에 대한 자세한 내용은 [마케팅 지출 및 ROI 최적화](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)를 참조하십시오.

## 예시 전술 사용 사례

다음은 이러한 패턴으로 구현할 수 있는 전술적 사용 사례의 예입니다.

- 캠페인 성과 대시보드 - 이메일, SMS, 푸시 및 유료 미디어 캠페인 간 게재 지표, 참여율, 전환 및 매출 기여도
- 고객 여정 폴아웃 분석 - 구매, 등록 또는 온보딩 유입 경로에서 고객이 이탈하는 지점을 식별합니다.
- 집단 유지 분석 — 몇 주, 몇 개월, 몇 분기에 걸쳐 다양한 획득 집단이 얼마나 잘 유지되는지 측정합니다.
- 채널 속성 모델링 — 첫 번째 터치, 마지막 터치, 선형 및 시간 감소 속성을 비교하여 전환을 유도하는 채널을 파악합니다
- 컨텐츠 성능 분석 — 세그먼트, 채널 및 라이프사이클 단계별로 가장 많이 활용되는 컨텐츠 식별
- 제품 사용 및 채택 분석 — 기능 채택, 참여 빈도 및 사용자 증가 트렌드를 추적합니다.
- 고객 라이프사이클 단계 분석 — 라이프사이클 단계(신규, 활성, 위험, 종료)별로 고객을 세분화하고 분석합니다.
- 마케팅 믹스 최적화 대시보드 - 채널 투자를 매출 기여도와 비교
- 크로스 채널 참여 점수 책정 및 보고 — 웹, 앱, 이메일 및 캠페인 상호 작용에서 복합 참여 점수 책정

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 성공을 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 효율성 | insight 시간 단축 및 수작업 보고 | CJA 구현 전후에 분석가가 보고서를 작성하는 데 소요한 시간 추적 |
| 생산성 | 비즈니스 사용자가 만든 셀프서비스 분석 수 | Workspace 프로젝트 생성 및 대시보드 사용 모니터링 |
| 증분 수익 | 인사이트 기반 최적화 결정으로 인한 매출 | CJA 분석을 기반으로 최적화된 캠페인의 매출 상승도를 측정합니다. |
| 전환율 | 주요 고객 여정 간 funnel 완료율 | CJA 폴아웃 시각화를 사용하여 각 여정 단계에서 폴아웃 비율 추적 |
| 참여 | 채널 간 고객 상호 작용 깊이 및 빈도 | CJA에서 참여 점수에 대한 계산된 지표 작성 |
| 유지 | 정의된 기간 동안의 고객 수익률 | CJA 집단 분석을 사용하여 유지 커브 측정 |

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Customer Journey Analytics] (CJA)** — 연결, 데이터 보기, 작업 공간 분석, 안내식 분석, 계산된 지표, 대시보드, 대상 게시 및 콘텐츠 분석
- **[!DNL Adobe Experience Platform] (AEP)** — CJA 연결에 데이터를 제공하는 데이터 레이크, 데이터 세트, XDM 스키마, 프로필 및 이벤트 데이터

## 관련 설명서

다음 리소스는 이 사용 사례 패턴에 대한 추가 정보를 제공합니다.

### [!DNL Customer Journey Analytics] — 시작

- [CJA 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJA 보호 기능](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-admin/guardrails)

### 연결

- [연결 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-connections/overview)
- [연결 만들기 또는 편집](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-connections/create-connection)
- [연결 관리](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-connections/manage-connections)

### 데이터 보기

- [데이터 보기 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/data-views)
- [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [구성 요소 설정 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [지속성 설정](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [속성 설정](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [형식 설정](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [지표 중복 제거](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication)
- [값 포함/제외](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/component-settings/include-exclude-values)
- [세션 설정](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/session-settings)
- [파생 필드](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dataviews/derived-fields)

### Workspace 및 분석

- [Workspace 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/home)
- [프로젝트 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [자유 형식 테이블](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [플로우 시각화](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [폴아웃 시각화](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [코호트 테이블](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [속성 패널](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [분류 차원](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [프로젝트 공유](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [프로젝트 예약](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [내보내기 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/export/export-cloud)

### 안내식 분석

- [안내식 분석 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel 보기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [트렌드 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/trends/usage)
- [참여 빈도 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [유지 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [활성 증가 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [릴리스 영향 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/impact/release)
- [첫 번째 사용 영향 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/impact/first-use)
- [타임라인 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/streams/timeline)

### 구성 요소

- [필터 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [필터 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [계산된 지표 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [계산된 지표 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [계산된 지표 함수](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [주석 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/annotations/overview)
- [날짜 범위](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)
- [지표 구성 요소](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/apply-create-metrics)

### 대상자 게시

- [대상 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [대상자 생성 및 게시](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/publish)
- [대상자 관리](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/manage)

### 콘텐츠 분석

- [Content Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/content-analytics/content-analytics)
- [Content Analytics 구성](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/config/configuration)

### 대시보드 및 스코어카드

- [모바일 스코어카드 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [스코어카드 구성 및 조정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics 대시보드 — 경영진 안내서](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [요약 번호 시각화](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)

### AEP 재단

- [데이터 세트 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/catalog/datasets/overview)
- [XDM 시스템 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/home)
- [소스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/home)
- [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home)
- [Audience Portal 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/audience-portal)

### AJO 보고 통합

- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [캠페인 이메일 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/campaign-global-report-cja-email)
- [여정 이메일 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/reporting/journey-global-report-cja-email)

### 튜토리얼 및 안내서

- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/schema/composition)
- [웹 SDK 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/home)
- [데이터스트림 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/configure)
