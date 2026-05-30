---
title: B2B Audience Activation
description: 웹, 이메일 및 광고 채널에서 계정 기반 B2B 대상자를 활성화하는 방법을 알아봅니다.
solution: Real-Time Customer Data Platform
exl-id: 2b979159-37aa-41d4-a6b4-1105538f6546
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 2%

---

# B2B 대상 활성화

이 안내서에서는 [!DNL Adobe Real-Time Customer Data Platform]&#x200B;([!DNL RT-CDP]) B2B edition을 사용하여 웹, 전자 메일, 광고 및 CRM 채널에서 계정 수준 대상을 빌드, 평가 및 활성화하는 B2B 대상 활성화 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

이 패턴은 대상 평가 및 활성화를 통한 계정 프로필 통합에서 [!DNL Marketo Engage], [!DNL LinkedIn] 및 CRM 시스템과 같은 B2B 관련 대상까지의 전체 라이프사이클을 다룹니다.

## 사용 사례 패턴

**B2B 대상 활성화**

웹, 이메일 및 광고 채널에서 계정 기반 B2B 대상을 활성화합니다.

**실행 계획:** 계정 프로필 보강 > 계정 대상 평가 > 대상 구성 > Audience Activation > 모니터링

## 사용 사례 개요

B2B 마케팅 팀은 개인 수준이 아닌 계정 수준에서 대상을 타겟팅하고 활성화해야 합니다. 타깃팅 단위가 단일 소비자 프로필인 B2C 대상 활성화와 달리 B2B 대상 활성화는 사람과 사람이 속한 계정 간의 관계를 이해하고, 사람 수준 참여 신호와 결합된 계정 수준 특성을 기반으로 대상 멤버십을 평가하고, 이러한 대상을 계정 기반 타깃팅을 지원하는 대상으로 전달해야 합니다.

[!DNL RT-CDP] B2B edition은 계정, 기회 및 캠페인에 대한 특수 XDM 클래스와 개인 대 계정 관계를 매핑하는 B2B ID 확인을 사용하여 표준 [!DNL Real-Time Customer Data Platform]을(를) 확장합니다. 이를 통해 마케터는 해당 계정과 연계된 직원의 그래픽 데이터(업계, 수입, 직원 수), 기술 데이터(기술 스택, 제품 사용) 및 행동 데이터(웹 방문, 이메일 참여, 이벤트 참석)를 결합하는 계정 대상을 구축할 수 있습니다.

활성화된 계정은 수요 창출 funnel에서 고급 사용 사례: [!DNL LinkedIn]의 funnel 인식 캠페인 및 디스플레이 광고, [!DNL Marketo Engage]의 중간 funnel 교육 프로그램, CRM 통합을 통한 funnel 판매 지원. 계정 억제 대상은 기존 고객, 마감된 손실 계정 또는 이미 활성 영업 주기에 있는 계정을 제외하여 비용 낭비를 방지합니다.

>[!NOTE]
>사용 사례에 계정 수준이 아닌 개인 수준(B2C)에서 대상을 활성화하는 것이 포함된 경우 [대상에 대상 활성화](../audience-building-activation/audience-activation-to-destinations.md)를 참조하십시오. 이 패턴은 표준 RT-CDP 데이터 모델을 사용하며 B2B edition이 필요하지 않습니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 리드 생성 늘리기

양식, 이벤트, 콘텐츠 및 멀티채널 참여를 통해 판매 파이프라인에 대해 보다 적합한 리드를 생성합니다.

**KPI:** 잠재 고객, 잠재 고객당 비용, 잠재 고객 전환

[리드 생성 증가에 대해 자세히 알아보기](/help/blueprints/business-objectives/acquisition-growth/increase-lead-generation.md)

### 리드 자격 및 전환 개선

점수 책정, 육성 및 개인화된 후속 조치를 통해 잠재 고객 품질을 높이고 파이프라인 진행을 가속화합니다.

**KPI:** 잠재 고객 전환, 잠재 고객/잠재 고객 전환, 효율성

[리드 자격 및 전환 개선에 대해 자세히 알아보기](/help/blueprints/business-objectives/qualification-sales-b2b/improve-lead-qualification-conversion.md)

### 신규 고객 확보

타겟팅 획득 캠페인, 유사 대상 및 유료 미디어 최적화를 통해 고객 기반을 확장합니다.

**KPI:**&#x200B;개의 신규 고객, 고객 확보 비용, 잠재 고객/잠재 고객 전환

[신규 고객 확보에 대해 자세히 알아보기](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### 마케팅 지출 및 ROI 최적화

더 나은 타겟팅, 속성, 대상자 억제 및 예산 할당을 통해 마케팅 투자에 대한 수익률을 개선합니다.

**KPI:** 비용 절감, 고객 확보 비용, 수익 증가

[마케팅 지출 및 ROI 최적화에 대해 자세히 알아보기](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## 예시 전술 사용 사례

다음 시나리오에서는 이 패턴을 실제로 적용하는 방법을 보여 줍니다.

- [!DNL LinkedIn]&#x200B;**의**&#x200B;계정 기반 광고 — [!DNL RT-CDP] B2B edition에서 활성화된 계정 목록을 사용하여 [!DNL LinkedIn]의 ICP(Ideal Customer Profile)와 스폰서 콘텐츠 및 InMail 캠페인이 일치하는 계정을 타겟팅합니다.
- **[!DNL Marketo Engage]육성 프로그램 타깃팅** — 계정 수준 자격 조건을 기반으로 연결된 리드 및 연락처를 타깃팅된 육성 스트림에 등록하려면 계정 대상을 [!DNL Marketo Engage]에 활성화하십시오.
- **CRM 계정 목록 동기화** — 영업 팀 가시성, 영역 할당 및 아웃바운드 전망 워크플로를 위해 자격 조건을 갖춘 계정 목록을 [!DNL Salesforce] 또는 [!DNL Microsoft Dynamics]에 푸시합니다.
- **유료 미디어에 대한 계정 억제** - 기존 고객, 비공개 계정 또는 활성 영업 주기의 계정을 유료 획득 캠페인에서 억제하여 낭비되는 지출을 줄입니다.
- **의도 기반 계정 타깃팅** — 타사 의도 신호를 계정 수준의 자사 참여 데이터와 결합하여 마켓 내 계정의 대상을 식별하고 활성화합니다
- **기존 계정에 대한 제품 교차 판매** - 한 제품군을 사용하지만 다른 제품군은 사용하지 않는 계정의 대상을 만든 다음 교차 판매 캠페인을 위해 이메일 및 광고 채널에 활성화합니다
- **이벤트 및 웨비나 타깃팅** - 계정 대상을 광고 및 이메일 채널에 활성화하여 대상 계정에서 이벤트 등록을 유도합니다.
- **경쟁사 교체 캠페인** - 광고 및 이메일 채널을 통해 활성화된 맞춤 메시지를 사용하여 경쟁사 제품을 사용하는 계정을 타깃팅합니다.
- **계층화된 계정 참여** — 집계된 사용자 수준 활동을 기반으로 계정을 참여 계층(높음, 중간, 낮음)으로 세그먼트화하고 각 계층에 대해 차별화된 캠페인을 활성화합니다
- **파트너 공동 마케팅 대상** - 클라우드 저장소 대상을 통해 채널 파트너 또는 공동 마케팅 프로그램과 계정 대상 세그먼트를 공유합니다.

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 성공을 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 계정 도달 | 활성화 채널에서 도달한 타겟 계정 수 | 대상별로 활성화된 고유 계정 추적 |
| 계정 참여 비율 | 참여 신호를 표시하는 활성화된 계정의 백분율 | 계정에 집계된 사용자 수준 참여 측정 |
| 파이프라인 영향 | 계정 기반 활성화 캠페인으로 인한 매출 파이프라인 | 활성화된 계정 대상으로부터 생성된 기회 추적 |
| 참여 계정당 비용 | 마케팅 비용을 참여를 보여주는 계정 수로 나눈 값 | 광고 및 이메일 채널 비용 전체 계산 |
| 잠재 고객 전환율 | 기회로 전환되는 활성화된 계정의 잠재 고객 비율 | 활성화된 대상에 대한 잠재 고객-기회 전환 추적 |
| 대상자 억제 절감 | 유료 캠페인에서 부적격 계정을 억제하여 비용 절감 | 제외 대상에서 비용 절감 측정 |
| 계정 범위 | 활성화된 대상자에 의해 적용되는 총 대응 가능 시장(TAM) 비율 | 활성화된 계정을 총 ICP Universe와 비교 |

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Real-Time CDP]B2B edition** — 계정 프로필 통합, B2B ID 해결, 계정 대상 평가, B2B별 대상 구성 및 계정 대상 활성화를 위한 핵심 플랫폼
- **[!DNL Adobe Experience Platform] (AEP)** — B2B XDM 데이터 모델링, CRM 및 마케팅 자동화 소스에서의 데이터 수집, ID 서비스 및 거버넌스를 위한 기본 인프라
- **[!DNL Marketo Engage]** — 활성화된 계정 대상자가 제공하는 리드 육성 프로그램, 점수 및 캠페인 실행을 위한 기본 B2B 마케팅 자동화 대상

## 관련 설명서

다음 리소스는 이 사용 사례 패턴에 사용된 기능에 대한 추가 컨텍스트 및 자세한 지침을 제공합니다.

**[!DNL RT-CDP]B2B edition**

- [Real-Time CDP B2B edition 개요](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Real-Time CDP의 B2B 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [계정 대상자](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [RT-CDP B2B edition 제품 설명](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

**대상 평가 및 세분화**

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [대상자 구성](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

**대상 및 활성화**

- [대상 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [대상 카탈로그](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Marketo Engage 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [LinkedIn 일치하는 대상 대상 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Salesforce CRM 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Microsoft Dynamics 365 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)
- [Amazon 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [스트리밍 대상에 대상 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [일괄 처리 대상에 대상자 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [활성화 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

**데이터 원본 및 커넥터**

- [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [Marketo Engage 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Salesforce 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/crm/salesforce)

**데이터 모델링 및 ID**

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

**데이터 거버넌스 및 개인 정보 보호**

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [동의 및 환경 설정](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**모니터링 및 관찰 가능성**

- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [대상 데이터 흐름 모니터링](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [소스 데이터 흐름 모니터링](https://experienceleague.adobe.com/en/docs/experience-platform/sources/api-tutorials/monitor)
- [라이선스 사용 대시보드](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**보고 및 분석**

- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [연결 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [데이터 보기 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)

**튜토리얼 및 가이드**

- [Real-Time CDP B2B edition 시작하기](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro)
- [B2B 소스에 대한 스키마 만들기](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [샌드박스 도구](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/overview)
