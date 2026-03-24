---
title: Customer Analytics & Insight 세대
description: 비헤이비어 및 성능 분석을 위한 크로스 채널 분석 작업 공간, 계산된 지표 및 대시보드를 작성하는 방법에 대해 알아봅니다.
solution: Customer Journey Analytics, Experience Platform
exl-id: 235a4eb0-91ae-4030-b90e-7eda08c67ae1
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8947'
ht-degree: 1%

---

# Customer analytics &amp; insight 세대

이 안내서는 고객 분석 및 insight 생성에 대한 전체 구현 참조를 제공합니다. [!DNL Adobe Experience Platform] 데이터 세트를 [!DNL Customer Journey Analytics]에 연결하고, 데이터 보기를 구성하고, 자유 형식 분석 작업 공간을 빌드하고, 계산된 지표를 만들고, 대시보드 및 모바일 스코어카드를 게시하고, 선택적으로 활성화를 위해 CJA 정의 대상을 [!DNL Adobe Experience Platform]에 다시 게시하는 방법에 대해 설명합니다.

실행 가능한 모든 구현 경로, 이들 간의 상충 관계 및 각 단계에서 필요한 구성 결정을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

활성화 및 참여(메시지 보내기, 콘텐츠 개인화, 대상자 활성화)에 중점을 두는 분류법의 다른 패턴과는 달리, 이 패턴은 고객 행동을 이해 - 분석, 캠페인 성과 측정, 트렌드 식별 및 전략 및 최적화 결정을 알리는 통찰력 생성에 중점을 둡니다. 거의 모든 활성화 또는 개인화 패턴과 가장 일반적으로 구성된 패턴 및 쌍입니다.

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

## 사용 사례 패턴

**고객 분석 및 insight 생성**

크로스 채널 분석 작업 공간, 계산된 지표 및 대시보드를 작성하여 고객 행동 및 캠페인 성과를 파악합니다.

**함수 체인:** 데이터 연결 > 데이터 보기 구성 > Workspace 분석 > 계산된 지표 만들기 > 대시보드 게시

컴포지션 지침은 [구현 옵션](#implementation-options) 섹션을 참조하십시오.

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Customer Journey Analytics] (CJA)** — 연결, 데이터 보기, 작업 공간 분석, 안내식 분석, 계산된 지표, 대시보드, 대상 게시 및 콘텐츠 분석
- **[!DNL Adobe Experience Platform] (AEP)** — CJA 연결에 데이터를 제공하는 데이터 레이크, 데이터 세트, XDM 스키마, 프로필 및 이벤트 데이터

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | 작업 영역 생성 및 데이터 보기 액세스 권한으로 프로비저닝된 CJA 제품 프로필입니다. CJA 연결에 액세스할 수 있는 AEP 데이터 세트입니다. 적절한 CJA 역할에 할당된 사용자. | [액세스 제어 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | CJA에 연결할 XDM 스키마 및 데이터 세트가 AEP에 있어야 합니다. 스키마 디자인은 CJA 데이터 보기에서 사용할 수 있는 차원 및 지표에 직접 영향을 줍니다. 이벤트 스키마에는 타임스탬프 필드가 필요하고 조회 스키마에는 키 필드가 필요합니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/home) |
| 데이터 소스 및 수집 | 필수 | 데이터는 AEP 데이터 세트(웹 SDK을 통한 웹 이벤트, 모바일 SDK을 통한 앱 이벤트, AJO 캠페인 이벤트, 소스 커넥터를 통한 CRM 데이터)로 유입되어야 합니다. 분석의 풍부성은 수집된 데이터의 범위에 따라 다릅니다. | [소스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/home) |
| ID 및 프로필 구성 | 필수 | CJA 연결의 개인 ID 구성은 데이터 세트 간에 이벤트가 결합되는 방법을 결정합니다. AEP의 크로스 디바이스 ID 결합은 완전한 고객 여정을 구축하는 CJA의 기능을 향상시킵니다. 개인 ID 필드에 대해 ID 네임스페이스를 구성해야 합니다. | [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home) |
| 대상 정의 및 세분화 | 해당 사항 없음 | CJA은 analysis 컨텍스트 내에 자체 필터 및 대상을 빌드합니다. CJA은 대상 게시를 통해 AEP에 대상을 다시 게시할 수 있지만 RT-CDP 대상은 필수 조건이 아닙니다(옵션 C). | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | AEP 계산된 속성은 CJA에 연결된 데이터 세트를 보강하여 분석에 추가 차원 및 지표(예: 라이프타임 구매 카운트, 마지막 활동 이후 일 수)를 제공할 수 있습니다. 이러한 프로필 수준 집계는 CJA 데이터 보기에서 차원으로 사용할 수 있습니다. | [계산된 특성 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | 데이터 세트 보존 정책은 CJA에서 사용할 수 있는 내역 데이터에 영향을 줍니다. 일반적으로 분석을 통해 연도별 비교 및 장기 추세 분석을 활성화하려면 장기 보존이 필요합니다. 적절한 내역 깊이를 보장하도록 데이터 세트 TTL을 구성합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 중요 필드의 거버넌스 레이블은 CJA 데이터 보기에 표시되는 항목을 제한할 수 있습니다. PII 또는 중요한 데이터가 CJA 연결에 포함된 경우 데이터 거버넌스 레이블이 규정을 준수하는 액세스를 보장하고 공유 대시보드에서 무단 노출을 방지합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home) |
| 모니터링 및 가시성 | 추천 | CJA 연결 상태 및 데이터 새로 고침이 모니터링되어야 합니다. 소스 데이터 흐름 실패 및 수집 문제에 대한 경고를 구성하여 데이터 피드 CJA의 안정성과 최신성을 보장합니다. | [Observability Insights 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | 보고 및 분석 구현입니다. 다른 패턴에 대한 참조 계획에 S5가 포함된 경우 이 고객 분석 및 insight 생성 계획을 분석 구현에 사용하십시오. | [CJA 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-overview/cja-overview) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Customer Journey Analytics]&#x200B;(CJA)

다음 표에는 이 패턴에 사용되는 CJA 애플리케이션 기능이 나와 있습니다.

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 데이터 연결 | 1단계: 데이터 연결 | 크로스 채널 분석을 위해 AEP 데이터 세트를 CJA 연결에 바인딩하고, 크로스 데이터 세트 결합을 위해 데이터 세트 유형 및 개인 ID를 구성합니다 |
| 데이터 보기 구성 | 2단계: 데이터 보기 구성 | 분석 관점을 형성하는 차원, 지표, 속성 모델, 지속성 설정, 세션 매개 변수 및 파생 필드를 정의합니다. |
| Workspace 분석 | 3단계: 분석 및 지표 만들기 | 테이블, 시각화, 필터, 주석 및 차원 분류를 사용하여 자유 형식 분석 프로젝트 빌드 (옵션 A, B, C) |
| 안내 분석 | 3단계: 분석 및 지표 만들기 | funnel, 트렌드, 유지, 사용자 증가 및 참여 빈도 분석에 대한 구조화된 가이드 워크플로 사용(옵션 D) |
| 계산된 지표 만들기 | 3단계: 분석 및 지표 만들기 | 전환율, 참여 점수 및 방문당 매출과 같은 재사용 가능한 KPI에 대해 공식, 필터 및 함수를 사용하여 계산된 지표를 정의합니다 |
| 대시보드 및 스코어카드 게시 | 4단계: 대시보드 게시 | 관련자 보고를 위한 대화형 대시보드 및 모바일 스코어카드 만들기 및 공유 |
| 대상자 게시 | 5단계: 대상자 게시(옵션 C만 해당) | 다운스트림 활성화를 위해 CJA 정의 대상을 AEP 실시간 고객 프로필에 다시 게시합니다 |
| Content Analytics | 3단계: 분석 및 지표 만들기 | 디지털 속성 전반에서 콘텐츠 성능 트렌드, 예외 항목 및 피로도 분석(콘텐츠 분석이 중요한 경우) |

### [!DNL Adobe Experience Platform]&#x200B;(AEP)

다음 표에는 이 패턴에 사용되는 AEP 애플리케이션 기능이 나와 있습니다.

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 데이터 레이크 및 데이터 세트 | 전제 조건(F2, F3) | CJA 연결을 제공하는 소스 이벤트, 프로필 및 조회 데이터 세트를 제공합니다 |
| ID 서비스 | 전제 조건(F4) | CJA 연결의 데이터 세트 간에 개인 ID 결합을 위한 ID 네임스페이스 구성을 제공합니다 |

## 필요 조건

이 사용 사례 패턴을 구현하기 전에 다음 전제 조건을 충족해야 합니다.

- [ ] CJA 제품 권한이 조직에 대해 프로비저닝되었습니다.
- [ ] CJA 제품 프로필이 적절한 사용자 액세스 권한(작업 영역 만들기, 데이터 보기 액세스)으로 구성되어 있습니다.
- [ ] AEP 샌드박스에는 데이터 흐름(웹 이벤트, 앱 이벤트, 캠페인 데이터, CRM 레코드)이 있는 대상 데이터 세트가 포함되어 있습니다.
- [ ] XDM 스키마는 적절한 필드 그룹이 있는 모든 소스 데이터 세트에 대해 정의됩니다
- [ ] 개인 ID 필드가 식별되며 연결할 모든 데이터 세트에서 일관되게 사용할 수 있습니다.
- [ AEP 연결 결합에 사용된 개인 ID에 대해 CJA에 ] ID 네임스페이스가 구성되어 있습니다.
- [ ]개의 관련자 요구 사항이 문서화되었습니다. 대상이 대시보드를 사용할 KPI, 세부 정보 수준
- [ ] 모바일 스코어카드용: 이해 당사자에게 [!DNL Adobe Analytics] 대시보드 모바일 앱이 설치되어 있습니다.
- [ 옵션 C의 ] (대상 게시): AEP 실시간 고객 프로필이 대상 샌드박스에서 활성화됩니다.
- [ 옵션 D의 ] (안내식 분석): CJA SKU에는 안내식 분석 기능이 포함되어 있습니다

## 구현 옵션

이 섹션에서는 이 사용 사례 패턴에 사용할 수 있는 구현 옵션에 대해 설명합니다.

### 옵션 A: Campaign 성능 분석

**우수 사례:** 캠페인 및 여정 효율성 측정 및 최적화 - 이메일 캠페인 대시보드, funnel 여정, 채널 성과 비교 및 마케팅 ROI 보고.

**작동 방식:**

이 옵션은 AJO 캠페인 및 여정 데이터 세트를 CJA에 연결하고, 게재 및 참여 지표(전송, 게재, 열기, 클릭, 바운스, 구독 취소)를 사용하여 데이터 보기를 구성하고, 캠페인 성과 대시보드를 작성하고, 마케팅 관련자를 위한 스코어카드를 게시합니다. 초점은 마케팅 캠페인이 채널 전반에서 시간에 따라 어떻게 수행되는지 이해하는 것입니다.

데이터 보기는 캠페인별 차원(캠페인 이름, 여정 이름, 채널 유형, 메시지 변형) 및 게재 지표로 구성됩니다. 계산된 지표는 열람율, 클릭스루 비율, 전환율 및 메시지당 매출과 같은 파생 측정값에 대해 생성됩니다. 대시보드는 추세 분석을 위해 이러한 KPI와 비교 기간을 제공합니다.

**주요 고려 사항:**

- AEP에서 AJO 캠페인 및 여정 이벤트 데이터 세트 필요
- 속성 모델은 조직의 캠페인 측정 철학에 부합해야 합니다
- AJO 기본 보고서(운영 게재 지표)와 CJA(크로스 채널 비즈니스 영향)를 모두 포함하는 것이 좋습니다.

**장점:**

- 캠페인 측정 및 최적화를 위해 특별히 제작됨
- 캠페인 간 비교 및 채널 혼합 분석 가능
- 계산된 지표는 모든 캠페인에 표준화된 KPI 정의를 제공합니다
- 모바일 스코어카드는 마케팅 리더에게 한 눈에 알 수 있는 성능을 제공합니다

**제한 사항:**

- 캠페인 및 여정 데이터로 제한됨. 전체 고객 여정 컨텍스트를 제공하지 않음
- 여정 경로 지정, 폴아웃 또는 집단 분석은 포함하지 않습니다
- 속성은 전체 고객 여정이 아닌 캠페인 터치포인트에 범위가 지정됩니다

**Experience League:**

- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Workspace 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/home)

### 옵션 B: 고객 여정 분석

**가장 적합한 대상:** 폴아웃 분석, 경로 분석, 집단 유지, 속성 모델링 및 웹, 앱, 이메일, CRM 및 오프라인 접점에서 라이프사이클 단계 분석 등 크로스 채널 고객 여정 이해

**작동 방식:**

이 옵션은 여러 AEP 데이터 세트(웹 이벤트, 앱 이벤트, CRM 데이터, 캠페인 상호 작용, 트랜잭션 레코드)를 연결하여 고객 여정에 대한 통합 크로스 채널 보기를 만듭니다. 데이터 보기는 모든 채널에 걸친 차원 및 지표로 구성됩니다. CJA의 플로우, 폴아웃, 집단 및 속성 시각화는 고객이 여정을 통해 어떻게 이동하는지, 어디에서 중단하는지, 서로 다른 세그먼트가 어떻게 유지되는지, 그리고 전환 시 크레딧을 받을 만한 채널이 무엇인지 분석하는 데 사용됩니다.

이는 가장 포괄적인 분석 옵션으로서, 엔드 투 엔드 고객 경험에 심층적인 insight을 제공합니다. 또한 구현하기 가장 복잡하여, 올바른 차원과 지표를 노출하기 위해 데이터 세트 간 스티칭 및 사려 깊은 데이터 보기 디자인에 대한 주의 깊은 개인 ID 구성이 필요합니다.

**주요 고려 사항:**

- 정확한 크로스 채널 분석을 위해 연결된 모든 데이터 세트에서 일관된 개인 ID 필요
- AEP의 스키마 디자인은 CJA 분석의 품질과 깊이에 직접적인 영향을 줍니다
- 연결에 데이터 세트가 많으면 분석이 풍부해지지만 채우기 시간이 길어질 수 있습니다
- 속성 모델링을 사용하려면 명확한 전환 이벤트 정의가 필요합니다

**장점:**

- 완벽한 크로스 채널 고객 여정 가시성
- 플로우, 폴아웃, 집단, 속성, 자유 형식 테이블 등 CJA 시각화의 전체 세트
- 단일 채널 보고에서 보이지 않는 인사이트를 검색할 수 있습니다.
- 고객 행동 및 라이프사이클에 대한 복잡한 분석 질문 지원

**제한 사항:**

- 다중 데이터 세트 연결 및 크로스 채널 결합으로 인해 구현 복잡성 증가
- 데이터 보기 구성 및 파생 필드에 대한 사전 계획 필요
- 대규모 다중 데이터 세트 연결을 위한 채우기는 며칠이 걸릴 수 있습니다.
- 분석 품질은 기본 데이터의 완전성 및 일관성에 따라 다릅니다

**Experience League:**

- [연결 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-connections/overview)
- [플로우 시각화](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [폴아웃 시각화](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [코호트 테이블](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [속성 패널](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/attribution)

### 옵션 C: 대상자 게시가 있는 Analytics

**최적의 대상:** 분석 기반 활성화 — CJA 분석을 통해 흥미로운 세그먼트를 검색한 다음 RT-CDP 대상, AJO 캠페인 또는 AJO 여정을 통해 활성화하기 위해 AEP에 다시 게시합니다.

**작동 방식:**

이 옵션은 CJA에서 게시하는 대상자로 옵션 A 또는 옵션 B를 확장합니다. 분석가는 크로스 채널 동작 데이터와 CJA 필터의 전체 분석 기능을 사용하여 CJA에서 세그먼트를 작성한 다음, 다운스트림 활성화를 위해 이러한 대상을 AEP 실시간 고객 프로필에 게시합니다. 이렇게 하면 insight과 작업 간의 차이가 해소됩니다. 탐색적 분석 중에 발견된 세그먼트는 AEP 세그먼트 빌더에서 수동으로 재작성하지 않아도 실행 가능한 대상이 됩니다.

게시된 대상은 AEP 대상 포털에서 원본 &quot;CJA&quot;와 함께 표시되며, 모든 RT-CDP 대상에 대해 활성화하거나 AJO에서 캠페인 대상으로 사용하거나 여정 항목 조건으로 사용할 수 있습니다.

**주요 고려 사항:**

- Target 샌드박스에서 AEP 실시간 고객 프로필을 활성화해야 함
- CJA 연결에는 AEP ID 네임스페이스로 확인되는 유효한 개인 ID가 있어야 합니다
- 게시된 대상은 조직의 AEP 대상 권한에 포함됩니다
- 새로 고침 케이던스는 활성화 요구 사항(1회, 4시간마다, 매일, 매주)을 기반으로 구성해야 합니다.

**장점:**

- 분석과 활성화 사이의 루프를 닫습니다.
- CJA의 크로스 채널 동작 데이터를 사용하여 고부가가치 세그먼트 검색 가능
- CJA에 정의된 대상은 AEP 세그먼트 빌더에서 사용할 수 없는 차원 및 필터를 활용할 수 있습니다
- 분석 통찰력을 기반으로 대상 기준의 반복적인 세분화를 지원합니다.

**제한 사항:**

- CJA 고객당 최대 75개의 게시된 대상
- 대규모 데이터 세트의 경우 초기 대상 평가에 최대 24시간이 소요될 수 있습니다
- CJA에서 게시한 대상은 AEP에서 편집할 수 없습니다. CJA에서 변경해야 합니다.
- 기본 분석 이상의 추가 ID 네임스페이스 및 프로필 구성 필요

**Experience League:**

- [대상 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [대상자 생성 및 게시](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/publish)

### 옵션 D: 제품 팀을 위한 가이드 분석

**최적의 대상:** 제품 경험 인사이트 — 복잡한 자유 형식 Workspace 프로젝트 설정 없이 CJA의 가이드 분석 워크플로를 사용하여 기능 채택, 사용자 참여 트렌드, 유지 분석, funnel 전환 및 릴리스 영향 분석.

**작동 방식:**

이 옵션은 체계적이고 템플릿화된 CJA 생성을 위해 insight Guided Analysis를 사용합니다. 안내식 분석에서는 funnel, 트렌드, 유지, 사용자 증가, 참여 빈도, 릴리스 영향, 처음 사용 및 타임라인 과 같은 미리 작성된 분석 유형을 제공하여 분석가가 구조화된 워크플로우를 통해 특정 제품 및 경험 질문에 답변할 수 있도록 합니다. 처음부터 자유 형식 프로젝트를 빌드하지 않고 빠르고 집중적인 통찰력이 필요한 제품 관리자 및 분석가에게 이상적입니다.

이 구현은 AEP 데이터 세트를 CJA에 연결하고, 이벤트 수준 차원 및 지표로 데이터 보기를 구성한 다음, 안내가 있는 분석 워크플로우를 사용하여 인사이트를 생성합니다. 추가적인 맞춤화를 위해 결과를 Workspace 프로젝트 내의 패널로 저장할 수 있습니다.

**주요 고려 사항:**

- 안내식 분석에는 안내식 분석 기능이 포함된 CJA 제품 권한이 필요합니다
- 캠페인 성과 측정보다는 제품 및 경험 분석에 가장 적합
- 비분석가 사용자가 보다 쉽게 액세스할 수 있는 구조화된 워크플로를 제공합니다
- 자유 형식 Workspace 분석과 결합하여 더 자세한 탐색 가능

**장점:**

- 진입에 대한 낮은 장벽 — 구조화된 워크플로는 사용자가 분석을 진행할 수 있도록 안내합니다
- 제품 경험 질문(funnel, 보존, 성장, 영향)을 위해 특별히 제작됨
- 일반적인 분석 질문에 대한 insight의 빠른 시간
- 저장된 분석은 자유 형식 분석과 함께 Workspace 프로젝트에 포함할 수 있습니다

**제한 사항:**

- 자유 형식 Workspace 분석보다 유연성이 낮음
- 사전 설치된 분석 유형(funnel, 트렌드, 유지, 성장, 빈도, 영향, 타임라인)으로 제한
- 세그먼트 비교는 최대 3개의 세그먼트를 동시에 지원
- Funnel 분석은 최대 15단계를 지원합니다

**Experience League:**

- [안내식 분석 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel 보기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [유지 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/retention/retention-rates)

### 옵션 비교

다음 표에서는 사용 가능한 구현 옵션을 비교합니다.

| 기준 | 옵션 A: 캠페인 성과 | 옵션 B: 고객 여정 | 옵션 C: Analytics + 활성화 | 옵션 D: 안내식 분석 |
| --- | --- | --- | --- | --- |
| 다음에 최적 | Campaign 측정 및 최적화 | 크로스 채널 여정 이해 | Insight 기반 대상 활성화 | 제품 경험 통찰력 |
| 복잡성 | Low-Medium | 높음 | 높음 | 낮음 |
| 데이터 세트 필요 | AJO 캠페인/여정 이벤트 | 여러 크로스 채널 데이터 세트 | A 또는 B와 동일하며 프로필 ID가 추가됩니다. | 제품 상호 작용이 있는 이벤트 데이터 세트 |
| 주요 시각화 | 자유 형식 테이블, 요약 번호, 꺾은 선형 | 플로우, 폴아웃, 집단, 속성 | A 또는 B와 동일하며 대상자 게시 | Funnel, 트렌드, 유지, 성장 |
| 활성화 기능 | 아니요(보고만 해당) | 아니요(보고만 해당) | 예(대상을 AEP에 게시) | 아니요(보고만 해당) |
| 대상자 필요 | 마케팅 분석가, 캠페인 관리자 | 데이터 분석가, 여정 설계자 | 분석가 + 활성화 팀 | 제품 관리자, 성장 분석가 |
| 사용된 CJA 함수 | 연결, 데이터 보기, Workspace, 계산된 지표, 대시보드 | 연결, 데이터 보기, Workspace, 계산된 지표, 대시보드 | A 또는 B와 동일하며 대상자 게시 | 연결, 데이터 보기, 안내식 분석, 대시보드 |
| 첫 번째 insight 시간 | 일 | 주 | 주 | 시간-일 |

### 적절한 옵션 선택

다음 지침을 사용하여 요구 사항에 가장 적합한 구현 옵션을 선택합니다.

- **기본 목표가 캠페인 효과를 측정하는 것이고** AJO 캠페인 데이터가 AEP에 유입되는 경우 **옵션 A**&#x200B;로 시작하십시오. 마케팅 성과 보고를 위한 가장 빠른 가치 창출 시간을 제공합니다.

- **웹, 앱, 전자 메일 및 오프라인 접점에서 전체 고객 여정을 이해해야 하고** 개인 ID가 일치하는 여러 데이터 세트가 있는 경우 **옵션 B**&#x200B;을(를) 선택하세요. 가장 심층적인 분석 기능을 제공하지만 데이터 보기 구성에 대한 추가 초기 투자가 필요합니다.

- **RT-CDP 또는 AJO에서 활성화하기 위해 CJA에서 검색한 세그먼트를 AEP에 다시 게시하여 통찰력에 따라 작업하려면** **옵션 C**&#x200B;을(를) 선택하십시오. 이렇게 하면 옵션 A 또는 B가 대상자 게시로 확장되며 AEP 실시간 고객 프로필 구성이 필요합니다.

- **팀에 복잡한 자유 형식의 Workspace 프로젝트 없이 빠르고 구조화된 제품 인사이트**&#x200B;가 필요하고 CJA SKU에 가이드 분석이 포함된 경우 **옵션 D**&#x200B;을(를) 선택하십시오. 특정 제품 경험 질문에 답변할 수 있는 가장 빠른 경로입니다.

- **많은 조직에서 여러 옵션을 구현합니다**: 마케팅 팀 캠페인 대시보드에 대한 옵션 A, 분석 팀의 크로스 채널 분석에 대한 옵션 B, 제품 팀 셀프서비스 인사이트에 대한 옵션 D. 이러한 옵션은 동일한 CJA 연결 및 데이터 보기 인프라를 공유합니다.

## 구현 단계

이 섹션에서는 이 사용 사례 패턴에 대한 단계별 구현 단계에 대해 자세히 설명합니다.

### 1단계: 데이터 연결

**응용 프로그램 함수:** CJA: 데이터 연결

이 단계에서는 분석을 위해 하나 이상의 AEP 데이터 세트를 CJA에 바인딩하는 CJA 연결을 구성합니다. 연결은 CJA으로 유입되는 데이터 세트, 개인 ID를 통해 데이터 세트 간에 이벤트가 결합되는 방법, 내역 및 스트리밍 데이터가 수집되는 방법을 정의합니다. 이는 AEP의 데이터 레이크와 CJA 간의 기본 연결입니다.

#### 의사 결정 지점

이 단계에서는 다음과 같은 결정을 내려야 합니다.

>[!NOTE]
>**결정: AEP 샌드박스 선택**
>
>소스 데이터 세트가 포함된 AEP 샌드박스
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 프로덕션 샌드박스 | 프로덕션 보고를 위한 라이브 고객 데이터 | 프로덕션 대시보드 및 관련자 보고에 사용 |
>| 개발 샌드박스 | 프로덕션 배포 전 테스트 및 반복 | 프로덕션으로 승격하기 전에 초기 구성 및 유효성 검사에 사용 |

>[!NOTE]
>**결정: 데이터 집합 선택 및 형식 지정**
>
>어떤 AEP 데이터 세트를 연결에 포함해야 하며 각각 어떤 유형을 할당해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 이벤트 데이터 세트 | 타임스탬프가 지정된 동작 데이터(웹 상호 작용, 앱 이벤트, 캠페인 상호 작용, 트랜잭션) | 타임스탬프 필드 필요(대부분의 분석 핵심 구성) |
>| 조회 데이터 세트 | 키-값 참조 데이터(제품 카탈로그, 캠페인 메타데이터, 스토어 위치) | 공유 키를 통해 이벤트 데이터에 참여합니다. 최신 상태만 사용됩니다. |
>| 프로필 데이터 세트 | 개인 수준 속성(충성도 계층, 라이프타임 값, CRM 속성) | 개인 수준에서 데이터 보강 제공. 최신 상태만 사용됨 |

>[!NOTE]
>**결정: 개인 ID 구성**
>
>크로스 데이터 세트 결합을 위한 개인 ID로 사용할 수 있는 필드는 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| CRM ID | 조직에 채널 간 일관된 CRM 식별자가 있음 | 알려진 고객에게 가장 정확한 크로스 채널 결합 제공 |
>| ECID (Experience Cloud ID) | 주로 익명 웹/앱 동작 분석 | 장치 범위, ID 확인 없이 장치 간에 결합하지 않음 |
>| 이메일(해시됨) | 이메일은 데이터 세트 간 공통 식별자입니다 | 이메일이 터치포인트 간에 일관되게 캡처될 때 잘 작동합니다 |
>| 사용자 정의 네임스페이스 | 조직에서 고유 식별자를 사용합니다. | 대상 게시를 위해 AEP ID 네임스페이스와 일치해야 함(옵션 C) |

>[!NOTE]
>**결정: 범위 채우기**
>
>연결에 가져와야 하는 내역 데이터의 양은 얼마입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 기존의 모든 데이터 | 연도별 비교 및 장기 추세에 필요한 최대 기록 깊이 | 대규모 데이터 세트(수십억 개의 레코드)에 대한 채우기를 완료하는 데 며칠이 걸릴 수 있습니다 |
>| 사용자 정의 날짜 범위 | 최근 기록만 관련성이 있거나 스토리지 최적화가 우려되는 경우 | 분석에 사용할 수 있는 기록 깊이를 제한합니다. |
>| 채우기 없음 | 향후 분석만 필요합니다. | 가장 빠른 연결 설정, 새 데이터가 유입될 때까지 사용 가능한 내역 데이터 없음 |

>[!NOTE]
>**결정: 스트리밍 활성화**
>
>새로운 데이터가 거의 실시간으로 CJA으로 전송되어야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 스트리밍 활성화 | 거의 실시간 보고가 필요합니다(AEP 수집 후 ~90분 이내에 데이터 사용 가능) | 프로덕션 연결에 가장 일반적으로 사용되며, 적시에 분석 가능 |
>| 일괄 처리만 | 주기적인 새로 고침으로 충분하며 스트리밍이 필요하지 않습니다. | 간단한 구성, 일괄 처리 후 데이터 사용 가능 |

#### 데이터 연결 구성

**UI 탐색:** CJA > 연결 > 새 연결 만들기

주요 구성 세부 정보:

- 연결 이름 및 설명은 조직 이름 지정 규칙을 따라야 합니다
- CJA 용량 계획에 사용되는 평균 일일 이벤트 수
- 단일 연결의 모든 데이터 세트는 동일한 AEP 샌드박스에서 가져와야 합니다
- 정확한 데이터 세트 간 결합을 위해 개인 ID 필드는 모든 데이터 세트에서 일관되어야 합니다
- 연결에 추가하기 전에 개인 ID 필드가 존재하고 각 데이터 세트에 채워져 있는지 확인하십시오

**Experience League 설명서:**

- [연결 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-connections/overview)
- [연결 만들기 또는 편집](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-connections/create-connection)
- [연결 관리](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-connections/manage-connections)
- [CJA 보호 기능](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-admin/guardrails)

### 2단계: 데이터 보기 구성

**응용 프로그램 함수:** CJA: 데이터 보기 구성

이 단계에서는 연결 데이터가 분석에 표시되는 방식을 정의하는 데이터 보기를 구성합니다. 데이터 보기는 차원 및 지표로 노출되는 스키마 필드, 값이 속성 및 지속되는 방법, 세션이 정의되는 방법 및 파생된 필드가 원시 데이터를 분석 준비가 된 구성 요소로 변환하는 방법을 결정합니다. 여러 분석 관점에 대해 단일 연결에서 여러 데이터 보기를 만들 수 있습니다.

#### 의사 결정 지점

이 단계에서는 다음과 같은 결정을 내려야 합니다.

>[!NOTE]
>**결정: 컨테이너 이름 지정**
>
>컨테이너가 비즈니스 도메인과 일치시키기 위해 어떤 용어를 사용해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 기본값(개인/세션/이벤트) | 표준 분석 용어는 팀에서 이해합니다 | 대부분의 구현에 작동 |
>| 사용자 정의 이름(예: 구매자/방문/상호 작용) | 비즈니스 도메인별 용어로 사용자 채택 향상 | 기술 전문가가 아닌 이해 당사자가 분석 범위를 이해할 수 있도록 지원 |
>| B2B 이름(예: 계정/참여/터치포인트) | 계정 수준 분석이 핵심인 B2B 분석 | B2B 비즈니스 개념에 따라 컨테이너 범위 조정 |

>[!NOTE]
>**결정: 세션 시간 초과**
>
>비활성 기간이 세션 경계를 정의합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 30분(기본값) | 표준 웹 분석 세션 정의 | 업계 표준, 대부분의 분석 벤치마크와 일치 |
>| 15분 | 사용자가 작업을 빠르게 완료할 수 있는 단기 콘텐츠 또는 트랜잭션 사이트 | 더 많은 세션을 생성하여 고유한 사용자 의도를 더 잘 포착할 수 있음 |
>| 60분 이상 | 긴 양식 콘텐츠, 복잡한 B2B 상호 작용 또는 연구 중심의 여정 | 세션 수 감소, 확장된 리서치를 단일 세션으로 캡처 |
>| 새 세션 이벤트로 사용자 지정 | 특정 이벤트(예: 앱 실행, 캠페인 클릭스루)는 항상 새 세션을 시작해야 합니다 | 비즈니스 논리 기반 세션 경계 제공 |

>[!NOTE]
>**결정: 속성 모델 기본값**
>
>전환 지표에 적용할 기본 속성 모델은 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 마지막 터치(기본값) | 크레딧이 전환 전에 가장 최근 접점으로 이동해야 합니다. | 단순하고 직관적이므로 인식 채널의 가치를 낮게 평가할 수 있음 |
>| 첫 번째 터치 | 초기 인지도 및 획득을 유도하는 채널 이해 | 획득 분석에 유용하며, 터치 포인트를 무시합니다 |
>| 선형 | 모든 접점은 동일한 크레딧을 공유해야 합니다. | 공정한 분배, 주요 접점의 영향을 희석할 수 있음 |
>| 시간 가치 감소 | 최근 접점은 먼 접점보다 더 많은 크레딧을 받아야 합니다 | 최신성과 과거 기여의 균형 잡기 |
>| U자형 | 첫 번째 및 마지막 접점은 가장 많은 크레딧을 받습니다 | 확보 및 종료 채널을 모두 이해하는 데 좋습니다. |
>| 알고리즘 | CJA의 AI 모델을 사용한 데이터 기반 속성 | 가장 정확하지만 충분한 변환 데이터 볼륨이 필요합니다. |

>[!NOTE]
>**결정: 파생된 필드 논리**
>
>원시 데이터를 분석 준비 차원으로 변환하려면 사용자 정의 비즈니스 규칙이 필요합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 마케팅 채널 분류(대/소문자) | 원시 추적 코드는 채널 그룹으로 분류되어야 합니다 | 가장 일반적으로 파생된 필드 사용 사례, 채널 분석에 중요 |
>| 값 버킷팅 | 연속 값은 범위로 그룹화되어야 합니다(예: 주문 값 계층). | 연속 지표의 분석을 간소화합니다. |
>| 필드 병합 | 여러 소스 필드를 단일 차원으로 결합해야 합니다 | 데이터 세트의 서로 다른 스키마 경로에 동일한 개념이 존재하는 경우 유용합니다 |
>| 정규 표현식 기반 추출 | 구조화된 값은 구문 분석해야 합니다(예: 캠페인 코드에서 캠페인 유형 추출) | 강력하지만 세심한 정규 표현식 패턴 디자인 필요 |

#### 데이터 보기 구성

**UI 탐색:** CJA > 데이터 보기 > 새 데이터 보기 만들기

주요 구성 세부 정보:

- 1단계에서 만든 상위 연결 선택
- 보고 요구 사항에 맞게 시간대 및 달력 유형 구성
- 적절한 지속성(할당 및 만료) 설정이 있는 차원에 XDM 스키마 필드 매핑
- 형식(십진수, 정수, 통화, 백분율, 시간) 및 속성 설정을 사용하여 XDM 스키마 필드를 지표에 매핑
- 관련 없는 값을 필터링하도록 차원에 대한 포함/제외 규칙 구성
- 필요한 경우 지표 중복 제거를 활성화하여 이중 계산 방지
- 마케팅 채널 분류, 값 버킷팅 또는 필드 병합을 위한 파생 필드 만들기
- 데이터 보기당 최대 5,000개의 차원 및 5,000개의 지표
- 데이터 보기당 최대 100개의 파생 필드

#### 옵션 분기 위치

**옵션 A(Campaign 성능 분석)의 경우:**

캠페인 특정 차원 매핑: 캠페인 이름, 여정 이름, 채널 유형, 메시지 변형, 제목 줄. 게재 지표 매핑: 전송, 게재, 열기, 클릭, 반송, 구독 취소. 캠페인 측정 철학을 기반으로 전환 지표에 대한 속성을 구성합니다.

**옵션 B(고객 여정 분석)의 경우:**

크로스 채널 차원 매핑: 페이지 이름, 앱 화면, 채널, 캠페인, 제품, 컨텐츠 유형. 모든 채널에 참여 및 전환 지표를 매핑합니다. 비교 분석을 위해 여러 속성 모델을 구성합니다. 채널 분류 및 여정 단계 식별을 위한 파생 필드를 만듭니다.

**옵션 D의 경우(가이드 분석):**

제품 경험 분석과 관련된 이벤트 수준 차원 및 지표(기능 이름, 사용자 작업, 참여 유형)를 매핑합니다. funnel 단계, 유지 기준 및 성장 신호를 정의하는 이벤트에 중점을 둡니다.

**Experience League 설명서:**

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

### 3단계: 분석 및 지표 만들기

**응용 프로그램 함수:** CJA: Workspace Analysis, CJA: 안내식 분석, CJA: 계산된 지표 만들기

이 단계에서는 분석 작업 공간(자유 형식 프로젝트 또는 안내식 분석), 파생된 KPI에 대한 계산된 지표, 세그먼트화된 분석에 대한 필터 및 주요 이벤트에 대한 주석을 빌드합니다. 비즈니스 질문에 답변할 수 있는 표, 시각화 및 지표를 구축하는 분석적 가치를 실현하는 곳입니다.

#### 의사 결정 지점

이 단계에서는 다음과 같은 결정을 내려야 합니다.

>[!NOTE]
>**결정: 분석 접근 방식**
>
>이 분석에서는 자유 형식 Workspace 프로젝트 또는 안내식 분석 워크플로를 사용해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 자유 형식 Workspace(옵션 A, B, C) | 심층 탐색 분석, 사용자 정의 레이아웃, 복잡한 분류, 고급 시각화 | 최고의 유연성, 분석가 기술 필요, 모든 시각화 유형 지원 |
>| 안내식 분석(옵션 D) | 구조화된 제품 인사이트, 특정 질문에 대한 빠른 답변, 기술 사용자 감소 | insight 출시 시간 단축, 사전 구축된 분석 유형으로 제한, 추가 맞춤화를 위해 Workspace에 저장 |
>| 모두 | 조직에는 심층적인 분석과 빠른 구조화된 인사이트가 모두 필요합니다. | 일반적인 질문에는 가이드 분석을 사용하고 심층적인 탐색에는 Workspace을 사용합니다. |

>[!NOTE]
>**결정: 시각화 유형**
>
>이 사용 사례에 대한 통찰력을 가장 잘 전달하는 시각화는 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 자유 형식 테이블 | 차원 분류를 사용한 자세한 데이터 탐색 | 대부분의 분석 기반, 최대 10개의 분류 수준 지원 |
>| 플로우 시각화 | 경로 지정 비헤이비어 이해(페이지 흐름, 채널 전환) | 여정 경로 발견에 탁월하며 카디널리티가 높은 복잡할 수 있음 |
>| 폴아웃 시각화 | 정의된 접점 시퀀스를 통해 전환 측정 | funnel 분석에 적합, 각 단계에서 드롭오프가 명확하게 표시됨 |
>| 코호트 테이블 | 고객 집단에 의한 시간 경과에 따른 유지 분석 | 서로 다른 그룹이 얼마나 잘 유지되는지 보여 줍니다. 라이프사이클 분석에 매우 중요합니다. |
>| 속성 패널 | 전환 지표에 대한 속성 모델 비교 | 병렬 모델 비교, 명확한 전환 이벤트 정의 필요 |
>| 요약 번호/변경 사항 | 기간별 비교를 통한 경영진 KPI 표시 | 깔끔하고 한 눈에 볼 수 있는 지표 표시, 대시보드 헤더에 이상적 |

>[!NOTE]
>**결정: 계산된 지표 수식**
>
>기본 데이터 보기 지표 외에 계산된 지표가 필요한 비즈니스 KPI는 무엇입니까?
>
>| 지표 패턴 | 공식 예 | 사용 시기 |
>| --- | --- | --- |
>| 비율 / 비율 | 주문 / 방문 횟수 | 전환율, 클릭스루 비율, 바운스 비율 |
>| 필터링된 지표 | 매출(여기서 channel = &quot;email&quot;) | 채널별 또는 세그먼트별 측정 |
>| 항목별 평균 | 매출 / 주문 | 평균 주문 가격, 방문당 매출 |
>| 복합 공식 | (수익 - 비용) / 수익 | 이익 백분율, ROI 계산 |
>| 참여 점수 | 상호 작용의 가중 합계 | 채널 간 복합 참여 점수 책정 |

#### 분석 및 지표 구성

**UI 탐색:**

- Workspace: CJA > Workspace > 프로젝트 > 프로젝트 만들기 > 빈 프로젝트
- 안내식 분석: CJA > 홈 > 안내식 분석(또는 Workspace > 만들기 > 안내식 분석)
- 계산된 지표: CJA > 구성 요소 > 계산된 지표 > 만들기
- 필터: CJA > 구성 요소 > 필터 > 필터 만들기

주요 구성 세부 정보:

- 2단계에서 만든 데이터 보기를 프로젝트 데이터 보기로 선택합니다
- 분석에 적합한 날짜 범위 및 비교 기간 설정
- 차원을 행으로, 지표를 열로 끌어 자유 형식 테이블 만들기
- 차원 분류를 추가하여 더 세부적인 수준에서 데이터를 탐색합니다(예: 캠페인별 채널, 제품별 페이지).
- 대상별 분석(개인 수준, 세션 수준 또는 이벤트 수준 범위)을 위한 재사용 가능한 필터(세그먼트) 만들기
- 주석을 추가하여 주요 비즈니스 이벤트(제품 출시, 캠페인, 인시던트)를 표시합니다.
- 계산된 지표 형식 (십진수, 퍼센트, 통화, 시간) 및 극성 설정 (증가가 양호/증가가 불량)
- 보기 또는 편집 권한에서 CJA 사용자와 작업 공간 프로젝트 공유

#### 옵션 분기 위치

**옵션 A(Campaign 성능 분석)의 경우:**

게재 및 참여 지표로 분류된 캠페인 차원을 사용하여 자유 형식 테이블을 작성합니다. 열람률, 클릭스루 비율, 전환율, 메시지당 매출 및 캠페인 ROI에 대한 계산된 지표를 만듭니다. 트렌드 시각화를 추가하여 시간 경과에 따른 캠페인 성과를 추적합니다. 캠페인 변형을 세그먼트 비교와 비교합니다.

**옵션 B(고객 여정 분석)의 경우:**

폴아웃 시각화를 작성하여 여정 드롭오프 지점을 식별합니다. 플로우 시각화를 만들어 채널 간 탐색 패턴을 살펴봅니다. 집단 테이블을 작성하여 획득 집단에 의한 유지를 측정합니다. 속성 패널을 구성하여 전환 지표에 대한 속성 모델을 비교합니다. 여정 완료율, 채널 간 참여 점수 및 라이프사이클 단계 전환에 대한 계산된 지표를 만듭니다.

**옵션 C의 경우(대상 게시가 있는 Analytics):**

옵션 A 또는 B에서 분석 작업 공간을 작성한 다음 분석 중에 고가치 또는 저성능 세그먼트를 식별합니다. 5단계에서 게시할 이러한 세그먼트를 캡처하는 CJA 필터를 만듭니다.

**옵션 D의 경우(가이드 분석):**

비즈니스 질문에 따라 적절한 가이드 분석 유형을 선택합니다. 주요 이벤트, 날짜 범위, 계산 방법 및 세그먼트 비교를 구성합니다. 추가적인 맞춤화를 위해 완료된 분석을 Workspace 프로젝트의 패널로 저장합니다.

**Experience League 설명서:**

- [Workspace 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/home)
- [프로젝트 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [자유 형식 테이블](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [플로우 시각화](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [폴아웃 시각화](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [코호트 테이블](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [속성 패널](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [분류 차원](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)
- [필터 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [필터 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-filters/create-filters)
- [주석 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/annotations/overview)
- [계산된 지표 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [계산된 지표 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [계산된 지표 함수](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-functions)
- [안내식 분석 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/overview)
- [Funnel 보기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/funnel/funnel)
- [트렌드 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/trends/usage)
- [유지 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/retention/retention-rates)
- [활성 증가 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/user-growth/active)
- [참여 빈도 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/trends/frequency)
- [릴리스 영향 보기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/guided-analysis/impact/release)
- [Content Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/content-analytics/content-analytics)

### 4단계: 대시보드 게시

**응용 프로그램 함수:** CJA: 대시보드 및 스코어카드 게시

이 단계에서는 관련자들에게 KPI 가시성을 제공하는 대화형 대시보드(Workspace 프로젝트) 및 모바일 스코어카드를 만듭니다. 대시보드는 요약 번호, 꺾은 선형, 분류 및 주석을 통해 실행 및 운영 가시성을 제공합니다. 모바일 스코어카드는 [!DNL Adobe Analytics] 대시보드 모바일 앱을 통해 한 눈에 성능 데이터를 제공합니다.

#### 의사 결정 지점

이 단계에서는 다음과 같은 결정을 내려야 합니다.

>[!NOTE]
>**결정: 대시보드 유형**
>
>데스크탑 Workspace 대시보드, 모바일 스코어카드 또는 둘 다입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| Workspace 프로젝트(데스크탑) | 분석가 및 마케터를 위한 자세한 대화형 대시보드 | 전체 시각화 기능, 패널, 테이블 및 복잡한 레이아웃 지원 |
>| 모바일 스코어카드 | 모바일 장치의 경영진 및 관련자를 위한 KPI 개요 | 16개 타일로 제한, 트렌드 스파크라인이 있는 요약 번호, 모바일 앱 필요 |
>| 모두 | 조직에는 상세한 분석과 경영진 수준의 모바일 보고가 모두 필요합니다. | 아티팩트를 구분하지만 동일한 데이터 보기와 계산된 지표를 공유할 수 있습니다 |

>[!NOTE]
>**결정: 모델 공유**
>
>대시보드는 누가 어떻게 받아야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 특정 사용자와 공유 | 특정 액세스 요구 사항이 있는 제한된 대상자 | 가장 세부적인 제어, 개별 사용자 관리 필요 |
>| 제품 프로필 그룹과 공유 | 조직 역할에 맞는 팀 수준 액세스 | 팀 전체 배포를 위한 효율성, CJA 제품 프로필을 통해 관리 |
>| 이메일 게재 예약 | CJA에 로그인하지 않는 이해 당사자를 위한 PDF/CSV 보고서 반복 | 자동 게재, 최대 빈도는 시간별, PDF 및 CSV 형식 |

>[!NOTE]
>**결정: 주석 가시성**
>
>대시보드 트렌드 라인에서 주요 이벤트에 주석을 달아야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 예 — 주석 생성 | 주요 캠페인, 제품 출시, 사이트 사고 또는 시즌 이벤트는 데이터 트렌드를 설명할 수 있습니다 | 주석은 선 차트 및 스코어카드 추세에 표식으로 표시되며 데이터 급증이나 감소에 대한 컨텍스트를 제공합니다 |
>| 아니요 | 대시보드 대상자는 비즈니스 컨텍스트에 익숙하며 주석은 혼란을 가중시킵니다 | 간단한 시각적 표현 |

#### 대시보드 구성

**UI 탐색:**

- Workspace 대시보드: CJA > Workspace > 프로젝트 만들기
- 모바일 스코어카드: CJA > 프로젝트 > 만들기 > 모바일 스코어카드
- 공유: CJA > Workspace > 공유 > Workspace 사용자와 공유
- 예약된 게재: CJA > Workspace > 공유 > 프로젝트 예약

주요 구성 세부 정보:

- 모바일 스코어카드의 경우 요약 번호 및 스파크라인 트렌드가 있는 단일 지표를 표시하는 타일을 만듭니다
- 기본 날짜 범위 및 비교 기간(예: 지난 30일과 이전 기간 비교 또는 월간) 구성
- 경영진이 모바일 스코어카드에서 전환할 수 있는 대상 범위 필터 추가
- 반복 PDF 또는 CSV 보고서에 대한 예약된 이메일 게재 구성
- 모바일 스코어카드당 최대 16개 타일, Workspace 프로젝트당 최대 15개 패널
- 주석은 데이터 보기당 100개로 제한됩니다

**Experience League 설명서:**

- [모바일 스코어카드 만들기](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [스코어카드 구성 및 조정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics 대시보드 — 경영진 안내서](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [프로젝트 공유](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [프로젝트 예약](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [요약 번호 시각화](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/visualizations/summary-number-change)
- [날짜 범위](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/date-ranges/overview)

### 5단계: 대상자 게시(옵션 C만 해당)

**응용 프로그램 함수:** CJA: 대상 게시

이 단계에서는 RT-CDP 대상, AJO 캠페인 또는 AJO 여정에서의 다운스트림 활성화를 위해 CJA 대상 게시를 구성하여 분석 검색된 세그먼트를 AEP 실시간 고객 프로필로 다시 푸시합니다.

#### 의사 결정 지점

이 단계에서는 다음과 같은 결정을 내려야 합니다.

>[!NOTE]
>**결정: 케이던스 새로 고침**
>
>대상 멤버십을 얼마나 자주 새로 고쳐야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 1회(스냅샷) | 지속적인 새로 고침이 필요하지 않은 캠페인 특정 대상 | 진행 중인 처리가 없습니다. 업데이트를 위해 다시 게시해야 합니다. |
>| 매 4시간 | 거의 실시간으로 활성화 요구 사항 | 높은 처리 비용, 시간에 민감한 대상자에게 최적 |
>| 매일 | 표준 마케팅 활성화 케이던스 | 균형 잡힌 신선도와 비용, 가장 일반적인 선택 |
>| 매주 | 안정적이고 느리게 변화하는 대상자 | 최소 처리, 장기 세그먼트에 적합 |

>[!NOTE]
>**결정: ID 네임스페이스**
>
>CJA은 대상 구성원 확인을 위해 어떤 ID 네임스페이스를 사용해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| CRM ID | 조직의 기본 고객 식별자 | 알려진 고객 일치를 위한 최상의 정확도 |
>| ECID | 주로 웹/앱 기반 대상 | 장치 범위, 일부 프로필 레코드로 확인되지 않을 수 있음 |
>| 이메일(해시됨) | 이메일은 활성화를 위한 공통 식별자입니다 | AEP ID 구성에 사용된 네임스페이스와 일치해야 함 |
>| 사용자 정의 네임스페이스 | 조직 전체에서 사용되는 고유 식별자 | AEP ID 서비스에서 구성해야 합니다. |

#### 대상자 게시 구성

**UI 탐색:** CJA > 구성 요소 > 대상 > 대상 게시

주요 구성 세부 정보:

- CJA 필터(개인, 세션 또는 이벤트 컨테이너 범위)를 사용하여 대상 기준을 정의합니다
- 게시할 데이터 보기 및 필터 선택
- AEP 프로필 확인을 위한 ID 네임스페이스 구성
- 활성화 요구 사항에 따라 새로 고침 케이던스 설정
- CJA 대상 목록(구성 요소 > 대상 > 상태 열)에서 게시 상태 모니터링
- AEP 대상 포털에 대상이 표시되는지 확인 (대상 > 찾아보기 > 원본을 기준으로 필터링 &quot;CJA&quot;)
- CJA 고객당 최대 75개의 게시된 대상(모든 샌드박스)
- 대규모 데이터 세트의 경우 초기 대상 평가에 최대 24시간이 소요될 수 있습니다

**Experience League 설명서:**

- [대상 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [대상자 생성 및 게시](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/publish)
- [대상자 관리](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/manage)
- [Audience Portal 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/audience-portal)

## 구현 시 고려 사항

이 섹션에서는 이 사용 사례 패턴에 대한 보호, 일반적인 위험, 우수 사례 및 보상 결정을 다룹니다.

### 보호 기능 및 제한 사항

이 구현에는 다음과 같은 보호 기능 및 제한이 적용됩니다.

- **연결 제한:** 조직당 최대 연결 수는 CJA SKU 권한으로 제한됩니다. 단일 연결에는 하나의 AEP 샌드박스의 데이터 세트만 포함될 수 있습니다. — [CJA 보호](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-admin/guardrails)
- **데이터 보기 제한:** 데이터 보기당 최대 5,000개의 차원과 5,000개의 지표를 사용할 수 있습니다. 최대 5개 수준의 중첩 함수를 사용하여 데이터 보기당 최대 100개의 파생 필드.
- **Workspace 제한:** 프로젝트당 최대 40개 패널. 자유 형식 테이블은 최대 10개의 차원 분류를 지원합니다. 보고서 요청당 최대 50,000개 행.
- **스코어카드 제한:** 모바일 스코어카드당 최대 16개 타일.
- **스트리밍 지연:** 스트리밍 데이터는 일반적으로 CJA 수집 후 90분 이내에 AEP에서 사용할 수 있습니다.
- **대상 게시 제한:** CJA 고객당 게시된 최대 대상 수는 75개입니다. 최소 새로 고침 간격은 4시간마다입니다.
- **안내가 있는 분석 제한:** Funnel 분석은 최대 15단계를 지원합니다. 세그먼트 비교는 최대 3개의 세그먼트를 동시에 지원합니다.

### 일반적인 함정

이 패턴을 구현할 때 다음과 같은 일반적인 문제에 유의하십시오.

- **데이터 세트 간 개인 ID 불일치:** 연결에 있는 모든 데이터 세트는 데이터 세트 간 분석을 위해 일관된 개인 ID 필드를 사용해야 합니다. 일치하지 않는 개인 ID로 인해 동일한 개인이 여러 사용자로 표시되는 고객 보기가 세분화됩니다. 연결을 만들기 전에 개인 ID 일관성을 확인하십시오.

- **다시 채우기가 예기치 않게 오래 걸립니다.** 수십 억 개의 레코드가 있는 대용량 데이터 세트는 다시 채우는 데 며칠이 걸릴 수 있습니다. 구현 타임라인 동안 이를 계획하고 채우기를 조기에 시작하십시오. 연결 세부 정보 보기에서 진행 상황 모니터링.

- **대부분의 차원 값에 대해 &quot;지정되지 않음&quot;을 표시하는 데이터 보기:** 매핑된 스키마 필드는 소스 데이터에서 드물게 채워질 수 있습니다. 구성 오류를 가정하기 전에 소스 데이터 세트에서 데이터 품질을 확인하십시오. 파생된 필드를 사용하여 null 값을 처리하는 것이 좋습니다.

- **세션 수가 잘못된 것 같습니다.** 세션 시간 제한 설정은 세션 범위 지표에 큰 영향을 줍니다. 매우 짧은 시간 제한은 더 많은 세션을 생성하고, 매우 긴 시간 제한은 더 적은 세션을 생성합니다. 새 세션 시작 이벤트는 세션을 예기치 않게 분할할 수도 있습니다. 알려진 사용자 동작 패턴에 대해 세션 설정을 검토하고 테스트합니다.

- **속성 모델이 예상대로 적용되지 않음:** 속성 모델은 차원이 아닌 지표에만 적용됩니다. 전환 확인 기간이 비즈니스 주기에 맞게 설정되어 있는지 확인합니다. 짧은 전환 확인 기간은 초기 funnel 터치포인트를 놓칠 수 있습니다.

- **0 또는 예기치 않은 값을 반환하는 계산된 지표:** 수식에서 참조된 기본 지표에 선택한 날짜 범위에 대한 대상 데이터 보기의 데이터가 있는지 확인하십시오. 비율 지표에서 0으로 나누기를 확인합니다. 지표 정의를 검색하고 공식 구조를 확인합니다.

- **대상 게시 실패(옵션 C):** CJA 연결에 AEP ID 네임스페이스로 확인되는 올바른 개인 ID가 있어야 합니다. ID 네임스페이스 구성을 확인하고 대상 샌드박스에서 AEP 실시간 고객 프로필이 활성화되었는지 확인합니다.

### 우수 사례

성공적인 구현을 위해 다음 모범 사례를 따르십시오.

- **단일 포괄적인 연결로 시작:** 관련된 모든 데이터 세트를 포함하는 하나의 연결을 만든 다음 다양한 분석 관점에 대해 여러 데이터 보기를 만듭니다. 이를 통해 접속 확산을 방지하고 관리를 간소화합니다.

- **마케팅 채널 분류에 파생 필드 사용:** 원시 추적 코드에 의존하지 않고 Case When 논리로 파생 필드를 만들어 트래픽을 마케팅 채널로 분류합니다. 이렇게 하면 모든 분석에서 일관된 채널 보고가 보장됩니다.

- **지표 사전 만들기:** 모든 계산된 지표를 해당 수식, 사용 목적 및 예상 값 범위로 문서화합니다. 분석 팀과 이 사전을 공유하여 프로젝트 간 일관된 지표 사용을 보장합니다.

- **대상자를 위한 데이터 보기 디자인:** 다양한 관련자 그룹에 대한 개별 데이터 보기(캠페인 중심 차원과 지표가 있는 마케팅 데이터 보기, 기능 및 참여 차원이 있는 제품 데이터 보기)를 만듭니다. 이렇게 하면 각 사용자 그룹에 대한 구성 요소 목록이 간소화됩니다.

- **모든 항목에 주석 달기:** 캠페인 시작, 사이트 변경, 기술 인시던트, 시즌 및 데이터 트렌드를 설명할 수 있는 모든 이벤트에 대한 주석을 만듭니다. 주석은 몇 달 후 대시보드를 검토할 때 중요한 컨텍스트를 제공합니다.

- **수동 계산에 대해 계산된 지표를 테스트합니다.** 대시보드에 대해 계산된 지표를 사용하기 전에 계산된 지표 및 기본 구성 요소를 함께 사용하여 보고서를 실행합니다. 계산된 값이 수동 계산과 일치하는지 확인합니다.

- **필터를 전략적으로 사용:** 일반적인 세분화 패턴(새 세그먼테이션과 재방문 세그먼트, 모바일과 데스크톱 세그먼트, 지역별로)에 대해 재사용 가능한 필터를 만듭니다. 이러한 매개 변수를 모든 자유 형식 테이블에 포함하지 않고 패널 수준 필터로 적용합니다.

- **정기적으로 연결 상태 모니터링:** 연결 세부 정보 보기에서 생략된 레코드, 실패한 일괄 처리 및 스트리밍 지연에 대해 확인하십시오. 연결 수준의 데이터 품질 문제는 모든 다운스트림 분석에 영향을 줍니다.

### 절충안 결정

구현을 계획할 때 다음 절충안을 고려하십시오.

>[!NOTE]
>**절충: 분석 깊이와 insight 소요 시간**
>
>옵션 B(고객 여정 분석)는 가장 심층적인 크로스 채널 인사이트를 제공하지만 연결 구성, 데이터 보기 디자인 및 파생된 필드 생성에 상당한 사전 투자가 필요합니다. 옵션 D(가이드 분석)는 구조화된 워크플로우를 통해 insight에 도달하는 시간이 더 빠르지만 분석적 유연성은 더 낮습니다.
>
>- **옵션 B는 다음과 같은 이점을 제공합니다.** 포괄적인 이해, 복잡한 다중 채널 분석, 속성 모델링, 사용자 지정 KPI 개발
>- **옵션 D는 다음을 선호합니다.** 속도, 비분석가 사용자의 접근성, 구조화된 제품 경험 질문
>- **권장 사항:** 옵션 B 인프라를 병렬로 빌드하는 동안 즉각적인 제품 통찰력을 위해 옵션 D로 시작합니다. 많은 조직이 서로 다른 팀에 대해 두 작업을 동시에 실행합니다.

>[!NOTE]
>**상충: 채우기 완성도와 연결 준비 비교**
>
>모든 이전 데이터를 가져오면 연도별 비교 및 장기 추세 분석에 대한 분석적 깊이가 최대화되지만 대규모 데이터 세트의 채우기에는 며칠이 걸릴 수 있습니다. 채우기 기간을 최근 기간으로 제한하면 연결이 더 빨리 준비되지만 기록 분석이 제한됩니다.
>
>- **모든 데이터 선호도:** 장기 트렌드 분석, 연도별 비교, 확장된 기록이 있는 집단 분석
>- **제한된 채우기 지원:** 연결 준비 시간 단축, 첫 번째 대시보드까지 빠른 시간, 스토리지 최적화
>- **권장 사항:** 전략 분석을 지원하는 프로덕션 연결에 대한 모든 데이터를 다시 채웁니다. 개발 연결 및 개념 증명 구현에 제한된 채우기를 사용합니다.

>[!NOTE]
>**절충: 단일 포괄적인 데이터 보기와 여러 중요 데이터 보기**
>
>모든 차원과 지표가 포함된 단일 데이터 보기는 통합 분석 작업 공간을 제공하지만 구성 요소 목록으로 사용자를 압도할 수 있습니다. 여러 개의 집중 데이터 보기(팀당 또는 사용 사례당 한 개)를 사용하면 구성 요소 경험이 간소화되지만 여러 구성을 유지 관리할 수 있습니다.
>
>- **단일 데이터 보기에 적합한 기능:** 통합 분석, 도메인 간 분류, 간편한 관리
>- **여러 데이터 보기를 선호하는 경우:** 구성 요소 목록, 팀별 용어, 사용 사례별로 다른 세션 정의
>- **권장 사항:** 기본 데이터 보기 하나로 시작한 다음 구성 요소 목록 복잡성으로 인해 채택이 방해가 되는 경우 추가 중요 데이터 보기를 만듭니다. 모든 데이터 보기는 동일한 연결을 참조할 수 있습니다.

>[!NOTE]
>**거래: 실시간 스트리밍과 일괄 처리 전용 수집 비교**
>
>CJA 연결에서 스트리밍을 활성화하면 실시간에 가까운 데이터(AEP 수집 후 ~90분 이내)를 제공하지만 더 많은 데이터를 지속적으로 처리합니다. 일괄 처리 전용 수집은 정기적으로 데이터를 처리하며 지연이 발생할 수 있습니다.
>
>- **스트리밍 우대:** 적시 보고, 활성 캠페인 모니터링, 실시간에 가까운 대시보드
>- **일괄 처리 전용 우대:** 간단한 구성, 예측 가능한 처리 기간, 주별 또는 월별 보고에 충분한 경우
>- **권장 사항:** 프로덕션 연결에 스트리밍을 사용합니다. 활성 캠페인 모니터링 및 운영 대시보드를 위해 시기적절한 데이터의 가치에 비해 증가되는 처리 비용은 미미합니다.

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
