---
title: B2B 분석
description: 크로스 채널 고객 여정 분석에 B2B 계정 수준 정보를 포함하는 방법을 알아봅니다.
solution: Customer Journey Analytics, Real-Time Customer Data Platform
exl-id: 9d576e5c-cbd2-4c60-a6b0-88f8b8b963b4
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1811'
ht-degree: 2%

---

# B2B 분석

이 안내서에서는 [!DNL Customer Journey Analytics]&#x200B;([!DNL CJA]) B2B edition 및 [!DNL Real-Time Customer Data Platform]&#x200B;([!DNL RT-CDP]) B2B edition을 사용하여 B2B 계정 수준 정보를 크로스 채널 고객 여정 분석에 통합하는 B2B 분석 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

B2B Analytics는 계정 기반 연결, B2B 관련 컨테이너(계정, 글로벌 계정, 영업 기회, 구매 그룹) 및 계정 수준 보고를 사용하여 표준 [!DNL CJA] 기능을 확장합니다. 이 기능을 통해 조직은 계정 수준에서 마케팅 및 판매 참여를 분석하고, 영업 기회 진행을 추적하고, 구매 그룹 완성도를 측정하고, 확장된 B2B 판매 주기 전반에 걸쳐 마케팅 접점에 매출을 연결할 수 있습니다.

## 사용 사례 패턴

**B2B 분석**

크로스 채널 고객 여정 분석에 B2B 계정 수준 정보를 포함합니다.

**실행 계획:** B2B 데이터 연결 > 계정 데이터 보기 구성 > Workspace 분석 > 대시보드 게시

## 사용 사례 개요

B2B 조직은 근본적인 분석 과제에 직면해 있습니다. 고객은 개인이 아니라 여러 관련자, 구매 그룹 및 기회로 구성된 계정입니다. 표준 사용자 기반 분석에서는 &quot;어떤 계정이 가장 많이 참여합니까?&quot;, &quot;구매 그룹은 얼마나 완료됩니까?&quot;, &quot;기회 진행을 유도하는 마케팅 접점은 무엇입니까?&quot;와 같은 질문에 답할 수 없습니다.

B2B Analytics는 [!DNL CJA] B2B edition을 활용하여 사용자 수준 행동 데이터와 계정, 기회 및 구매 그룹 차원을 결합하는 계정 중심 분석 보기를 만들어 이를 해결합니다. [!DNL RT-CDP] B2B edition은 분석 계층에 데이터를 제공하는 기본 계정 프로필 통합 및 B2B ID 확인을 제공합니다. 이러한 솔루션을 함께 사용하여 조직은 계정 수준에서 크로스 채널 여정 분석을 구축하고, 마케팅 참여와 파이프라인 진행을 연관시키고, 마케팅 팀과 영업 팀 모두에게 실행 가능한 통찰력을 제공할 수 있습니다.

대상 대상에는 B2B 마케팅 운영 팀, 수요 창출 리더, 수익 운영 분석가 및 계정 수준 참여 및 파이프라인 상태에 대한 가시성이 필요한 영업 리더십 등이 포함됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 분석 및 보고 개선

통합 대시보드 및 셀프서비스 도구를 통해 보다 빠르고 실행 가능한 마케팅 통찰력을 위해 보고 기능을 향상시킵니다. B2B Analytics를 통해 조직은 여러 소스의 계정 수준 참여 데이터를 단일 분석 환경으로 통합하여 마케팅 프로그램이 파이프라인 및 매출에 미치는 영향에 대한 크로스 채널 가시성을 제공할 수 있습니다.

**KPI:** 효율성, 생산성

[분석 및 보고 향상에 대해 자세히 알아보기](/help/blueprints/business-objectives/analytics-insights/improve-analytics-reporting.md)

### 데이터 중심의 의사 결정 활성화

셀프서비스 분석, 실시간 고객 인사이트 및 AI 기반 예측을 통해 팀에 권한을 부여하여 전략을 안내합니다. 계정 수준 분석에서는 마케팅 및 영업 팀에 계정의 우선 순위를 정하고, 참여 전략을 최적화하고, 파이프라인 기회에 맞춰 조정하는 데 필요한 데이터를 제공합니다.

**KPI:** 효율성, 생산성

[데이터 기반 의사 결정 활성화에 대해 자세히 알아보기](/help/blueprints/business-objectives/analytics-insights/enable-data-driven-decision-making.md)

### 리드 자격 및 전환 개선

점수 책정, 육성 및 개인화된 후속 조치를 통해 잠재 고객 품질을 높이고 파이프라인 진행을 가속화합니다. CJA B2B edition은 B2B 판매 주기를 위해 특별히 설계된 확장 13개월 계정 전환 확인 기간을 제공하므로 전체 계정 여정에서 정확한 멀티 터치 속성을 사용할 수 있습니다.

**KPI:** 효율성, 수익 증가

[리드 자격 및 전환 개선에 대해 자세히 알아보기](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

## 예시 전술 사용 사례

다음 시나리오에서는 이 패턴을 실제로 적용하는 방법을 보여 줍니다.

- **계정 참여 점수 분석** - 웹, 이메일, 이벤트 및 콘텐츠 상호 작용 전반에 걸쳐 집계 참여로 계정을 측정하고 순위를 지정하여 판매 후속 조치를 위한 높은 의도의 계정을 식별합니다
- **구매 그룹 완전성 추적** — 계정 간 구매 그룹 구성을 분석하여 역할 적용 범위의 차이를 식별하고 불완전 구매 그룹에 대한 잠재 고객 확보 우선 순위를 지정합니다
- **영업 기회 파이프라인 상관 관계** - 마케팅 참여 데이터를 영업 기회 단계 진행과 상호 연관시켜 파이프라인 개선을 유도하는 캠페인과 접점을 파악합니다.
- **멀티 터치 B2B 속성** — 13개월 전환 확인 기간이 있는 속성 모델을 첫 번째 터치부터 마감된 원까지 전체 B2B 구매 여정의 신용 마케팅 접점에 적용합니다
- **계정 여정 매핑** - 영업 기회 생성 및 폐기를 통해 초기 인식에서 크로스 채널 계정 여정을 시각화하여 공통 경로와 마찰 지점을 식별합니다
- **파이프라인에 대한 캠페인의 영향** - 특정 캠페인이 계정 파이프라인 생성, 기회 향상 및 수익 생성에 미치는 영향을 측정합니다.
- **구매 그룹 참여 진행률** - 구매 그룹 참여 점수가 시간에 따라 어떻게 발전하는지 추적하고 참여 임계값과 영업 기회 결과의 상관 관계를 추적합니다.
- **계정 기반 콘텐츠 성능** - 특정 계정 세그먼트, 업계 또는 구매 그룹 역할과 공감하는 콘텐츠 자산 및 주제를 분석합니다.
- **판매 및 마케팅 정렬 대시보드** - 마케팅 및 영업 팀에 계정 참여, 파이프라인 상태 및 수익 속성에 대한 통합 보기를 제공하는 공유 대시보드를 빌드합니다.
- **활성화를 위한 계정 세분화** — 계정 수준 분석을 기반으로 B2B 세그먼트를 만들고(예: &quot;열려 있는 기회가 없는 참여도가 높은 계정&quot;) 다운스트림 활성화를 위해 게시합니다.

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 성공을 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 계정 참여 점수 | 계정 내 모든 연락처에 걸쳐 참여 지표 집계 | 계정 수준에서 웹 방문, 이메일 상호 작용, 이벤트 참석 및 컨텐츠 다운로드를 결합한 계산된 지표 |
| 구매 그룹 완성도 | 구매 그룹 내에 채워진 필수 역할의 백분율 | 시간이 지남에 따라 추적된 구매 그룹당 총 필수 역할에 대한 채워진 역할의 비율 |
| 마케팅의 영향을 받은 파이프라인 | 마케팅 활동으로 터치된 파이프라인의 매출 | 연결된 계정 담당자가 속성 창 내에서 마케팅 접점을 갖는 기회 값 |
| 계정-영업 기회 전환율 | 적격 기회를 생성하는 참여 계정 비율 | 정의된 기간 동안 총 참여 계정으로 나눈 영업 기회가 있는 계정 |
| 평균 거래 주기 길이 | 첫 번째 마케팅 터치에서 마감된 터치까지의 시간 | 첫 번째 속성 접점 날짜부터 영업 기회 종료 날짜까지의 평균 기간 |
| 마케팅 속성 수익 | 마케팅 접점으로 인한 매출 | 속성 모델별로 배포된 마케팅 터치로 성사된 기회의 수익 |
| 계정 도달 범위 및 침투 | 대상 계정당 참여 중인 연락처 수 | 알려진 총 연락처와 비교하여 계정당 마케팅 상호 작용을 사용하는 고유 연락처 |
| 구매 역할별 콘텐츠 참여 | 구매 그룹 역할별로 분류된 참여 지표 | 구매 그룹 내 개인/역할별로 분류된 페이지 보기, 다운로드 및 체류 시간 |

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Customer Journey Analytics]B2B edition** — 계정 기반 연결, B2B별 데이터 보기 컨테이너, 계정 수준 작업 영역 분석, 구매 그룹 분석, 기회 분석, B2B 세그멘테이션 및 B2B 속성과 확장된 전환 확인 기간을 제공합니다
- **[!DNL Real-Time CDP]B2B edition** — 계정 프로필 통합, B2B ID 해결, B2B 스키마 클래스(계정, 영업 기회, 구매 그룹) 및 B2B 참여 데이터 수집을 위한 [!DNL Marketo Engage] 통합을 포함하는 B2B 데이터 기반을 제공합니다.

## 관련 설명서

다음 리소스는 이 사용 사례 패턴을 구현하기 위한 추가 정보를 제공합니다.

**[!DNL CJA]B2B edition**

- [CJA B2B edition 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJA 보호 기능](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)

**연결**

- [연결 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [연결 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [연결 관리](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)

**데이터 보기**

- [데이터 보기 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [구성 요소 설정 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [지속성 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [속성 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [형식 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/format)
- [파생 필드](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [세션 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)

**Workspace 및 분석**

- [Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [프로젝트 만들기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [자유 형식 테이블](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [플로우 시각화](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [폴아웃 시각화](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [코호트 테이블](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [속성 패널](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [프로젝트 공유](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [프로젝트 예약](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [분류 차원](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

**구성 요소**

- [필터 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [필터 만들기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [계산된 지표 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [계산된 지표 만들기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [주석 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [날짜 범위](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

**대상**

- [대상 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [대상자 생성 및 게시](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
- [대상자 관리](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/manage)

**대시보드 및 스코어카드**

- [모바일 스코어카드 만들기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [스코어카드 구성 및 조정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics 대시보드 — 경영진 안내서](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)

**분석 가이드**

- [안내식 분석 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel 보기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [트렌드 보기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/trends/usage)
- [유지 보기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

**[!DNL RT-CDP]B2B edition**

- [RT-CDP B2B edition 개요](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#702702)
- [B2B edition 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [B2B 소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/sources/b2b)

**AEP 데이터 기반**

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Marketo Engage 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home)

**데이터 거버넌스 및 라이프사이클**

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [고급 데이터 수명주기 관리](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

**튜토리얼 및 가이드**

- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
