---
title: 대상에 대한 대상자 활성화
description: Adobe Real-Time CDP을 사용하여 타깃팅 또는 제외를 위해 대상 세그먼트를 평가하고 외부 대상에 게시하는 방법을 알아봅니다.
solution: Real-Time Customer Data Platform, Experience Platform
exl-id: b0b9d937-45d2-48f9-ac4c-3611c6e35f58
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 4%

---

# 대상에 대한 대상자 활성화

이 안내서에서는 대상에 대한 대상 활성화 사용 사례 패턴에 대해 설명합니다. 이 패턴은 Adobe [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP)의 대상 세그먼트를 평가하고 타깃팅, 억제, 유사 모델링 또는 분석 데이터 강화를 위해 광고 플랫폼, 클라우드 스토리지, CRM 시스템 또는 데이터 파트너에 게시합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

이 패턴은 대상 연결 구성 및 대상 게시를 통한 대상 세그먼트 정의 및 평가에서 활성화 상태 모니터링 및 거버넌스 규정 준수에 이르기까지 대상 활성화의 전체 라이프사이클을 다룹니다.

## 사용 사례 패턴

**대상에 대한 Audience Activation** - 타깃팅 또는 제외를 위해 대상 세그먼트를 평가하고 외부 대상에 게시합니다.

**실행 계획:** 대상 평가 > 대상 구성 > Audience Activation > 모니터링

## 사용 사례 개요

조직은 외부 시스템에 대상 데이터를 전달하여 유료 미디어 캠페인을 강화하고, CRM 레코드를 보강하고, 파트너와 데이터를 공유하거나, 다운스트림 분석을 피드해야 합니다. Audience Activation to 대상은 RT-CDP의 기본 활성화 패턴입니다. 어떤 프로필이 타겟 대상에 적합한지 평가하고, 하나 이상의 외부 대상에 연결하고, 프로필 속성을 대상별 필드에 매핑하고, 다운스트림 소비를 위해 대상을 게시합니다.

이 패턴은 대상 데이터를 적절한 시간에 적절한 형식으로 외부 시스템에 가져오는 것이 목표일 때마다 적용됩니다. 메시지 게재, 현장 개인화 또는 분석은 포함되지 않습니다. RT-CDP 구현의 가장 일반적인 시작점이며 다른 패턴이 맨 위에 구성하는 빌딩 블록 역할을 합니다.

대표적인 이해 당사자로는 유료 미디어를 관리하는 디지털 마케팅 팀, 웨어하우스를 보강하는 데이터 팀, 캠페인을 위한 연락처 목록을 준비하는 CRM 팀, 아웃바운드 데이터 흐름에 대한 거버넌스 준수를 보장하는 개인 정보 보호 팀 등이 있습니다.

>[!NOTE]
>조직에서 [!DNL Real-Time CDP] B2B edition을 사용하고 계정 기반 대상으로 활성화하는 경우 [B2B 대상 활성화](../b2b/account-audience-activation.md)를 참조하십시오. 이 패턴은 동일한 활성화 방식을 공유하지만 B2B 계정 및 개인 데이터 모델을 사용하며 B2B edition 라이센스가 필요합니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 신규 고객 확보

타겟팅 획득 캠페인, 유사 대상 및 유료 미디어 최적화를 통해 고객 기반을 확장합니다.

**KPI:**&#x200B;개의 신규 고객, 고객 확보 비용, 잠재 고객/잠재 고객 전환

[신규 고객 확보에 대해 자세히 알아보기](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

### 고객 확보 비용 절감

타깃팅 효율성을 개선하고, 기존 고객을 획득 캠페인으로부터 억제하며, 미디어 지출을 최적화합니다.

**KPI:** 고객 확보 비용, 리드당 비용, 효율성

[고객 확보 비용 절감에 대해 자세히 알아보기](/help/blueprints/business-objectives/cost-efficiency/reduce-customer-acquisition-cost.md)

### 마케팅 지출 및 ROI 최적화

더 나은 타겟팅, 속성, 대상자 억제 및 예산 할당을 통해 마케팅 투자에 대한 수익률을 개선합니다.

**KPI:** 비용 절감, 고객 확보 비용, 수익 증가

[마케팅 지출 및 ROI 최적화에 대해 자세히 알아보기](/help/blueprints/business-objectives/cost-efficiency/optimize-marketing-spend-roi.md)

## 예시 전술 사용 사례

- **광고 플랫폼 대상 타깃팅** - 캠페인 타깃팅을 위해 적격 세그먼트를 유료 미디어 플랫폼에 푸시
- **기존 고객에 대한 유료 미디어 억제** - 알려진 고객을 광고 플랫폼의 획득 캠페인에서 제외하여 낭비되는 비용을 제거합니다.
- **유사 시드 대상** — 고부가가치 고객 세그먼트를 유사 확장을 위한 시드 대상으로 Facebook, Google Ads 또는 The Trade Desk에 푸시합니다.
- **판매 활성화를 위한 CRM 동기화** - 고의성 또는 고가치 대상 활성화로 영업팀이 우선적으로 지원을 제공할 수 있습니다.
- **데이터 파트너 대상 공유** - Co-op 타기팅 또는 측정을 위해 데이터 파트너와 적격 대상 세그먼트 공유
- **데이터 웨어하우스 강화를 위한 클라우드 저장소 내보내기** - 다운스트림 분석을 위해 대상 멤버십 및 프로필 특성을 Amazon S3, Azure Blob, Google Cloud Storage 또는 SFTP로 내보냅니다.
- **대상 재타겟팅 활성화** - 재타겟팅 플랫폼으로 전환되지 않은 사이트 방문자를 활성화합니다
- **전자 메일 서비스 공급자에 대한 연락처 목록 동기화** — 조정된 전달을 위해 대상자 멤버십을 서드파티 전자 메일 플랫폼으로 푸시합니다.

## 주요 성과 지표

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 고객 확보 비용(CAC) | 활성화된 대상을 통해 새 고객을 확보하는 데 드는 비용 | 활성화된 대상자에 속하는 총 미디어 지출/신규 고객 |
| 대상 일치율 | 대상에서 성공적으로 일치하는 활성화된 프로필의 비율 | 대상에서 일치하는 프로필 / RT-CDP에서 내보낸 프로필 |
| 억제 절감 | 기존 고객을 확보 캠페인에서 억제하여 미디어 비용 절감 | 예상 CPM x 억제된 대상 크기 |
| 활성화 게재율 | 대상에 성공적으로 전달된 프로필 비율 | 제공된 프로필 / 소스 대상의 프로필 |
| 활성화 시간 | 대상 정의에서 첫 번째 전달까지 경과된 시간 | 세그먼트 생성에서 처음 확인된 데이터 흐름 실행으로 측정 |
| 대상자 모집단 정확도 | 대상에서 예상 및 실제 대상 크기 정렬 | 대상 대상자 규모/RT-CDP 대상자 규모 |

## 애플리케이션

- **Adobe [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP)** - 대상 평가, 대상 관리, 대상 활성화, 동의 및 거버넌스 적용
- **Adobe [!DNL Experience Platform]&#x200B;(AEP)** - 프로필 저장소, ID 서비스, 세그먼테이션 엔진, 데이터 거버넌스

## 아키텍처

다음 참조 아키텍처는 대상 및 프로필 데이터가 Real-Time CDP에서 클라우드 스토리지, 스트리밍 끝점 및 SaaS 애플리케이션을 포함한 엔터프라이즈 대상으로 이동하는 방식을 보여 줍니다.

![Enterprise 대상에 대한 대상 및 프로필 활성화를 위한 참조 아키텍처](/help/blueprints/audience-activation/assets/known_activation.png)

## 관련 설명서

**대상**

- [대상 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/home)
- [대상 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/overview)
- [스트리밍 대상에 대상 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [프로필 내보내기 대상을 일괄 처리하도록 대상자 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [배치 대상에 대한 온디맨드 대상자 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [대상 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/guardrails)
- [Destination SDK 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/destination-sdk/overview)

**대상 및 세분화**

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language 참조](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/pql/overview)
- [스트리밍 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/edge-segmentation)
- [대상 구성 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/audience-composition)
- [세그먼테이션 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)

**ID 및 프로필**

- [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [아이덴티티 그래프 연결 규칙](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/identity-linking-logic)
- [프로필 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/home)
- [병합 정책 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/merge-policies/overview)

**데이터 모델링 및 스키마**

- [XDM 시스템 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/schema/composition)

**데이터 거버넌스**

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [데이터 거버넌스 정책](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/policies/overview)
- [정책 시행](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/enforcement/overview)
- [동의 및 환경 설정](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)

**모니터링 및 관찰 가능성**

- [대상에 대한 데이터 흐름 모니터링](https://experienceleague.adobe.com/ko/docs/experience-platform/dataflows/ui/monitor-destinations)
- [경고 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/alerts/overview)
- [Observability Insights 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/home)
- [라이선스 사용 대시보드](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

**계산된 특성**

- [계산된 속성 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/overview)
- [계산된 속성 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/ui)

**데이터 수집 및 원본**

- [소스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/home)
- [웹 SDK 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/home)
- [데이터스트림 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/configure)

**관리**

- [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home)
- [액세스 제어 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/home)
- [속성 기반 액세스 제어](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/abac/overview)

**보호 기능**

- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/guardrails)
- [활성화 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/guardrails)
- [수집 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/ingestion/guardrails)
