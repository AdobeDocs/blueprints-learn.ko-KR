---
title: 구매 그룹 기반 마케팅 및 여정 관리
description: B2B 마케팅 효과를 향상시키기 위해 구매 그룹으로 잠재 고객을 선별하는 계정 수준 여정을 개발하는 방법에 대해 알아봅니다.
solution: Journey Optimizer B2B Edition, Real-Time Customer Data Platform
exl-id: 2bf57f67-80c8-4368-98d2-05706427772d
source-git-commit: c0a9cba3d6a55fae8f149f7ca479625458cd1b22
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 1%

---

# 구매 그룹 기반 마케팅 및 여정 관리

이 안내서에서는 [!DNL Adobe Journey Optimizer B2B Edition] 및 [!DNL Real-Time CDP B2B Edition]을(를) 사용하여 구매 그룹 관리와 함께 계정 수준 여정 오케스트레이션을 구현하는 구매 그룹 기반 마케팅 및 여정 관리 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

개인 수준 여정 패턴과 달리 이 패턴은 계정 수준에서 작동하며, 자격을 갖춘 개인은 솔루션 관심사와 관련된 구매 그룹으로 이어지고, 구매 그룹 수준에서 참여 점수를 매기고, 파이프라인 단계를 거쳐 판매 준비로 계정을 진행하는 여러 단계 계정 여정을 조정합니다.

## 사용 사례 패턴

**그룹 기반 마케팅 및 여정 관리 구매**

B2B 마케팅 효과를 개선하기 위해 잠재 고객을 구매 그룹으로 분류하는 계정 수준 여정을 개발합니다.

**실행 계획:** 계정 식별 > 구매 그룹 정의 > 잠재 고객 자격 > 계정 여정 실행 > 참여 점수 > 보고

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

## 애플리케이션

이 사용 사례 패턴에는 다음 Adobe 애플리케이션이 사용됩니다.

- **[!DNL Journey Optimizer B2B Edition]([!DNL AJO B2B])** — 계정 수준 여정을 조정하고, 역할 템플릿과 솔루션 관심사를 사용하여 구매 그룹을 관리하고, 개인 및 구매 그룹 수준에서 참여 점수를 매기고, 작성자 B2B 이메일 콘텐츠를 작성하고, SMS 메시지를 보내고, 판매 알림을 구성하고, B2B 분석 대시보드를 제공합니다.
- **[!DNL Real-Time CDP B2B Edition]([!DNL RT-CDP B2B])** — 소스 간 B2B 데이터에서 계정 프로필을 통합하고, 개인 대 계정 관계를 확인하고, 계정 수준 대상을 평가하고, B2B별 대상([!DNL Marketo Engage], [!DNL LinkedIn], CRM)을 구성하고, B2B 데이터 전반에 걸쳐 데이터 거버넌스를 적용합니다.

## 관련 설명서

다음 리소스는 이 안내서에서 참조하는 애플리케이션 및 기능에 대한 추가 세부 정보를 제공합니다.

### [!DNL Journey Optimizer B2B Edition]

- [Journey Optimizer B2B edition 설명서 홈](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview)
- [구매 그룹 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-overview)
- [솔루션 관심 분야](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/solution-interests)
- [역할 템플릿](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-role-templates)
- [구매 그룹 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-groups-create)
- [구매 그룹 단계](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/buying-groups/buying-group-stages)
- [계정 여정 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-overview)
- [계정 여정 노드](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/account-journeys/journey-nodes)
- [영업 경고 이메일](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/journey-content/email-channel/sales-alert-email)
- [CRM 영업 인사이트](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/accounts/buying-groups/incrm-insights)

### B2B 이메일 및 콘텐츠

- [B2B 이메일 작성](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/journey-content/email-channel/email-authoring)
- [B2B SMS 작성](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/journey-content/sms-authoring)
- [이메일 작성을 위한 콘텐츠 생성](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/journey-content/email-channel/ai-assistant-emails)

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
