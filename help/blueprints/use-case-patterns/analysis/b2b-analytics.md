---
title: B2B 분석
description: 크로스 채널 고객 여정 분석에 B2B 계정 수준 정보를 포함하는 방법을 알아봅니다.
solution: Customer Journey Analytics, Real-Time Customer Data Platform
exl-id: 9d576e5c-cbd2-4c60-a6b0-88f8b8b963b4
source-git-commit: ccfd8c987a0090ca690e15a4bd89f4d96ec9c01f
workflow-type: tm+mt
source-wordcount: '7528'
ht-degree: 1%

---

# B2B 분석

이 안내서에서는 [!DNL Customer Journey Analytics]&#x200B;([!DNL CJA]) B2B edition 및 [!DNL Real-Time Customer Data Platform]&#x200B;([!DNL RT-CDP]) B2B edition을 사용하는 B2B 계정 수준 분석에 대한 포괄적인 구현 참조를 제공합니다. 크로스 채널 고객 여정 분석에 B2B 계정 수준 정보를 통합해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

각 옵션을 선택할 시기에 대한 지침과 함께 플랫 계정 구조에서 복잡한 글로벌 계정 계층에 이르기까지 계정 중심 분석을 위한 모든 실행 가능한 접근 방식을 다룹니다. 이 계획은 B2B 데이터 연결, 계정 데이터 보기 구성, 작업 공간 분석 및 대시보드 게시를 해결합니다.

B2B Analytics는 계정 기반 연결, B2B 관련 컨테이너(계정, 글로벌 계정, 영업 기회, 구매 그룹) 및 계정 수준 보고를 사용하여 표준 [!DNL CJA] 기능을 확장합니다. 이 기능을 통해 조직은 계정 수준에서 마케팅 및 판매 참여를 분석하고, 영업 기회 진행을 추적하고, 구매 그룹 완성도를 측정하고, 확장된 B2B 판매 주기 전반에 걸쳐 마케팅 접점에 매출을 연결할 수 있습니다.

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

## 사용 사례 패턴

**B2B 분석**

크로스 채널 고객 여정 분석에 B2B 계정 수준 정보를 포함합니다.

**함수 체인:** B2B 데이터 연결 > 계정 데이터 보기 구성 > Workspace 분석 > 대시보드 게시

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Customer Journey Analytics]B2B edition** — 계정 기반 연결, B2B별 데이터 보기 컨테이너, 계정 수준 작업 영역 분석, 구매 그룹 분석, 기회 분석, B2B 세그멘테이션 및 B2B 속성과 확장된 전환 확인 기간을 제공합니다
- **[!DNL Real-Time CDP]B2B edition** — 계정 프로필 통합, B2B ID 해결, B2B 스키마 클래스(계정, 영업 기회, 구매 그룹) 및 B2B 참여 데이터 수집을 위한 [!DNL Marketo Engage] 통합을 포함하는 B2B 데이터 기반을 제공합니다.

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 필수 | [!DNL CJA] B2B edition 및 [!DNL RT-CDP] B2B edition 권한으로 구성된 샌드박스. [!DNL CJA] 및 B2B 데이터 모델에 대한 액세스 권한이 있는 데이터 엔지니어, 애널리스트 및 마케팅 작업 사용자에게 제공된 역할입니다. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home) |
| 데이터 모델링 및 준비 | 필수 | B2B 클래스를 사용하여 구성된 B2B XDM 스키마: XDM 비즈니스 계정, XDM 비즈니스 영업 기회, XDM 비즈니스 계정 사용자 관계, XDM 비즈니스 영업 기회 사용자 관계 및 XDM 비즈니스 마케팅 목록 멤버. 계정 속성, 영업 기회 단계 및 구매 그룹 역할에 대한 필드 그룹을 정의해야 합니다. 프로필용으로 생성되어 활성화된 데이터 세트. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [B2B edition 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| 데이터 소스 및 수집 | 필수 | B2B 데이터 원본은 일반적으로 [!DNL Marketo Engage] 원본 커넥터 또는 [!DNL Salesforce] CRM 원본 커넥터를 통해 연결됩니다. 계정 레코드, 영업 기회 레코드, 개인-계정 관계 및 행동 참여 이벤트가 AEP 데이터 세트로 흘러야 합니다. [!DNL Web SDK] 또는 [!DNL Marketo] 통합은 계정 연결이 있는 동작 이벤트를 캡처해야 합니다. | [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [Marketo Engage 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| ID 및 프로필 구성 | 필수 | 개인-계정 관계를 확인하도록 구성된 B2B ID 해결입니다. 계정 ID, 개인 ID([!DNL Marketo] 리드 ID 또는 CRM 연락처 ID) 및 교차 장치 ID(ECID, 이메일)가 연결되어 있어야 합니다. ID 그래프는 B2B 데이터 모델에 내재된 다대다 개인 대 계정 매핑을 지원해야 합니다. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [B2B ID 확인](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| 대상 정의 및 세분화 | 가정 위치 | 활성화를 위해 B2B 세그먼트가 [!DNL CJA]에서 AEP으로 다시 게시되는 경우 계정 수준 대상 정의를 사용할 수 있어야 합니다. 분석 전용 사용 사례의 경우 엄격한 사전 요구 사항은 아니지만 세그먼트 기반 분석에 권장됩니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 계정 프로필의 계산된 특성(예: 총 참여 점수, 마지막 활동 이후 일수, 기회 수)은 계정 수준 분석을 위해 [!DNL CJA]에서 사용할 수 있는 분석 차원을 보강합니다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | B2B 데이터 세트, 특히 [!DNL Marketo Engage]의 동작 이벤트 데이터는 빠르게 증가할 수 있습니다. 데이터 세트 만료 정책은 스토리지를 관리하고 데이터 보존 요구 사항을 준수하는 데 도움이 됩니다. | [고급 데이터 수명 주기 관리](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | B2B 데이터에는 중요한 비즈니스 정보(계약 가치, 경쟁 인텔리전스)가 포함되는 경우가 많습니다. 데이터 사용 레이블 및 거버넌스 정책은 분석 및 활성화 워크플로 전반에서 이 데이터가 적절하게 사용되도록 합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| 모니터링 및 가시성 | 추천 | B2B 소스 커넥터([!DNL Marketo], [!DNL Salesforce])는 수집 상태에 대한 모니터링이 필요합니다. [!DNL CJA]의 연결 상태 모니터링은 분석을 위한 데이터 새로 고침을 보장합니다. 수집 실패에 대한 경고 규칙은 오래된 대시보드를 방지합니다. | [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | 이 패턴은 그 자체로 분석 패턴입니다. 이 기능은 핵심 기능 체인이 보고 및 분석 기능을 전달함에 따라 본질적으로 포함되어 있다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Customer Journey Analytics] B2B edition

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 계정 기반 연결 | 1단계: B2B 데이터 연결 | 계정 또는 글로벌 계정을 조직 수준 분석을 위한 기본 식별자로 사용하여 연결 구성 |
| B2B 데이터 보기 구성 | 2단계: 계정 데이터 보기 구성 | 표준 사용자, 세션 및 이벤트 컨테이너와 함께 B2B 관련 컨테이너(계정, 글로벌 계정, 기회, 구매 그룹)를 사용하여 데이터 보기를 정의합니다 |
| 계정 수준 Workspace 분석 | 3단계: Workspace 분석 | 계정 수준 차원, 지표 및 조직 수준 여정 통찰력을 위한 B2B 컨테이너를 사용하여 자유 형식 분석 빌드 |
| 구매 그룹 분석 | 3단계: Workspace 분석 | 구매 결정 프로세스를 통해 구매 그룹 구성, 참여 및 진행 상황 분석 |
| 영업 기회 분석 | 3단계: Workspace 분석 | 영업 funnel 단계를 통해 영업 기회 진행 상황을 추적하고 마케팅 참여 데이터와의 상관 관계를 파악합니다 |
| B2B 세그멘테이션 | 3단계: Workspace 분석 | 필터링된 계정 수준 분석을 위해 B2B 컨테이너를 사용하여 세그먼트 만들기 |
| B2B 속성 | 3단계: Workspace 분석 | B2B 판매 주기 분석을 위해 확장 13개월 계정 전환 확인 기간을 사용하여 속성 모델 적용 |
| 계산된 지표 만들기 | 3단계: Workspace 분석 | 계정 참여율, 구매 그룹 완성도 및 파이프라인 영향과 같은 B2B KPI에 대해 계산된 지표를 정의합니다 |
| 대시보드 및 스코어카드 게시 | 4단계: 대시보드 게시 | 마케팅 및 영업 리더십을 위해 대시보드 및 모바일 스코어카드를 만들고 공유 |
| 대상자 게시 | 4단계: 대시보드 게시 | AEP 다운스트림 활성화를 위해 [!DNL CJA]에서 정의한 계정 기반 대상 게시 |

### [!DNL Customer Journey Analytics] — 표준 함수

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 데이터 연결 | 1단계: B2B 데이터 연결 | 채널 간 분석을 위해 AEP B2B 데이터 세트를 [!DNL CJA] 연결에 바인딩 |
| 데이터 보기 구성 | 2단계: 계정 데이터 보기 구성 | B2B 데이터 보기 내에서 표준 차원, 지표, 속성 및 지속성 설정 구성 |
| Workspace 분석 | 3단계: Workspace 분석 | 테이블, 폴아웃, 플로우, 집단 및 속성 시각화를 사용하여 자유 형식 분석 구축 |
| 안내 분석 | 3단계: Workspace 분석 | 계정 수준에서 funnel, 트렌드 및 유지 분석에 대한 가이드 워크플로 사용 |

### [!DNL Real-Time CDP] B2B edition

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 계정 프로필 통합 | 전제 조건(F2/F4) | 특수 XDM B2B 스키마 클래스를 사용하여 교차 소스 B2B 데이터를 통합 계정 프로필로 통합 |
| B2B Id 확인 | 전제 조건(F4) | 여러 수준의 계정 계층 및 다대다 매핑을 지원하는 개인 대 계정 관계 해결 |
| [!DNL Marketo Engage] 통합 | 전제 조건(F3) | 기본 B2B 소스 커넥터를 통해 [!DNL Marketo Engage]에서 행동 참여 데이터 및 계정/잠재 고객 레코드 수집 |

## 필요 조건

구현이 시작되기 전에 다음 항목이 있어야 합니다.

- [!DNL CJA] B2B edition 라이선스가 활성화되어 있고 조직에 대해 프로비저닝되었습니다.
- [!DNL RT-CDP] B2B edition 라이선스가 B2B 스키마 및 계정 프로필이 구성된 상태로 활성 상태입니다.
- B2B XDM 스키마가 정의됩니다(계정, 기회, 계정 사용자 관계, 기회 사용자 관계, 마케팅 목록 멤버).
- [!DNL Marketo Engage] 및/또는 CRM 원본 커넥터가 구성되어 있으며 현재 데이터를 수집 중입니다.
- 계정 수준 행동 이벤트 데이터(웹 방문, 이메일 상호 작용, 양식 제출)가 계정 연결과 함께 AEP으로 흘러가고 있습니다
- ID 그래프에서 개인 대 계정 관계가 설정됩니다
- 최소 30일의 내역 B2B 참여 데이터를 의미 있는 분석에 사용할 수 있습니다
- 이해 당사자는 그룹 역할 정의 및 솔루션 관심 매핑을 구입하는 데 동의했습니다.
- [!DNL CJA]개의 사용자 계정이 B2B edition 기능에 적합한 제품 프로필로 프로비저닝되었습니다.
- 타겟 KPI 및 보고 요구 사항은 마케팅 및 영업 리더십에 의해 정의되었습니다

## 구현 옵션

다음 섹션에서는 이러한 사용 사례 패턴을 구현하기 위한 다양한 접근 방식을 설명합니다.

### 옵션 A: 계정 중심 분석

**계정의 렌즈를 통해 모든 참여 및 파이프라인 데이터를 분석하려는 조직:**&#x200B;에 가장 적합합니다. 이 접근 방법에서는 계정 컨테이너를 기본 분석 단위로 사용하여 구매 여정을 통해 계정이 어떻게 진행되는지에 대한 하향식 보기를 제공합니다.

**작동 방식:**

계정을 기본 식별자로 사용하여 [!DNL CJA] B2B 연결을 구성합니다. 모든 행동 이벤트, 기회 및 구매 그룹 데이터가 계정 레벨로 적상됩니다. 데이터 보기는 계정 내에서 중첩된 개인, 세션 및 이벤트를 사용하여 계정을 최상위 컨테이너로 사용합니다. 이렇게 하면 &quot;몇 개의 계정이 가격 페이지를 방문하여 30일 이내에 영업 기회를 만들었습니까?&quot;와 같은 분석이 가능합니다.

계정 중심 분석은 계정이 구매 단위인 B2B 조직에 대해 가장 자연스러운 보기를 제공합니다. 업계, 회사 규모, 계정 계층 및 계정 소유자와 같은 차원을 사용하여 참여 패턴 및 파이프라인 지표를 분류할 수 있습니다. 속성은 긴 B2B 판매 주기를 수용하는 13개월 전환 확인 기간과 함께 계정 수준에서 적용됩니다.

**주요 고려 사항:**

- ID 그래프에서 깔끔한 계정 간 매핑 필요
- 모든 개인 수준 이벤트는 계정에 귀속되어야 합니다.
- 계정과 연결할 수 없는 익명 웹 트래픽은 계정 수준 분석에 표시되지 않습니다

**장점:**

- 전체 구매 여정에 대한 실제 계정 수준 보기를 제공합니다.
- B2B 매출이 생성되는 방식과 일치하는 계정 기반 속성을 사용합니다.
- 계정 내에서 중첩된 컨테이너로 구매 그룹 및 기회 분석을 지원합니다.
- ABM(계정 기반 마케팅) 전략에 맞게 분석 조정

**제한 사항:**

- 강력한 사용자-계정 ID 해결 필요
- 익명 또는 일치하지 않는 참여 데이터는 분석에서 제외됩니다
- 사용자 중심 분석보다 구성하는 것이 더 복잡함

**Experience League:**

- [CJA B2B edition 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)
- [B2B edition 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)

### 옵션 B: 글로벌 계정 중심 분석

**모회사에 여러 자회사 계정이 있는 복잡한 계정 계층 구조를 가진 기업 조직**&#x200B;에 가장 적합합니다. 이 접근 방법에서는 글로벌 계정을 기본 식별자로 사용하여 모든 자회사 계정 활동을 상위 조직 레벨로 롤업합니다.

**작동 방식:**

계정 대신 기본 식별자로 전역 계정과의 [!DNL CJA] B2B 연결을 구성하십시오. 이는 해당 모회사 조직의 모든 자회사 계정에서 참여 데이터를 집계합니다. 예를 들어 &quot;Acme Corp&quot;에 지역 자회사인 &quot;Acme EMEA&quot; 및 &quot;Acme APAC&quot;가 있는 경우 글로벌 계정 연결은 세 엔티티 모두의 참여를 단일 분석 보기로 통합합니다.

데이터 보기에는 계정, 사용자, 세션 및 이벤트를 중첩 컨테이너로 사용하는 최상위 컨테이너인 글로벌 계정이 포함됩니다. 이를 통해 동일한 작업 영역 프로젝트 내의 글로벌 및 자회사 계정 수준에서 분석을 수행할 수 있습니다. 기여도 분석 전환 확인 기간은 글로벌 계정 수준에서 적용되며, 전체 기업 계층에 걸쳐 모든 접점을 캡처합니다.

**주요 고려 사항:**

- B2B 데이터 모델에 정의된 상위-하위 관계가 있는 계정 계층 데이터가 필요합니다.
- 글로벌 계정 ID는 모든 계정 레코드에서 채워지고 정확해야 합니다
- 자회사 계정은 모회사에 올바르게 매핑되어야 합니다.

**장점:**

- 복잡한 엔터프라이즈 계정 구조에 대한 통합 가시성 제공
- 단일 기업 고객이 여러 개의 계정 기록을 보유하고 있는 경우 단편적인 분석 방지
- 단일 글로벌 계정 내에서 지역 자회사 간 비교 가능
- 엔터프라이즈급 파이프라인 및 매출 보고 지원

**제한 사항:**

- 많은 조직에서 유지 관리에 어려움을 겪고 있는 정확한 계정 계층 데이터가 필요합니다.
- 글로벌 수준에서만 볼 때 하위 수준 패턴을 가릴 수 있음
- 계층 관계를 설정하고 유지하기 위한 추가적인 데이터 모델링 노력

**Experience League:**

- [CJA B2B edition 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### 옵션 C: 하이브리드 사용자 + 계정 분석

**가장 좋은 방법:** 사용자 기반 분석에서 계정 기반 분석으로 전환하는 조직 또는 사용자 수준 보기와 계정 수준 보기가 모두 필요한 조직 이 접근 방식은 동일한 연결에서 두 개의 데이터 보기 (한 사람 중심 및 한 계정 중심)를 만듭니다.

**작동 방식:**

모든 B2B 데이터 세트(이벤트, 계정, 영업 기회, 구매 그룹, 사용자-계정 관계)를 포함하는 단일 [!DNL CJA] B2B 연결을 구성합니다. 그런 다음 Person을 기본 컨테이너로 사용하는 보기(표준 [!DNL CJA]과 유사)와 Account를 기본 컨테이너로 사용하는 보기, 이렇게 두 개의 데이터 보기를 만듭니다. 분석가는 묻는 질문에 따라 데이터 보기 간에 전환할 수 있습니다.

개인 중심 데이터 보기는 기존의 개별 수준 여정 분석을 제공합니다(예: &quot;기회가 되는 잠재 고객에 대한 전환 경로는 무엇입니까?&quot;). 반면, 계정 중심 데이터 보기는 조직 수준 분석을 제공합니다(예: &quot;참여 대 파이프라인 전환율이 가장 높은 계정&quot;). 두 보기 모두 동일한 기본 데이터를 사용하므로 일관성이 보장됩니다.

**주요 고려 사항:**

- 잠재적으로 다른 차원 및 지표 구성을 가진 두 개의 데이터 보기 필요
- 분석가는 각 보기를 사용할 시기에 대한 교육이 필요합니다.
- 계산된 지표는 각 데이터 보기에 대해 별도로 생성해야 할 수 있습니다

**장점:**

- 개인 및 계정 수준 모두에서 데이터를 분석할 수 있는 유연성 제공
- 개인 수준 분석에 익숙한 팀의 쉬운 채택 경로
- 사용자 수준 및 계정 수준 지표를 비교할 수 있습니다
- 리드 기반 및 계정 기반 마케팅 전략 모두 지원

**제한 사항:**

- 유지 관리 및 동기화 유지를 위한 두 개의 데이터 보기
- 사용할 보기에 대한 분석가의 잠재적 혼동
- 계산된 지표 및 필터는 보기 간에 중복이 필요할 수 있습니다

**Experience League:**

- [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [데이터 보기 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

### 옵션 비교

| 기준 | 옵션 A: 계정 중심 | 옵션 B: 글로벌 계정 중심 | 옵션 C: 하이브리드 사용자 + 계정 |
| --- | --- | --- | --- |
| 다음에 최적 | 플랫 계정 구조를 사용하는 표준 B2B | 상위-하위 계층이 있는 Enterprise | 조직 또는 이중 요구 사항 전환 |
| 복잡성 | 중간 | 높음 | Medium 하이 |
| 데이터 요구 사항 | 계정-사용자 매핑 | 계정 계층 구조 + 매핑 | 계정-사용자 매핑 |
| 속성 범위 | 계정 수준(13개월 전환 확인) | 글로벌 계정 수준(13개월 전환 확인) | 개인 및 계정 수준 모두 |
| 익명 데이터 | 계정 보기에서 제외됨 | 전역 보기에서 제외됨 | 개인 보기에 포함됨, 계정 보기에서 제외됨 |
| 필요 | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition, 계층 데이터 | [!DNL RT-CDP] B2B edition, [!DNL CJA] B2B edition |
| 유지 관리 노력 | 단일 데이터 보기 | 단일 데이터 보기 | 2개의 데이터 보기 |

### 적절한 옵션 선택

- **옵션 A를 선택합니다** 조직에 일반 계정 구조(상위-하위 계층 없음)가 있고 ABM 전략이 개별 계정 수준에서 작동하며 계정 수준 분석에 대한 가장 간단한 경로를 원하는 경우.
- **옵션 B**&#x200B;을(를) 선택하십시오. 대상 계정이 지역 또는 사업부의 자회사 계정을 가진 대기업이고 기업 상위 수준에서 통합 보고가 필요한 경우. 이 옵션을 사용하려면 고품질 계정 계층 구조 데이터가 필요합니다.
- **옵션 C를 선택합니다** 조직에서 리드 기반에서 계정 기반 마케팅으로 전환하는 경우, 분석가는 개인 수준 funnel 분석과 계정 수준 참여 분석을 모두 필요로 하거나 B2B와 B2C 비즈니스 라인이 혼합된 경우.

## 구현 단계

다음 단계에서는 권장 구현 순서를 간략하게 설명합니다.

### 1단계: B2B 데이터 연결

**응용 프로그램 함수:** [!DNL CJA] B2B: 계정 기반 연결, [!DNL CJA]: 데이터 연결

분석을 위해 AEP B2B 데이터 세트를 [!DNL CJA]에 바인딩하는 [!DNL CJA] 연결을 구성하십시오. 이 연결은 [!DNL CJA]&#x200B;(으)로 유입되는 데이터 세트, 기본 식별자 유형(계정 또는 글로벌 계정), 내역 및 스트리밍 데이터를 수집하는 방법을 정의합니다. 이 연결은 모든 후속 분석의 기초입니다.

#### 결정: 기본 식별자 유형

연결에 계정 ID 또는 글로벌 계정 ID를 기본 식별자로 사용할지 여부를 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 계정 ID | 플랫 계정 구조, 상위-하위 계층 없음 | 설정이 간단합니다. 각 계정은 독립적으로 분석됩니다. 중소기업 중심 B2B를 위한 가장 일반적인 선택. |
| 글로벌 계정 ID | 자회사 계층이 있는 기업 계정 | 계층 데이터가 필요합니다. 상위에 있는 모든 자회사를 집계합니다. 엔터프라이즈 ABM 프로그램에 적합합니다. |

#### 의사 결정: 데이터 세트 선택 및 유형 지정

포함해야 하는 B2B 데이터 세트와 각 데이터 유형을 지정하는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이벤트 데이터 세트(동작) | 항상 포함 | 웹 인터랙션, 이메일 이벤트, 양식 제출, 콘텐츠 다운로드. 타임스탬프 필드가 있어야 합니다. 이것은 참여 신호입니다. |
| 계정 레코드 데이터 세트(프로필) | 항상 포함 | 업계, 크기, 계층, 소유자 등 계정 속성. 계정 분석을 위한 차원 컨텍스트를 제공합니다. |
| 영업 기회 데이터 세트(조회/프로필) | 파이프라인 분석에 포함 | 영업 기회 단계, 가치, 종료 날짜. 파이프라인 및 수익 속성 분석에 필요합니다. |
| 구매 그룹 데이터 세트(조회/프로필) | 구매 그룹 분석에 포함 | 그룹 역할, 참여 점수, 완성도 구매 구매 그룹 구성 분석에 필요합니다. |
| 사용자-계정 관계 데이터 세트(조회) | 항상 포함 | 사용자를 계정에 매핑합니다. 개인 레벨 이벤트를 계정 레벨 분석과 연관시키는 데 중요합니다. |
| 캠페인/프로그램 데이터 세트(조회) | 속성에 포함 | 캠페인 메타데이터, 프로그램 유형, 채널. 캠페인 영향 분석을 사용합니다. |

#### 의사 결정: 범위 채우기

연결에 가져와야 하는 내역 데이터의 양을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기존의 모든 데이터 | B2B 판매 주기는 길며(6~18개월) 전체 기록이 필요합니다 | B2B에 권장됩니다. 채우기 작업에는 큰 데이터 세트의 경우 일 정도 걸릴 수 있지만 완전한 속성 데이터를 제공합니다. |
| 사용자 지정 날짜 범위(최근 2~3년) | 데이터 품질이 특정 시점 이상으로 저하됨 | 완전성과 데이터 품질의 균형을 맞춥니다. CRM 데이터에 기록 불일치가 있는 경우 일반적입니다. |
| 채우기 없음 | 테스트 또는 개발만 해당 | 새 데이터만 전송됩니다. 프로덕션 B2B 분석에 적합하지 않습니다. |

#### B2B 데이터 연결 구성

**UI 탐색:** [!DNL Customer Journey Analytics] > 연결 > 새 연결 만들기

주요 구성 세부 정보:

- B2B 데이터 세트를 포함하는 AEP 샌드박스 를 선택합니다
- 능력 계획에 대한 일일 평균 이벤트 수 설정
- 각 데이터 세트를 추가하고 해당 유형(이벤트, 조회 또는 프로필)을 지정합니다.
- B2B 연결에 계정 ID 또는 글로벌 계정 ID를 사용하도록 개인 ID 필드를 구성합니다
- 실시간에 가까운 업데이트가 필요한 데이터 세트에 대한 스트리밍 활성화
- 내역 채우기에 대해 &quot;기존 데이터 모두 가져오기&quot; 활성화

**옵션이 나뉘는 위치:**

**옵션 A(계정 중심)의 경우:**
기본 식별자를 계정 ID로 설정합니다. 계정 레코드, 영업 기회, 구매 그룹 및 개인 계정 관계 데이터 세트를 추가합니다. 교차 데이터 세트 조인을 위해 계정 ID 필드로 개인 수준 이벤트 데이터 세트를 구성합니다.

**옵션 B(전역 계정 중심)의 경우:**
기본 식별자를 글로벌 계정 ID로 설정합니다. 계정 계층 구조 데이터에 글로벌 계정 ID 필드가 포함되어 있는지 확인합니다. 모든 데이터 세트에는 적절한 롤업을 위해 글로벌 계정 ID가 포함되어 있거나 가입할 수 있어야 합니다.

**옵션 C(하이브리드)의 경우:**
모든 B2B 데이터 세트와 단일 연결을 만듭니다. 계정 ID를 기본 식별자로 사용합니다. 동일한 연결에 대해 다른 데이터 보기 구성을 사용하여 2단계에서 사람 중심 보기가 만들어집니다.

**Experience League 설명서:**

- [연결 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [연결 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [연결 관리](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/manage-connections)
- [CJA B2B edition 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### 2단계: 계정 데이터 보기 구성

**응용 프로그램 함수:** [!DNL CJA] B2B: B2B 데이터 보기 구성, [!DNL CJA]: 데이터 보기 구성

분석에 연결 데이터가 표시되는 방식을 정의하는 데이터 보기를 구성합니다. B2B 분석의 경우 B2B별 컨테이너(계정, 영업 기회, 구매 그룹) 구성, B2B 스키마 필드를 차원 및 지표에 매핑, B2B에 적합한 전환 확인 기간을 사용하여 속성 모델 설정, B2B 비즈니스 로직에 대한 파생 필드 생성 등이 포함됩니다.

#### 결정: 컨테이너 구성

활성화할 B2B 컨테이너와 컨테이너의 이름을 지정하는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 계정 + 개인 + 세션 + 이벤트 | 구매 그룹 또는 영업 기회 분석이 없는 표준 B2B | 가장 간단한 B2B 컨테이너 계층 구조. 계정은 최상위 컨테이너입니다. |
| 계정 + 영업 기회 + 개인 + 세션 + 이벤트 | 파이프라인 및 매출 분석 필요 | 영업 기회를 컨테이너 수준으로 추가하여 영업 기회 범위를 분석할 수 있습니다. |
| 계정 + 구매 그룹 + 기회 + 개인 + 세션 + 이벤트 | 구매 그룹 구성을 포함한 전체 B2B 분석 | 가장 포괄적입니다. B2B 데이터 모델의 모든 수준에서 분석을 활성화합니다. |
| 글로벌 계정 + 계정 + 개인 + 세션 + 이벤트 | 글로벌 계정 계층 구조 분석 | 글로벌 계정을 계정 위의 최상위 수준 컨테이너로 추가합니다. |

#### 의사 결정: B2B 지표에 대한 속성 모델

전환 지표에 대해 어떤 속성 모델이 기본값이 되어야 하는지 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 선형 속성(13개월 전환 확인) | B2B 여정의 모든 접점과 동일한 크레딧 | 마케팅 활동의 전체 혼합을 이해하는 데 가장 적합합니다. B2B의 권장 시작점. |
| U자형 속성(13개월 전환 확인) | 크레딧을 이용한 첫 번째 및 마지막 터치 강조 | 리드 생성 및 기회 전환 순간을 강조합니다. 수요 생성 분석에서 일반적입니다. |
| 시간 감소(13개월 전환 확인) | 최근 터치포인트가 더 많은 크레딧을 받아야 합니다. | 참여 최신성이 판매 준비에 중요한 신호가 될 때 가장 좋습니다. |
| 마지막 터치 | 전환 전 최종 터치포인트에 대한 간단한 보고 | 이해하기는 쉽지만 초기 단계 마케팅은 저평가된다. 빠른 운영 보고에만 사용합니다. |

#### 의사 결정: B2B에 대한 세션 정의

B2B 참여에 대해 세션을 정의하는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 30분 시간 초과(기본값) | 표준 웹 분석 세션 동작 | 웹 참여 분석을 위한 표준. 긴 콘텐츠 소비 세션을 조각화할 수 있습니다. |
| 확장된 시간 초과(60-120분) | B2B 사용자는 더 긴 리서치 세션에 참여합니다. | B2B 구매자는 기술 콘텐츠, 가격 및 설명서를 검토하는 데 오랜 시간을 소비하는 경우가 많습니다. |
| 이벤트 기반 새 세션 | 특정 이벤트는 항상 새 세션을 시작해야 합니다. | 캠페인 클릭스루 또는 데모 요청이 항상 새 분석 세션을 시작해야 하는 경우 사용합니다. |

#### 계정 데이터 보기 구성

**UI 탐색:** [!DNL Customer Journey Analytics] > 데이터 보기 > 새 데이터 보기 만들기

주요 구성 세부 정보:

- 1단계에서 생성된 연결 선택
- 조직에 적합한 시간대 및 달력 유형 구성
- 컨테이너의 이름을 B2B 관련 용어(예: 계정/참여/터치포인트)로 변경합니다.
- B2B 스키마 필드를 차원에 매핑: 계정 이름, 계정 ID, 업계, 회사 규모, 계정 계층, 계정 소유자, 기회 단계, 기회 값, 구매 그룹 역할, 솔루션 관심
- 참여 지표 매핑: 이벤트(발생 횟수), 사람, 세션, 페이지 보기 수, 양식 제출, 이메일 열기, 이메일 클릭 수
- 주요 차원에 대한 지속성 구성(예: 계정 산업은 계정 수준에서 지속됨)
- 전환 지표에 대한 기본값으로 13개월 전환 확인을 사용하여 속성을 선형으로 설정합니다
- 마케팅 채널 분류, 참여 점수 책정 계층 및 영업 기회 단계 그룹화를 위한 파생 필드 만들기

**옵션이 나뉘는 위치:**

**옵션 A(계정 중심)의 경우:**
계정을 최상위 컨테이너로 사용하여 단일 데이터 보기를 구성합니다. 파이프라인 및 구매 그룹 분석이 필요한 경우 영업 기회 및 구매 그룹 컨테이너를 포함합니다.

**옵션 B(전역 계정 중심)의 경우:**
글로벌 계정을 최상위 컨테이너로 구성합니다. 글로벌 및 자회사 분석을 모두 사용할 수 있도록 계정을 하위 컨테이너로 포함합니다.

**옵션 C(하이브리드)의 경우:**
동일한 연결에서 두 개의 데이터 보기를 만듭니다. 데이터 보기 1은 사용자를 기본 컨테이너로 사용합니다(표준 [!DNL CJA] 동작). 데이터 보기 2는 B2B 컨테이너와 함께 계정을 기본 컨테이너로 사용합니다. 적용 가능한 경우 동일한 지표를 두 보기에 매핑합니다.

**Experience League 설명서:**

- [데이터 보기 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [구성 요소 설정 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview)
- [지속성 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)
- [속성 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/attribution)
- [파생 필드](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/derived-fields)
- [세션 설정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/session-settings)

### 3단계: Workspace 분석

**응용 프로그램 기능:** [!DNL CJA] B2B: 계정 수준 Workspace 분석, 구매 그룹 분석, 영업 기회 분석, B2B 세분화, B2B 속성, [!DNL CJA]: Workspace 분석, 계산된 지표 만들기, 안내식 분석

KPI에 정의된 분석 통찰력을 제공하는 작업 공간 프로젝트를 빌드합니다. 이 단계에는 B2B 차원 및 지표를 사용하여 자유 형식 테이블 작성, B2B KPI에 대한 계산된 지표 만들기, B2B별 시각화 구성(계정 수준 플로우, 영업 기회 funnel, 구매 그룹 참여), B2B 컨테이너를 사용하여 필터/세그먼트 만들기, B2B 속성 모델 적용 등이 포함됩니다.

#### 의사 결정: Analysis workspace 구조

작업 영역 프로젝트를 구성하는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 여러 패널이 있는 단일 종합 프로젝트 | 소규모 팀, 모든 이해 당사자가 동일한 보고서 보기 | 유지 관리가 쉬워집니다. 패널을 사용하여 주제(참여, 파이프라인, 속성)를 구분합니다. 프로젝트당 최대 40개의 패널. |
| 대상자별 다중 집중 프로젝트 | 이해 당사자마다 다른 견해가 필요합니다. | 마케팅은 참여/속성을 가져옵니다. 판매는 파이프라인/계정 상태를 가져옵니다. 작업이 데이터 품질을 가져옵니다. 유지 보수는 늘었지만 타겟팅은 향상되었습니다. |
| 가이드 분석을 통한 템플릿 기반 프로젝트 | 전문가가 아닌 사용자를 위한 셀프서비스 분석 | funnel 및 트렌드 보기에 대해 안내식 분석을 사용합니다. 반복 가능한 분석을 위해 템플릿으로 저장합니다. 광범위한 채택에 적합합니다. |

#### 결정: B2B 계산된 지표

B2B KPI에 필요한 계산된 지표를 결정합니다.

| 지표 | 공식 | 생성 시기 |
| --- | --- | --- |
| 계정 참여 비율 | (총 계정 이벤트 / 총 계정) | 항상 — 핵심 B2B 지표 |
| 구매 그룹 완전성 % | (채워진 역할 / 필수 역할) * 100 | 구매 그룹 분석이 범위 내에 있는 경우 |
| 계정-영업 기회 전환 | 영업 기회 / 참여 계정 보유 고객 | 파이프라인 분석이 필요한 경우 |
| 파이프라인 영향 % | 영향을 받은 파이프라인 값 / 총 파이프라인 값 | 마케팅 속성이 필요한 경우 |
| 연락처당 평균 참여 | 계정당 이벤트 / 고유 사용자 | 계정 침투 분석이 필요한 경우 |
| 역할별 콘텐츠 참여 | 구매 그룹 역할로 필터링된 이벤트 | B2B에 대한 콘텐츠 최적화가 필요한 경우 |

#### 결정: B2B 필터/세그먼트 범위

어떤 컨테이너 수준 필터를 만들어야 하는지 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 계정 수준 필터 | 계정 일치 기준(예: 엔터프라이즈 계정, 특정 산업)으로 범위가 지정된 분석 | 적격 계정의 모든 이벤트를 포함합니다. B2B에 가장 일반적입니다. |
| 영업 기회 수준 필터 | 특정 영업 기회 유형 또는 단계에 대한 분석 | 영업 기회 검증과 관련된 모든 이벤트를 포함합니다. |
| 그룹 수준 필터 구매 | 특정 구매 그룹 상태에 대한 분석 범위 | 적격 구매 그룹에 있는 사람들의 이벤트를 포함합니다. |
| 개인 수준 필터 | 개별 일치 기준(예: 특정 역할, 제목)에 대한 분석 범위 | 표준 필터 동작. B2B 컨텍스트 내에서 개별 참여를 분석할 때 를 사용합니다. |

#### 작업 공간 분석 빌드

**UI 탐색:** [!DNL Customer Journey Analytics] > Workspace > 프로젝트 > 프로젝트 만들기

주요 구성 세부 정보:

- 2단계에서 만든 B2B 데이터 보기 선택
- 참여 지표로 분류된 계정 수준 차원(계정 이름, 업계, 계층)을 사용하여 자유 형식 테이블 작성
- 단계를 통한 기회 진행을 보여주는 기회 funnel 시각화 만들기
- 역할별 역할 충족률 및 참여를 보여 주는 구매 그룹 구성 표를 작성합니다.
- 기여도 분석 모델(선형, U자형, 시간 감소)과 13개월 전환 확인을 비교하는 B2B 기여도 분석 패널 구성
- 구매 여정을 통한 일반적인 경로를 보여 주는 계정 플로우 시각화 만들기
- 시간에 따른 계정 유지 및 재참여를 분석하는 집단 테이블 작성
- 계정 계층, 업계 또는 참여 수준별 세그먼트 분석에 B2B 필터 적용
- 중요 이벤트(캠페인 시작, 제품 릴리스, 가격 변경)에 대한 주석 만들기

**Experience League 설명서:**

- [Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [프로젝트 만들기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/build-workspace-project/create-projects)
- [자유 형식 테이블](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/freeform-table/freeform-table)
- [속성 패널](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/attribution)
- [플로우 시각화](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/flow/flow)
- [폴아웃 시각화](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/fallout/fallout-flow)
- [코호트 테이블](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/visualizations/cohort-table/cohort-analysis)
- [필터 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-filters/filters-overview)
- [계산된 지표 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)
- [계산된 지표 만들기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/cm-workflow/cm-build-metrics)
- [주석 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/annotations/overview)
- [안내식 분석 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/guided-analysis/overview)
- [분류 차원](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/components/dimensions/t-breakdown-fa)

### 4단계: 대시보드 게시

**응용 프로그램 함수:** [!DNL CJA]: 대시보드 및 스코어카드 게시, [!DNL CJA]: 대상 게시

관련자들에게 B2B 분석 통찰력을 제공하는 공유 가능한 대시보드 및 모바일 스코어카드를 만드십시오. 이 단계에서는 B2B 대상 활성화와 같은 다운스트림 사용 사례에서 활성화를 위해 [!DNL CJA] 정의된 B2B 대상을 AEP에 다시 게시하는 작업도 다룹니다.

#### 의사 결정: 대시보드 게재 방법

B2B 분석 통찰력이 이해 당사자에게 전달되는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| Workspace 프로젝트(데스크탑) | 대화식 탐색이 필요한 분석가 및 마케팅 운영 | 전체 상호 작용, 드릴다운, 필터 전환. [!DNL CJA] 액세스 권한이 필요합니다. |
| 모바일 스코어카드 | KPI를 한눈에 파악해야 하는 경영진 및 영업 리더 | 추세선이 있는 요약 번호. [!DNL Adobe Analytics] 대시보드 앱을 통해 액세스할 수 있습니다. 제한된 상호 작용. |
| 예약된 PDF/CSV 내보내기 | 정기 업데이트가 필요한 [!DNL CJA] 액세스 권한이 없는 이해 당사자 | 일정에 따른 자동 게재. 인터랙티브 없음. 주간/월간 경영진 요약에 가장 적합합니다. |
| 위의 모든 항목 | 다양한 이해 관계자의 요구 사항을 가진 대규모 조직 | 최대 도달 거리. 유지 관리 작업 향상 성숙 B2B 분석 프로그램에 권장됩니다. |

#### 결정: [!DNL CJA]에서 게시하는 대상

활성화를 위해 B2B 세그먼트를 AEP에 다시 게시해야 하는지 여부를 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 계정 기반 대상 게시 | Analytics 인사이트는 타겟팅 및 억제에 대해 알려야 함 | [!DNL RT-CDP]을(를) 통해 [!DNL CJA]개의 정의된 세그먼트(예: &quot;열려 있는 기회가 없는 참여도가 높은 계정&quot;)를 활성화할 수 있습니다. 케이던스 새로 고침: 매주 4시간 |
| 게시 안 함 | Analytics는 보고 전용이며, 활성화는 아닙니다. | 간단한 구성. 활성화가 [!DNL RT-CDP]에서 별도로 처리되었습니다. |

#### 대시보드 및 대상자 게시

**UI 탐색:** [!DNL Customer Journey Analytics] > 프로젝트 > 공유(Workspace의 경우), 프로젝트 > 만들기 > 모바일 스코어카드(스코어카드의 경우), 구성 요소 > 대상 > 게시(대상 게시의 경우)

주요 구성 세부 정보:

- 주요 B2B KPI에 대한 요약 번호를 사용하여 경영진 대시보드를 작성합니다(총 참여 계정, 파이프라인 가치, 구매 그룹 완성도).
- 트렌드 지표에 대한 비교 기간(월별, 분기별)을 구성합니다.
- 계정 참여, 파이프라인 상태 및 속성 지표에 대한 타일을 사용하여 모바일 스코어카드 만들기
- 경영진이 지역, 업계 또는 계정 계층별로 보기를 전환할 수 있는 필터를 추가합니다.
- 주간 경영진 보고서에 대한 예약된 프로젝트 게재 구성
- 대상 게시: B2B 필터를 선택하고 ID 네임스페이스(계정 ID)를 구성한 다음 새로 고침 간격을 설정합니다

**Experience League 설명서:**

- [모바일 스코어카드 만들기](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/create-scorecard)
- [프로젝트 공유](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/share-projects)
- [프로젝트 예약](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/curate-share/send-schedule-files)
- [스코어카드 구성 및 조정](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/curate)
- [Adobe Analytics 대시보드 — 경영진 안내서](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dashboards/set-up-execs)
- [대상 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/audiences-overview)
- [대상자 생성 및 게시](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)

## 구현 시 고려 사항

다음 섹션에서는 구현 중에 기억해야 할 보호 기능, 일반적인 위험, 모범 사례 및 상충 결정을 다룹니다.

### 보호 기능 및 제한 사항

- [!DNL CJA] 연결에는 하나의 AEP 샌드박스에서만 데이터 세트를 포함할 수 있습니다. [CJA 보호](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-admin/guardrails)
- 데이터 보기당 최대 5,000개의 차원 및 5,000개의 지표
- 데이터 보기당 최대 100개의 파생 필드
- B2B 속성은 계정 수준 분석을 위해 최대 13개월까지 전환 확인 기간을 지원합니다
- 모든 샌드박스에서 [!DNL CJA] 고객당 최대 75개의 게시된 대상
- 대상자 게시 최소 새로 고침 케이던스는 4시간마다 입니다.
- AEP에서 [!DNL CJA]&#x200B;(으)로의 스트리밍 지연은 일반적으로 90분 미만입니다.
- 자유 형식 테이블은 최대 10개의 차원 분류를 지원합니다
- 모바일 스코어카드는 스코어카드당 최대 16개의 타일을 지원합니다
- Workspace 프로젝트는 프로젝트당 최대 40개의 패널을 지원합니다
- 대규모 B2B 데이터 세트(수십억 개의 레코드)에 대한 채우기를 완료하는 데 며칠이 걸릴 수 있습니다

### 일반적인 함정

- **불완전한 개인-계정 매핑:** 개인 수준 이벤트를 계정과 연결할 수 없는 경우 계정 수준 분석에 나타나지 않습니다. 모든 이벤트 데이터 세트에는 직접 또는 사용자 계정 관계 조회 데이터 세트를 통해 계정 ID에 연결할 수 있는 필드가 포함되어 있는지 확인합니다. 계정 연결이 누락된 이벤트의 비율을 감사한 후 분석을 빌드합니다.
- **잘못된 데이터 세트 유형 지정:** B2B 조회 데이터 세트(영업 기회, 구매 그룹, 개인 계정 관계)는 [!DNL CJA] 연결에서 조회 또는 프로필 유형으로 올바르게 지정되어야 합니다. [!DNL CJA]이(가) 각 레코드를 타임스탬프가 지정된 이벤트로 처리하려고 하므로 조회 데이터 세트를 이벤트 데이터 세트로 잘못 입력하면 잘못된 결과가 생성됩니다.
- **B2B에 대한 속성 기간이 너무 짧음:** 기본 30일 속성 기간을 사용하면 일반적으로 6~18개월에 걸친 B2B 여정의 초기 단계 접점이 누락됩니다. 항상 B2B 속성 지표에 대한 13개월 전환 확인 기간을 구성합니다.
- **계정 수준 및 사용자 수준 지표를 잘못 혼합:** 계정 수준 분석에서 &quot;사람&quot;을 계산하는 것은 오해의 소지가 있을 수 있습니다. 계산된 지표가 적절한 컨테이너 수준에서 정의되었는지 확인합니다. &quot;계정 참여 비율&quot;은 계정 수준 이벤트를 사람이 아닌 계정으로 나눈 값을 사용해야 합니다.
- **오래된 구매 그룹 데이터:** 구매 그룹 구성 및 역할 할당이 시간이 지남에 따라 변경됩니다. 구매 그룹 데이터 세트를 정기적으로 새로 고치지 않으면 완전성 지표가 부정확해집니다. 소스 시스템([!DNL Marketo Engage] 또는 [!DNL AJO] B2B edition)에서 구매 그룹 데이터를 동기화하고 있는지 확인하십시오.
- **단일 작업 영역 프로젝트 오버로드:** B2B 분석은 참여, 파이프라인, 속성 및 구매 그룹에 적용됩니다. 모든 항목을 한 프로젝트에 추가하려고 하면 로드 속도가 느려지고 탐색이 혼란스러워집니다. 여러 개의 포커스가 있는 프로젝트 또는 명확하게 레이블이 지정된 패널을 사용합니다.

### 우수 사례

- 나중에 옵션 B(글로벌 계정)를 사용할 계획이더라도 옵션 A(계정 중심)로 시작합니다. 계정 중심 분석은 단순하며 계층 복잡성을 추가하기 전에 데이터 모델의 유효성을 검사합니다.
- 계정 연결, 고아 계정 수 및 구매 그룹 완전성 지표가 있는 이벤트의 비율을 추적하는 전용 &quot;B2B 데이터 품질&quot; 작업 영역 프로젝트를 만듭니다. 데이터 문제를 조기에 발견하려면 이 주간을 실행하십시오.
- 파생 필드를 사용하여 계정 수준 이벤트 수를 기반으로 참여 점수 책정 계층(높음/Medium/낮음)을 만듭니다. 이렇게 하면 분석을 단순화하고 기술 전문가가 아닌 이해 당사자에게 대시보드의 작업을 보다 효과적으로 수행할 수 있습니다.
- B2B 속성을 구성할 때 선형 속성을 기준으로 시작한 다음 U자형 및 시간 감소 모델과 비교합니다. 모델 간의 차이로 인해 마케팅 믹스가 인지도 또는 전환 활동에 가중치가 부여되는지 여부가 드러나는 경우가 많습니다.
- 리더십에 가장 중요한 KPI를 다루는 타일이 8개 이하인 &quot;B2B 실행 요약&quot; 모바일 스코어카드를 게시합니다. 집중 유지 - 경영진 스코어카드는 &quot;어떻게 하고 있습니까?&quot;에 답해야 합니다. &quot;왜?&quot;가 아니라
- 주요 이벤트(제품 출시, 주요 캠페인 출시, 가격 변경, 판매 프로세스 변경)에 주석을 달아 데이터 트렌드에 대한 컨텍스트를 제공합니다. B2B 데이터는 종종 이벤트 컨텍스트 없이 설명할 수 없는 급등과 급감을 표시합니다.
- [!DNL CJA]에서 B2B 대상자를 게시할 때 표준 활성화 세그먼트에 대해서는 매일 새로 고침을 사용하고 시간에 민감한 세그먼트에 대해서는 4시간 새로 고침을 사용하십시오. 잦은 새로 고침은 처리 리소스를 사용합니다.

### 절충안 결정

>[!NOTE]
>다음의 상충 결정은 조직의 특정 요구 사항과 제약 조건을 기반으로 평가되어야 합니다.

**데이터 완전성과 분석 정확성 비교**

계정 분석에 모든 개인 수준 이벤트(계정 연관성이 약한 이벤트도 포함)는 데이터 완전성을 향상시키지만 계정 매핑을 신뢰할 수 없는 경우 분석 정확도를 줄일 수 있습니다.

- **모든 이벤트를 포함하는 것:** 포괄적인 참여 측정, 더 높은 계정 참여 점수, 더 넓은 가시성
- **일치하지 않는 이벤트를 제외하는 것이 좋습니다.** 정확한 계정 수준 지표, 신뢰할 수 있는 속성, 신뢰할 수 있는 파이프라인 상관 관계
- **권장 사항:** 일치하지 않는 이벤트를 계정 수준 분석에서 제외하되, 전체 상황을 이해하려면 별도의 사용자 수준 데이터 보기(옵션 C)에 포함하십시오. 병렬 워크스트림으로 계정 연결 데이터 품질 개선을 우선적으로 고려하십시오.

**B2B 속성 전환 확인 기간 길이**

더 긴 전환 확인 기간(13개월)은 더 많은 접점을 캡처하지만 현재 구매 결정과 더 이상 관련이 없는 마케팅 활동을 포함할 수 있습니다.

- **더 긴 전환 확인(13개월) 필요:** 전체 B2B 여정 캡처, 인식 단계 활동 크레딧, 긴 판매 주기 수용
- **더 짧은 전환 확인(6개월) 혜택:** 최근 참여에 집중하여 이전 접점에서 소음을 줄이고 현재 구매 의도를 더 잘 반영합니다.
- **권장 사항:** 판매 주기가 긴 엔터프라이즈 계정(12개월 이상)에 대해 13개월 전환 확인을 사용합니다. 주기가 짧은 중간 시장 계정에 대해 6개월 전환 확인을 사용합니다. 비교할 각 창에 대해 별도의 계산된 지표를 만듭니다.

**하나의 포괄적인 데이터 보기와 여러 개의 중요 데이터 보기**

모든 B2B 컨테이너와 차원이 있는 하나의 데이터 보기는 유지 관리가 더 간단하지만 분석가에게 복잡성이 가중될 수 있습니다. 여러 개의 포커스가 있는 데이터 보기(참여, 파이프라인, 속성)는 사용하기 더 쉽지만 유지 관리가 더 어렵습니다.

- **단일 보기 기능 지원:** 일관성, 간편한 유지 관리, 단일 프로젝트 내 도메인 간 분석
- **여러 뷰를 선호하는 이유:** 분석가를 위한 단순성, 더 빠른 로드 시간, 사용 사례별 맞춤 구성 요소 목록
- **권장 사항:** 포괄적인 단일 데이터 보기로 시작합니다. 분석가가 적합한 차원 및 지표를 찾는 데 어려움을 보고하면 여러 보기로 분할하기 전에 동일한 보기 내에서 조정된 구성 요소 그룹을 생성합니다. 작업 공간 템플릿을 사용하여 분석가에게 적합한 구성 요소를 안내합니다.

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
