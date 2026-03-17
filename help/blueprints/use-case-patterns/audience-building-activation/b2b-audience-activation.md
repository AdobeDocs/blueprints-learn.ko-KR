---
title: B2B Audience Activation
description: 웹, 이메일 및 광고 채널에서 계정 기반 B2B 대상자를 활성화하는 방법을 알아봅니다.
solution: Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '7567'
ht-degree: 0%

---


# B2B 대상 활성화

이 안내서에서는 [!DNL Adobe Real-Time Customer Data Platform]&#x200B;([!DNL RT-CDP]) B2B edition을 사용하여 계정 기반 B2B 대상을 활성화하기 위한 포괄적인 구현 참조를 제공합니다. 웹, 이메일, 광고 및 CRM 채널에서 계정 수준 대상을 구축, 평가 및 활성화해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

대상 평가 및 활성화를 통한 계정 프로필 통합부터 [!DNL Marketo Engage], [!DNL LinkedIn] 및 CRM 시스템과 같은 B2B 관련 대상까지의 전체 라이프사이클을 다룹니다. 실행 가능한 모든 구현 접근 방식에는 조직의 올바른 경로를 선택하는 데 도움이 되는 절충안 및 의사 결정 지침이 제공됩니다.

## 사용 사례 개요

B2B 마케팅 팀은 개인 수준이 아닌 계정 수준에서 대상을 타겟팅하고 활성화해야 합니다. 타깃팅 단위가 단일 소비자 프로필인 B2C 대상 활성화와 달리 B2B 대상 활성화는 사람과 사람이 속한 계정 간의 관계를 이해하고, 사람 수준 참여 신호와 결합된 계정 수준 특성을 기반으로 대상 멤버십을 평가하고, 이러한 대상을 계정 기반 타깃팅을 지원하는 대상으로 전달해야 합니다.

[!DNL RT-CDP] B2B edition은 계정, 기회 및 캠페인에 대한 특수 XDM 클래스와 개인 대 계정 관계를 매핑하는 B2B ID 확인을 사용하여 표준 [!DNL Real-Time Customer Data Platform]을(를) 확장합니다. 이를 통해 마케터는 해당 계정과 연계된 직원의 그래픽 데이터(업계, 수입, 직원 수), 기술 데이터(기술 스택, 제품 사용) 및 행동 데이터(웹 방문, 이메일 참여, 이벤트 참석)를 결합하는 계정 대상을 구축할 수 있습니다.

활성화된 계정은 수요 창출 funnel에서 고급 사용 사례: [!DNL LinkedIn]의 funnel 인식 캠페인 및 디스플레이 광고, [!DNL Marketo Engage]의 중간 funnel 교육 프로그램, CRM 통합을 통한 funnel 판매 지원. 계정 억제 대상은 기존 고객, 마감된 손실 계정 또는 이미 활성 영업 주기에 있는 계정을 제외하여 비용 낭비를 방지합니다.

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

## 사용 사례 패턴

**B2B 대상 활성화**

웹, 이메일 및 광고 채널에서 계정 기반 B2B 대상을 활성화합니다.

**함수 체인:** 계정 프로필 보강 > 계정 대상 평가 > 대상 구성 > Audience Activation > 모니터링

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Real-Time CDP]B2B edition** — 계정 프로필 통합, B2B ID 해결, 계정 대상 평가, B2B별 대상 구성 및 계정 대상 활성화를 위한 핵심 플랫폼
- **[!DNL Adobe Experience Platform] (AEP)** — B2B XDM 데이터 모델링, CRM 및 마케팅 자동화 소스에서의 데이터 수집, ID 서비스 및 거버넌스를 위한 기본 인프라
- **[!DNL Marketo Engage]** — 활성화된 계정 대상자가 제공하는 리드 육성 프로그램, 점수 및 캠페인 실행을 위한 기본 B2B 마케팅 자동화 대상

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 필수 | [!DNL RT-CDP] B2B edition이 활성화된 샌드박스가 프로비저닝되었습니다. B2B 데이터 관리, 대상 만들기 및 대상 활성화를 위해 구성된 역할입니다. 계정 데이터에 제한된 필드가 포함된 경우 ABAC 정책이 적용됩니다. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | XDM 비즈니스 계정, XDM 비즈니스 영업 기회, XDM 비즈니스 캠페인 및 XDM 개별 프로필 클래스를 사용하여 구성된 B2B XDM 스키마. 계정 속성, 개인-계정 관계 및 기회 데이터에 적용되는 B2B 필드 그룹. 각 B2B 엔티티에 대해 생성되고 프로필이 활성화된 데이터 세트입니다. 계정, 개인, 영업 기회 및 캠페인 엔터티 간에 정의된 스키마 관계. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), Real-Time CDP의 [B2B 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b) |
| 데이터 소스 및 수집 | 필수 | 계정, 사용자, 기회 및 캠페인 데이터를 수집하기 위해 CRM([!DNL Salesforce], [!DNL Microsoft Dynamics]) 및 마케팅 자동화([!DNL Marketo Engage])용으로 구성된 Source 커넥터입니다. 일괄 처리 또는 스트리밍 수집 파이프라인 활성화. 소스 데이터를 B2B XDM 스키마로 변환하도록 구성된 데이터 준비 매핑. | [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home), [Marketo Engage 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) |
| ID 및 프로필 구성 | 필수 | 계정 식별자(계정 ID, CRM 계정 ID) 및 개인 식별자(이메일, CRM 연락처 ID, Marketo 잠재 고객 ID)에 대해 구성된 B2B ID 네임스페이스입니다. B2B ID 해결을 통해 해결된 개인 대 계정 관계. 계정 프로필 통합을 위해 구성된 병합 정책. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [Real-Time CDP의 B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b) |
| 대상 정의 및 세분화 | 필수 | 계정 속성, 개인 속성 및 활동 데이터를 사용하여 작성된 계정 수준 대상 정의입니다. 계정 대상에 대해 구성된 평가 일정. 부적격 계정을 제외하기 위해 정의된 제외 대상입니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [계정 대상자](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 계정 수준에서 집계된 참여 점수, 라이프타임 값 및 활동 지표는 대상자 정밀도를 향상시킵니다. 계산된 속성은 세분화에 사용할 개인 수준 이벤트(이메일 열기, 웹 방문, 콘텐츠 다운로드)를 계정 수준으로 롤업할 수 있습니다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | B2B 데이터 보존 정책을 통해 오래된 계정 및 영업 기회 데이터를 정리할 수 있습니다. B2B 연락처에 대한 동의 관리를 통해 이메일 마케팅 규정 준수를 보장합니다. 데이터 세트 만료 정책은 오래된 CRM 동기화 데이터의 축적을 방지합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 포함됨 | B2B 계정 데이터에는 계약 제한 사항(매출액, 서드파티 공급자의 직원 수)이 포함되어 있는 경우가 많습니다. 데이터 사용 레이블은 제한된 계정 속성이 권한 없는 대상으로 활성화되지 않도록 합니다. 거버넌스 정책은 활성화 중에 연락처 레코드의 PII 필드가 적절하게 처리되도록 합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| 모니터링 및 가시성 | 포함됨 | CRM 및 [!DNL Marketo Engage] 원본 커넥터 데이터 흐름을 모니터링하여 계정 데이터가 최신 상태를 유지하도록 합니다. 대상 활성화 모니터링에서 대상이 [!DNL LinkedIn], [!DNL Marketo] 및 CRM 대상으로 배달되었는지 확인합니다. 경고 규칙이 오래된 계정 데이터를 발생시키는 수집 실패를 catch합니다. | [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [대상 데이터 흐름 모니터링](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations) |
| 보고 및 분석 | 추천 | [!DNL CJA] B2B edition은 대상 도달, 참여 및 파이프라인 영향을 포함한 계정 수준 분석을 제공합니다. 계정 기반 속성은 활성화 캠페인이 기회 진행 및 매출에 미치는 영향을 측정하는 데 도움이 됩니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Real-Time CDP] B2B edition([!DNL RT-CDP] B2B)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 계정 프로필 통합 | 1단계: 계정 프로필 보강 | B2B XDM 스키마 클래스를 사용하여 CRM, 마케팅 자동화 및 서드파티 소스의 계정 데이터를 통합 계정 프로필로 통합 |
| B2B Id 확인 | 1단계: 계정 프로필 보강 | 기본 식별자를 사용하여 개인-계정 관계를 해결하고, 연락처를 매핑하고 관련 계정으로 연결 |
| 계정 대상자 평가 | 2단계: 계정 대상자 평가 | 계정 속성, 개인 속성 및 개인 활동 데이터를 결합하여 계정 레벨 세그먼트 멤버십을 평가합니다. |
| 계정 대상 구성 | 3단계: 대상 구성 | 계정 수준 필드 매핑을 사용하여 B2B별 대상([!DNL Marketo Engage], [!DNL LinkedIn], CRM, 클라우드 저장소)에 대한 연결 구성 |
| 계정 Audience Activation | 4단계: Audience Activation | 타깃팅, 제외 또는 CRM 동기화를 위해 구성된 대상에 계정 기반 대상 게시 |
| [!DNL Marketo Engage] 통합 | 3단계: 대상 구성 | 기본 B2B 원본 및 대상 커넥터를 사용하여 [!DNL Marketo Engage]과(와) 함께 양방향 데이터 흐름을 구성하십시오. |
| B2B 데이터 거버넌스 | 5단계: 거버넌스 및 모니터링 | B2B 계정 데이터 활성화 전반에 걸쳐 데이터 사용 정책 및 동의를 시행하여 무단 데이터 노출 방지 |

### [!DNL Real-Time CDP]&#x200B;([!DNL RT-CDP]) — 표준 함수

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 2단계: 계정 대상자 평가 | 계정 수준 세그먼트 정의에 대한 일괄 평가를 지원하는 계정 대상에 대한 기본 평가 엔진 |
| 대상 구성 | 3단계: 대상 구성 | B2B 관련 대상 구성에서 사용하는 핵심 대상 연결 인프라 |
| Audience Activation | 4단계: Audience Activation | 계정 대상자 활성화에서 사용하는 핵심 활성화 데이터 흐름 인프라 |
| 동의 및 거버넌스 적용 | 5단계: 거버넌스 및 모니터링 | 활성화 시 동의 환경 설정 및 데이터 사용 정책 적용 |

## 필요 조건

구현을 시작하기 전에 다음을 완료하십시오.

- [ ] [!DNL RT-CDP] B2B edition 라이선스가 조직에서 프로비저닝되고 활성화됨
- [ 소스 커넥터 구성을 위한 API 자격 증명으로 액세스할 수 있는 ] CRM 시스템([!DNL Salesforce] 또는 [!DNL Microsoft Dynamics])
- [ [!DNL Marketo]을(를) 대상으로 사용하는 경우 ] [!DNL Marketo Engage] 인스턴스가 API 액세스(Munchkin ID, 클라이언트 ID, 클라이언트 암호)로 프로비저닝됨
- [ [!DNL LinkedIn]을(를) 대상으로 사용하는 경우 일치하는 대상 기능이 있는 ] [!DNL LinkedIn] Campaign Manager 계정
- [ 계정, 사용자, 영업 기회 및 캠페인 클래스(F2)를 사용하여 만든 ]개의 B2B XDM 스키마
- [ CRM 및 마케팅 자동화 데이터(F3)를 구성하고 수집 중인 ] Source 커넥터
- [ ]개의 개인-계정 ID 관계가 해결되었으며 계정 프로필이 통합되었습니다(F4).
- [ 대상 정의에 대해 합의된 ] 계정 이름 지정 규칙 및 분류법
- [ 계정 수준 데이터 민감도 분류에 대해 정의된 ] 데이터 거버넌스 정책

## 구현 옵션

다음 옵션에서는 이 사용 사례 패턴을 구현하기 위한 다양한 접근 방식을 설명합니다. 각 옵션을 검토하고 요구 사항에 가장 적합한 옵션을 선택합니다.

### 옵션 A: [!DNL Marketo Engage]&#x200B;(으)로 대상 활성화 스트리밍

**가장 적합한 대상:** 기본 B2B 마케팅 자동화 플랫폼으로 [!DNL Marketo Engage]을(를) 사용하는 조직에서는 거의 실시간으로 대상 멤버십을 업데이트하여 육성 프로그램을 트리거하거나, 잠재 고객 점수를 업데이트하거나, 캠페인 멤버십을 계정 자격 또는 자격 상실로 수정해야 합니다.

**작동 방식:**

이 옵션은 [!DNL RT-CDP]의 기본 [!DNL Marketo Engage] 대상 커넥터를 사용하여 계정 대상자 멤버십 변경 사항을 [!DNL Marketo Engage]&#x200B;(으)로 직접 스트리밍합니다. 계정이 대상 세그먼트에 대한 자격이 되거나 종료되면 [!DNL Marketo]의 연결된 잠재 고객 및 연락처가 세그먼트 멤버십 특성으로 업데이트됩니다. [!DNL Marketo] 그런 다음 스마트 캠페인이 이러한 멤버십 변경 사항을 기반으로 트리거될 수 있습니다.

[!DNL Marketo Engage] 대상은 스트리밍 대상입니다. 즉, 대상 멤버십 변경 사항은 예약된 배치가 아니라 발생하는 대로 증분 전송됩니다. 이를 통해 계정 자격 변경에 응답해야 하는 캠페인에 대해 보다 빠른 작업 시간을 제공할 수 있습니다. 필드 매핑은 [!DNL RT-CDP] 프로필 특성을 [!DNL Marketo] 리드/연락처 필드에 연결하여 [!DNL RT-CDP]의 계정 수준 데이터로 [!DNL Marketo] 레코드를 보강할 수 있도록 합니다.

**주요 고려 사항:**

- API 액세스를 통해 활성 [!DNL Marketo Engage] 구독 필요
- 스트리밍 활성화는 전체 대상 스냅샷이 아닌 증분 업데이트를 전송합니다.
- [!DNL Marketo]의 개인 수준 레코드가 업데이트되며 계정 수준 레코드가 직접 업데이트되지 않습니다.
- [!DNL Marketo] 스마트 캠페인이 세그먼트 멤버십 필드 업데이트에 따라 작동하도록 구성되어야 합니다.

**장점:**

- [!DNL Marketo]의 실시간에 가까운 대상 멤버십 업데이트
- 기본 양방향 커넥터를 통해 통합 간소화
- 증분 업데이트로 데이터 전송 볼륨 최소화
- [!DNL Marketo]은(는) 대상 변경 내용에 따라 육성 프로그램을 즉시 트리거할 수 있습니다.

**제한 사항:**

- 활성화 대상으로 [!DNL Marketo Engage]&#x200B;(으)로 제한
- 스트리밍 평가 자격 제한 사항은 기본 대상 정의에 적용됩니다
- [!DNL RT-CDP] 계정 대상자와 [!DNL Marketo] 리드/연락처 레코드 간의 매핑이 필요합니다.
- 사용자 수준 업데이트를 계정 수준 작업으로 변환하려면 복잡한 [!DNL Marketo] 프로그램 논리가 필요할 수 있습니다.

**Experience League:**

- [Marketo Engage 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [Marketo Engage 대상에 대상 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage#activate)

### 옵션 B: 광고 플랫폼에 대한 대상자 일괄 활성화

**최적의 용도:** 매일 대상자를 새로 고칠 수 있는 [!DNL LinkedIn], 디스플레이 네트워크 또는 기타 광고 플랫폼에서 계정 기반 광고 캠페인을 사용하는 경우 기본 목표는 실시간 응답이 아닌 계정 수준 도달 및 인식입니다.

**작동 방식:**

이 옵션은 예약된 일괄 처리 케이던스에서 광고 플랫폼 대상([!DNL LinkedIn] 일치하는 대상, [!DNL Google] 고객 일치, [!DNL Facebook] 사용자 지정 대상 또는 [!DNL The Trade Desk])에 대한 계정 대상을 활성화합니다. 활성화 데이터 흐름은 광고 플랫폼이 사용자 기반과 일치시키기 위해 사용하는 매핑된 ID 필드(일반적으로 연결된 연락처의 해시된 이메일 주소)를 사용하여 계정 대상자 구성원을 내보냅니다.

[!DNL LinkedIn]의 경우 특히 [!DNL LinkedIn] 일치된 대상 대상은 전자 메일 기반 일치 외에 회사 이름 및 도메인 기반 일치를 허용하므로 실제 계정 수준 타깃팅을 사용할 수 있습니다. 다른 광고 플랫폼에서는 일반적으로 자격 계정과 연결된 연락처의 개인 수준 식별자(이메일, 전화)가 필요합니다.

배치 활성화는 구성 가능한 일정(매일, 6시간마다 등)에서 실행됩니다. 대상 유형에 따라 전체 대상 스냅샷 또는 증분 변경 사항을 내보냅니다. 이 접근 방식은 대상 신선도 요구 사항을 분 단위가 아닌 시간 단위로 측정하는 지속적인 인식 캠페인에 적합합니다.

**주요 고려 사항:**

- 대상자 신선도는 배치 일정에 따라 다릅니다(일반적으로 매일)
- Advertising 플랫폼에는 자체 일치율 제한이 있습니다
- [!DNL LinkedIn]은(는) 계정 수준 일치를 지원합니다. 다른 플랫폼에는 개인 수준 식별자가 필요합니다.
- 내보내기 파일 형식 및 ID 요구 사항은 대상에 따라 다릅니다

**장점:**

- 여러 광고 플랫폼을 동시에 지원
- 일괄 처리를 통해 대규모 대상 볼륨을 효율적으로 처리
- 계정 억제 대상을 통해 낭비되는 광고 비용 감소
- [!DNL LinkedIn]개의 일치하는 대상이 기본 계정 수준 타깃팅을 사용하도록 설정합니다.

**제한 사항:**

- 대상 업데이트는 실시간이 아닙니다. 지연 시간은 일괄 처리 일정에 따라 다릅니다
- 일치율은 플랫폼 및 사용 가능한 ID 필드에 따라 다릅니다
- 일부 플랫폼은 실제 계정 수준 일치를 지원하지 않으며, 개인 수준만 지원합니다
- 각 광고 플랫폼에 대해 별도의 대상 구성 필요

**Experience League:**

- [LinkedIn 일치하는 대상 대상 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Google Customer Match 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/google-customer-match)
- [대상 카탈로그](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)

### 옵션 C: 클라우드 스토리지에 대한 파일 기반 활성화

**최적의 용도:** CRM 가져오기, 데이터 웨어하우스 보강, 파트너 데이터 공유 또는 파일 기반 핸드오프를 선호하는 사용자 지정 통합을 포함하여 계정 대상을 다운스트림으로 사용하는 방법에 대한 유연성을 극대화해야 하는 조직

**작동 방식:**

이 옵션은 예약된 케이던스에서 계정 대상을 CSV, JSON 또는 Parquet 파일로 클라우드 저장소 대상([!DNL Amazon S3], [!DNL Azure Blob Storage], [!DNL Google Cloud Storage], SFTP)으로 내보냅니다. 내보내기에는 계정 속성, 연결된 연락처의 개인 수준 필드 및 대상 멤버십 메타데이터가 포함됩니다. 다운스트림 시스템은 자체 가져오기 프로세스를 통해 이러한 파일을 사용합니다.

파일 기반 활성화를 통해 내보내기 형식, 필드 선택 및 예약을 가장 잘 제어할 수 있습니다. 전체 내보내기(실행할 때마다 전체 대상 스냅샷)와 증분 내보내기(마지막 실행 이후의 변경 사항만)를 모두 지원합니다. 이 방법은 일반적으로 대상 시스템에 기본 [!DNL RT-CDP] 대상 커넥터가 없거나 조직에서 데이터를 대상 시스템으로 로드하기 전에 데이터를 사전 처리하거나 변환해야 하는 경우에 사용됩니다.

**주요 고려 사항:**

- 클라우드 스토리지 인프라([!DNL S3], [!DNL Azure Blob], [!DNL GCS] 또는 SFTP) 필요
- 다운스트림 가져오기 프로세스 구축 및 유지 관리
- 파일 형식(CSV, JSON, Parquet)은 다운스트림 시스템 요구 사항과 일치해야 합니다.
- 내보내기 예약은 다운스트림 처리 창과 일치해야 함

**장점:**

- 대상 데이터 사용 방식의 유연성 극대화
- 파일을 읽을 수 있는 모든 다운스트림 시스템 지원
- 내보내기 형식, 필드 및 예약에 대한 모든 권한
- 단일 내보내기에서 여러 다운스트림 소비자에게 제공 가능
- 전체 및 증분 내보내기 모드 지원

**제한 사항:**

- 모든 옵션 중 대기 시간이 가장 높음(일괄 처리만 해당)
- 다운스트림 가져오기 워크플로우 구축 및 유지 관리 필요
- 네이티브 통합 없음 — 추가적인 개발 노력 필요
- 파일 관리(정리, 보관)는 별도로 처리해야 함

**Experience League:**

- [Amazon 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)
- [Azure Blob 저장소 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/azure-blob)
- [일괄 처리 대상에 대상자 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/api/connect-activate-batch-destinations)

### 옵션 D: CRM 시스템으로 스트리밍 활성화

**영업 팀 가시성, 지역 할당 업데이트 또는 자동화된 영업 워크플로를 위해 거의 실시간으로 계정 자격 변경 내용이 CRM([!DNL Salesforce] 또는 [!DNL Dynamics])에 반영되어야 하는 영업 마케팅 정렬 사용 사례입니다.**

**작동 방식:**

이 옵션은 스트리밍 대상 커넥터([!DNL Salesforce] CRM, [!DNL Microsoft Dynamics])를 사용하여 계정 대상자 멤버십 변경 사항을 CRM 계정 또는 연락처 레코드로 직접 푸시합니다. 계정이 대상에 적합하거나 대상을 종료하면 CRM 레코드는 세그먼트 멤버십을 나타내는 사용자 지정 필드로 업데이트됩니다. 그런 다음 영업 팀이 이러한 필드를 기반으로 CRM 보고서, 보기 및 경고를 만들 수 있습니다.

스트리밍 커넥터는 대상 멤버십이 변경되면 증분 업데이트를 보냅니다. 필드 매핑은 [!DNL RT-CDP] 계정 및 사용자 특성을 CRM 필드에 연결하여 [!DNL RT-CDP]의 통합 데이터로 CRM 레코드를 보강합니다. 이 접근 방식은 마케팅 인텔리전스(계정 자격)와 판매 실행(CRM 워크플로우) 간의 루프를 닫습니다.

**주요 고려 사항:**

- 적절한 쓰기 권한이 있는 CRM API 액세스 필요
- 대상자 멤버십 데이터를 수신하려면 CRM 사용자 지정 필드를 만들어야 합니다.
- 스트리밍 볼륨은 CRM API 속도 제한 내에 있어야 합니다.
- CRM 워크플로 자동화는 필드 업데이트 시 작동하도록 구성해야 합니다.

**장점:**

- 영업팀 가시성을 위한 실시간에 가까운 CRM 업데이트
- 대상자 변경에 의해 트리거된 자동화된 CRM 워크플로 활성화
- [!DNL RT-CDP]의 통합 계정 데이터를 사용하여 CRM 레코드 강화
- 계정 수준 및 연락처 수준 필드 업데이트 모두 지원

**제한 사항:**

- CRM API 속도 제한으로 대량 업데이트가 조절될 수 있음
- CRM 사용자 지정 필요(사용자 지정 필드, 워크플로)
- 네이티브 커넥터로 [!DNL Salesforce] 및 [!DNL Microsoft Dynamics]&#x200B;(으)로 제한됨
- 스트리밍 평가 제한은 기본 대상에 적용됩니다.

**Experience League:**

- [Salesforce CRM 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Microsoft Dynamics 365 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/microsoft-dynamics-365)

### 옵션 비교

다음 표에서는 각 구현 옵션의 주요 특성을 비교합니다.

| 기준 | 옵션 A: [!DNL Marketo] 스트리밍 | 옵션 B: Advertising 일괄 처리 | 옵션 C: 클라우드 스토리지 | 옵션 D: CRM 스트리밍 |
| --- | --- | --- | --- | --- |
| 다음에 최적 | 육성 프로그램 활성화 | 계정 기반 광고 | 유연한 다운스트림 통합 | 영업-마케팅 정렬 |
| 복잡성 | 낮음 | 중간 | Medium 하이 | 중간 |
| 지연 | 거의 실시간으로(분) | 일괄 처리(시간) | 일괄 처리(시간) | 거의 실시간으로(분) |
| 유연성 | 낮음([!DNL Marketo]만) | Medium(광고 플랫폼) | 높음(모든 다운스트림 시스템) | 낮음(CRM만 해당) |
| 필요 | [!DNL Marketo Engage] 라이선스 | Advertising 플랫폼 계정 | 클라우드 스토리지 인프라 | CRM API 액세스 |
| 계정 수준 타기팅 | 개인 레코드를 통해 | [!DNL LinkedIn]만(기타 사용자 수준) | 구성 가능 | 계정/연락처 레코드를 통해 |
| 유지 관리 노력 | 낮음 | Low-Medium | 높음 | 중간 |

### 적절한 옵션 선택

다음 의사 결정 지침을 사용하여 올바른 활성화 접근 방식을 선택합니다.

1. **기본 목표가 B2B 리드 양육이고[!DNL Marketo Engage]**&#x200B;을(를) 사용하는 경우 옵션 A를 선택합니다. 기본 스트리밍 커넥터는 마케팅 자동화 워크플로를 위한 가장 빠른 작업 시간을 제공합니다.

2. **계정 기반 인식 및 광고를 통한 수요 생성이 기본 목표인 경우** 옵션 B를 선택합니다. [!DNL LinkedIn] 일치하는 대상 은 가장 강력한 계정 수준 타깃팅을 제공합니다. 더 넓은 범위를 위해 다른 광고 플랫폼을 사용합니다.

3. **기본 [!DNL RT-CDP] 커넥터가 없는 시스템에 계정 대상자를 공급해야 하는 경우** 또는 데이터 형식 및 다운스트림 처리에 대한 최대 제어가 필요한 경우 옵션 C를 선택합니다. 이는 파트너 데이터 공유 또는 데이터 웨어하우스 강화를 위한 최적의 선택이기도 합니다.

4. **주요 목표가 마케팅 자격 계정의 판매 활성화 및 CRM 가시성이라면** 옵션 D를 선택하십시오. 이렇게 하면 거의 실시간으로 CRM 레코드를 업데이트하여 Marketing-to-Sales 전달 루프를 닫습니다.

대부분의 B2B 조직은 육성 프로그램용 옵션 A, [!DNL LinkedIn] 광고용 옵션 B, CRM 동기화용 옵션 D와 같은 여러 옵션을 동시에 구현합니다. 이러한 옵션은 함께 사용할 수 있습니다. 동일한 계정 대상자를 여러 대상에 동시에 활성화할 수 있습니다.

## 구현 단계

다음 단계에서는 이 사용 사례 패턴을 구현하기 위한 단계별 프로세스를 설명합니다.

### 1단계: 계정 프로필 보강

이 단계에서는 CRM, 마케팅 자동화 및 서드파티 소스의 데이터를 통합하여 통합 계정 프로필을 설정합니다.

**응용 프로그램 함수:** [!DNL RT-CDP] B2B: 계정 프로필 통합, [!DNL RT-CDP] B2B: B2B Id 확인

**구성할 내용:** 이 단계에서는 CRM, 마케팅 자동화 및 타사 소스의 데이터를 통합하여 통합 계정 프로필을 설정합니다. B2B ID 해결은 개인 수준 참여 데이터(이메일 열기, 웹 방문, 콘텐츠 다운로드)를 집계하여 계정 수준 대상 평가에 사용할 수 있도록 개인 대 계정 관계를 매핑합니다. 이 단계는 기본 함수 F2, F3 및 F4를 기반으로 하며, 이 함수는 이미 제자리에 있어야 합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 계정 식별자 전략**
>
>시스템에서 기본 계정 키로 사용되는 식별자는 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| CRM 계정 ID(예: [!DNL Salesforce] 계정 ID) | CRM은 계정의 기록 시스템입니다 | 가장 일반적인 접근 방식. [!DNL RT-CDP]과(와) CRM 간의 정렬을 확인합니다. 모든 소스 시스템에서 동일한 CRM 계정 ID를 참조하도록 합니다. |
>| 사용자 정의 계정 ID | 여러 CRM 인스턴스 또는 전용 계정 마스터 | 소스 시스템 ID와 표준 계정 ID 간의 매핑 레이어가 필요합니다. 유연성은 향상되지만 복잡성은 증가합니다. |
>| DUNS 번호 또는 도메인 | 타사 데이터 보강은 기본 계정 소스입니다. | 그래픽 데이터 공급자가 기본 소스일 때 유용합니다. 도메인 기반 해상도에 대한 유사 항목 일치가 필요할 수 있습니다. |

>[!NOTE]
>**결정: 개인-계정 관계 모델**
>
>사람(잠재 고객, 연락처)은 계정과 어떻게 연결되어 있습니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 일대일(각 사용자가 하나의 계정에 속함) | 깨끗한 CRM 데이터를 가진 간단한 B2B 모델 | 간단한 해결책. 중간 시장 B2B에 가장 일반적으로 사용됩니다. |
>| 다대다(사용자가 여러 계정에 속할 수 있음) | 복잡한 기업 관계, 컨설턴트 또는 파트너 네트워크 | [!DNL RT-CDP] B2B edition에서 기본적으로 지원합니다. 대상의 복잡성은 증가하지만 실제 관계를 정확하게 반영합니다. |

**UI 탐색:** 플랫폼 > 프로필 > 찾아보기(통합 계정 프로필 확인)

**키 구성 세부 정보:**

- B2B XDM 스키마(XDM 비즈니스 계정, XDM 비즈니스 사용자 계정)가 F2에서 제대로 작동하는지 확인합니다.
- CRM 및 [!DNL Marketo] 소스 커넥터가 F3에서 계정 및 개인 데이터를 수집 중인지 확인
- 개인-계정 관계가 F4의 ID 그래프에서 확인되는지 확인합니다.
- 샘플 계정 프로필을 검색하여 계정 프로필 완성도 검토

**Experience League 설명서:**

- [Real-Time CDP B2B edition 개요](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/overview#rtcdp-b2b)
- [Real-Time CDP의 B2B 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Marketo Engage 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Salesforce 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/crm/salesforce)

### 2단계: 계정 대상자 평가

이 단계에서는 계정 속성, 개인 속성 및 개인 활동 데이터의 조합을 사용하여 계정 수준 대상을 정의하고 평가합니다.

**응용 프로그램 함수:** [!DNL RT-CDP] B2B: 계정 대상 평가, [!DNL RT-CDP]: 대상 평가

**구성할 내용:** 이 단계에서는 계정 특성, 사용자 특성 및 사용자 활동 데이터의 조합을 사용하여 계정 수준 대상을 정의하고 평가합니다. [!DNL RT-CDP] B2B edition의 계정 대상을 사용하면 조직 구조 특성(업계, 수입, 직원 수)과 해당 계정과 연결된 사람들의 참여 행동을 기반으로 계정을 세그먼트화할 수 있습니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 대상 평가 방법**
>
>얼마나 빨리 계정 대상자 멤버십을 업데이트해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 일괄 처리 평가(일별) | 일별 케이던스, 파일 기반 활성화, 광고 플랫폼 대상자에서 새로 고침된 캠페인 대상자 | 대부분의 계정 대상자는 일괄 평가를 사용합니다. 계정 및 사용자 특성을 결합하는 복잡한 다중 엔티티 쿼리를 처리합니다. 일별 새로 고침이 허용되는 대부분의 B2B 사용 사례에 충분합니다. |
>| 스트리밍 평가 | 실시간에 가까운 자격이 필요한 [!DNL Marketo] 또는 CRM 활성화 | 계정 대상에는 제한된 스트리밍 자격 요건이 있습니다. 간단한 계정 속성 조건만 스트리밍 평가를 받을 수 있습니다. 개인 수준 행동 조건에는 일반적으로 일괄 처리가 필요합니다. |

>[!NOTE]
>**결정: 계정 대상 정의 접근 방식**
>
>계정 대상 기준을 어떻게 정의합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 계정 속성만 | 간단한 사진 타겟팅(업계, 수익, 지역) | 가장 빠른 구현. 계정 수준 데이터로 제한됩니다. 광범위한 타겟팅에 사용합니다. |
>| 계정 + 개인 속성 | 연결된 사람들이 특정 기준(직함, 부서)과 일치하는 계정 타겟팅 | 더 정밀한 타기팅. 초기 통계와 인구 통계 데이터를 결합합니다. |
>| 계정 + 개인 속성 + 개인 활동 | 참여 중인 연락처(이메일 열기, 웹 방문, 콘텐츠 다운로드)가 있는 계정 타겟팅 | 가장 강력하지만 가장 복잡합니다. F3의 동작 이벤트 데이터가 필요합니다. 일반적으로 일괄 처리 평가가 필요합니다. |
>| 대상자 구성 | 등급, 분할, 제외 또는 강화 작업이 필요한 복잡한 대상 논리 | 파생 계정 대상에 대해 시각적 대상 구성 캔버스를 사용합니다. 일괄 평가로 제한됩니다. |

>[!NOTE]
>**결정: 비표시 대상 전략**
>
>활성화에서 제외해야 하는 계정은 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 기존 고객 억제 | 신규 계정을 대상으로 하는 고객 확보 캠페인 | 활성 구독 또는 기회에 도달하지 않은 계정 제외 |
>| 활성 판매 주기 억제 | 활성 영업 활동에 관여하는 고객을 방해하지 않음 | 특정 단계 이상 영업 기회가 열려 있는 계정 제외 |
>| 최근 참여 비표시 | 최근에 연락한 계정의 과도한 메시지 방지 | 전환 확인 기간(예: 30일) 내에 관여하는 계정 제외 |
>| 제외 없음 | 자격을 갖춘 모든 계정을 대상으로 하는 브랜드 인지도 캠페인 | 신중하게 사용, 부적격 계정에 대한 비용 낭비 발생 가능 |

**UI 탐색:** 고객 > 대상 > 대상 만들기 > 규칙 빌드(대상 유형으로 계정 선택)

**키 구성 세부 정보:**

- 세그먼트 빌더에서 새 대상을 만들 때 대상 유형으로 &quot;계정&quot;을 선택합니다.
- 계정 속성은 세그먼트 빌더의 계정 섹션 아래에 표시됩니다(업계, 수익, 계정 상태)
- 사용자 특성 및 활동은 계정 대상자 빌더의 &quot;사용자&quot; 관계를 통해 추가할 수 있습니다
- 샌드박스에 대한 일괄 평가 일정이 없는 경우 이를 구성합니다.
- 타겟팅 대상자(포함할 계정)와 제외 대상자(제외할 계정)를 모두 만듭니다

**Experience League 설명서:**

- [계정 대상자](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/types/account-audiences)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [대상자 구성](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)

### 3단계: 대상 구성

이 단계에서는 계정 대상이 전달될 타겟 대상에 대한 인증된 연결을 설정합니다.

**응용 프로그램 함수:** [!DNL RT-CDP] B2B: 계정 대상 구성, [!DNL RT-CDP] B2B: [!DNL Marketo Engage] 통합, [!DNL RT-CDP]: 대상 구성

**구성할 내용:** 이 단계에서는 계정 대상이 전달될 대상 대상에 대한 인증된 연결을 설정합니다. 구성에는 카탈로그에서 대상 선택, 인증 자격 증명 제공, 계정 수준 및 사용자 수준 필드 매핑 구성, 내보내기 일정 설정 등이 포함됩니다. 각 대상 유형에는 고유한 요구 사항 및 기능이 있습니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 대상 선택**
>
>활성화된 계정 대상을 받을 대상은 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| [!DNL Marketo Engage] | B2B 리드 육성, 채점 및 캠페인 실행 | 기본 스트리밍 커넥터. 리드/연락처 레코드를 업데이트합니다. [!DNL Marketo] API 자격 증명(Munchkin ID, 클라이언트 ID, 클라이언트 암호)이 필요합니다. |
>| 일치하는 대상 [!DNL LinkedIn]명 | [!DNL LinkedIn]의 계정 기반 광고 | 계정 수준 타겟팅을 위해 회사 이름 및 도메인 일치를 지원합니다. 일괄 활성화. [!DNL LinkedIn] 캠페인 관리자 액세스 권한이 필요합니다. |
>| [!DNL Salesforce] CRM | 영업 지원 및 CRM 계정 목록 동기화 | 스트리밍 커넥터는 계정 또는 연락처 레코드를 업데이트합니다. 쓰기 권한이 있는 [!DNL Salesforce] API 액세스가 필요합니다. |
>| [!DNL Microsoft Dynamics 365] | [!DNL Dynamics] 기반 조직에 대한 영업 지원 | 스트리밍 커넥터. [!DNL Dynamics 365] API 액세스 권한이 필요합니다. |
>| 클라우드 저장소([!DNL S3], [!DNL Azure Blob], [!DNL GCS], SFTP) | 사용자 정의 통합, Data Warehouse, 파트너 공유 | 파일 기반 일괄 내보내기. 유연성을 최대화하지만 다운스트림 처리가 필요합니다. |
>| [!DNL Google] 고객 일치 | 광고 타깃팅 검색 및 표시 | 해시된 이메일을 통한 개인 수준 일치. 일괄 활성화. |
>| [!DNL The Trade Desk] | 프로그래밍 방식의 디스플레이 및 비디오 광고 | 사용자 수준 일치. 일괄 활성화. |

>[!NOTE]
>**결정: 필드 매핑 전략**
>
>어떤 계정 및 사용자 필드를 대상에 매핑해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| ID 필드만 | 일치하는 식별자만 필요한 Advertising 플랫폼 | 최소 데이터 전송. 대상이 이메일 또는 회사 도메인에서 일치합니다. |
>| ID + 핵심 계정 속성 | CRM 또는 계정 컨텍스트가 타깃팅을 개선하는 [!DNL Marketo] | 업계, 수익, 직원 수, 계정 계층을 포함합니다. 다운스트림 레코드 강화 |
>| 전체 속성 집합 | 클라우드 스토리지 또는 데이터 웨어하우스 내보내기 | 모든 관련 계정 및 개인 속성을 포함합니다. 최대 내보내기 페이로드. |

**UI 탐색:** 연결 > 대상 > 카탈로그 > 대상 검색 > 구성

**키 구성 세부 정보:**

- 대상 카탈로그로 이동하고 대상 대상을 선택합니다
- 대상 유형과 관련된 인증 자격 증명 제공
- [!DNL RT-CDP]개의 XDM 필드를 대상 필드에 연결하는 필드 매핑 구성
- [!DNL Marketo Engage]의 경우: Munchkin ID, 클라이언트 ID 및 클라이언트 암호를 제공하십시오.
- [!DNL LinkedIn]의 경우: OAuth를 통해 인증하고 [!DNL LinkedIn] 광고 계정을 선택합니다.
- 클라우드 스토리지의 경우: 버킷/컨테이너 이름, 경로, 파일 형식 및 자격 증명을 제공합니다.
- CRM의 경우: 인스턴스 URL, API 자격 증명 및 대상 오브젝트 유형(계정 또는 연락처)을 제공합니다.

**옵션이 나뉘는 위치:**

**옵션 A([!DNL Marketo Engage] 스트리밍)의 경우:**

대상 > 카탈로그 > Adobe > [!DNL Marketo Engage]&#x200B;(으)로 이동합니다. Munchkin ID 및 API 자격 증명을 구성합니다. [!DNL RT-CDP] ID 필드(전자 메일) 및 프로필 특성을 [!DNL Marketo] 리드 필드에 매핑합니다. 대상은 증분 스트리밍 업데이트를 자동으로 처리합니다.

**옵션 B(Advertising Platform 일괄 처리)의 경우:**

대상 > 카탈로그 > Advertising/소셜 > 플랫폼 선택으로 이동합니다. OAuth를 통해 권한을 부여합니다. 내보내기 일정을 구성합니다(권장: 일별). 해시된 이메일 식별자 및 지원되는 모든 일치 필드를 매핑합니다. [!DNL LinkedIn]의 경우 계정 수준 일치를 위해 회사 이름과 도메인 필드를 추가로 매핑합니다.

**옵션 C(클라우드 저장소 파일 기반)의 경우:**

대상 > 카탈로그 > 클라우드 스토리지 > 공급자 선택으로 이동합니다. 버킷/컨테이너, 파일 경로 템플릿 및 파일 형식(CSV, JSON 또는 Parquet)을 구성합니다. 내보내기 일정을 설정하고 전체 또는 증분 내보내기를 선택합니다. 원하는 모든 계정 및 사용자 속성 필드를 매핑합니다.

**옵션 D(CRM 스트리밍)의 경우:**

대상 > 카탈로그 > CRM으로 이동하고 [!DNL Salesforce] 또는 [!DNL Dynamics]을(를) 선택합니다. API 자격 증명 및 인스턴스 URL을 제공합니다. [!DNL RT-CDP] 필드를 CRM 계정 또는 연락처 필드에 매핑합니다. 대상 멤버십 데이터를 받으려면 CRM에 사용자 지정 필드가 있는지 확인하십시오.

**Experience League 설명서:**

- [대상 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)
- [대상 카탈로그](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/overview)
- [Marketo Engage 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/adobe/marketo-engage)
- [LinkedIn 일치하는 대상 대상 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin)
- [Salesforce CRM 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/crm/salesforce)
- [Amazon 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage/amazon-s3)

### 4단계: 대상자 활성화

이 단계에서는 평가된 계정 대상을 구성된 대상에 게시합니다.

**응용 프로그램 함수:** [!DNL RT-CDP] B2B: 계정 Audience Activation, [!DNL RT-CDP]: Audience Activation

**구성할 내용:** 이 단계에서는 평가된 계정 대상을 구성된 대상에 게시합니다. 활성화는 계정 대상(소스)을 외부 대상(타겟)에 연결하는 데이터 흐름을 만들고, 속성 매핑을 적용하고, 구성된 예약 또는 스트리밍 동작에 따라 내보내기를 시작합니다. 또한 부적격 계정을 활성화에서 제외하도록 제외 대상을 구성합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 내보내기 유형**
>
>활성화가 전체 대상 스냅샷을 내보내야 합니까, 아니면 증분 변경 사항만 내보내야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 증분 내보내기 | 다운스트림 시스템에서 델타를 처리하는 스트리밍 대상([!DNL Marketo], CRM) 또는 배치 대상 | 내보내기당 데이터 볼륨이 작습니다. 처리 속도 향상. 상태를 관리하려면 다운스트림 시스템이 필요합니다. 스트리밍 대상의 기본값 |
>| 전체 내보내기 | 다운스트림 시스템이 실행될 때마다 전체 대상자를 대체하는 배치 대상 | 데이터 볼륨은 커지지만 다운스트림 논리는 간단합니다. 다운스트림 시스템이 상태를 유지하지 않는 경우 유용합니다. 파일 기반 대상에 사용할 수 있습니다. |

>[!NOTE]
>**결정: 활성화 범위**
>
>대상당 몇 개의 대상을 활성화해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 데이터 흐름당 단일 대상 | 명확한 대상자 간 매핑을 통한 간편한 활성화 | 모니터링 및 문제 해결이 가장 쉽습니다. 한 대상자 실패는 다른 대상자에게 영향을 주지 않습니다. |
>| 데이터 흐름당 여러 대상 | 동일한 대상으로 이동하는 여러 관련 대상 | 대상 연결을 보다 효율적으로 사용할 수 있습니다. 모든 대상이 동일한 필드 매핑과 일정을 공유합니다. |

**UI 탐색:** 연결 > 대상 > 찾아보기 > 대상 선택 > 대상 활성화

**키 구성 세부 정보:**

- 대상 목록에서 대상 대상 선택
- 3단계에서 구성된 필드 매핑 검토 및 확인
- 배치 대상의 경우: 내보내기 일정(시간, 빈도)을 구성합니다.
- 스트리밍 대상의 경우: 구성 직후 활성화가 시작됩니다.
- 선택적으로 제외 기능을 사용하여 제외 대상 추가
- 초기 테스트 활성화 실행을 트리거하여 데이터 흐름의 유효성을 확인합니다

**옵션이 나뉘는 위치:**

**옵션 A([!DNL Marketo Engage] 스트리밍)의 경우:**

활성화할 계정 대상을 선택하십시오. 활성화가 즉시 스트리밍을 시작합니다. 리드/연락처 레코드가 세그먼트 멤버십 필드로 업데이트되고 있는지 [!DNL Marketo]에서 확인하십시오. 이러한 필드 변경 내용에 따라 트리거할 [!DNL Marketo] 스마트 캠페인을 구성하십시오.

**옵션 B(Advertising Platform 일괄 처리)의 경우:**

계정 대상을 선택하고 일별 내보내기 일정을 구성합니다. 첫 번째 내보내기가 완료되면, 광고 플랫폼에서 대상이 나타나고 채워진 멤버 수가 있는지 확인합니다. 플랫폼에서 초기 대상 파일을 처리할 수 있도록 24~48시간을 허용합니다.

**옵션 C(클라우드 저장소 파일 기반)의 경우:**

계정 대상을 선택하고 내보내기 일정 및 파일 형식을 구성합니다. 첫 번째 내보내기 후 파일이 대상 저장소 위치에 예상 형식 및 콘텐츠와 함께 표시되는지 확인합니다. 다운스트림 가져오기 프로세스가 내보낸 파일을 성공적으로 사용하는지 확인합니다.

**옵션 D(CRM 스트리밍)의 경우:**

활성화할 계정 대상을 선택하십시오. 활성화가 즉시 스트리밍을 시작합니다. CRM에서 계정 또는 연락처 레코드가 매핑된 필드로 업데이트되고 있는지 확인합니다. 업데이트된 필드에 작동하도록 CRM 보고서, 목록 보기 또는 워크플로 자동화를 구성합니다.

**Experience League 설명서:**

- [스트리밍 대상에 대상 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [일괄 처리 대상에 대상자 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [활성화 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- [대상 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/home)

### 5단계: 거버넌스 및 모니터링

이 단계에서는 계정 대상자 활성화가 데이터 거버넌스 정책 및 동의 환경 설정을 준수하고 진행 중인 활성화 데이터 흐름이 상태를 모니터링합니다.

**응용 프로그램 함수:** [!DNL RT-CDP] B2B: B2B 데이터 거버넌스, [!DNL RT-CDP]: 동의 및 거버넌스 적용

**구성할 내용:** 이 단계에서는 계정 대상자 활성화가 데이터 거버넌스 정책 및 동의 환경 설정을 준수하고 진행 중인 활성화 데이터 흐름이 상태를 모니터링하도록 합니다. B2B 데이터 거버넌스는 중요 계정 속성(매출, 서드파티 공급자의 직원 수)에 대한 제한을 시행하는 반면, 동의 적용은 개인 수준 통신이 옵트아웃 환경 설정을 준수하도록 합니다. 모니터링을 통해 활성화 데이터 흐름이 정상적으로 완료되고 있는지 확인합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 거버넌스 적용 수준**
>
>B2B 활성화를 위해 데이터 거버넌스를 얼마나 엄격하게 적용해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 전체 적용(위반 시 차단) | 중요한 데이터를 사용한 프로덕션 활성화 | 거버넌스 정책을 위반하는 모든 활성화를 방지합니다. 위반을 해결하기 위해 반복적인 필드 매핑 조정이 필요할 수 있습니다. |
>| 경고 및 진행 | 개발 또는 테스트 환경 | 활성화를 계속 진행할 수 있지만 경고를 기록합니다. 잠재적 문제를 식별하기 위해 초기 설정 중에 유용합니다. |

>[!NOTE]
>**결정: 접근 방식 모니터링**
>
>활성화 상태를 모니터링하려면 어떻게 해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 경고 기반 모니터링 | 오류를 신속하게 포착해야 하는 프로덕션 환경 | 대상 활성화 실패, 소스 흐름 실패 및 데이터 흐름 지연에 대한 경고를 구성합니다. 경고 구독 설정이 필요합니다. |
>| 수동 모니터링 | 개발 또는 낮은 볼륨 활성화 | 대상 UI에서 데이터 흐름 실행을 정기적으로 검토합니다. 오버헤드가 적지만 장애 감지 지연 위험이 있습니다. |
>| 모두 | 복잡한 다중 대상 활성화를 사용하는 프로덕션 환경 | 중요한 장애에 대한 경고와 트렌드에 대한 정기적인 대시보드 검토. 대부분의 B2B 구현에 권장됩니다. |

**UI 탐색:** 개인 정보 > 정책(거버넌스용), 연결 > 대상 > 찾아보기 > 대상 선택 > 데이터 흐름 실행(모니터링용)

**키 구성 세부 정보:**

- 제한된 속성이 포함된 B2B 데이터 세트에 데이터 사용 레이블 적용
- 대상 마케팅 액션에 대한 활성화를 평가하여 거버넌스 정책이 적용되는지 확인합니다.
- 대상 활성화 실패 및 소스 커넥터 실패에 대한 경고 구성
- 각 활성화 주기 후 데이터 흐름 실행 지표(내보낸 프로필, 실패한 레코드) 검토
- 라이선스 사용 대시보드 검토를 설정하여 권한에 대한 계정 프로필 볼륨을 추적합니다.

**Experience League 설명서:**

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [동의 및 환경 설정](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [대상 데이터 흐름 모니터링](https://experienceleague.adobe.com/en/docs/experience-platform/dataflows/ui/monitor-destinations)
- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [활성화 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)

## 구현 시 고려 사항

다음 섹션에서는 성공적인 구현을 위한 추가 지침을 제공합니다.

### 보호 기능 및 제한 사항

이 사용 사례 패턴에 적용되는 다음 플랫폼 보호 및 제한을 검토하십시오.

- 샌드박스당 계정 대상을 포함하여 최대 4,000개의 세그먼트 정의 — [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 계정 대상은 주로 일괄 처리 평가를 사용하여 평가됩니다. 스트리밍 자격은 간단한 계정 속성 조건으로 제한됩니다
- 대상 연결당 최대 100개의 데이터 흐름 — [대상 보호](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
- 배치 대상은 파일 세그먼트당 최대 5백만 개의 프로필을 내보냅니다.
- 스트리밍 대상에는 대상 파트너가 설정한 초당 처리량 제한(예: [!DNL Marketo] API 속도 제한)이 있습니다.
- 구성된 대상(대상 구성에서) 은 일괄 평가로 제한되며 스트리밍을 사용할 수 없습니다
- 대상 컴포지션 캔버스당 최대 10개의 컴포지션 블록
- [!DNL LinkedIn]개의 일치하는 대상을 활성화하려면 최소 대상 크기(일반적으로 구성원 300명)가 필요합니다.
- CRM 스트리밍 대상에는 CRM 공급자의 API 속도 제한(예: [!DNL Salesforce] 벌크 API 일일 제한)이 적용됩니다.
- [!DNL RT-CDP] B2B edition 라이선스가 비즈니스 계정 프로필의 총 수를 제어합니다. — [RT-CDP 제품 설명](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

### 일반적인 함정

이 사용 사례 패턴을 구현할 때 다음과 같은 일반적인 문제에 유의하십시오.

- **미완료 개인 대 계정 매핑:** 개인 레코드(잠재 고객, 연락처)가 B2B ID 확인을 통해 계정 레코드에 제대로 연결되어 있지 않으면 개인 특성이나 활동에 의존하는 계정 대상자가 자격 있는 계정을 과소 계산합니다. 계정 대상을 빌드하기 전에 F4에서 개인-계정 관계를 확인합니다.

- **부실 CRM 데이터로 인해 대상 드리프트가 발생하는 경우:** CRM 소스 커넥터가 정기적인 일정에서 실행되고 있지 않거나 자동으로 실패하는 경우 계정 특성(업계, 수익, 상태)이 부실 상태가 됩니다. 이로 인해 대상자는 더 이상 자격을 충족하지 않는 계정을 포함하거나 자격을 충족해야 하는 계정을 제외합니다. 소스 커넥터 데이터 흐름 상태를 모니터링합니다.

- **Advertising 플랫폼 일치율 예상:** 계정 대상을 [!DNL LinkedIn] 이외의 광고 플랫폼으로 활성화할 때 일치율은 자격 있는 계정과 연결된 연락처에 대해 유효한 개인 수준 식별자(해시된 이메일)가 있어야 합니다. 이메일 주소가 있는 연결된 연락처가 없는 계정은 일치하지 않습니다. 일치율을 모니터링하고 연락처 데이터를 보강하는 것을 고려합니다.

- **[!DNL Marketo]필드 매핑 정렬이 잘못되었습니다.** [!DNL Marketo Engage]&#x200B;(으)로 스트리밍할 때 [!DNL RT-CDP] 필드 매핑은 기존 [!DNL Marketo]개의 리드 또는 연락처 필드를 대상으로 해야 합니다. 매핑된 [!DNL Marketo] 필드가 없으면 자동으로 업데이트가 실패합니다. 대상을 구성하기 전에 [!DNL Marketo]에서 모든 대상 필드를 미리 만드십시오.

- **거버넌스 정책 차단 활성화:** 계정 특성 필드(특히 타사 그래픽 데이터)의 데이터 사용 레이블은 광고 대상으로 활성화할 때 거버넌스 위반을 트리거할 수 있습니다. 필요한 경우 필드 매핑을 활성화하고 조정하여 제한된 필드를 제외하기 전에 거버넌스 규정 준수를 평가합니다.

- **계정 및 개인 데이터를 일괄 처리 전용 평가와 결합하는 계정 대상자:** 개인 수준 동작 이벤트(예: &quot;지난 30일 동안 한 명 이상의 연락처가 이메일을 열람한 계정&quot;)를 참조하는 계정 대상자는 일괄 처리 평가가 필요합니다. 사용 사례에서 실시간 자격이 필요한 경우 이 제한으로 인해 예기치 않은 지연이 발생할 수 있습니다.

### 우수 사례

최적의 결과를 얻으려면 다음 권장 사항을 따르십시오.

- 복잡한 다중 속성 정의로 확장하기 전에 적은 수의 잘 정의된 계정 대상(ICP 계층, 업계 카테고리, 참여 계층)으로 시작합니다
- 기존 고객, 활성 기회 및 최근 참여 계정에 대한 전용 억제 대상을 만들어 낭비되는 지출과 채널 충돌을 방지합니다
- 대상자 구성을 사용하여 집계된 참여 점수에 계정을 순위를 매겨 계층화된 계정 대상자(높음/중간/낮음 참여)를 만듭니다
- 조정된 다중 채널 캠페인에 대해 동일한 계정 대상을 여러 대상에 동시에 활성화합니다(예: 광고의 경우 [!DNL LinkedIn], 이메일의 경우 [!DNL Marketo], 판매 가시성의 경우 CRM).
- 타겟팅 기준 및 의도한 채널을 포함하는 계정 대상에 대해 일관된 명명 규칙을 구현합니다(예: &quot;B2B_ICP_Enterprise_Tech_LinkedIn&quot; 또는 &quot;B2B_Suppression_ActiveOpps&quot;)
- 사용량이 적은 시간 동안 일괄 처리 활성화를 예약하여 다운스트림 시스템에 미치는 영향을 최소화하고 광고 플랫폼 처리 기간에 맞게 조정
- 초기 활성화 후 대상별 일치율을 모니터링하고 ID 필드 매핑을 반복하여 일치를 개선합니다
- [!DNL Marketo Engage]을(를) 사용하여 양방향 데이터 흐름 유지: [!DNL Marketo]에서 [!DNL RT-CDP]&#x200B;(원본 커넥터)로 참여 데이터를 수집하고 폐쇄 루프 시스템을 위해 대상을 [!DNL Marketo]&#x200B;(대상 커넥터)으로 다시 활성화합니다

### 절충안 결정

구현 결정을 내릴 때 다음 절충점을 고려하십시오.

>[!NOTE]
>**절충: 대상 새로 고침 대 평가 복잡성**
>
>계정 속성을 사용자 수준 행동 데이터와 결합하는 계정 대상은 가장 정확한 타겟팅을 제공하지만 일괄 평가(일일 새로 고침)로 제한됩니다. 계정 속성만 기반으로 하는 더 간단한 대상은 실시간에 가까운 업데이트를 통해 스트리밍 평가를 받을 자격이 있습니다.
>
>- **일괄 처리(복잡한 기준) 우대:** 정밀한 타겟팅, 그래픽 및 동작 신호 결합, 포괄적인 계정 점수 책정
>- **스트리밍(단순 기준) 우대:** 대상 업데이트 속도, 계정 변경 사항에 대한 실시간 응답, [!DNL Marketo] 및 CRM의 작업 시간 단축
>- **권장 사항:** 매일 새로 고침을 허용할 수 있는 기본 타깃팅 대상에 대해 일괄 처리 평가를 사용합니다(대부분의 B2B 사용 사례). 계정 상태 변경 또는 고가치 계정 경고와 같이 시간에 민감한 트리거에 대한 스트리밍 평가를 예약합니다.

>[!NOTE]
>**절충: 중앙 집중식 활성화와 대상별 대상 비교**
>
>단일 통합 계정 대상을 여러 대상에 활성화하거나 각 채널의 기능 및 요구 사항에 맞게 대상별 대상을 만들 수 있습니다.
>
>- **중앙 집중식 대상 선호:** 채널 전반의 일관성, 간단한 대상 관리, 통합 보고
>- **대상별 대상자는 다음과 같은 이점을 갖습니다.** 채널당 타깃팅이 최적화되었습니다(예: [!DNL Marketo]은(는) 리드 수준 세부 정보가 필요한 반면 [!DNL LinkedIn]은(는) 회사 수준 특성으로 인한 이점). 채널별 제외 규칙
>- **권장 사항:** 일관성을 위해 중앙 집중식 대상으로 시작한 다음 채널 요구 사항이 크게 차이 나는 경우에만(예: 광고와 이메일의 경우 서로 다른 제외 기간) 대상별 변형을 만듭니다.

>[!NOTE]
>**할인: 실시간 CRM 동기화와 일괄 처리 CRM 업데이트**
>
>CRM으로 스트리밍하면 즉시 판매 가시성이 제공되지만 CRM API 할당량을 사용합니다. 배치 파일 내보내기가 더 효율적이지만 지연이 발생합니다.
>
>- **스트리밍 CRM 동기화 우대:** 판매 응답, 즉시 계정 알림, 실시간 파이프라인 가시성
>- **일괄 CRM 업데이트 추가:** API 할당량 보존, 일괄 업데이트 효율성, CRM 데이터 로드 창 정렬
>- **권장 사항:** 우선 순위가 높은 계정 자격 변경(예: 계정이 &quot;판매 준비&quot; 계층으로 이동)에 스트리밍 CRM 동기화를 사용합니다. 월별 계정 채점 새로 고침 또는 영역 재지정 목록과 같은 대량 업데이트에 배치 파일 내보내기를 사용합니다.

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
