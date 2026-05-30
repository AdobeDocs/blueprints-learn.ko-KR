---
title: Audience Collaboration
description: 세그먼트 일치를 사용하여 샌드박스 또는 조직 간에 대상 세그먼트를 공유하고 일치시키는 방법을 알아봅니다.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: 7014849c-5e32-4ec3-a531-c0e8ce896f44
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 3%

---

# Audience Collaboration

이 안내서에서는 [!DNL Real-Time CDP] 및 [!DNL Adobe Experience Platform]의 [!DNL Segment Match]을(를) 사용하여 샌드박스 또는 조직에서 개인 정보에 안전한 방식으로 대상 세그먼트를 공유하고 일치시키는 대상 공동 작업 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

[!DNL Segment Match]을(를) 사용하면 두 개 이상의 [!DNL Experience Platform] 조직(또는 조직 내의 샌드박스)에서 기본 PII를 노출하지 않고 세그먼트 멤버십 정보를 공유하여 대상 데이터에 대해 공동 작업을 수행할 수 있습니다. 참가자는 중복을 예측하고 대상을 공유하며 다운스트림 대상에 일치하는 프로필을 활성화할 수 있습니다.

## 사용 사례 패턴

이 사용 사례는 대상 Collaboration 패턴을 따릅니다.

[!DNL Segment Match]을(를) 사용하여 샌드박스 또는 조직에서 대상 세그먼트를 공유하고 일치시킵니다.

**실행 계획:** 세그먼트 선택 > 일치 구성 > 겹침 예측 > 대상 공유 > 활성화

## 사용 사례 개요

조직은 엄격한 개인 정보 보호 제어를 유지하면서 파트너, 자회사 또는 여러 비즈니스 부서와 대상 데이터에 대해 공동 작업을 수행해야 하는 경우가 점점 늘어나고 있습니다. 대상 공동 작업은 두 개 이상의 [!DNL Experience Platform] 조직(또는 샌드박스)에서 해시된 개인 정보 보호 식별자를 사용하여 대상 멤버십 정보를 교환할 수 있도록 하는 [!DNL Real-Time CDP] 내의 기능인 [!DNL Segment Match]을(를) 통해 보안 세그먼트 공유를 활성화하여 이러한 요구를 해결합니다.

비즈니스 시나리오는 일반적으로 중요한 대상 세그먼트를 구축했으며 공동 타기팅, 억제 또는 강화를 위해 파트너 조직(수신자)과 공유하고자 하는 조직(발신자)에 포함됩니다. 공유하기 전에 양 당사자는 대상 중복을 추정하여 가치를 평가할 수 있습니다. 공유되면 수신 조직은 자체 대상을 통해 일치하는 대상자를 활성화할 수 있습니다.

이 패턴은 외부 광고 또는 마케팅 대상보다는 조직 또는 샌드박스 간에 작동하므로 표준 대상 활성화와 다릅니다. [!DNL Experience Platform] ID 인프라를 사용하여 Adobe 생태계 내에서 기본적으로 작동하기 때문에 데이터 클린룸 또는 서드파티 협업 플랫폼과도 구별됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 신규 고객 확보

타겟팅 획득 캠페인, 유사 대상 및 유료 미디어 최적화를 통해 고객 기반을 확장합니다. Audience Collaboration을 통해 조직은 파트너 대상과 세그먼트를 일치시키고, 고가치 중복을 식별하며, 공동 활성화를 통해 신규 고객에게 도달함으로써 새로운 잠재 고객을 발견할 수 있습니다.

- **KPI:**&#x200B;개의 신규 고객, 고객 확보 비용, 잠재 고객/잠재 고객 전환
- [신규 고객 확보](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### 고객 확보 비용 절감

타깃팅 효율성을 개선하고, 기존 고객을 획득 캠페인으로부터 억제하며, 미디어 지출을 최적화합니다. 팀은 조직 또는 비즈니스 부서 간에 억제 세그먼트를 공유함으로써 이미 전환된 고객에게 낭비되는 지출을 방지하고 진정한 새로운 잠재 고객에 예산을 집중할 수 있습니다.

- **KPI:** 고객 확보 비용, 리드당 비용, 효율성
- [고객 확보 비용 절감](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### 마케팅 지출 및 ROI 최적화

더 나은 타겟팅, 속성, 대상자 억제 및 예산 할당을 통해 마케팅 투자에 대한 수익률을 개선합니다. [!DNL Segment Match]을(를) 사용하면 조직 간 대상 억제 및 공동 타깃팅을 통해 중복을 줄이고 정밀도를 향상시킬 수 있습니다.

- **KPI:** 비용 절감, 고객 확보 비용, 수익 증가
- [마케팅 지출 및 ROI 최적화](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## 예시 전술 사용 사례

- **게시자-광고주 대상 일치** — 브랜드는 가치가 높은 고객 세그먼트를 미디어 게시자와 공유하여 겹치는 사용자를 예측하고 개인화된 광고와 일치하는 사용자를 타겟팅하므로 PII를 노출하지 않고도 캠페인 관련성을 향상시킬 수 있습니다.
- **지주 회사 내에서 브랜드 간 억제** — 상위 조직의 여러 브랜드가 고객 세그먼트를 공유하여 자매 브랜드의 기존 고객을 획득 캠페인에서 억제하여 광고 비용 낭비를 줄입니다.
- **소매 미디어 네트워크 대상 강화** — retailer은 구매 기반 세그먼트를 CPG 브랜드 파트너와 공유하므로, 브랜드가 더 높은 전환율로 retailer 미디어 네트워크에서 검증된 구매자를 타깃팅할 수 있습니다.
- **공동 마케팅 파트너 대상 검색** - 경쟁사가 아닌 두 브랜드는 대상 정렬을 확인하기 위해 겹치기 추정을 사용하여 공동 캠페인을 시작하기 전에 대상 겹침을 평가하여 파트너 가능성을 평가합니다.
- **데이터 협력 세그먼트 공유** - 데이터 협력 공유에 있는 조직이 대상 세그먼트를 해시하여 개인 정보 보호 규정 준수 및 데이터 거버넌스 제어를 유지하면서 타깃팅 범위를 확장합니다.
- **다중 샌드박스 대상 페더레이션** - 글로벌 기업이 지역 샌드박스 간에 대상 세그먼트를 공유하여 지역 데이터 상주 요구 사항을 준수하면서 시장 간에 일관된 고객 타깃팅을 가능하게 합니다.
- **충성도 프로그램 크로스 파트너 활성화** — 충성도 연합은 참여 가맹점과 충성도 계층 세그먼트를 공유하므로 각 파트너는 공유 고객 기반에 계층에 적합한 프로모션을 제공할 수 있습니다.
- **측정 및 속성 공동 작업** - 광고주가 미디어 파트너와 전환 세그먼트를 공유하므로 파트너는 노출된 사용자를 전환자와 비교하여 캠페인 효과를 측정할 수 있습니다.

## 주요 성과 지표

다음 KPI는 대상자 공동 작업 구현의 성공을 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 대상 겹침 비율 | 공유 세그먼트에 있는 보낸 사람과 받은 사람 간에 일치하는 프로필의 비율 | [!DNL Segment Match] 중복 예상 보고서 |
| 일치하는 대상 크기 | 성공적으로 일치하여 활성화할 수 있는 프로필 수 | [!DNL Segment Match] 공유 상태 및 대상 모집단 수 |
| 일치하는 대상으로부터 새 고객 확보 | 일치하는 세그먼트를 타겟팅하는 캠페인을 통해 획득한 순 신규 고객 | 일치하는 대상을 사용하는 캠페인에 대한 전환 추적 |
| 고객 확보 비용 절감 | 일치하는 대상과 광범위한 타겟팅을 사용할 때 획득당 비용 감소 | 일치하는 대상 성능과 일치하지 않는 대상 성능을 비교하는 캠페인 비용 분석 |
| 억제 절감 | 알려진 고객을 확보 캠페인에서 억제하여 미디어 비용 절감 | 제외 전/후 미디어 지출 비교 |
| 캠페인 성과 향상 | 일치하는 대상을 사용하는 캠페인에 대한 전환율, 클릭스루 비율 또는 참여 개선 | 일치하는 대상 캠페인과 컨트롤을 비교하는 A/B 테스트 |
| Collaboration에 간 시간 | 세그먼트 공유 시작에서 활성화 준비까지 경과된 시간 | [!DNL Segment Match]개의 워크플로우 타임스탬프 |

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Real-Time CDP]** — 개인 정보 보호 대상 공유, 세그먼트 생성을 위한 대상 평가 및 일치하는 대상의 다운스트림 사용을 위한 대상 활성화를 위한 [!DNL Segment Match] 기능을 제공합니다.
- **[!DNL Adobe Experience Platform]** — [!DNL Segment Match]이(가) 종속된 ID 확인, 프로필 통합, 데이터 거버넌스 및 동의 적용을 비롯한 기본 데이터 인프라를 제공합니다.

## 관련 설명서

다음 리소스는 이 사용 사례 패턴에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

### [!DNL Segment Match]

- [세그먼트 일치 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/overview)
- [세그먼트 매치 문제 해결](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-match/troubleshooting)

### 세분화 및 대상자

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [대상 구성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### ID 및 프로필

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### 데이터 거버넌스 및 동의

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [정책 시행](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview)
- [동의 및 환경 설정](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

### 대상 및 활성화

- [대상 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [대상 카탈로그](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [대상에 대한 데이터 흐름 모니터링](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)

### 데이터 모델링 및 스키마

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### 관리 및 액세스 제어

- [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home)
- [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home)

### 모니터링 및 가시성

- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### 가드레일

- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/guardrails)
- [활성화 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

### 튜토리얼

- [스키마 만들기](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [프로필에 대한 데이터 세트 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/enable-for-profile)
