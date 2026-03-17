---
title: 대상에 대한 대상자 활성화
description: Adobe Real-Time CDP을 사용하여 타깃팅 또는 제외를 위해 대상 세그먼트를 평가하고 외부 대상에 게시하는 방법을 알아봅니다.
solution: Real-Time Customer Data Platform, Experience Platform
source-git-commit: b2e496eb521fc3dd3290fccdd9a8203384934b88
workflow-type: tm+mt
source-wordcount: '7005'
ht-degree: 1%

---


# 대상에 대한 대상자 활성화

이 안내서에서는 Adobe [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP)에서 외부 대상으로 대상을 활성화하는 데 필요한 전체 구현 참조를 제공합니다. 타겟 지정, 억제, 유사 모델링 또는 분석 강화를 위해 대상 세그먼트를 평가하고 광고 플랫폼, 클라우드 스토리지, CRM 시스템 또는 데이터 파트너에 게시해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

이 섹션에서는 절충 분석, 의사 결정 지침, UI 탐색 경로 및 Experience League 설명서 참조와 함께 실행 가능한 모든 구현 옵션을 제공합니다.

이 안내서에서는 대상 연결 구성 및 대상 게시를 통한 대상 세그먼트 정의 및 평가에서 활성화 상태 모니터링 및 거버넌스 규정 준수에 이르기까지 대상 활성화의 전체 라이프사이클을 다룹니다.

## 사용 사례 개요

조직은 외부 시스템에 대상 데이터를 전달하여 유료 미디어 캠페인을 강화하고, CRM 레코드를 보강하고, 파트너와 데이터를 공유하거나, 다운스트림 분석을 피드해야 합니다. Audience Activation to 대상은 RT-CDP의 기본 활성화 패턴입니다. 어떤 프로필이 타겟 대상에 적합한지 평가하고, 하나 이상의 외부 대상에 연결하고, 프로필 속성을 대상별 필드에 매핑하고, 다운스트림 소비를 위해 대상을 게시합니다.

이 패턴은 대상 데이터를 적절한 시간에 적절한 형식으로 외부 시스템에 가져오는 것이 목표일 때마다 적용됩니다. 메시지 게재, 현장 개인화 또는 분석은 포함되지 않습니다. RT-CDP 구현의 가장 일반적인 시작점이며 다른 패턴이 맨 위에 구성하는 빌딩 블록 역할을 합니다.

대표적인 이해 당사자로는 유료 미디어를 관리하는 디지털 마케팅 팀, 웨어하우스를 보강하는 데이터 팀, 캠페인을 위한 연락처 목록을 준비하는 CRM 팀, 아웃바운드 데이터 흐름에 대한 거버넌스 준수를 보장하는 개인 정보 보호 팀 등이 있습니다.

## 주요 비즈니스 목표

다음 비즈니스 목표는 이 사용 사례 패턴을 통해 해결됩니다.

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

| KPI | 설명 | 측정 지침 |
| --- | --- | --- |
| 고객 확보 비용(CAC) | 활성화된 대상을 통해 새 고객을 확보하는 데 드는 비용 | 활성화된 대상자에 속하는 총 미디어 지출/신규 고객 |
| 대상 일치율 | 대상에서 성공적으로 일치하는 활성화된 프로필의 비율 | 대상에서 일치하는 프로필 / RT-CDP에서 내보낸 프로필 |
| 억제 절감 | 기존 고객을 확보 캠페인에서 억제하여 미디어 비용 절감 | 예상 CPM x 억제된 대상 크기 |
| 활성화 게재율 | 대상에 성공적으로 전달된 프로필 비율 | 제공된 프로필 / 소스 대상의 프로필 |
| 활성화 시간 | 대상 정의에서 첫 번째 전달까지 경과된 시간 | 세그먼트 생성에서 처음 확인된 데이터 흐름 실행으로 측정 |
| 대상자 모집단 정확도 | 대상에서 예상 및 실제 대상 크기 정렬 | 대상 대상자 규모/RT-CDP 대상자 규모 |

## 사용 사례 패턴

**대상에 대한 Audience Activation** - 타깃팅 또는 제외를 위해 대상 세그먼트를 평가하고 외부 대상에 게시합니다.

**함수 체인:** 대상 평가 > 대상 구성 > Audience Activation > 모니터링

## 애플리케이션

- **Adobe [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP)** - 대상 평가, 대상 관리, 대상 활성화, 동의 및 거버넌스 적용
- **Adobe [!DNL Experience Platform]&#x200B;(AEP)** - 프로필 저장소, ID 서비스, 세그먼테이션 엔진, 데이터 거버넌스

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | RT-CDP 샌드박스가 프로비저닝되고 활성 상태입니다. 구현 역할에 할당된 대상 관리 및 활성화 권한. 대상 플랫폼에 사용할 수 있는 대상 계정 자격 증명입니다. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 프로필 스키마에는 대상 필드에 매핑될 속성(예: 이메일, 전화 번호, 해시된 식별자, 인구 통계 속성)이 포함되어야 합니다. 활발하게 데이터를 받는 데이터 세트에서 스키마를 프로필로 활성화할 수 있어야 합니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/home), [스키마 구성 기본 사항](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/schema/composition) |
| 데이터 소스 및 수집 | 가정 위치 | 대상 평가를 강화하는 프로필 데이터는 수집해야 하며 최신 상태여야 합니다. 일괄 처리 및/또는 스트리밍 수집 파이프라인이 작동 중입니다. 프로필 지원 데이터 세트로 데이터를 제공하는 웹 SDK, 소스 커넥터 또는 일괄 수집. | [소스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/home), [웹 SDK 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/home) |
| ID 및 프로필 구성 | 필수 | 대상 일치를 위한 ID 네임스페이스는 구성해야 합니다(예: Facebook 사용자 지정 대상을 위한 해시된 이메일, Google Ads 고객 일치). 병합 정책은 활성화에 필요한 모든 특성이 있는 통합 프로필을 생성해야 합니다. | [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home), [병합 정책 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/merge-policies/overview) |
| 대상 정의 및 세분화 | 필수 | 세그먼트 빌더, 대상 구성 또는 연결된 대상 구성을 사용하여 정의된 Target 대상입니다. 활성화 지연 요구 사항에 따라 선택한 평가 방법(일괄 처리, 스트리밍 또는 에지)입니다. 이 함수는 이 플랜의 단계 1에서 실행됩니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home), [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 라이프타임 값, 참여 점수 또는 성향 점수와 같은 계산된 속성은 대상 정밀도를 향상시키고 대상에 매핑할 데이터 보강 속성을 제공합니다. 대상이 값 기반 또는 점수 기반 대상 세분화의 이점을 얻을 때 특히 유용합니다. | [계산된 특성 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | 데이터 세트 및 프로필 만료 정책은 데이터의 최신 상태 및 규정 준수를 보장합니다. 동의 스키마 구성은 동의한 프로필만 활성화되도록 합니다. 외부 시스템으로 데이터를 내보낼 때 규정 준수에 매우 중요합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 거버넌스 레이블 및 정책은 제한된 데이터를 승인되지 않은 대상(예: 광고 플랫폼에 대한 PII, 데이터 파트너에 대한 중요한 세그먼트)으로 활성화하지 않습니다. 외부 서드파티 시스템에 대한 대상 활성화에 특히 중요합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home), [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview) |
| 모니터링 및 가시성 | 포함됨 | 활성화 모니터링은 기능 체인(5단계)의 일부입니다. 데이터 흐름 실행 모니터링, 게재 상태 경고, 대상자 모집단 추적 및 라이선스 사용량 가시성을 다룹니다. | [대상 데이터 흐름 모니터링](https://experienceleague.adobe.com/ko/docs/experience-platform/dataflows/ui/monitor-destinations), [경고 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/alerts/overview) |
| 보고 및 분석 | 추천 | CJA의 대상 활성화 효과 분석을 통해 활성화된 대상(예: 억제의 전환 상승도, 유사 대상의 ROAS)에 대한 성능을 측정할 수 있습니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Real-Time CDP]&#x200B;(RT-CDP)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 1단계: 대상 평가 | 일괄 처리, 스트리밍 또는 에지 평가 방법을 사용하여 대상 규칙을 정의하고 세그먼트 멤버십을 평가합니다 |
| 대상자 구성 | 1단계: 대상 평가 | 복잡한 대상 논리를 위해 강화, 등급 지정, 분할, 제외 및 조인 작업을 통해 파생 대상을 구성할 수 있습니다(선택 사항) |
| 대상 구성 | 2단계: 대상 구성 | 필드 매핑 및 예약 매개 변수를 사용하여 외부 대상에 대한 인증된 연결 구성 |
| Audience Activation | 3단계: Audience Activation | 속성 매핑 및 내보내기 일정을 사용하여 평가된 대상을 구성된 대상에 게시 |
| 동의 및 거버넌스 적용 | 4단계: 거버넌스 유효성 검사 | 외부 시스템에 대한 대상 활성화 전후에 동의 환경 설정 및 데이터 사용 정책 적용 |

## 필요 조건

- [ ] RT-CDP 라이선스가 대상 활성화 권한으로 활성 상태입니다.
- [ ] 대상 샌드박스가 프로비저닝되어 구현 팀에 액세스할 수 있습니다.
- [ ] 사용자 역할에는 대상 관리 및 대상 활성화 권한이 포함됩니다.
- [ 각 대상 대상에 대한 ] 인증 자격 증명을 사용할 수 있습니다(OAuth 토큰, API 키, S3 액세스 키 또는 서비스 계정 자격 증명).
- [ ] 프로필 스키마에 대상 필드에 매핑해야 하는 모든 특성이 포함되어 있습니다.
- [ 대상 일치에 필요한 ] ID 네임스페이스가 구성되어 있습니다(예: 해시된 이메일, 휴대폰, 장치 ID).
- [ ] 데이터 수집 파이프라인이 작동 중이고 프로필이 프로필 저장소를 채우는 중입니다.
- [ ] 데이터 거버넌스 레이블 및 정책을 활성화할 특성(특히 외부 대상에 대해)에 대해 검토합니다.
- [ 동의 기반 필터링이 필요한 경우 ] 동의 필드가 프로필에 채워집니다

## 구현 옵션

이 사용 사례 패턴에는 다음 구현 옵션을 사용할 수 있습니다. 각 옵션과 비교 테이블을 검토하여 요구 사항에 가장 적합한 접근 방식을 결정하십시오.

### 옵션 A: 스트리밍 대상 활성화

**최적의 대상:** Facebook 사용자 지정 대상, Google Ads 고객 일치, LinkedIn 일치 대상, Trade Desk 및 유사한 스트리밍 API 기반 대상 등 광고 플랫폼 또는 파트너 시스템에 대한 실시간 대상 멤버십 업데이트.

**작동 방식:**

스트리밍 대상 활성화는 프로필이 세그먼트에서 자격을 부여하거나 자격을 박탈할 때 거의 실시간으로 대상에 대상 멤버십을 변경합니다. 프로필 속성이 변경되거나 프로필이 대상자를 입력하거나 종료하는 행동 이벤트가 발생하면 몇 분 내에 멤버 자격 업데이트가 대상으로 스트리밍됩니다.

이 접근 방법에는 스트리밍 대상 커넥터(대부분의 주요 광고 플랫폼이 이를 지원)와 스트리밍 또는 에지 대상 평가 방법이 필요합니다. 대상 평가는 자격 프로필 변경을 지속적으로 모니터링하고 업데이트 발생 시 활성화 데이터 흐름이 업데이트를 푸시합니다. 대상이 전체 대상 스냅샷이 아닌 증분 멤버십 변경 사항을 수신합니다.

스트리밍 활성화는 RT-CDP 카탈로그의 대부분의 광고 플랫폼 대상에 대한 기본값입니다. 대상 커넥터는 API 인증, 속도 제한 및 재시도 로직을 자동으로 처리합니다.

**주요 고려 사항:**

- 대상 평가는 스트리밍 또는 에지 평가를 사용해야 합니다(배치 전용 대상은 실시간으로 스트리밍 대상을 제공할 수 없음)
- 모든 세그먼트 표현식이 스트리밍 평가를 위한 것은 아닙니다. 복잡한 집계, 다중 엔티티 쿼리 및 특정 시간 기반 함수에는 일괄 처리가 필요합니다
- 대상 파트너 API 속도 제한은 대규모 대상 자격 이벤트 동안 처리량에 영향을 줄 수 있습니다
- 프로필 속성 업데이트는 멤버 자격 변경과 함께 전송되며 대상 데이터를 최신 상태로 유지합니다

**장점:**

- 대상의 거의 실시간 대상 새로 고침(시간이 아닌 분)
- 증분 업데이트는 전체 내보내기에 비해 데이터 전송 볼륨을 줄입니다.
- 자격 및 자격 박탈 이벤트 자동 처리
- 대부분의 광고 플랫폼 대상은 기본적으로 스트리밍을 지원합니다

**제한 사항:**

- 스트리밍 가능 세그먼트 정의 필요(제한된 세그먼트 기능 세트)
- 파일 형식이나 내보내기 구조를 제어할 수 없음 - 대상 커넥터에서 결정하는 데이터 형식
- 파일 기반 스토리지 대상(S3, Azure Blob, SFTP)으로 내보낼 수 없음
- 대상 API 속도 제한으로 대용량 변경 사항이 조절될 수 있음

**Experience League:**

- [스트리밍 대상에 대상 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [스트리밍 대상 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/overview)

### 옵션 B: 배치 대상 활성화(파일 내보내기)

**최적의 대상:** 파일 기반 가져오기를 사용하는 클라우드 저장소, 데이터 웨어하우스 또는 시스템(Amazon S3, Azure Blob 저장소, Google 클라우드 저장소, SFTP, 데이터 랜딩 영역)으로 예약된 대상을 내보냅니다.

**작동 방식:**

배치 대상 활성화는 예약된 케이던스에서 대상을 평가하고 결과를 구성된 저장소 대상에 파일(CSV, JSON 또는 Parquet)로 내보냅니다. 내보내기에는 전체 대상 스냅샷 또는 증분 변경 사항이 포함될 수 있습니다(마지막 내보내기 이후 새로운 자격 및 결격).

구현에는 스토리지 자격 증명, 파일 형식 환경 설정(구분 기호, 압축, 명명 규칙) 및 내보내기 일정(매일, 3시간마다, 6시간마다 등)을 사용하여 파일 기반 대상 연결을 구성하는 작업이 포함됩니다. 각 내보내기 실행은 대상 멤버십과 매핑된 프로필 속성을 포함하는 파일을 생성합니다.

파일 기반 데이터 교환이 보편적으로 지원되므로 가장 광범위한 다운스트림 고객을 지원합니다. 또한 클라우드 스토리지 및 데이터 웨어하우스 보강 사용 사례에 대한 유일한 옵션입니다.

**주요 고려 사항:**

- 대상 평가는 모든 방법(일괄 처리, 스트리밍 또는 에지)을 사용할 수 있습니다. 내보내기 자체는 에 관계없이 일정에 따라 실행됩니다
- 파일 형식, 압축 및 이름 지정 규칙은 대상별로 구성할 수 있습니다
- 증분 내보내기(변경만 해당) 및 전체 내보내기(전체 대상 스냅샷) 모두 지원
- 예약 세부기간 내보내기 범위는 매 3시간에서 일별로

**장점:**

- 내보내기 파일 형식(CSV, JSON, Parquet), 압축 및 이름 지정에 대한 모든 권한
- 파일을 사용할 수 있는 모든 다운스트림 시스템과 호환
- 증분 및 전체 내보내기 모드 모두 지원
- 모든 평가 방법(복잡한 세분화 논리를 사용하는 배치 전용 세그먼트 포함)으로 대상을 내보낼 수 있습니다
- 정규 일정 외에 애드혹(주문형) 내보내기 실행 지원

**제한 사항:**

- 지연 시간은 기본적으로 더 높음 — 대상 데이터가 실시간으로 도착하지 않고 일정에 따라 대상에 도착함
- 파일 기반 내보내기를 사용하려면 대상 시스템이 파일을 처리하고 수집해야 합니다
- 내보낸 파일의 대상 스토리지 비용
- 증분 스트리밍 업데이트와 비교하여 내보내기당 더 큰 데이터 볼륨

**Experience League:**

- [프로필 내보내기 대상을 일괄 처리하도록 대상자 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [파일 기반 대상 카탈로그](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/cloud-storage)

### 옵션 C: 다중 대상 활성화

**가장 좋은 방법:** 동일한 대상을 여러 대상으로 동시에 활성화(예: 모든 광고 플랫폼으로 억제 목록 푸시, CRM 및 광고 플랫폼 모두로 고가치 세그먼트 동기화 또는 여러 미디어 파트너 간 대상 도달 조정).

**작동 방식:**

다중 대상 활성화는 별도의 기술 메커니즘이 아니라 여러 대상 연결에서 동일한 대상에 적용되는 옵션 A와 B의 구성입니다. 동일한 대상이 각각 고유한 연결 구성, 필드 매핑 및 일정이 있는 둘 이상의 대상에 활성화됩니다.

각 대상 연결은 독립적으로 작동합니다. Facebook으로의 스트리밍 활성화와 S3으로의 일괄 내보내기는 동일한 소스 대상자에서 동시에 실행될 수 있습니다. 필드 매핑은 대상별로 구성되므로 각 대상에 필요한 사항과 거버넌스 정책이 허용하는 값에 따라 다른 시스템에 다른 속성을 보낼 수 있습니다.

이는 여러 광고 플랫폼에서 작동하거나, 미디어 활성화와 함께 CRM 동기화를 유지하거나, 대상 데이터를 운영 및 분석 시스템 모두에 배포해야 하는 조직에 일반적인 프로덕션 패턴입니다.

**주요 고려 사항:**

- 각 대상에는 독립적인 필드 매핑, 일정 조정 및 거버넌스 평가가 있습니다
- 거버넌스 정책은 대상마다 적용됩니다. 대상 유형마다 다른 속성을 사용할 수 있습니다.
- 단일 대상을 스트리밍 대상과 배치 대상을 동시에 혼합하여 활성화할 수 있습니다
- 새 대상을 추가해도 기존 활성화를 변경할 필요가 없습니다

**장점:**

- 단일 대상 정의에서 모든 외부 시스템에 걸쳐 조정된 대상 배포
- 대상별 독립적인 구성을 통해 최적화된 매핑 및 일정 허용
- 대상별 거버넌스 적용 을 통해 다양한 대상 유형 간의 규정 준수 보장
- 분산 활성화를 지원하면서 고객 관리를 중앙 집중화합니다.

**제한 사항:**

- 구성, 인증 및 유지 관리를 위한 추가 대상 연결
- 각 대상에 따라 모니터링 복잡성 증가 — 대상별로 활성화 실패를 추적해야 함
- 라이선스 사용량(활성화된 프로필)은 권한에 따라 대상별로 카운트될 수 있습니다
- 여러 대상 간의 필드 매핑 유지 관리에는 조정이 필요합니다.

**Experience League:**

- [대상 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/home)
- [대상 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/overview)

### 옵션 비교

| 기준 | 옵션 A: 스트리밍 | 옵션 B: 일괄 처리(파일 내보내기) | 옵션 C: 다중 대상 |
| --- | --- | --- | --- |
| 다음에 최적 | 실시간 광고 플랫폼 타기팅 및 억제 | 데이터 웨어하우스 보강, 파일 기반 시스템 통합 | 플랫폼 간 대상 배포 조정 |
| 복잡성 | 낮음 | 중간 | 높음 |
| 지연 | 분 (거의 실시간으로) | 시간(예약됨) | 대상당 시간 및 분 혼합 |
| 파일 형식 제어 | 없음(대상이 형식을 결정함) | 전체(CSV, JSON, Parquet, 압축, 이름 지정) | 대상별 |
| 대상 평가 | 스트리밍 또는 에지 필요 | 모든 방법(일괄 처리, 스트리밍, 에지) | 대상별 요구 사항 |
| 필요 | 스트리밍 대상 커넥터, 스트리밍 가능 세그먼트 | 파일 기반 대상 커넥터, 스토리지 자격 증명 | 여러 대상 커넥터 및 자격 증명 |
| 거버넌스 | 단일 대상 평가 | 단일 대상 평가 | 대상별 평가 |

### 적절한 옵션 선택

다음 의사 결정 논리를 사용하여 올바른 구현 접근 방식을 선택합니다.

1. **대상이 몇 개나 필요하십니까?** 둘 이상의 대상에 대해 동일한 대상을 활성화해야 하는 경우 대상별 옵션 A와 B를 구성하는 옵션 C를 구현합니다. 각 대상에 대해 질문 2와 3으로 진행합니다.

2. **대상이 스트리밍을 지원합니까?** 대상이 광고 플랫폼(Facebook, Google Ads, LinkedIn, The Trade Desk)이거나 스트리밍 API와 파트너 통합인 경우, 해당 대상에 대해 옵션 A를 사용하십시오. 대상이 클라우드 저장소(S3, Azure Blob, GCS, SFTP)이거나 파일을 사용하는 시스템인 경우 옵션 B를 사용합니다.

3. **대상자가 대상에 얼마나 빨리 도착해야 합니까?** 대상 멤버십이 몇 분 내에 대상에 반영되어야 하는 경우(예: 활성 캠페인 중 실시간 제외) 옵션 A를 사용합니다. 일별 또는 다중 시간별 게재가 충분한 경우(예: 주간 데이터 웨어하우스 새로 고침, CRM 일괄 동기화) 옵션 B를 사용합니다.

4. **대상자가 복잡한 세분화 논리를 사용합니까?** 대상 정의에 다중 이벤트 집계, 대규모 기간 또는 스트리밍 평가에 적합하지 않은 함수가 포함된 경우 옵션 B(배치 대상)를 사용하거나 옵션 A 대상도 일정에 따라 배치 평가를 받은 대상을 받도록 하십시오.

## 구현 단계

구현은 다음 단계를 따릅니다. 각 단계에는 구성 세부 사항, 의사 결정 지점 및 Experience League 설명서에 대한 링크가 포함되어 있습니다.

### 1단계: 대상 평가

**응용 프로그램 함수:** RT-CDP: 대상 평가, RT-CDP: 대상 구성

**구성할 내용:** 대상에 대해 활성화할 대상 대상을 정의합니다. 여기에는 대상 기준(프로필이 자격을 부여함) 지정, 평가 방법(멤버십 업데이트 속도) 선택 및 대상 모집단 유효성 검사가 포함됩니다. 이것은 모든 활성화의 시작점입니다. 정의되고 평가된 대상이 없으면 활성화할 내용이 없습니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 대상 만들기 방법**
>
>타겟 대상자를 어떻게 정의해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 세그먼트 빌더(규칙 기반) | 프로필 속성, 행동 이벤트 및 세그먼트 멤버십 조건을 사용하는 표준 대상 정의 | 가장 유연한 규칙 정의, 적합한 표현식에 대한 스트리밍 및 에지 평가 지원, 단일 조건 또는 적당히 복잡한 대상에 이상적 |
>| 대상자 구성 | 대상자는 기존 대상자를 결합, 순위 지정, 분할 또는 제외해야 합니다 | 순차적 작업에 대한 시각적 캔버스. 결과는 일괄 평가만 가능하며 캔버스당 최대 10개의 컴포지션 블록 |
>| 페더레이션 대상 구성 | 대상 기준은 AEP으로 수집하지 않고 외부 데이터 웨어하우스의 데이터에 대해 평가해야 합니다 | 외부 데이터베이스를 직접 쿼리하여 데이터 중복을 방지하고 Federated Audience Composition 라이센스가 필요합니다. |

>[!NOTE]
>
>**결정: 평가 메서드**
>
>프로필은 얼마나 빨리 대상자를 출입해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 일괄 처리 | 예약된 캠페인, 일일 대상자 새로 고침 또는 스트리밍에 적합하지 않은 복잡한 세분화 논리 | 작업당 최대 2,400만 개의 프로필을 처리합니다. 모든 세분화 기능이 지원됩니다. 일정에 따라 실행됩니다(일일 기본 또는 사용자 정의 크론 일정). |
>| 스트리밍 | 스트리밍 대상 활성화 또는 이벤트 트리거 사용 사례에 필요한 실시간 대상 멤버십 변경 | 거의 실시간으로(초~분), 제한된 세분화 기능 세트(간단한 이벤트, 속성 비교 및 제한된 시간 창만 해당), 다중 엔티티 쿼리 없음 |
>| Edge | 가장자리에 필요한 동일 페이지 개인화 또는 즉각적인 대상 자격 | 밀리초 지연, 가장 제한적인 규칙 세트 — 프로필 속성 및 간단한 세그먼트 멤버십 확인만 해당, 주로 온사이트 개인화에 사용됨(대상 활성화의 경우 덜 일반적임) |

>[!NOTE]
>
>**결정: 병합 정책**
>
>대상 평가는 어떤 병합 정책을 사용해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 타임스탬프 정렬(기본값) | 대부분의 사용 사례 — 프로필 조각이 충돌할 때 최근 데이터가 우선시되어야 합니다. | 가장 일반적으로, 가장 최근에 업데이트된 속성 값을 사용합니다. |
>| 데이터 세트 우선 순위 | 특정 데이터 소스는 타임스탬프에 관계없이 다른 데이터 소스를 재정의해야 함 | 데이터 세트 우선 순위 정의 필요. 레코드의 CRM 시스템이 항상 웹에서 수집한 데이터를 재정의해야 하는 경우 유용함 |

**UI 탐색:** 고객 > 대상 > 대상 만들기 > 규칙 빌드(세그먼트 빌더) 또는 대상 구성(대상 구성)

**키 구성 세부 정보:**

- 프로필 속성, 행동 이벤트, 세그먼트 멤버십 또는 시간 기반 조건 등 사용 사례에 따라 대상 기준을 정의합니다
- 활성화해서는 안 되는 프로필(예: 최근에 전환됨, 전체적으로 구독 취소됨)을 제외하려면 제외 규칙을 적용합니다
- 활성화를 진행하기 전에 대상자 모집단 크기 확인
- 평가 방법이 2단계에서 선택한 대상 유형에 맞는지 확인합니다.

**옵션이 나뉘는 위치:**

**옵션 A(스트리밍 대상 활성화)의 경우:**
대상자는 스트리밍 또는 에지 평가를 사용하여 실시간 멤버십 업데이트를 전달해야 합니다. 세그먼트 규칙 식이 스트리밍 평가에 적합한지 확인합니다. 시간 기반 집계 함수, 다중 엔티티 쿼리 및 일괄 처리 전용 세그먼트에 대한 `inSegment()` 참조를 사용하지 않도록 합니다.

**옵션 B(일괄 처리 대상 활성화)의 경우:**
모든 평가 방법이 적용됩니다. 내보내기 자체가 일정에 따라 실행되므로 배치 평가가 가장 일반적인 선택입니다. 샌드박스에 일괄 평가 일정이 있는지 확인하거나 일정을 만드십시오.

**옵션 C(다중 대상 활성화)의 경우:**
평가 방법은 가장 까다로운 목적지를 수용해야 한다. 스트리밍이 필요한 대상이 있으면 대상자는 스트리밍 평가를 사용해야 합니다. 모든 대상이 일괄 처리인 경우 일괄 처리로 평가하면 됩니다.

**Experience League 설명서:**

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language 참조](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/pql/overview)
- [스트리밍 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/edge-segmentation)
- [대상 구성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [평가 방법](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home#evaluation-methods)


### 2단계: 대상 구성

**응용 프로그램 함수:** RT-CDP: 대상 구성

**구성할 내용:** 대상자가 게시될 외부 대상에 대한 인증된 연결을 설정합니다. 여기에는 카탈로그에서 대상을 선택하고, 인증 자격 증명을 제공하고, 파일 형식, 저장소 위치 및 내보내기 예약과 같은 대상별 매개 변수를 구성하는 작업이 포함됩니다. 각 대상에는 자체 연결 구성이 필요합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 대상 유형**
>
>대상은 어디에서 전달되어야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| Advertising 대상(스트리밍) | 광고 플랫폼(Facebook, Google 광고, LinkedIn, Trade Desk 등)에서의 타겟팅 또는 억제 | 스트리밍 커넥터, 실시간에 가깝게 멤버십 업데이트, 해시된 이메일, 전화 또는 장치 ID를 통한 ID 일치 |
>| 클라우드 스토리지 대상(일괄 처리) | 데이터 웨어하우스 강화를 위해 S3, Azure Blob, GCS, SFTP 또는 데이터 랜딩 영역으로 내보내기 | 파일 기반 내보내기, 구성 가능한 형식(CSV, JSON, Parquet), 예약된 케이던스 |
>| CRM 대상 | 판매 활성화를 위해 대상을 Salesforce, Microsoft Dynamics 또는 HubSpot에 동기화 | 일반적으로 스트리밍, CRM별 필드 매핑 필요, CRM 관리자 권한이 필요할 수 있음 |
>| 데이터 파트너 대상 | 측정 또는 타겟팅 파트너와 대상 데이터 공유 | 파트너마다 다름, 외부에 데이터 공유에 대한 거버넌스 영향 검토 |
>| 사용자 지정 대상(Destination SDK) | 카탈로그에서 타겟 시스템을 사용할 수 없음 | Destination SDK을 사용하여 사용자 지정 대상을 작성해야 합니다. 더 높은 구현 노력 |

>[!NOTE]
>
>**결정: 인증 방법**
>
>대상에 필요한 자격 증명은 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| OAuth 2.0 | 광고 플랫폼 및 SaaS 대상(Facebook, Google, Salesforce) | 초기 인증 흐름 필요, 토큰이 자동으로 새로 고침, 스트리밍 대상의 경우 가장 일반적인 방법 |
>| 액세스 키/비밀 키 | 클라우드 저장소(S3, Azure Blob) | 정적 자격 증명, 순환을 계획해야 하며 파일 기반 대상에 적합함 |
>| 서비스 계정/API 키 | 파트너 API 및 사용자 정의 통합 | 대상 파트너의 자격 증명 프로비저닝 필요 |
>| 연결 문자열 | Azure 기반 대상 | 모든 연결 매개 변수를 포함하는 단일 문자열 |

>[!NOTE]
>
>**결정: 내보내기 유형(일괄 처리 대상만 해당)**
>
>내보내기를 위해 대상 데이터를 패키지하려면 어떻게 해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 증분 내보내기 | 마지막 수출 이후 새로운 자격 및 결격만 | 파일 크기가 작으며 대상 시스템에서 처리 속도 향상, 대상 시스템에서 상태 유지 필요 |
>| 전체 내보내기 | 실행할 때마다 대상 스냅샷 완료 | 파일이 클수록 대상자가 매번 전체 이미지를 가져오며, 전체 교체를 수행하는 시스템의 경우 단순함 |

**UI 탐색:** 연결 > 대상 > 카탈로그 > [대상 선택] > 구성

**키 구성 세부 정보:**

- 대상 카탈로그를 검색하고 대상 대상 선택
- 인증 자격 증명 제공 및 연결 테스트
- 배치 대상의 경우: 파일 형식(CSV, JSON, Parquet), 압축, 파일 이름 지정 템플릿 및 내보내기 일정 구성
- 스트리밍 대상의 경우: 일반적으로 OAuth 인증 흐름을 통해 연결이 설정됩니다.
- 활성화를 진행하기 전에 대상 연결 상태가 활성으로 표시되는지 확인하십시오.

**옵션이 나뉘는 위치:**

**옵션 A(스트리밍 대상 활성화)의 경우:**
카탈로그(Advertising 또는 소셜 범주)에서 스트리밍 대상을 선택합니다. OAuth 인증 흐름을 완료합니다. 인증이 확인되면 연결을 활성화할 준비가 되었습니다.

**옵션 B(일괄 처리 대상 활성화)의 경우:**
카탈로그(클라우드 스토리지 범주)에서 파일 기반 대상을 선택합니다. 스토리지 경로, 파일 형식, 압축, 명명 규칙 및 내보내기 일정을 구성합니다. 저장소 위치에 대한 쓰기 액세스를 확인하여 연결을 테스트합니다.

**옵션 C(다중 대상 활성화)의 경우:**
각 대상에 대해 이 단계를 반복합니다. 각 연결은 독립적입니다. 즉, 스트리밍 대상과 배치 대상이 혼용되어 있을 수 있습니다. 작동 참조를 위해 각 연결의 인증 및 구성을 문서화합니다.

**Experience League 설명서:**

- [대상 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/overview)
- [대상 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/home)
- [프로필 내보내기 대상을 일괄 처리하도록 대상자 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [스트리밍 대상에 대상 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [Destination SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/overview)
- [Destination SDK 구성 옵션](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/configuration-options)


### 3단계: 대상자 활성화

**응용 프로그램 함수:** RT-CDP: Audience Activation

**구성할 내용:** 활성화 데이터 흐름을 만들어 평가된 대상을 구성된 대상에 게시합니다. 여기에는 활성화할 대상을 선택하고, 프로필 속성을 대상 필드에 매핑하고, 내보내기 일정을 구성하는 작업이 포함됩니다. 활성화 데이터 흐름은 소스 대상자를 타겟 대상에 연결하고 지속적인 데이터 전달을 관리합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 특성 매핑**
>
>활성화에는 어떤 프로필 속성을 포함해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| ID 필드만 | 대상은 프로필과 일치해야 합니다(예: 광고 플랫폼의 대상 멤버십). | 최소 데이터 전송, 가장 안전한 개인 정보 보호, 광고 플랫폼 타깃팅 및 억제에 일반적인 기능 |
>| ID + 프로필 속성 | 대상에는 개인화 또는 세분화를 위한 데이터 보강 속성(예: CRM 동기화, 파트너 공유)이 필요합니다. | 더 많은 데이터가 전송됨, 각 속성에 대한 거버넌스 검토 필요, 대상 마케팅 액션에 대해 데이터 사용 레이블 확인 |
>| ID + 계산된 속성 | 파생 점수 또는 집계로 인한 대상 이점(예: 라이프타임 값 계층, 파트너 타겟팅에 대한 성향 점수) | 구성을 위해 계산된 속성 필요, 다운스트림 시스템에 대한 높은 가치 향상 |

>[!NOTE]
>
>**결정: 내보내기 예약(일괄 처리 대상만 해당)**
>
>대상 데이터는 얼마나 자주 내보내야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 매일 | 표준 새로 고침 케이던스, 대부분의 일괄 사용 사례 | 신선도와 처리 비용의 균형을 맞춥니다. 가장 일반적인 기본값 |
>| 3-6시간마다 | 당일 캠페인 최적화와 같은 빈도가 높은 사용 사례 | 파일 생성 빈도 증가, 대상 스토리지 및 처리 부하 증가 |
>| 온디맨드(애드혹) | 일회성 내보내기 또는 긴급 주기 외 활성화 | 수동 트리거는 일정을 무시하고 테스트나 긴급한 캠페인 요구에 유용 |

**UI 탐색:** 연결 > 대상 > 찾아보기 > [대상 선택] > 대상 활성화

**키 구성 세부 정보:**

- 대상에 대해 활성화할 대상을 하나 이상 선택하십시오.
- 프로필 속성 및 ID 필드를 대상별 필드에 매핑
- 스트리밍 대상의 경우: ID 네임스페이스 매핑 확인(예: Facebook의 extern_id에 대한 해시된 이메일)
- 배치 대상의 경우: 내보내기 일정을 구성하고 증분 또는 전체 내보내기 모드를 선택한 다음 첫 번째 내보내기 날짜를 설정합니다
- 게시 전에 활성화 요약을 검토하여 모든 매핑 및 일정을 확인하십시오.

**옵션이 나뉘는 위치:**

**옵션 A(스트리밍 대상 활성화)의 경우:**
대상을 선택하고 ID 네임스페이스를 대상 ID 필드에 매핑합니다. 활성화는 게시 즉시 시작되며, 대상자 멤버십은 거의 실시간으로 대상에 대한 스트림을 변경합니다. 내보내기 일정이 필요하지 않으며 활성화가 지속됩니다.

**옵션 B(일괄 처리 대상 활성화)의 경우:**
대상을 선택하고, 프로필 속성을 매핑하고, 내보내기 일정을 구성합니다. 증분 및 전체 내보내기 모드 중에서 선택합니다. 선택적으로 정규 스케줄 이외의 즉각적인 전달을 위해 임시 내보내기를 트리거합니다.

**옵션 C(다중 대상 활성화)의 경우:**
각 대상에 대해 활성화 워크플로우를 반복합니다. 대상별로 속성 매핑이 다른 여러 대상에 대해 동일한 대상을 활성화할 수 있습니다. 예를 들어 해시된 이메일만 광고 플랫폼에 보내고 CRM에 인구 통계학적 특성을 포함하십시오.

**Experience League 설명서:**

- [스트리밍 대상에 대상 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [프로필 내보내기 대상을 일괄 처리하도록 대상자 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [배치 대상에 대한 온디맨드 대상자 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [대상에 대한 데이터 흐름 모니터링](https://experienceleague.adobe.com/ko/docs/experience-platform/dataflows/ui/monitor-destinations)


### 4단계: 거버넌스 유효성 검사

**응용 프로그램 함수:** RT-CDP: 동의 및 거버넌스 적용

**구성할 내용:** 활성화 전후에 거버넌스 정책 및 동의 환경 설정이 올바르게 적용되는지 확인하십시오. 이 단계에서는 제한된 데이터(PII, 중요 속성)가 승인되지 않은 대상으로 전송되지 않고 유효한 동의가 없는 프로필이 활성화에서 제외되도록 합니다. 거버넌스 적용은 활성화 시 자동으로 발생하지만 사전 예방적 유효성 검사는 차단된 활성화 및 규정 준수 위반을 방지합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 거버넌스 적용 접근 방식**
>
>언제 거버넌스 규정 준수를 검증해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 사전 예방적(사전 활성화) | 모든 구현에 권장됨, 특히 외부 타사 시스템으로 활성화할 때 권장됨 | 필드 매핑을 구성하기 전에 데이터 사용 레이블 및 정책을 검토하십시오. 활성화 실패를 방지하고 처음부터 규정을 준수하십시오. |
>| 반응(활성화 시) | 거버넌스 정책이 이미 잘 수립되어 있고 팀이 규정 준수에 자신 있는 경우 | Platform은 활성화 시 정책을 자동으로 시행합니다. 위반은 활성화를 차단하거나 제한된 속성을 제외합니다. 정책이 잘 이해되지 않을 경우 예기치 않은 오류가 발생할 수 있습니다 |

>[!NOTE]
>
>**결정: 동의 필터링**
>
>동의 환경 설정이 활성화에 어떤 영향을 미칩니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 동의 적용 활성화됨 | 법적으로 동의가 필요한 광고 또는 마케팅 대상을 활성화할 때 필요합니다. | 유효한 동의가 없는 프로필(consents.marketing.{channel}.val = &#39;y&#39;)은 활성화에서 자동으로 제외됩니다. 동의 데이터를 수집해야 합니다. |
>| 동의 필터링 없음 | 동의가 데이터 전송에 적용되지 않는 내부 사용 대상 또는 분석 내보내기 | 데이터 사용이 동의를 필요로 하는 마케팅 조치를 구성하지 않는 경우에만 적합합니다. 법률/개인정보 보호팀에 문의하십시오. |

**UI 탐색:** 개인 정보 보호 > 정책 > 동의 정책(동의 검토용); 데이터 거버넌스 > 정책(데이터 사용 정책 검토용)

**키 구성 세부 정보:**

- 활성화 중인 데이터 세트 및 스키마 필드에 적용된 데이터 사용 레이블 검토
- 거버넌스 정책이 대상과 연결된 마케팅 작업에 대해 활성 상태인지 확인합니다(예: 광고 플랫폼의 경우 &quot;서드파티로 내보내기&quot;).
- 동의 필드가 프로필에 채워지고 관련 채널에 대해 동의 시행이 활성화되었는지 확인합니다
- 정책 위반이 감지되면 대상 매핑에서 제한된 필드를 제거하거나 대체 대상을 선택하여 해결합니다

**Experience League 설명서:**

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home)
- [정책 시행](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/enforcement/overview)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [동의 및 환경 설정](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/consent/adobe/overview)
- [동의 정책 시행](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/policies/user-guide)


### 5단계: 모니터링 및 유효성 검사

**응용 프로그램 함수:** 모니터링 및 관찰 가능성

**구성할 내용:** 활성화 데이터 흐름에 대한 지속적인 모니터링을 설정하고, 오류에 대한 경고를 구성하고, 대상에서 대상 모집단을 확인하고, 라이선스 사용량을 추적합니다. 게재 실패가 캠페인 성과 및 미디어 지출에 직접적인 영향을 미치는 프로덕션 활성화에는 모니터링이 중요합니다.

**키 구성 세부 정보:**

- 각 활성 대상에 대한 데이터 흐름 실행 상태를 검토하여 대상이 정상적으로 전달되는지 확인하십시오
- 대상 활성화 실패, 데이터 흐름 지연 및 대상 모집단 이상에 대한 경고 구성
- 내보낸 프로필과 데이터 흐름 실행당 실패한 프로필 추적
- 대상(대상 보고를 사용할 수 있는 곳)에서 대상 일치율 모니터링
- 라이선스 사용을 검토하여 사용 권한에 대해 활성화된 프로필 볼륨을 추적하십시오.

**UI 탐색:** 연결 > 대상 > 찾아보기 > [대상 선택] > 데이터 흐름 실행(활성화 모니터링용), 경고 > 경고 규칙 > 가입(경고 구성용), 관리 > 라이선스 사용(라이선스 추적용)

**Experience League 설명서:**

- [대상에 대한 데이터 흐름 모니터링](https://experienceleague.adobe.com/ko/docs/experience-platform/dataflows/ui/monitor-destinations)
- [경고 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/alerts/overview)
- [Observability Insights 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/home)
- [라이선스 사용 대시보드](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/license-usage-dashboard)

## 구현 시 고려 사항

구현 전 및 구현 중에 다음 고려 사항을 검토하십시오.

### 보호 기능 및 제한 사항

- **세그먼트 정의 제한:** 샌드박스당 최대 4,000개의 세그먼트 정의 — [세그먼테이션 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)
- 대상당 **데이터 흐름:** 대상 연결당 최대 데이터 흐름 수: [대상 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/guardrails)
- **일괄 내보내기 파일 크기:** 파일 기반 대상에 최대 내보내기 파일 크기 제한이 있습니다. 큰 대상은 자동으로 여러 파일로 분할됩니다
- **스트리밍 대상 처리량:** 초당 처리량 제한은 각 대상 파트너에 의해 설정되며, 대량 대상 변경은 조절될 수 있습니다
- **일괄 처리 평가 용량:** 기본적으로 세그먼트 평가 작업당 최대 2,400만 개의 프로필
- **대상 구성:** 캔버스당 최대 10개의 구성 블록입니다. 구성된 대상은 일괄 평가만 됩니다.
- **ID 그래프:** 그래프당 최대 50개의 ID — [ID 서비스 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/guardrails)
- **연산 속성:** 샌드박스당 최대 25개의 연산 속성 — [연산 속성 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/overview#guardrails)
- **활성화 보호 개요:** [활성화 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/guardrails)

### 일반적인 함정

- **자격 없는 규칙 논리를 사용하는 스트리밍 세그먼트:** 복잡한 집계 함수 또는 다중 엔터티 쿼리가 있는 대상을 정의하고 스트리밍 평가를 예상합니다. 이러한 세그먼트는 자동으로 일괄 처리 평가로 대체되므로 예기치 않은 지연이 발생합니다. 예방: 대상자를 정의하기 전에 스트리밍 자격 요구 사항을 검토하십시오.

- **동의 필터링으로 인해 0개의 프로필을 내보냈습니다.** 대상자의 모든 프로필에 유효한 동의 값이 없으므로 활성화 시 대상자 전체가 필터링됩니다. 예방: 동의 데이터 수집이 작동 중인지 확인하고 활성화하기 전에 동의 필드가 채워져 있는지 확인합니다.

- **예기치 않게 활성화를 차단하는 거버넌스 정책:** 스키마 필드의 데이터 사용 레이블이 활성화를 방지하는 정책 위반을 트리거합니다. 예방: 필드 매핑을 구성하기 전에 사전 예방적으로 거버넌스 규정 준수 평가(4단계). 스키마에서 상속된 레이블을 검토합니다.

- **대상 자격 증명 만료:** OAuth 토큰 또는 API 키가 만료되어 즉시 경고 없이 활성화 오류가 발생합니다. 예방: 대상 활성화 실패에 대한 경고를 구성하고 자격 증명 순환 예약을 설정합니다.

- **일치하지 않는 ID 네임스페이스:** 활성화 매핑에서 구성된 ID 네임스페이스가 대상이 예상하는 ID 네임스페이스와 일치하지 않습니다(예: 대상에 SHA-256 해시된 이메일이 필요한 경우 일반 텍스트 이메일 보내기). 예방: 매핑을 구성하기 전에 필요한 ID 형식에 대한 대상 설명서를 검토하십시오.

- **내보내기 오류를 일으키는 필드 매핑 오류:** 프로필 특성을 호환되지 않는 데이터 형식 또는 형식의 대상 필드에 매핑합니다. 예방: 프로덕션 대상으로 확장하기 전에 먼저 소규모 대상으로 활성화를 테스트하고 매핑 오류에 대한 데이터 흐름 실행 세부 정보를 검토하십시오.

- **RT-CDP와 대상 간의 대상 모집단 드리프트:** ID 일치 차이, 대상 중복 제거 논리 또는 타이밍으로 인해 RT-CDP의 대상자 규모가 대상의 카운트와 일치하지 않습니다. 이는 예상 동작 — 예방: 대상당 예상 일치율 벤치마크를 문서화하고 상당한 편차를 모니터링합니다.

### 우수 사례

- **테스트 대상으로 시작:** 프로덕션 대상을 활성화하기 전에 각 새 대상에 대해 잘 알고 있는 작은 테스트 대상을 활성화합니다. 테스트 대상을 사용하여 필드 매핑, ID 일치 및 게재 지표의 유효성을 검사합니다.

- **계층 구조 조기:** 대상 활성화를 구성하기 전에 데이터 사용 레이블을 적용하고 거버넌스 정책을 구성합니다. 이렇게 하면 차단된 활성화를 방지하고 처음부터 규정을 준수할 수 있습니다.

- **일괄 처리 대상에 증분 내보내기 사용:** 증분 내보내기를 사용하면 파일 크기가 줄어들고 대상에서 처리 속도가 빨라지며 저장소 비용이 최소화됩니다. 대상 시스템에 전체 대상 교체가 필요한 경우에만 전체 내보내기를 사용하십시오.

- **명명 규칙을 표준화합니다.** 조직 전체의 대상, 대상 연결 및 데이터 흐름에 대해 일관된 명명을 설정합니다. 이름에 사용 사례, 대상 및 평가 방법이 포함됩니다(예: &quot;Suppression_ExistingCustomers_Facebook_Streaming&quot;).

- **일치율 모니터링:** RT-CDP에서 내보낸 프로필과 각 대상에서 일치하는 프로필의 비율을 추적합니다. 일치율의 급격한 감소는 ID 해결 문제, 자격 증명 문제 또는 대상 API 변경을 나타낼 수 있습니다.

- **대상 간 억제 조정:** 억제 대상을 사용할 때(예: 획득 캠페인에서 기존 고객 제외) 일관성을 유지하기 위해 동시에 모든 관련 광고 플랫폼에 억제 대상을 활성화합니다.

- **비활성 활성화를 검토하고 정리합니다.** 대상 데이터 흐름을 정기적으로 검토하고 더 이상 필요하지 않은 대상을 비활성화합니다. 비활성 활성화는 라이선스 용량을 사용하고 모니터링 오버헤드를 추가합니다.

### 절충안 결정

>[!NOTE]
>
>**절충: 대상 새로 고침 대 세그먼테이션 유연성**
>
>스트리밍 평가는 거의 실시간 대상 업데이트를 제공하지만 사용할 수 있는 세그먼트 규칙 기능을 제한합니다. 일괄 처리 평가는 전체 세그먼트 규칙 함수 집합을 지원하지만 지연(분 대신 시간)을 도입합니다.
>
>- **스트리밍 선호:** 대상 멤버십이 몇 분 내에 대상에 반영되어야 하는 실시간 사용 사례(활성 캠페인 제외, 실시간 재타겟팅)
>- **일괄 처리 선호:** 집계 함수, 다중 엔터티 쿼리 또는 큰 기간 조건(수명 값 계층, 다중 터치 동작 세그먼트)이 필요한 복잡한 대상 논리입니다.
>- **권장 사항:** 실시간 신선도가 비즈니스 가치를 창출하는 스트리밍 대상으로 활성화된 대상에 대해 스트리밍 평가를 사용합니다. 파일 기반 대상으로 활성화되거나 매일 새로 고침으로 충분한 경우 복잡한 대상에 대해 배치 평가를 사용합니다. 두 가지 버전이 모두 필요한 대상의 경우 두 가지 버전, 즉 실시간 활성화를 위한 간소화된 스트리밍 세그먼트와 정기적인 강화를 위한 포괄적인 배치 세그먼트를 만드는 것이 좋습니다.

>[!NOTE]
>
>**트레이드 오프: 최소 데이터 내보내기와 서식 있는 특성 매핑**
>
>ID 필드(해시된 이메일, 디바이스 ID)만 내보내면 데이터 노출이 최소화되고 거버넌스가 단순화됩니다. 추가 프로필 속성(인구 통계, 가치 계층, 참여 점수)을 내보내면 대상이 풍부해지지만 거버넌스 복잡성 및 데이터 책임이 증가합니다.
>
>- **최소 내보내기 지원:** 개인 정보 우선 접근 방식, 낮은 거버넌스 위험, 간단한 필드 매핑, 대부분의 광고 플랫폼 타기팅 및 억제 사용 사례에 충분함
>- **풍부한 내보내기 지원:** 대상의 다운스트림 개인화, CRM 강화, 특성 수준 세부 정보가 필요한 파트너 데이터 공유
>- **권장 사항:** 기본적으로 광고 대상에 대한 최소 ID 전용 내보내기가 사용됩니다. 대상 사용 사례에서 프로필 속성을 특별히 요구하고 거버넌스 검토 결과 규정 준수가 확인된 경우에만 프로필 속성을 추가하십시오. 계산된 속성을 사용하여 원시 PII 대신 집계된 덜 민감한 데이터 보강 값을 제공합니다.

>[!NOTE]
>
>**절충: 대상당 단일 대상자와 통합된 다중 대상 데이터 흐름**
>
>각 대상을 별도의 데이터 흐름으로 활성화하면 격리 및 세분화된 모니터링이 제공됩니다. 대상으로의 단일 데이터 흐름을 통해 여러 대상을 활성화하면 관리가 간소화되지만 격리가 줄어듭니다.
>
>- **개별 데이터 흐름을 선호하는 경우:** 독립 모니터링, 간편한 문제 해결, 다른 사용자에게 영향을 주지 않고 개별 대상 활성화를 일시 중지하는 기능
>- **통합 데이터 흐름은 다음을 선호합니다.** 유지 관리를 위한 연결 수 감소, 간소화된 자격 증명 관리, 운영 오버헤드 감소
>- **권장 사항:** 동일한 대상에 대해 여러 관련 대상(예: Facebook에 대한 모든 제외 세그먼트)을 활성화할 때 통합된 데이터 흐름을 사용합니다. 대상에 SLA가 다르거나, 속성 매핑이 다르거나, 장애 격리가 중요한 경우에는 별도의 데이터 흐름을 사용하십시오.

## 관련 설명서

**대상**

- [대상 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/home)
- [대상 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/overview)
- [스트리밍 대상에 대상 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations)
- [프로필 내보내기 대상을 일괄 처리하도록 대상자 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [배치 대상에 대한 온디맨드 대상자 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/api/ad-hoc-activation-api)
- [대상 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/guardrails)
- [Destination SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/overview)

**대상 및 세분화**

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language 참조](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/pql/overview)
- [스트리밍 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/edge-segmentation)
- [대상 구성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [세그먼테이션 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)

**ID 및 프로필**

- [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [아이덴티티 그래프 연결 규칙](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/identity-linking-logic)
- [프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
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
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)

**관리**

- [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home)
- [액세스 제어 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/home)
- [속성 기반 액세스 제어](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/abac/overview)

**보호 기능**

- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/guardrails)
- [활성화 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
