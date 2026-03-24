---
title: 구매 그룹 기반 마케팅 및 여정 관리
description: B2B 마케팅 효과를 향상시키기 위해 구매 그룹으로 잠재 고객을 선별하는 계정 수준 여정을 개발하는 방법에 대해 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 2bf57f67-80c8-4368-98d2-05706427772d
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7932'
ht-degree: 0%

---

# 구매 그룹 기반 마케팅 및 여정 관리

이 안내서에서는 구매 그룹 기반 마케팅 및 여정 관리에 대한 포괄적인 구현 참조를 제공합니다. [!DNL Adobe Journey Optimizer B2B Edition] 및 [!DNL Real-Time CDP B2B Edition]을(를) 사용하여 구매 그룹 관리를 통해 계정 수준 여정 오케스트레이션을 구현해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

이 문서를 사용하여 구성할 내용, 구현 선택 사항이 있는 위치 및 각 의사 결정에 영향을 미치는 요인을 파악합니다.

개인 수준 여정 패턴과 달리 이 패턴은 계정 수준에서 작동하며, 자격을 갖춘 개인은 솔루션 관심사와 관련된 구매 그룹으로 이어지고, 구매 그룹 수준에서 참여 점수를 매기고, 파이프라인 단계를 거쳐 판매 준비로 계정을 진행하는 여러 단계 계정 여정을 조정합니다.

## 사용 사례 개요

B2B 조직은 근본적인 과제에 직면해 있습니다. 구매 결정은 단일 개인이 수행하는 경우는 거의 없습니다. 복합 B2B 구매에는 여러 관련자(의사 결정자, 인플루언서, 챔피언, 예산 보유자, 기술 평가자)가 포함되며 이들은 집합적으로 &quot;구매 그룹&quot;을 형성합니다. 기존의 리드 기반 마케팅은 계정 내에서 적절한 역할 조합이 이루어지고 구매 준비가 되어 있는지에 대한 중요한 신호를 누락하고 각 개인을 독립적으로 취급합니다.

구매 그룹 기반 마케팅 및 여정 관리는 오케스트레이션 단위를 개별 리드에서 계정 및 구매 그룹으로 이동하여 이를 해결합니다. 이 패턴을 통해 B2B 마케터는 솔루션 관심 분야(판매 중인 제품 또는 서비스)를 정의하고, 구매 결정에 필요한 역할을 지정하는 구매 그룹 템플릿을 만들고, 이러한 역할에 대해 수신 리드를 검증하고, 구매 그룹 수준에서 참여를 평가하고, 구매 그룹 완전성 및 준비 신호에 응답하는 계정 여정을 오케스트레이션할 수 있습니다.

원하는 결과를 얻을 수 있는 파이프라인 품질 및 속도 향상: 마케팅은 계정 내 적합한 인력이 투입되고 구매 그룹이 충분히 완료될 때만 매출에 계정을 전달하여 불필요한 판매 노력을 줄이고 거래 진행을 가속화합니다.

## 주요 비즈니스 목표

이 사용 사례 패턴은 다음과 같은 비즈니스 목표를 지원합니다.

### 리드 자격 및 전환 개선

점수 책정, 육성 및 개인화된 후속 조치를 통해 잠재 고객 품질을 높이고 파이프라인 진행을 가속화합니다.

**KPI:** 잠재 고객 전환, 잠재 고객/잠재 고객 전환, 효율성

[리드 자격 및 전환 개선에 대해 자세히 알아보기](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### 리드 생성 늘리기

양식, 이벤트, 콘텐츠 및 멀티채널 참여를 통해 판매 파이프라인에 대해 보다 적합한 리드를 생성합니다.

**KPI:** 잠재 고객, 잠재 고객당 비용, 잠재 고객 전환

[리드 생성 증가에 대해 자세히 알아보기](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### 매출 및 판매 증대

최적화된 디지털 채널, 캠페인 및 고객 여정을 통해 매출 성장을 촉진합니다.

**KPI:** 매출 성장, 파이프라인 속도, 거래 마감률

[매출 및 판매 증가에 대해 자세히 알아보기](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

## 예시 전술 사용 사례

다음은 이 패턴을 적용할 수 있는 특정 시나리오입니다.

- **솔루션별 구매 그룹 자격** - 필요한 담당자(경제 구매자, 기술 평가자, 챔피언, 최종 사용자)를 지정하는 역할 템플릿을 사용하여 각 제품 라인에 대한 구매 그룹(예: &quot;Enterprise CRM&quot;, &quot;Data Platform&quot;, &quot;Security Suite&quot;)을 정의하고 CRM 및 마케팅 자동화 시스템의 리드를 해당 역할에 대해 검증합니다.
- **파이프라인 가속화를 위한 계정 여정** — 타깃팅된 육성 이메일을 구매 그룹 내의 미참여 역할에 보내고, 참여 임계값에 도달하면 판매 알림을 트리거하고, 계정을 판매 준비 단계로 전환하는 여러 단계 계정 여정을 조정합니다.
- **구매 그룹 완전성 캠페인** — 구매 그룹에 역할이 누락된 계정을 식별하고(예: 경제 구매자가 식별되지 않음) 타깃팅된 획득 캠페인을 시작하여 해당 계정 내에서 적합한 담당자를 참여시킵니다.
- **교차 판매 계정 여정** — 초기 거래가 종료된 후 보완 솔루션 관심사를 위해 새 구매 그룹을 만들고 확장된 구매 위원회를 구성하는 계정 여정을 조정합니다.
- **지연된 거래에 대한 다시 참여** — 구매 그룹 참여 점수가 하락한 계정을 감지하고 새 콘텐츠, 경영진 지원 또는 이벤트 초대로 다시 참여 여정을 트리거합니다.
- **CRM 인사이트를 통한 판매 및 마케팅 정렬** - [!DNL Salesforce] 또는 [!DNL Dynamics 365] 내에서 직접 구매 그룹 상태, 참여 데이터 및 계정 여정 진행 상황을 표면화하므로 영업 담당자가 마케팅 자격 있는 계정을 실시간으로 볼 수 있습니다.
- **이벤트 기반 구매 그룹 업데이트** — 잠재 고객이 웨비나에 참석하거나, 백서를 다운로드하거나, 가격 페이지를 방문하거나, 데모를 요청하면 구매 그룹 멤버십과 참여 점수를 자동으로 업데이트합니다.
- **여러 지역 계정 조정** — 다른 지역 연락처가 다른 역할을 담당하는 글로벌 계정의 구매 그룹을 관리하여 지역 간 참여 점수를 통합합니다.

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 효과를 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 구매 그룹 완전성 비율 | 모든 필수 역할이 채워진 구매 그룹의 백분율 | [!DNL AJO B2B] Analytics 대시보드: 구매 그룹당 역할 범위를 추적합니다. |
| 구매 그룹 참여 점수 | 구매 그룹의 모든 구성원에 대한 참여 점수 집계 | [!DNL AJO B2B] 참여 점수: 개인 수준 점수가 구매 그룹에 롤업됨 |
| MQA(마케팅 적격 계정) 비율 | 마케팅 자격 임계값에 도달한 계정의 비율 | 계정 여정 종료 기준: 계정이 판매 준비 단계로 전환됨 |
| 파이프라인 속도 | 구매 그룹 생성에서 판매 적격 기회까지의 평균 시간 | CRM 통합: [!DNL AJO B2B]에서 CRM 파이프라인으로의 단계 전환 추적 |
| 잠재 고객-구매 그룹 자격률 | 구매 그룹 역할에 대한 적격 잠재 고객 비율 | [!DNL AJO B2B] 구매 그룹 관리: 적격 대 비적격 리드 비율 |
| 영업 경고 응답률 | 판매 후속 활동을 유발하는 판매 경보의 백분율 | CRM Sales Insights: 경고에서 활동으로 전환 추적 |
| 계정 여정 완료율 | 의도한 여정 경로를 완료하는 계정의 백분율 | [!DNL AJO B2B] Analytics 대시보드: 여정 완료 지표 |
| 이메일 참여 비율(B2B) | B2B 육성 이메일에 대한 오픈율 및 클릭스루 비율 | [!DNL AJO B2B] 보고: 전자 메일 게재 및 참여 지표 |

## 사용 사례 패턴

**그룹 기반 마케팅 및 여정 관리 구매**

B2B 마케팅 효과를 개선하기 위해 잠재 고객을 구매 그룹으로 분류하는 계정 수준 여정을 개발합니다.

**기능 체인:** 계정 식별 > 구매 그룹 정의 > 잠재 고객 자격 > 계정 여정 실행 > 참여 점수 > 보고

## 애플리케이션

이 사용 사례 패턴에는 다음 Adobe 애플리케이션이 사용됩니다.

- **[!DNL Journey Optimizer B2B Edition] ([!DNL AJO B2B])** — 계정 수준 여정을 조정하고, 역할 템플릿과 솔루션 관심사를 사용하여 구매 그룹을 관리하고, 개인 및 구매 그룹 수준에서 참여 점수를 매기고, 작성자 B2B 이메일 콘텐츠를 작성하고, SMS 메시지를 보내고, 판매 알림을 구성하고, B2B 분석 대시보드를 제공합니다.
- **[!DNL Real-Time CDP B2B Edition] ([!DNL RT-CDP B2B])** — 소스 간 B2B 데이터에서 계정 프로필을 통합하고, 개인 대 계정 관계를 확인하고, 계정 수준 대상을 평가하고, B2B별 대상([!DNL Marketo Engage], [!DNL LinkedIn], CRM)을 구성하고, B2B 데이터 전반에 걸쳐 데이터 거버넌스를 적용합니다.

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 필수 | 샌드박스가 [!DNL AJO B2B Edition] 및 [!DNL RT-CDP B2B Edition] 권한을 활성화한 상태로 프로비저닝되었습니다. 구매 그룹 관리, 계정 여정 및 CRM 통합 설정에 대한 적절한 권한이 있는 B2B 마케터, 영업 작업 및 관리자를 위해 구성된 역할입니다. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | B2B 관련 클래스(XDM 비즈니스 계정, XDM 비즈니스 영업 기회, XDM 비즈니스 사용자(리드/연락처), XDM 비즈니스 캠페인 및 XDM 비즈니스 마케팅 목록)를 사용하여 구성된 B2B XDM 스키마. 계정 속성, 개인 속성 및 활동/참여 데이터에 대한 필드 그룹이 있어야 합니다. 각 스키마에 대해 생성되고 프로필이 활성화된 데이터 세트. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [B2B 스키마 클래스](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| 데이터 소스 및 수집 | 필수 | B2B 데이터 수집 파이프라인은 일반적으로 [!DNL Marketo Engage] 소스 커넥터 또는 [!DNL Salesforce]/[!DNL Dynamics] CRM 소스 커넥터를 통해 설정됩니다. 계정, 사용자, 기회, 캠페인 및 캠페인 멤버 데이터가 AEP 데이터 세트로 유입되어야 합니다. 참여 점수를 얻기 위해 행동 참여 데이터(웹 방문, 이메일 상호 작용, 콘텐츠 다운로드)도 수집해야 합니다. | [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [Marketo Engage 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| ID 및 프로필 구성 | 필수 | 개인-계정 관계를 확인하도록 구성된 B2B ID 해결입니다. B2B 식별자의 ID 네임스페이스([!DNL Marketo] 개인 ID, [!DNL Salesforce] 리드/연락처 ID, 계정 ID)가 있어야 합니다. B2B 프로필 통합을 위해 구성된 병합 정책. 계정 프로필은 소스 간 데이터에서 통합되어야 합니다. | [Identity Service 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [B2B Identity Resolution](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview) |
| 대상 정의 및 세분화 | 필수 | 계정 속성, 개인 속성 및 활동 데이터를 사용하여 작성된 계정 수준 대상 정의입니다. 계정 대상은 구매 그룹 여정을 입력하는 계정을 식별합니다. 일괄 처리 평가는 B2B 계정 여정에 대해 충분하지만, 스트리밍 평가는 실시간 계정 자격 트리거에 사용할 수 있습니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [계정 대상자](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 계산된 속성은 개인 수준 참여 이벤트(이메일 열기, 콘텐츠 다운로드, 웨비나 출석)를 구매 그룹 점수 및 계정 자격 논리에 도움이 되는 계정 수준 참여 지표로 집계할 수 있습니다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | 동의 관리는 B2B 이메일 및 SMS 통신에 중요합니다. 데이터 세트 만료 정책은 임시 참여 데이터의 라이프사이클을 관리하고 데이터 보존 요구 사항을 준수하는 데 도움이 됩니다. | [고급 데이터 수명 주기 관리](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | B2B 데이터에는 종종 민감한 회사 정보와 비즈니스 연락처의 개인 데이터가 포함됩니다. 데이터 거버넌스 정책은 특히 광고 플랫폼 또는 서드파티 시스템으로 활성화할 때 대상 간에 B2B 데이터를 호환하여 사용할 수 있도록 해줍니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| 모니터링 및 가시성 | 추천 | 모니터링을 통해 B2B 데이터 파이프라인(CRM/[!DNL Marketo] 동기화)이 정상이고, 계정 프로필이 업데이트되고, 계정 여정 실행이 실패 없이 진행 중인지 확인합니다. 소스 데이터 흐름 실패에 대한 경고는 데이터 통화를 유지 관리하는 데 중요합니다. | [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | [!DNL AJO B2B Edition] 내의 B2B 분석 대시보드는 구매 그룹 참여, 계정 여정 성능 및 파이프라인 지표를 제공합니다. [!DNL CJA B2B Edition] 계정 수준 작업 영역 분석, 구매 그룹 분석 및 영업 기회 상관 관계를 통해 분석을 확장합니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer B2B Edition] ([!DNL AJO B2B])

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 솔루션 관심 영역 구성 | 1단계: 솔루션 관심 및 구매 그룹 설정 | 제품 또는 서비스를 구매 그룹 자격 기준에 매핑하는 솔루션 관심사 정의 |
| 구매 그룹 관리 | 1단계: 솔루션 관심 및 구매 그룹 설정 | 역할 템플릿, 사용자 매핑 및 솔루션 관심 분야 정의를 사용하여 구매 그룹을 만들고 관리합니다. |
| 계정 Journey Orchestration | 3단계: 계정 여정 디자인 및 실행 | 조건, 작업 및 참여 기반 분기를 사용하여 여러 단계 계정 여정을 디자인하고 관리합니다. |
| 참여 점수 | 2단계: 잠재 고객 자격 및 참여 점수 책정 | 구매 그룹 내에서 개인 수준 참여에 점수를 매겨 구매 그룹 완성도 및 준비도를 측정합니다. |
| 계정 자격 조건 | 2단계: 잠재 고객 자격 및 참여 점수 책정 | AI 기반 계정 자격 에이전트를 사용하여 계정 준비 및 파이프라인 품질 평가 |
| B2B 이메일 작성 | 3단계: 계정 여정 디자인 및 실행 | 템플릿, 시각적 조각, 브랜드 테마 및 AI 지원 콘텐츠 생성을 사용하여 B2B 이메일 콘텐츠를 만듭니다 |
| SMS 채널 관리 | 3단계: 계정 여정 디자인 및 실행 | B2B 계정 여정 내에서 SMS 통신 구성 및 관리 |
| 영업 경고 구성 | 4단계: 판매 정렬 및 CRM 통합 | 영업 팀에 계정 참여 이정표 및 구매 신호를 알리도록 영업 경고 이메일 구성 |
| CRM 영업 인사이트 | 4단계: 판매 정렬 및 CRM 통합 | 그룹 상태, 참여 데이터 및 계정 여정 진행률을 구매하기 위해 CRM 내 가시성([!DNL Salesforce], [!DNL Dynamics])을 제공합니다. |
| B2B Analytics 대시보드 | 5단계: 보고 및 최적화 | 지능형 및 참여 대시보드를 통해 계정 여정 성과, 구매 그룹 참여 및 파이프라인 지표 모니터링 |

### [!DNL Real-Time CDP B2B Edition] ([!DNL RT-CDP B2B])

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 계정 프로필 통합 | 0단계: B2B 데이터 기반 | 특수 XDM B2B 스키마 클래스 및 필드 그룹을 사용하여 교차 소스 B2B 데이터를 통합 계정 프로필로 통합 |
| B2B Id 확인 | 0단계: B2B 데이터 기반 | 기본 식별자를 사용하여 개인 대 계정 관계를 해결하고, 여러 수준의 계정 계층 구조 및 다대다 개인 대 계정 매핑을 지원합니다. |
| 계정 대상자 평가 | 0단계: B2B 데이터 기반 | 계정 속성, 개인 속성 및 활동 데이터를 결합한 계정 레벨 세그먼트 멤버십을 평가합니다. |
| 계정 대상 구성 | 4단계: 판매 정렬 및 CRM 통합 | 계정 수준 필드 매핑을 사용하여 B2B별 대상([!DNL Marketo Engage], [!DNL LinkedIn], CRM 시스템)에 대한 연결 구성 |
| 계정 Audience Activation | 4단계: 판매 정렬 및 CRM 통합 | 계정 기반 타기팅 및 제외를 위해 계정 기반 대상을 대상에 게시 |
| [!DNL Marketo Engage] 통합 | 0단계: B2B 데이터 기반 | 기본 B2B 소스 및 대상 커넥터를 사용하여 [!DNL Marketo Engage]&#x200B;(으)로 양방향으로 데이터 수집 및 활성화 |
| B2B 데이터 거버넌스 | 0단계: B2B 데이터 기반 | B2B 계정 데이터 중앙 집중화 및 활성화 프로세스에서 데이터 사용 정책 및 동의 적용 |

## 필요 조건

구현을 시작하기 전에 다음을 완료하십시오.

- [ 대상 샌드박스에서 ] [!DNL AJO B2B Edition] 라이선스가 프로비저닝되고 활성화되었습니다.
- [ 대상 샌드박스에서 ] [!DNL RT-CDP B2B Edition] 라이선스가 프로비저닝되고 활성화되었습니다.
- [ 양방향 데이터 동기화를 위해 적절한 API 자격 증명을 사용하여 액세스할 수 있는 ] CRM 시스템([!DNL Salesforce] 또는 [!DNL Microsoft Dynamics 365])
- [ 소스 커넥터가 구성된 상태에서 ] [!DNL Marketo Engage] 인스턴스가 연결됨([!DNL Marketo]을(를) 마케팅 자동화 플랫폼으로 사용하는 경우)
- [ ]개의 B2B XDM 스키마 배포됨: 필수 필드 그룹이 있는 계정, 개인, 영업 기회, 캠페인 및 캠페인 멤버 클래스
- [ ] 계정 및 개인 데이터가 개인 대 계정 관계가 해결된 AEP으로 수집됨
- [ ] 전자 메일 채널 구성됨: 하위 도메인 위임됨, IP 풀 워밍됨, B2B 전자 메일 전송을 위해 만들어진 채널 표면
- [ ] SMS 공급자가 구성됨(계정 여정에 SMS 채널이 사용되는 경우): [!DNL Sinch], [!DNL Twilio] 또는 [!DNL Infobip] 자격 증명이 프로비저닝됨
- [ CRM Sales Insights 구성 요소에 온보딩된 ] 영업 팀([!DNL Salesforce] AppExchange 패키지 또는 [!DNL Dynamics] 솔루션 설치됨)
- [ 준비된 ]개의 콘텐츠 자산: B2B 이메일 템플릿, 브랜드 테마, 그리고 교육 및 판매 경고 이메일에 대한 시각적 조각
- [ ] 솔루션 관심 분류법 정의: 구매 그룹과 연결할 제품/서비스 목록
- [ ] 구매 그룹 역할 템플릿 디자인: 각 솔루션에 필요한 담당자 및 역할(예: 경제 구매자, 기술 평가자, 챔피언)

## 구현 옵션

이 섹션에서는 사용 가능한 구현 접근 방식에 대해 설명하며, 각 접근 방식은 다양한 조직의 요구 사항 및 성숙도 수준에 맞게 조정됩니다.

### 옵션 A: 선형 계정 여정이 포함된 단일 솔루션 관심

**최적의 용도:** 단일 제품군이나 솔루션 제공으로 시작하고, 접근 방식을 검증하고, 여러 솔루션 관심사로 확장하기 전에 반복하기를 원하는 구매 그룹 관리를 처음 사용하는 조직입니다.

**작동 방식:**

이 접근 방식은 하나의 구매 그룹 템플릿을 사용하는 단일 솔루션 관심(하나의 제품 또는 서비스)에 중점을 둡니다. 선형 계정 여정은 계정 식별, 구매 그룹 형성, 육성 참여, 참여 점수 임계값 및 판매 핸드오프와 같은 순차적 단계로 설계되었습니다. 여정은 복잡한 분기나 평행 트랙 없이 간단한 경로를 따릅니다.

CRM 또는 [!DNL Marketo Engage]에서 수집된 리드에 대해 그룹 역할을 구입할 수 있는 자격이 부여됩니다. 계정 여정은 미참여 역할에 육성 이메일을 보내고, 참여 점수를 모니터링하고, 구매 그룹이 정의된 완전성 및 참여 임계값에 도달하면 판매 경고를 트리거합니다. 이러한 접근 방식은 복잡성을 도입하기 전에 명확하고 측정 가능한 개념 증명을 제공합니다.

**주요 고려 사항:**

- 구현 및 유효성 검사가 단순하여 첫 번째 배포에 적합합니다.
- 한 번에 하나의 제품/서비스 구매 동작으로 제한
- 선형 여정 구조는 복잡한 다단계 구매 사이클을 수용하지 않을 수 있습니다

**장점:**

- 구성 복잡성을 최소화하면서 가장 빠른 가치 창출
- 단일 솔루션 관심사와 관련된 성공 지표 지우기
- 보다 쉽게 설명하고 조직의 승인을 얻으십시오.
- 간단한 보고 및 KPI 측정

**제한 사항:**

- 교차 판매 또는 다중 제품 시나리오를 다루지 않음
- 여러 솔루션에 관심이 있는 고객에게는 별도의 조정되지 않은 여정이 필요합니다
- 구매 그룹 관리 기능을 완전히 활용하지 못할 수 있음

**Experience League:**

- [AJO B2B edition 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [구매 그룹 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)

### 옵션 B: 분기 계정 여정이 있는 여러 솔루션 관심

**가장 적합한 대상:** 솔루션 관심사별로 개별 구매 그룹을 관리해야 하는 여러 제품 라인 또는 서비스 오퍼링을 사용하는 조직, 활성화된 솔루션 관심사와 각 구매 그룹의 자격 절차 진행 정도에 따라 분기되는 계정 여정이 있습니다.

**작동 방식:**

각각 고유한 구매 그룹 역할 템플릿을 가진 여러 솔루션 관심사가 정의됩니다. 계정 여정은 계정 식별에서 시작하며 행동 신호, 그래픽 데이터 또는 명시적 의도를 기반으로 각 계정에 적용되는 솔루션 관심사를 평가합니다. 이 여정은 각 활성 솔루션 관심사를 해결하기 위해 분기되며, 동일한 계정 내에서 서로 다른 구매 그룹에 대해 병렬 육성 트랙을 실행합니다.

참여 점수는 구매 그룹별로 독립적으로 운영되므로 한 구매 그룹이 판매 준비에 도달할 수 있고 다른 구매 그룹은 여전히 육성되고 있습니다. 솔루션 관심사별로 영업 경고를 구성하므로 특정 구매 그룹이 자격을 얻으면 해당 영업 팀이나 전문가에게 알립니다. CRM 인사이트는 계정에 대한 모든 활성 구매 그룹을 표면화하여 판매에 전체적인 보기를 제공합니다.

**주요 고려 사항:**

- 잘 정의된 솔루션 관심 분류법 및 고유한 구매 그룹 템플릿 필요
- 추가적인 솔루션 관심에 따라 여정 복잡성 증가
- 구매 그룹 간 조정(예: 여러 구매 그룹에서 역할을 담당하는 공유 연락처)을 계획해야 합니다

**장점:**

- 교차 판매 및 다중 제품 계정 전략 지원
- 구매 그룹당 독립적인 점수 책정을 통해 세부적인 파이프라인 가시성 제공
- 영업 팀은 솔루션 관심에 따라 타겟팅된 경고를 받습니다.
- [!DNL AJO B2B Edition] 구매 그룹 관리 기능 최대화

**제한 사항:**

- 구현 복잡성 증가 및 배포 시간 증가
- 더 많은 컨텐츠 자산 필요(솔루션 관심사별로 별도의 이메일 트랙)
- 보고는 계정당 여러 구매 그룹이 있는 경우 더 복잡합니다
- 여러 구매 그룹에 있는 메시징 연락처의 위험(빈도 관리 필요)

**Experience League:**

- [솔루션 관심 분야](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [계정 여정](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)

### 옵션 C: 자동화된 여정 진행을 통한 AI 지원 계정 자격

**최적의 용도:** AI 기반 계정 자격 에이전트를 활용하여 계정 준비 상태 평가를 자동화하고, 수동 자격 노력을 줄이고, AI가 생성한 준비 상태 점수를 기반으로 여정 경로를 동적으로 조정하려는 유의미한 과거 데이터를 보유한 성숙 B2B 조직

**작동 방식:**

이 접근 방식은 옵션 B의 다중 솔루션 이익 기반을 기반으로 구축되지만 여정 단계 간 전환을 자동화하기 위해 AI 기반의 계정 자격을 추가합니다. AI 자격 에이전트는 규칙 기반 참여 점수 임계값에만 의존하는 대신 구매 그룹 완성도, 참여 속도, 그래픽 적합성, 과거 전환 패턴 및 의도 데이터와 같은 광범위한 신호 세트를 사용하여 계정 준비 상태를 평가합니다.

계정 여정은 AI 검증 결과를 사용하여 준비도가 높은 계정은 영업 경고를 빠르게 추적하고 중간 계층의 계정은 강화된 육성 기능을 받으며 준비도가 낮은 계정은 장기 인식 트랙에 배치됩니다. AI 에이전트는 새로운 참여 데이터가 도착하면 지속적으로 재평가하여 수동 개입 없이 동적 여정 진행을 가능하게 합니다.

**주요 고려 사항:**

- 효과적인 검증 모델을 교육하기 위해 충분한 내역 데이터 필요
- 전체 배포 전에 실제 파이프라인 결과에 대해 AI 출력의 유효성을 검사해야 함
- 자격 정확도 및 파이프라인 상관 관계 분석을 위해 [!DNL CJA B2B Edition]과(와) 잘 결합됩니다.

**장점:**

- 수작업 검증 작업 감소 및 임의 임계값 기반 처리 제거
- 변화하는 계정 행동 및 참여 패턴에 맞게 동적으로 조정
- 단순한 참여 점수 이상으로 여러 신호를 통합하여 파이프라인 품질 향상
- 지속적인 재평가를 통해 계정이 잘못된 여정 단계에서 고착되지 않도록 합니다.

**제한 사항:**

- 의미 있는 AI 교육을 위해 과거 전환 데이터가 필요합니다.
- 영업 팀이 초기에 이해하고 신뢰하기 어려운 &quot;블랙박스&quot; 자격 결정
- 예기치 않게 계정이 인증되거나 전혀 인증되지 않을 때 문제를 해결하는 것이 더 복잡합니다.
- 모든 입력 신호에 대한 데이터 품질 및 완전성에 따라 다름

**Experience League:**

- [계정 자격 조건](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [AJO B2B의 AI 지원](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)

### 옵션 비교

| 기준 | 옵션 A: 관심 있는 단일 솔루션 | 옵션 B: 다양한 솔루션 관심 분야 | 옵션 C: AI 지원 자격 |
| --- | --- | --- | --- |
| 다음에 최적 | 첫 번째 배포, 단일 제품 라인 | 여러 제품 조직 | 이전 데이터가 있는 성숙한 조직 |
| 복잡성 | 낮음 | Medium 하이 | 높음 |
| 가치 창출 시간 | 2-4주 | 4-8주 | 6-12주 |
| 솔루션 관심 분야 | 1 | 복수 | 복수 |
| 여정 구조 | 선형 | 분기, 평행 트랙 | 역동적인 AI 기반 진행 |
| 채점 접근법 | 규칙 기반 임계값 | 구매 그룹당 규칙 기반 | AI 기반 검증 + 규칙 |
| 콘텐츠 요구 사항 | 최소(하나의 육성 트랙) | 높음(솔루션 관심당) | 높음 + 다이내믹 콘텐츠 선택 |
| 판매 정렬 | 단일 경고 워크플로우 | 솔루션별 관심 경고 | 우선 순위가 지정되고 AI 점수가 매겨진 경고 |
| 필요 | 기본 B2B 데이터 기반 | 잘 정의된 솔루션 분류 체계 | 과거 전환 데이터 + 분류 |

### 적절한 옵션 선택

가장 적합한 구현 접근 방식을 결정하려면 다음 질문을 시작하십시오.

1. **독립적인 구매 위원회가 있는 제품이나 서비스는 몇 개입니까?** 만약 답이 1이라면(혹은 조직이 먼저 개념을 증명하고자 한다면) 옵션 A부터 시작한다. 여러 개일 경우 질문 2로 이동합니다.

2. **성사/상실 거래, 구매 위원회 구성 및 참여 패턴에 대한 내역 데이터가 충분합니까?** 이 경우 조직에서 수동 자격을 최소화하려는 경우 옵션 C는 가장 자동화된 접근 방식을 제공합니다. 그렇지 않은 경우 옵션 B는 규칙 기반 점수로 다중 솔루션 관심 지원을 제공합니다.

3. **조직의 변경 관리 용량은 얼마입니까?** 옵션 B와 C는 보다 조직적인 구성(컨텐츠 제작, 영업 지원, 다양한 분야의 업무에 대한 조정)이 필요합니다. 용량이 제한되어 있으면 옵션 A로 시작하여 를 확장합니다.

일반적인 진행 경로는 하나의 솔루션 관심사로 개념을 입증하기 위해 옵션 A로 시작하고, 신뢰도가 증가함에 따라 솔루션 관심사를 추가하여 옵션 B로 확장한 다음 모델을 효과적으로 교육할 수 있는 충분한 내역 데이터를 사용할 수 있게 되면 옵션 C의 AI 자격에서 계층화합니다.

## 구현 단계

다음 단계에서는 이 사용 사례 패턴에 대한 단계별 구현 프로세스를 설명합니다.

### 0단계: B2B 데이터 기반

**응용 프로그램 함수:** [!DNL RT-CDP B2B]: 계정 프로필 통합, B2B Id 확인, [!DNL Marketo Engage] 통합, B2B 데이터 거버넌스, 계정 대상 평가

이 단계는 [!DNL RT-CDP B2B Edition]에서 B2B 데이터 인프라를 설정합니다. CRM, 마케팅 자동화 및 기타 소스의 계정 데이터를 단일 계정 프로필로 통합하고, 개인-계정 관계를 해결하고, B2B 데이터 거버넌스를 구성하고, [!DNL AJO B2B Edition] 구매 그룹 관리에 사용되는 계정 수준 대상을 만듭니다.

#### 의사 결정: B2B 데이터 소스 전략

계정, 사용자 및 참여 데이터의 기본 소스 역할을 하는 시스템은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기본 소스로 [!DNL Marketo Engage] | [!DNL Marketo]은(는) 풍부한 참여 기록을 가진 조직의 마케팅 자동화 플랫폼입니다. | 기본 양방향 커넥터를 사용하면 설정이 단순화되고, 참여 데이터가 자동으로 전송되며, [!DNL Marketo]에서 상속된 개인-계정 관계가 상속됩니다. |
| 기본 소스로 CRM([!DNL Salesforce]/[!DNL Dynamics]) | CRM은 계정 및 연락처의 기록 시스템입니다. [!DNL Marketo]은(는) 사용되지 않습니다. | CRM 소스 커넥터 구성 필요, 참여 데이터에 보충 소스 필요, CRM 계정 연락처 연결의 개인 대 계정 관계 |
| 하이브리드: 계정용 CRM + 참여용 [!DNL Marketo] | [!DNL Marketo]이(가) 동작 참여를 캡처하는 동안 CRM에서 계정/연락처 마스터 데이터를 소유합니다. | 두 가지를 모두 사용하는 조직의 가장 일반적인 패턴입니다. [!DNL Marketo]명을 CRM 연락처에 연결하려면 신중한 ID 확인이 필요합니다. |

#### 의사 결정: 고객 대상 전략

여정 입력에 대한 계정 대상은 어떻게 정의해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 그래픽 기반 계정 대상자 | 업계, 회사 규모, 수익 계층 또는 지역을 기반으로 하는 타겟 고객 | ABM 대상 목록에 적합하며, 참여 데이터가 필요하지 않습니다. 광범위할 수 있습니다. |
| 참여 기반 계정 대상자 | 사람들이 행동 의도 신호를 보인 타겟 계정 | 참여 데이터 흐름 필요, 보다 정확한 타겟팅, 잠재적 관심 항목이 있는 계정 누락 |
| 결합된 첫 화면 + 참여 | 이상적인 고객 프로필과 일치하고 참여를 보여 주는 계정을 타깃팅합니다. | 가장 정확함, 두 데이터 유형 모두 필요, 적격 파이프라인 생성에 권장 |

**UI 탐색:** 플랫폼 > 소스 > 카탈로그 > 소스 선택([!DNL Marketo Engage], [!DNL Salesforce] 등) > 데이터 흐름 설정

**키 구성 세부 정보:**

- 필수 필드 그룹을 사용하여 각 B2B 엔티티(계정, 개인, 영업 기회, 캠페인, 캠페인 멤버)에 대한 B2B XDM 스키마 구성
- 적절한 일정(일반적으로 B2B 데이터의 경우 1~4시간 간격)으로 CRM 및/또는 [!DNL Marketo Engage]에 대한 소스 커넥터를 설정하십시오.
- B2B 식별자에 대한 ID 네임스페이스 구성([!DNL Marketo] 개인 ID, SFDC 리드 ID, SFDC 연락처 ID, 계정 ID)
- B2B ID 확인을 활성화하여 개인을 계정에 연결
- [!DNL RT-CDP]의 계정 대상 기능을 사용하여 계정 수준 대상 만들기

**Experience League 설명서:**

- [RT-CDP B2B edition 개요](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Real-Time CDP의 B2B 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Marketo Engage 소스 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [계정 대상자](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [B2B id 확인](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)

### 1단계: 솔루션 관심 및 구매 그룹 설정

**응용 프로그램 함수:** [!DNL AJO B2B]: 솔루션 관심사 구성, 구매 그룹 관리

이 단계에서는 구매 그룹 관리 모델의 핵심을 구성하는 솔루션 관심사(제품/서비스) 및 구매 그룹 템플릿을 정의합니다. 솔루션 관심사를 생성하고, 성향 요구 사항을 가진 역할 템플릿을 정의하고, 잠재 고객이 그룹 역할을 구매할 수 있는 자격을 부여하는 방법을 구성합니다.

#### 의사 결정: 솔루션 관심 영역 세부기간

해결책 관심사는 어느 수준에서 정의되어야 하는가?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 제품 수준 솔루션 관심 분야 | 각 개별 제품에는 자체 구매 그룹이 있습니다 | 가장 세분화된 단위, 제품별 구매 그룹 템플릿을 활성화합니다. 계정당 많은 구매 그룹을 생성할 수 있습니다. |
| 솔루션 범주 수준의 관심 분야 | 관련 제품을 솔루션 카테고리로 그룹화(예: 개별 제품 대신 &quot;Marketing Cloud&quot;) | 관리가 간편하고, 구매 그룹이 적으며, 역할이 더 일반적일 수 있습니다. 초기 배포에 권장됨 |
| 사용 사례 수준의 관심 분야 | 제품이 아닌 비즈니스 결과에 대한 관심사 정의(예: &quot;디지털 전환&quot;) | 컨설팅 판매에 맞춰 조정. 구매 그룹 역할은 여러 제품에 걸쳐 있을 수 있으며 CRM 파이프라인 단계에 매핑하기가 더 어렵습니다. |

#### 의사 결정: 그룹 역할 템플릿 디자인 구매

각 구매 그룹 내에서 역할을 어떻게 정의해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 표준 역할 템플릿 | 모든 솔루션 관심사에 공통된 역할 집합 사용(예: 경제적 구매자, 기술 평가자, 챔피언, 최종 사용자) | 일관된 점수 및 검증, 관리 용이성, 솔루션별 역할 포착 불가 |
| 솔루션별 역할 템플릿 | 해당 제품에 대한 실제 구매 위원회를 기반으로 솔루션 관심사별로 고유한 역할 정의 | 보다 정확한 검증, 각 구매 프로세스에 대한 심층적인 지식 필요, 높은 유지 관리 |
| 계층화된 역할 템플릿 | 필수 역할(자격의 경우 필수) 및 선택적 역할 정의(완결성 향상(필수 아님)) | 정밀도와 유연성의 균형 유지, 엄격한 자격 기준이 파이프라인을 차단하는 방지 |

**UI 탐색:** [!DNL AJO B2B Edition] > 구매 그룹 > 솔루션 관심 항목 > 솔루션 관심 항목 만들기

**UI 탐색:** [!DNL AJO B2B Edition] > 구매 그룹 > 역할 템플릿 > 역할 템플릿 만들기

**키 구성 세부 정보:**

- 이름, 설명 및 비즈니스 결과를 사용하여 각 솔루션의 관심 분야를 정의합니다.
- 각 구매 그룹에 필요한 담당자를 지정하는 역할 템플릿을 만듭니다(예: &quot;의사 결정자&quot;, &quot;영향력 행사자&quot;, &quot;실무자&quot;, &quot;경영 스폰서&quot;).
- 리드-투-롤 자격 기준 구성: 시스템에서 리드가 매핑되는 담당자를 결정하는 방법(직함, 부서, 연공 순위 또는 사용자 지정 속성에 따라)
- 완전성 임계값 설정: 구매 그룹이 &quot;완료&quot;로 간주되기 위해 채워야 하는 역할 비율을 정의합니다.
- 잠재적인 관심을 나타내는 계정 대상자 또는 계정 속성에 솔루션 관심 분야 연결

**옵션이 나뉘는 위치:**

**옵션 A의 경우(단일 솔루션 관심):**
하나의 솔루션 관심사와 하나의 역할 템플릿을 만듭니다. 조직의 주요 제품 또는 서비스에 대한 명확하고 이해하기 쉬운 구매 움직임에 초점을 맞추십시오.

옵션 B의 **다중 솔루션 관심 분야:**
각각 고유한 역할 템플릿을 사용하여 여러 솔루션 관심사를 만듭니다. 다운스트림 파이프라인 추적을 위해 각 솔루션 관심사를 적절한 CRM 제품/기회 유형에 매핑합니다.

**옵션 C의 경우(AI 지원 자격):**
옵션 B와 같이 솔루션 관심 분야 및 역할 템플릿을 구성하되, 성공적인 구매 그룹 구성 및 거래 결과에 대한 내역 데이터로 AI 자격 에이전트를 추가로 구성하여 자격 모델을 교육합니다.

**Experience League 설명서:**

- [구매 그룹 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [솔루션 관심 분야](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [역할 템플릿](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [구매 그룹 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)

### 2단계: 잠재 고객 자격 및 참여 점수 책정

**응용 프로그램 함수:** [!DNL AJO B2B]: 참여 점수, 계정 자격

이 단계에서는 구매 그룹 내에서 개인 수준 참여를 측정하는 참여 점수 모델을 설정하고 이를 구매 그룹 및 계정 수준 준비 점수로 롤업합니다. 채점 규칙을 구성하고, 자격 조건을 위한 참여 임계값을 정의하고, 선택적으로 AI 기반 계정 자격을 활성화합니다.

#### 의사 결정: 참여 점수 모델

개인 및 구매 그룹 수준에서 참여를 어떻게 평가해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 활동 기반 점수 책정 | 특정 작업에 포인트 값 할당 (이메일 열기 = 5포인트, 콘텐츠 다운로드 = 15포인트, 데모 요청 = 50포인트) | 투명하고 손쉽게 조정할 수 있으며, 콘텐츠 및 채널이 변경될 때 지속적인 유지 관리가 필요합니다. [!DNL Marketo]명의 사용자에게 가장 친숙함 |
| 최신성 가중 채점 | 최근 활동 중요도가 이전 활동보다 높음(점수감소 모델) | 현재 의도를 더 잘 반영하고, 부실한 높은 점수가 자격을 부풀리지 않도록 하며, 구성하는 것이 더 복잡합니다. |
| AI 기반 점수 책정 | [!DNL AJO B2B] AI 자격 에이전트를 사용하여 패턴 인식을 기반으로 준비 점수를 생성합니다. | 가장 정교하고, 자동으로 조정되며, 내역 데이터가 필요하며, 처음에 영업 팀에 불투명할 수 있음 |

#### 의사 결정: 자격 임계값 접근 방식

구매 그룹은 언제 판매 핸드오프에 대한 준비가 된 것으로 간주되어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 점수 임계값만 | 집계 참여 점수가 정의된 값을 초과하는 경우 구매 그룹이 적격 처리됨 | 구현이 간단합니다. 점수 임계값은 시간에 따라 조정해야 할 수 있으며 역할 구성을 고려하지 않습니다. |
| 완성도 + 점수 임계값 | 최소 역할 범위 및 점수 임계값이 모두 충족되면 구매 그룹이 자격을 얻습니다. | 보다 강력한 검증, 높은 점수를 얻었지만 주요 역할이 누락된 구매 그룹의 전달 방지 |
| AI 결정 준비 | AI 자격 에이전트는 점수 및 완성도를 넘어 여러 신호를 사용하여 준비 상태를 결정합니다 | 가장 정교함, 구매 속도, 경쟁 신호 및 과거 패턴 고려, 옵션 C만 해당 |

**UI 탐색:** [!DNL AJO B2B Edition] > 구매 그룹 > 참여 점수 > 점수 규칙 구성

**키 구성 세부 정보:**

- 참여 점수 규칙 정의: 행동 이벤트(이메일 열기, 클릭 수, 웹 페이지 방문, 콘텐츠 다운로드, 양식 제출, 웨비나 출석, 데모 요청)에 점수 값을 할당합니다.
- 시간에 민감한 점수를 사용하는 경우 점수 감소 또는 최신성 가중치 구성
- 구매 그룹 수준 점수 집계 설정: 개인 점수가 구매 그룹 점수로 결합되는 방법(합계, 가중 평균 또는 역할당 최소 임계값)
- 자격 임계값 정의: 다음 구매 단계로 전환하는 점수 및 완성도 레벨
- AI 자격 에이전트 구성(옵션 C): 이전 거래 데이터를 교육하고 에이전트가 고려해야 하는 신호를 정의하며 신뢰 임계값을 설정합니다.

**Experience League 설명서:**

- [참여 점수 책정](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [구매 그룹 단계](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [계정 자격 조건](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)

### 3단계: 계정 여정 설계 및 실행

**응용 프로그램 함수:** [!DNL AJO B2B]: 계정 Journey Orchestration, B2B 전자 메일 작성, SMS 채널 관리

이 단계에서는 구매 그룹 구성원에 대한 참여를 조정하는 계정 여정을 디자인하고 배포합니다. 시작 조건, 작업 노드(이메일, SMS), 조건 분기(구매 그룹 단계, 참여 점수, 역할 범위 기반), 대기 단계 및 종료 기준을 사용하여 계정 여정을 만듭니다.

#### 결정: 여정 항목 트리거

어떤 이벤트 또는 조건으로 인해 계정이 여정을 입력했습니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 계정 대상자 자격 조건 | 대상 계정 대상자에 참여하면 계정이 입력됨 | 배치 지향, ABM 목록 기반 항목에 적합, 대상자를 사전 정의해야 함 |
| 구매 그룹 생성 이벤트 | 계정에 대해 구매 그룹이 처음 생성될 때 계정이 입력됩니다. | 이벤트 기반, 구매 그룹 역할로의 잠재 고객 자격에 의해 트리거됨, 보다 실시간 |
| 계정 속성 변경 | 특정 속성이 변경될 때(예: 의도 점수, 계정 계층) 계정이 들어갑니다. | 트리거링 속성을 실시간 또는 실시간에 가깝게 업데이트해야 함 |

#### 의사 결정: B2B 보육을 위한 채널 혼합

구매 그룹 구성원의 참여를 유도하기 위해 계정 여정은 어떤 채널을 사용해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이메일만 | 대부분의 B2B 상호 작용은 이메일을 통해 발생하며 SMS 옵트인 인프라가 존재하지 않습니다 | 가장 간단한 구성, 가장 일반적인 B2B 패턴, 모바일 최초 연락처가 누락될 수 있음 |
| 이메일 + SMS | 조직에서 비즈니스 담당자의 SMS 옵트인을 가지고 있습니다. 긴급도가 높은 알림이 보장됨 | SMS는 시간에 민감한 알림(이벤트 미리 알림, 모임 확인)에 유효합니다. SMS 공급자 구성이 필요합니다. |
| 이메일 + SMS + 판매 경고 | 전체 범위: 이메일/SMS와 영업팀 알림을 통한 마케팅 강화 | 가장 포괄적, 영업 팀이 경고 워크플로를 채택해야 함, 마케팅 및 영업 접점 조정 |

#### 의사 결정: 여정 분기 전략

여정 지점은 거래처 및 구매 그룹 상태를 기준으로 어떻게 해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 스테이지 기반 분기 | 구매 그룹 단계를 기반으로 한 지점(예: 인지도, 고려 사항, 결정) | 기존 funnel 단계에 맞게 조정, 단계에 매핑된 콘텐츠, 진행 경로 지우기 |
| 역할 기반 분기 | 분기별로 서로 다른 구매 그룹 역할에 다른 콘텐츠 전송(평가자에게는 기술 콘텐츠, 경제 구매자에게는 ROI 콘텐츠) | 더 개인화되고 역할별 콘텐츠 자산이 필요하며 콘텐츠 제작 노력이 향상됩니다. |
| 참여 기반 분기 | 참여 점수 임계값을 기반으로 한 분기(낮은 참여 = 다시 참여, 높은 참여 = 가속화) | 동적 및 반응형, 실제 동작에 적응, 복잡한 분기 트리를 만들 수 있음 |

**UI 탐색:** [!DNL AJO B2B Edition] > 계정 여정 > 여정 만들기

**키 구성 세부 정보:**

- 선택한 항목 조건으로 계정 여정 캔버스 만들기
- 계정 여정 노드 추가: 이메일 작업, SMS 작업, 대기 단계, 조건 분할 및 경로 분기
- 브랜드 테마, 시각적 조각 및 AI 지원 콘텐츠 생성과 함께 B2B 이메일 Designer을 사용하여 B2B 이메일 콘텐츠를 작성합니다
- 계정 속성, 개인 속성 및 구매 그룹 데이터를 참조하는 개인화 토큰 구성
- 터치포인트 간 대기 기간 설정(B2B 여정은 일반적으로 더 긴 대기 시간을 사용합니다(이메일 간 3~7일).
- 종료 기준 정의: 계정이 여정을 벗어나는 조건(구매 그룹이 자격 임계값에 도달함, CRM에서 생성된 영업 기회, 계정 옵트아웃)
- SMS 채널을 사용하는 경우 SMS 작업 구성(SMS 공급자 구성 필요 및 옵트인 문의)
- 게시하기 전에 테스트 계정으로 여정 테스트

**옵션이 나뉘는 위치:**

**옵션 A의 경우(단일 솔루션 관심):**
순차적 단계를 사용하는 선형 여정을 디자인합니다. 입력은 단일 계정 대상자 또는 구매 그룹 생성 이벤트를 기반으로 합니다. 컨텐츠의 긴급도와 깊이가 증가하는 하나의 이메일 육성 트랙입니다.

옵션 B의 **다중 솔루션 관심 분야:**
솔루션 관심사별로 병렬 분기를 사용하는 여정을 디자인합니다. 조건 노드를 사용하여 구매 그룹이 존재하는 적절한 육성 트랙으로 계정을 라우팅합니다. 각 분기에는 자체 콘텐츠 및 점수 임계값이 있습니다.

**옵션 C의 경우(AI 지원 자격):**
조건 노드가 규칙 기반 임계값이 아닌(또는 이에 추가하여) AI 자격 점수를 평가하는 여정을 디자인합니다. AI가 계정을 가속화할지, 유지관리할지 또는 우선 순위 지정을 취소할지 여부를 결정하는 동적 경로 선택을 포함합니다.

**Experience League 설명서:**

- [계정 여정 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [계정 여정 노드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [B2B 이메일 작성](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [AJO B2B의 SMS 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [이메일 작성을 위한 AI Assistant](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### 4단계: 판매 정렬 및 CRM 통합

**응용 프로그램 함수:** [!DNL AJO B2B]: 영업 경고 구성, CRM 영업 인사이트; [!DNL RT-CDP B2B]: 계정 대상 구성, 계정 Audience Activation

이 단계에서는 판매 경고 이메일을 구성하고, CRM 내 가시성을 위해 CRM Sales Insights를 배포하고, 원할 경우 B2B 대상([!DNL LinkedIn], [!DNL Marketo], CRM 시스템)으로 계정 대상을 활성화하여 마케팅과 판매 사이의 다리를 만듭니다.

#### 의사 결정: 영업 경고 트리거 전략

계정의 구매 그룹 상태에 대한 판매 통지는 언제 받아야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이정표 기반 경고 | 구매 그룹이 특정 중요 시점에 도달하면 판매에 알림(적격, 완료, 높은 참여) | 명확한 개별 알림, 경고 피로 방지, 점진적인 참여 트렌드 누락 |
| 임계값 기반 경고 | 참여 점수가 정의된 임계값을 초과할 때 판매 알림 | 지속적인 모니터링: 점수가 임계값 근처에서 변동할 때 여러 경고를 트리거할 수 있음 |
| 단계 전환 경고 | 구매 그룹이 새 단계로 전환될 때 판매에 알림(예: 고려에서 결정으로) | 파이프라인 단계에 맞게 조정, 영업 활동에 대한 가장 명확한 신호, 잘 정의된 단계 정의 필요 |

#### 의사 결정: CRM 통합 깊이

구매 그룹 데이터가 CRM에서 얼마나 깊이 표시되어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 영업 경고만(CRM 내 구성 요소 없음) | 조직에서 [!DNL Salesforce] 또는 [!DNL Dynamics]을(를) 사용하지 않거나 CRM 통합을 사용할 수 없습니다. | 가장 낮은 통합 노력, 영업팀이 이메일 알림을 수신하지만 CRM 대시보드는 받지 못함, 제한된 가시성 |
| CRM 판매 통찰력 대시보드 | 조직에서 [!DNL Salesforce] 또는 [!DNL Dynamics]을(를) 사용하고 CRM 내에 구매 그룹 상태를 표시하려고 합니다. | CRM Sales Insights 패키지 설치 필요, 풍부한 계정 수준 인텔리전스 제공, 대부분의 구현에 권장 |
| 전체 양방향 CRM 동기화 | 구매 그룹 단계 및 점수가 CRM 개체에 다시 기록되어 CRM 워크플로 및 보고에 영향을 미침 | 최고의 통합 복잡성, CRM 기반 파이프라인 보고 활성화, 사용자 지정 CRM 구성 필요 |

**UI 탐색:** [!DNL AJO B2B Edition] > 관리 > 판매 경고 구성

**UI 탐색:** [!DNL AJO B2B Edition] > 관리 > CRM Sales Insights > 구성

**키 구성 세부 정보:**

- 영업 경고 이메일 템플릿 구성: 구매 그룹 상태, 참여 담당자, 참여 점수 및 권장되는 다음 작업 포함
- 경고 라우팅 규칙 정의: 영업 담당자 또는 팀이 계정 소유권, 영역 또는 솔루션 관심사에 따라 경고를 수신하는지 여부
- [!DNL Salesforce] 또는 [!DNL Dynamics 365]에 대한 CRM Sales Insights 설치 및 구성
- 구매 그룹 데이터를 CRM 개체에 매핑하여 판매자가 해당 CRM 워크플로 내에서 구매 그룹 구성, 참여 및 여정 진행률을 확인할 수 있도록 합니다.
- 필요한 경우 계정 대상을 [!DNL LinkedIn]&#x200B;(ABM 광고의 경우), [!DNL Marketo Engage]&#x200B;(리드 수준 후속 조치의 경우) 또는 기타 B2B 대상으로 활성화하도록 계정 대상 연결을 구성하십시오

**Experience League 설명서:**

- [영업 경고 이메일](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [CRM 영업 인사이트](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)
- [대상 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [LinkedIn 일치하는 대상 대상 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)

### 5단계: 보고 및 최적화

**응용 프로그램 함수:** [!DNL AJO B2B]: B2B Analytics 대시보드

이 단계에서는 보고 및 분석 프레임워크를 설정하여 구매 그룹 성과, 계정 여정 효율성 및 파이프라인 영향을 측정합니다. [!DNL AJO B2B Edition] 기본 제공 analytics 대시보드를 제공합니다. [!DNL CJA B2B Edition]&#x200B;(라이선스가 있는 경우)은(는) 더 자세한 크로스 채널 계정 수준 인사이트를 통해 분석을 확장합니다.

#### 의사 결정: 보고 접근 방식

지속적인 성능 모니터링을 위해 어떤 분석 도구를 구성해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| [!DNL AJO B2B] 대시보드만 | [!DNL AJO B2B Edition]의 기본 제공 대시보드로 구매 그룹 및 여정 지표로 충분합니다. | 가장 빠른 구성, 핵심 B2B 지표, 제한된 맞춤형 분석 기능 포함 |
| [!DNL AJO B2B]개 대시보드 + [!DNL CJA B2B Edition] | 조직에서는 심층적인 크로스 채널 분석, 구매 그룹 분석, 영업 기회 상관 관계 및 사용자 정의 속성이 필요합니다. | [!DNL CJA B2B Edition] 라이선스가 필요합니다. 가장 포괄적이며 계정 수준의 자유 형식 분석을 지원합니다. |
| [!DNL AJO B2B]개 대시보드 + CRM 보고 | 조직은 구매 그룹 지표와 함께 CRM에서 파이프라인 보고를 중앙 집중화하는 것을 선호합니다 | CRM 대시보드 개발 필요, 마케팅 및 판매 지표를 한 곳에 결합, CRM 보고 기능으로 제한 |

**UI 탐색:** [!DNL AJO B2B Edition] > 대시보드 > 참여 개요/지능형 대시보드

**키 구성 세부 정보:**

- [!DNL AJO B2B] 참여 대시보드에 액세스하여 구매 그룹 참여 점수, 완료율 및 단계 분포를 모니터링합니다.
- 계정 준비 및 파이프라인 품질에 대한 AI 기반 인사이트를 위한 지능형 대시보드에 액세스
- [!DNL CJA B2B Edition]을(를) 사용하는 경우: [!DNL AJO B2B] 데이터 세트를 포함하는 계정 기반 CJA 연결을 구성하고, 구매 그룹 및 계정 컨테이너를 사용하여 B2B 데이터 보기를 설정하고, 구매 그룹 진행, 기회 상관 관계 및 속성을 위한 작업 영역 분석을 빌드합니다.
- 보고 케이던스 정의: 주간 구매 그룹 성과 검토, 월간 파이프라인 영향 분석, 분기별 프로그램 최적화
- 중요한 이벤트(캠페인 시작, 콘텐츠 새로 고침, 점수부여 모델 변경)에 대한 주석을 만들어 성능 트렌드와 상관 관계를 맺습니다.

**Experience League 설명서:**

- [B2B 분석 대시보드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [참여 대시보드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [지능형 대시보드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [CJA B2B edition 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

## 구현 시 고려 사항

다음 섹션에서는 구현 중에 기억해야 할 보호 기능, 일반적인 위험, 모범 사례 및 상충 결정을 다룹니다.

### 보호 기능 및 제한 사항

- 최대 동시 여정 수 및 계정당 최대 여정 수를 포함한 [!DNL AJO B2B Edition] 계정 여정 제한은 [!DNL AJO B2B Edition] 제품 가드레일을 따릅니다. — [AJO B2B 가드레일](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [!DNL RT-CDP B2B Edition]은(는) 최대 50개의 B2B 스키마 클래스를 지원하며 표준 프로필 및 세분화 가드레일 — [실시간 고객 프로필 가드레일](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 계정 대상 평가는 일괄 처리 일정에서 작동합니다. 실시간 계정 대상 업데이트는 모든 세그먼트 유형에 대해 지원되지 않습니다. [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- B2B 소스 커넥터 수집에는 최소 예약 간격(일반적으로 [!DNL Marketo]의 경우 15분, CRM 소스의 경우 변경)이 있습니다. — [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- 이메일 채널 표면은 샌드박스당 채널 유형당 10개로 제한됩니다. [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

### 일반적인 함정

- **구매 그룹당 너무 많은 역할을 정의하는 중:** 역할을 너무 많이 지정하면(예: 8~10개의 고유한 가상 사용자 필요) 구매 그룹이 완전성 임계값에 도달하는 것이 거의 불가능합니다. 3-5개의 필수 역할로 시작하여 모델이 성숙함에 따라 확장하십시오.
- **참여 점수 임계값을 너무 높거나 낮게 설정:** 임계값이 너무 높으면 구매 그룹이 공급되지 않고 파이프라인이 부족합니다. 너무 적으면 부적격 계좌가 매출을 급증시킨다. 내역 데이터 분석으로 시작하고(가능한 경우) 영업 피드백을 기반으로 반복합니다.
- **계정 간 해결 방법 품질 무시:** 계정에 올바르게 연결되어 있지 않은 사람이 있는 경우 적합한 사람이 참여하더라도 구매 그룹에 누락된 구성원이 생깁니다. 구매 그룹 여정을 시작하기 전에 ID 해결 품질에 투자하십시오.
- **여러 구매 그룹의 메시징 연락처:** 단일 연락처가 여러 구매 그룹의 역할을 가질 수 있습니다(예: CRM 및 데이터 플랫폼 구매의 기술 평가자인 CTO). 빈도 관리 없이 이 사람은 모든 활성 여정에서 이메일을 수신합니다. 여정 간 빈도 규칙을 구현합니다.
- **판매 활성화를 무시하는 중:** 영업 팀은 구매 그룹 데이터, 참여 점수 및 영업 경고를 해석하는 방법을 이해해야 합니다. 교육과 채택이 없으면 데이터 품질에 관계없이 Marketing-to-Sales 전달에 실패합니다.
- **계정 여정을 사용자 여정과 같이 처리:** 계정 여정은 계정 수준에서 작동하여 계정의 구매 그룹 내의 사용자에게 이메일을 보냅니다. 여정 디자인은 계정 여정 실행당 여러 사람이 메시지를 수신한다고 간주해야 하는데, 이는 사용자 수준 [!DNL AJO] 노드와는 근본적으로 다릅니다.

### 우수 사례

- **하나의 솔루션 관심 분야로 시작 및 확장** — 여러 솔루션 관심 분야로 확장하기 전에 하나의 구매 모션에 대해 모델이 작동하는지 확인하십시오. 이를 통해 팀은 복잡성을 추가하기 전에 역할 템플릿, 채점 모델 및 콘텐츠를 구체화할 수 있습니다.
- **구매 그룹 역할을 CRM 영업 프로세스와 연계합니다** - 구매 그룹 역할을 영업 팀이 이미 인식하는 담당자에게 매핑합니다. 동일한 언어 사용 (경제적 구매자, 챔피언 등) 그래서 핸드오프는 직관적입니다.
- **판매 관련 피드백 루프 구현** - 마케팅 자격을 갖춘 계정의 품질에 대한 판매 피드백을 정기적으로 수집합니다. 이 피드백을 사용하여 참여 점수 임계값 및 역할 자격 기준을 조정합니다.
- **단순한 단계가 아닌 역할을 위한 콘텐츠 디자인** — 구매 그룹 역할마다 다른 콘텐츠가 필요합니다. 경영진은 ROI와 전략적 영향을 원하며, 기술 평가자는 아키텍처와 통합 세부 정보를 원하며, 최종 사용자는 사용하기 쉬운 데모를 원합니다. 콘텐츠 에셋을 역할에 매핑하여 보다 효과적으로 육성합니다.
- **CRM 영업 인사이트를 조기에 설정** — 전체 여정이 라이브로 생성되어 CRM 가시성이 배포될 때까지 기다리지 마십시오. 영업 팀은 역할 정확성 및 계정 타깃팅에 대한 피드백을 제공하기 위해 구매 그룹 데이터가 조기에 형성되는 것을 확인해야 합니다.
- **대기 단계를 전략적으로 사용** — B2B 구매 주기가 깁니다. 계정 여정 대기 단계는 소비자 스타일의 긴급성(1~3일)보다는 이러한 현실(터치 간 5~14일 간격)을 반영해야 합니다.
- **참여 속도 모니터링** — 2주 동안 20점에서 80점까지 올라간 구매 그룹은 6개월 동안 80점에 도달한 구매 그룹보다 더 강한 의도를 나타냅니다. 속도를 고려하도록 점수 및 자격을 구성합니다.

### 절충안 결정

조직의 특정 요구 사항에 따라 다음 절충안을 평가해야 합니다.

#### 구매 그룹 완성도와 파이프라인 볼륨 비교

구매 그룹에 자격을 부여하기 전에 모든 역할을 채워야 하는 것은 파이프라인 품질을 최대화하지만 자격을 갖춘 계정의 수를 심각하게 제한할 수 있습니다(특히 조직의 데이터베이스에 적용 범위가 제한된 신규 제품 또는 시장의 경우).

- **높은 완성도 임계값 우대:** 파이프라인 품질, 판매는 완전히 구성된 구매 그룹을 받습니다. 계정당 더 높은 승률
- **완결성 임계값 우대 낮음:** 파이프라인 볼륨, 더 많은 계정이 판매에 도달함, 더 광범위한 범위, 더 많은 볼륨이지만 더 낮은 품질
- **권장 사항:** 보통 임계값(역할 범위 60~70%)으로 시작하고 실제 승률 데이터를 기반으로 조정합니다. 데이터 적용 범위가 좋은 기존 시장의 경우 80% 이상으로 증가합니다. 신규 시장의 경우 초기에 50~60%를 수락하고 구매 그룹 완전성 캠페인을 사용하여 차이를 메웁니다.

#### 채점 세부기간 대 운영 간소화

세분화된 점수 모델(수십 개의 활동 유형, 최신성 가중치 및 역할별 점수 책정)은 더 정확한 자격 신호를 제공하지만 유지 관리, 설명 및 문제 해결이 더 어렵습니다.

- **세부 기간 우대:** 자격의 정밀도, 계정 간의 미묘한 차이, 복잡한 구매 프로세스와의 더 나은 정렬
- **낮은 세분화 우선 순위:** 운영 간소화, 유지 관리 및 판매 설명 용이, 신속한 구현, 적은 에지 케이스
- **권장 사항:** 간단한 점수 모델(10~15개의 활동 유형, 균일한 포인트 값)로 시작하고 간단한 모델이 계정 품질을 차별화하지 못하는 경우에만 복잡성을 추가하십시오. 영업 정렬을 위해 채점 모델을 철저히 문서화합니다.

#### 단일 여정과 여러 전문 여정 비교

하나의 캔버스에서 모든 단계와 솔루션 관심사를 처리하는 포괄적인 단일 계정 여정은 통합된 제어를 제공하지만 까다로워질 수 있습니다. 여러 전문 여정(스테이지나 솔루션 관심사당 하나)는 개별적으로 더 간단하지만 조정하기가 더 어렵습니다.

- **단일 여정의 장점:** 전체적인 보기, 일관성 있는 타이밍 및 메시징을 보다 쉽게 확인, 모니터링이 더 간단함, 모든 논리를 한 곳에서 확인
- **여러 여정의 장점:** 모듈성, 다른 팀에 영향을 주지 않고 한 단계를 쉽게 업데이트할 수 있음, 다른 팀이 다른 여정을 소유할 수 있음, 캔버스 디자인 간소화
- **권장 사항:** 옵션 A의 경우 단일 여정이 적절합니다. 옵션 B와 C의 경우, 솔루션 관심 분야 또는 구매 단계별로 계정을 전문 하위 여정으로 라우팅하는 기본 &quot;오케스트레이션&quot; 여정을 사용하십시오.

## 관련 설명서

다음 리소스는 이 안내서에서 참조하는 애플리케이션 및 기능에 대한 추가 세부 정보를 제공합니다.

### [!DNL AJO B2B Edition]

- [AJO B2B edition 설명서 홈](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [구매 그룹 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [솔루션 관심 분야](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [역할 템플릿](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [구매 그룹 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)
- [구매 그룹 단계](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [계정 여정 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [계정 여정 노드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [영업 경고 이메일](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sales-alert-email)
- [CRM 영업 인사이트](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/crm-sales-insights)

### B2B 이메일 및 콘텐츠

- [B2B 이메일 작성](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/email-authoring)
- [AJO B2B에서 SMS 작성](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/sms-authoring)
- [이메일 작성을 위한 AI Assistant](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/content/ai-assistant-emails)

### B2B 분석 및 대시보드

- [구매 그룹 대시보드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/buying-groups-dashboard)
- [참여 대시보드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/engagement-dashboard)
- [지능형 대시보드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/dashboards/intelligent-dashboard)
- [CJA B2B edition 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b)

### [!DNL RT-CDP B2B Edition]

- [RT-CDP B2B edition 개요](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-overview)
- [Real-Time CDP의 B2B 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [계정 대상자](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [Marketo Engage 소스 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)

### 데이터 기반

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### 데이터 거버넌스 및 개인 정보 보호

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [고급 데이터 수명주기 관리](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### 대상

- [대상 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [대상 카탈로그](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [LinkedIn 일치하는 대상 대상 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)

### 가드레일

- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)

### 튜토리얼 및 시작하기

- [AJO B2B edition 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [RT-CDP B2B edition 자습서](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/b2b-tutorial)
