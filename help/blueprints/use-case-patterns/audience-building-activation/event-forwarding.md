---
title: 이벤트 전달
description: Edge Network을 통해 수집된 실시간 이벤트 데이터를 분석, 저장 또는 광고를 위한 Adobe이 아닌 대상으로 전달하는 방법을 알아봅니다.
solution: Experience Platform
exl-id: 24964d27-db56-4fa4-a79f-1b6750564b34
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '6342'
ht-degree: 0%

---

# 이벤트 전달

이 안내서에서는 [!DNL Adobe Experience Platform] Edge Network을 사용하여 서버측 이벤트 전달을 구현하는 방법에 대해 설명합니다. Edge Network을 통해 수집된 실시간 이벤트 데이터를 타사 분석 플랫폼, 클라우드 스토리지 엔드포인트, 광고 네트워크 또는 사용자 지정 웹후크와 같은 Adobe이 아닌 대상에 배포해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

이벤트 전달을 구성하기 위한 모든 가능한 접근 방식을 제시하고, 이들 간의 장단점을 설명하며, 자세한 절차 지침을 위한 [!DNL Adobe Experience League] 설명서 링크를 제공합니다.

## 사용 사례 개요

[!DNL Adobe Experience Platform] Web SDK, Mobile SDK 또는 Server API를 통해 동작 데이터를 수집하는 조직은 종종 [!DNL Google Analytics] 또는 [!DNL Snowflake]과(와) 같은 분석 플랫폼, 전환 추적을 위한 광고 네트워크, 장기 저장을 위한 데이터 웨어하우스 또는 사용자 지정 내부 서비스 등 Adobe이 아닌 시스템과 동일한 이벤트 스트림을 공유해야 합니다. 일반적으로 이러한 클라이언트측 태그의 증가는 페이지 가중치를 높이고, 지연을 초래하며, 개인 정보 및 거버넌스 위험을 만듭니다.

이벤트 전달은 Edge Network에서 서버측을 운영하여 이 문제를 해결합니다. 방문자 상호 작용이 웹 SDK 또는 서버 API를 통해 이벤트를 트리거하면 해당 이벤트는 데이터 스트림을 통해 Edge Network으로 라우팅됩니다. 전용 이벤트 전달 속성에 구성된 이벤트 전달 규칙은 들어오는 이벤트 데이터를 평가하여 하나 이상의 구성된 대상에 선택적으로 전달합니다. 이 서버측 접근 방식은 클라이언트측 태그 증가를 줄이고, 페이지 성능을 개선하며, 데이터 거버넌스를 중앙 집중화하고, 조직이 Adobe 에코시스템에서 나가는 데이터를 정확하게 제어할 수 있도록 합니다.

이 패턴의 대상 대상에는 데이터 수집을 위해 [!DNL Adobe Experience Platform] Web SDK 또는 서버 API를 이미 배포했거나 배포할 계획이며 클라이언트측 JavaScript 태그를 추가하지 않고 이벤트 데이터를 Adobe이 아닌 끝점에 배포하여 해당 투자를 연장하려는 조직이 포함됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 데이터 품질 및 거버넌스 향상

정확하고 완벽하며 규정을 준수하는 데이터를 보장하여 정확한 타겟팅, 줄어든 낭비 및 안정적인 분석을 수행할 수 있습니다. 이벤트 전달은 서버측에서 데이터 배포를 중앙 집중화하여 조직에서 외부 시스템과 공유하는 데이터에 대한 단일 제어 지점을 제공하여 데이터 유출 위험을 줄이고 데이터가 [!DNL Adobe] Edge Network에서 나가기 전에 거버넌스 정책을 적용하도록 합니다.

**KPI:** 효율성, 비용 절감

자세한 내용은 [데이터 품질 및 거버넌스 개선](../../business-objectives/cost-efficiency/improve-data-quality-governance.md)을 참조하세요.

### 마케팅 기술 통합 및 현대화

확장성이 뛰어난 통합 플랫폼으로 마이그레이션하여 툴 조각화 및 기술적 부담 감소 이벤트 전달을 통해 조직은 여러 클라이언트측 공급업체 태그를 단일 서버측 데이터 배포 메커니즘으로 대체할 수 있으므로 페이지 로드 오버헤드가 줄어들고 기술 스택이 단순화됩니다.

**KPI:** 비용 절감, 효율성, 출시 속도

자세한 내용은 [마케팅 기술 통합 및 현대화](../../business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)를 참조하십시오.

## 예시 전술 사용 사례

다음은 이러한 사용 사례 패턴이 적용되는 일반적인 전술적 시나리오입니다.

- **타사 분석 데이터 보강** — 페이지 보기, 클릭 및 전환 이벤트를 클라이언트측 태그를 추가하지 않고 실시간으로 [!DNL Google Analytics], [!DNL Snowflake] 또는 다른 분석 플랫폼으로 전달합니다
- **Advertising 전환 추적** — 서버 측 전환 측정 및 최적화를 위해 구매 및 리드 생성 이벤트를 [!DNL Meta] 전환 API, [!DNL Google Ads], [!DNL TikTok] 또는 [!DNL Snap]&#x200B;(으)로 보냅니다.
- **Data Warehouse 스트리밍** — 장기 저장 및 오프라인 분석을 위해 원시 이벤트 데이터를 클라우드 데이터 웨어하우스([!DNL Google BigQuery], [!DNL Amazon S3], [!DNL Azure Event Hubs])로 라우팅합니다.
- **사용자 지정 웹후크 통합** - 필터링되거나 변환된 이벤트 데이터를 HTTP 끝점을 통해 내부 마이크로서비스, CRM 시스템 또는 파트너 플랫폼으로 전달합니다.
- **태그 감소 및 페이지 성능 개선** — 여러 클라이언트측 공급업체 JavaScript 태그를 단일 웹 SDK 구현 및 서버측 이벤트 전달 규칙으로 대체하여 페이지 가중치를 줄이고 Core Web Vitals을 개선합니다.
- **개인 정보 보호 준수 데이터 공유** — 이벤트 데이터를 서드파티와 공유하기 전에 데이터 필터링 및 필드 수준 교정 규칙을 서버측에서 적용하여, 외부 시스템에 도달하기 전에 PII가 제거되거나 해시되도록 합니다
- **다중 클라우드 이벤트 배포** — 동일한 이벤트 스트림을 단일 서버측 규칙 집합에서 여러 대상(예: 분석, 광고 및 데이터 웨어하우스)으로 동시에 전달합니다.
- **실시간 사기 신호 전달** - 실시간 위험 점수 및 알림을 위해 가치가 높은 트랜잭션 이벤트를 사기 탐지 시스템으로 전달합니다.

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 성공을 측정하는 데 도움이 됩니다.

- **페이지 로드 시간 감소** — 클라이언트측 태그를 서버측 이벤트 전달로 마이그레이션한 후 페이지 로드 속도와 Core Web Vitals이 개선되었습니다.
- **데이터 배달 성공률** — 오류나 시간 초과 없이 대상 끝점에 성공적으로 전달된 이벤트의 비율
- **태그 수 감소** — 서버측 해당 태그를 구현한 후 제거된 클라이언트측 공급업체 태그의 수
- **데이터 새로 고침/지연** — 클라이언트의 이벤트 발생과 대상 끝점의 이벤트 도착 사이의 시간(대상: 초~초)
- **거버넌스 준수율** — 서버측 필터링 규칙을 통과하는 아웃바운드 데이터 공유의 백분율로, PII 또는 제한된 데이터가 승인되지 않은 대상에 도달하지 않도록 합니다.
- **운영 효율성** — 개발자가 클라이언트측 태그 배포 관리 및 태그 충돌 문제 해결에 소요하는 시간 감소

## 사용 사례 패턴

이 섹션에서는 이벤트 전달을 구현하는 데 사용되는 패턴 및 기능 체인에 대해 설명합니다.

**이벤트 전달** - Edge Network을 통해 수집된 실시간 이벤트 데이터를 분석, 저장 또는 광고를 위한 Adobe 이외의 대상으로 전달합니다.

**함수 체인:** 데이터 스트림 구성 > 이벤트 규칙 정의 > 대상 매핑 > 전달 실행 > 모니터링

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Adobe Experience Platform] (Edge Network)** - 구성된 데이터스트림을 통해 Web SDK, Mobile SDK 또는 Server API에서 실시간 이벤트 데이터를 수신하고 라우팅합니다.
- **[!DNL Adobe Experience Platform] (이벤트 전달)** — 이벤트 데이터를 평가, 필터링, 변환 및 외부 대상으로 전달하기 위한 서버측 규칙 엔진을 제공합니다.
- **[!DNL Adobe Experience Platform] (태그/데이터 수집)** — 이벤트 전달 속성 라이프사이클, 확장, 규칙 및 게시 워크플로우를 관리합니다.

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 필수 | 샌드박스는 적절한 사용자 역할과 권한을 구성하여 활성화해야 합니다. 이벤트 전달을 관리하는 사용자에게는 이벤트 전달 속성, 확장 및 규칙을 관리할 수 있는 권한을 포함하여 [!DNL Adobe Admin Console]에서 데이터 수집 권한이 필요합니다. | [액세스 제어 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | Edge Network을 통해 흐르는 이벤트 데이터에 대해 XDM 스키마를 정의해야 합니다. 이벤트 전달 규칙이 필터링, 변환 및 매핑을 위한 구조화된 필드에 액세스할 수 있도록 데이터 스트림은 유효한 XDM ExperienceEvent 스키마를 참조해야 합니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/home) |
| 데이터 소스 및 수집 | 필수 | 구성된 데이터 스트림을 통해 이벤트를 전송하는 데이터 수집 메커니즘(웹 SDK, Mobile SDK 또는 Edge Network Server API)이 활성화되어 있어야 합니다. 데이터 스트림은 클라이언트측 컬렉션을 서버측 이벤트 전달에 연결하는 기본 라우팅 계층입니다. | [데이터스트림 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/configure) |
| ID 및 프로필 구성 | 해당 사항 없음 | 이벤트 전달은 ID 확인 또는 프로필 통합이 발생하기 전에 Edge Network 레이어의 원시 이벤트 데이터에 대해 작동합니다. 전달된 이벤트가 실시간 고객 프로필(이벤트 전달의 문제가 아닌 별도의 데이터스트림 서비스 구성)에도 기여해야 하는 경우가 아니면 ID 네임스페이스 및 병합 정책이 필요하지 않습니다. | |
| 대상 정의 및 세분화 | 해당 사항 없음 | 이벤트 전달은 개별 이벤트를 실시간으로 처리하며 대상 멤버십을 평가하지 않습니다. 대상 기반 필터링은 이벤트 전달 기능 체인의 일부가 아닙니다. 대상자 기반 활성화가 필요한 경우 대상 Audience Activation 참조 계획을 참조하십시오. | |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 해당 사항 없음 | 이벤트 전달은 프로필 수준의 계산된 속성이 아니라 원시 이벤트 데이터에서 작동합니다. 이벤트 전달 컨텍스트에서는 계산된 속성을 사용할 수 없습니다. | |
| 데이터 수명 주기 관리 | 추천 | 이벤트 데이터를 동일한 데이터 스트림을 통해 AEP 데이터 세트에도 수집하는 경우 스토리지 비용 및 규정 준수를 관리하기 위해 해당 데이터 세트에 대해 데이터 보존 정책(만료)을 구성해야 합니다. 이벤트 전달 자체는 데이터를 저장하지 않지만 병렬 AEP 수집 경로는 저장합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 이벤트 전달 규칙은 필드 수준 필터링을 제공하지만(전달된 페이로드에서 민감한 데이터를 제외할 수 있음), 데이터 사용 레이블을 기본 스키마 및 데이터 세트에 적용하면 동일한 데이터가 대상자 활성화 또는 개인화에 사용되는 경우 거버넌스 정책이 적용되도록 합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home) |
| 모니터링 및 가시성 | 포함됨 | 이벤트 전달에는 모니터링이 필수적입니다. 이벤트 전달 모니터링 대시보드는 전달 성공률, 오류율 및 대상 응답 코드에 대한 가시성을 제공합니다. 대상 실패에 대한 경고를 구성해야 합니다. | [이벤트 전달 모니터링](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/monitoring) |
| 보고 및 분석 | 추천 | 전달된 이벤트가 서드파티 분석 플랫폼을 제공하는 경우 통합 크로스 채널 보기를 위해 동일한 AEP 이벤트 데이터 세트를 CJA에 연결하는 것이 좋습니다. 이를 통해 Adobe 측과 서드파티 측 분석을 비교할 수 있습니다. | [CJA 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-overview/cja-overview) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Adobe Experience Platform]&#x200B;(AEP)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 데이터 스트림 구성 | 1단계: 데이터스트림 구성 | Edge Network 이벤트를 수신하고 이벤트 전달 서비스를 사용하도록 데이터스트림 구성 |
| 이벤트 전달 속성 설정 | 2단계: 이벤트 전달 속성 및 확장 | 이벤트 전달 속성을 만들고 대상별 확장을 설치합니다. |
| 이벤트 규칙 정의 | 3단계: 이벤트 규칙 정의 | 들어오는 이벤트 데이터를 평가하고 전달할 내용과 위치를 결정하는 규칙을 정의합니다. |
| 대상 매핑 | 3단계: 이벤트 규칙 정의 | 이벤트 데이터 요소를 전달 규칙 내의 대상별 페이로드 형식에 매핑 |
| 실행 전달 | 4단계: 게시 및 활성화 | 라이브 실행을 위해 Edge Network에 이벤트 전달 구성을 게시합니다. |
| 모니터링 | 5단계: 모니터링 및 유효성 검사 | 전달 성공률, 오류 코드 및 대상 상태 모니터링 |

## 필요 조건

구현을 시작하기 전에 다음 사항이 준비되었는지 확인하십시오.

- [ Edge Network 및 이벤트 전달 권한이 있는 ] [!DNL Adobe Experience Platform] 라이선스
- [ [!DNL Adobe Admin Console]에 구성된 ] 데이터 수집 권한(이벤트 전달을 위한 속성, 확장, 규칙 및 게시 관리)
- [ ] 데이터 스트림을 통해 이벤트를 전송하는 하나 이상의 활성 데이터 수집 메커니즘(웹 SDK, Mobile SDK 또는 서버 API)
- [ 수집 중인 이벤트 데이터에 대해 정의된 ] XDM ExperienceEvent 스키마
- [ ] 데이터 스트림을 만들어 컬렉션 메커니즘에 연결했습니다.
- [ ] 대상 끝점 자격 증명과 사용 가능한 설명서(예: [!DNL Meta] 전환 API 액세스 토큰, [!DNL Google Analytics] 측정 ID, 웹후크 URL, 클라우드 저장소 자격 증명)
- [ ] 이벤트 데이터 모델 및 각 대상에 필요한 필드/이벤트에 대한 이해

## 구현 옵션

이 섹션에서는 이벤트 전달을 구현하는 데 사용할 수 있는 방법에 대해 설명하고 올바른 옵션을 선택하는 방법에 대한 지침을 제공합니다.

### 옵션 A: 확장 기반 이벤트 전달

**잘 지원되는 대상 플랫폼([!DNL Meta], [!DNL Google], [!DNL AWS], [!DNL Azure], [!DNL Snowflake] 등)을 사용하는 팀:** 데이터 수집 카탈로그에서 사용 가능한 사전 빌드된 이벤트 전달 확장이 있습니다.

**작동 방식:**

확장 기반 이벤트 전달은 Adobe 또는 타사 파트너가 유지 관리하는 사전 설치된 통합을 활용합니다. 각 확장은 특정 대상을 위해 특별히 빌드되었으며 인증, 페이로드 형식 지정 및 끝점 통신을 처리합니다. 구현자는 이벤트 전달 속성에 확장을 설치하고, 인증 자격 증명을 구성하고, XDM 데이터 요소를 확장의 작업 필드에 매핑하는 규칙을 빌드합니다.

이 접근 방식은 확장이 대상의 API 요구 사항을 추출하므로 사용자 지정 개발을 최소화합니다. 예를 들어 [!DNL Meta] 전환 API 확장은 XDM 상거래 이벤트를 [!DNL Meta]에서 예상하는 형식으로 변환하여 PII 필드 해싱, 중복 제거 매개 변수 및 액세스 토큰 관리를 처리합니다. 마찬가지로 [!DNL Google Cloud Platform] 또는 [!DNL AWS] 확장 프로그램은 해당 클라우드 서비스에 대한 인증 및 페이로드 형식을 처리합니다.

장단점은 확장 가용성에 따라 지원되는 대상이 결정된다는 것입니다. 대상 대상에 대한 확장이 없는 경우 옵션 B(사용자 지정 웹후크)를 대신 사용해야 합니다.

**주요 고려 사항:**

- 확장 가용성은 다양합니다. 계획하기 전에 [데이터 수집 확장 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/overview)를 확인하십시오.
- 확장은 Adobe 또는 파트너에 의해 유지 관리됩니다. 업데이트는 규칙을 조정해야 하는 새로운 변경 사항을 도입할 수 있습니다
- 일부 확장은 특정 이벤트 유형만 지원하거나 특정 XDM 필드 매핑이 필요합니다
- 확장은 구성 UI 내에서 인증 및 자격 증명 관리를 처리합니다

**장점:**

- 지원되는 대상에 대한 가장 빠른 구현 시간
- 사전 설치된 페이로드 서식으로 매핑 오류 감소
- 확장에서 처리하는 인증 및 자격 증명 관리
- Adobe 또는 인증된 파트너가 유지 관리 및 업데이트
- 사용자 정의 코드 감소 및 유지 관리 부담 감소

**제한 사항:**

- 사용 가능한 확장이 있는 대상으로 제한됨
- 사용자 정의 웹후크에 비해 페이로드 사용자 정의 유연성 감소
- 확장 업데이트는 규칙을 재구성해야 할 수 있습니다.
- 일부 확장은 일부 대상 API 기능을 지원하지 않을 수 있습니다

**Experience League:**

- [이벤트 전달 확장 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/overview)
- [Meta 전환 API 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/meta/overview)
- [Google Cloud Platform 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [AWS 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/aws/overview)
- [Snowflake 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/snowflake/overview)

### 옵션 B: 사용자 지정 웹후크(API 가져오기) 이벤트 전달

**미리 빌드된 확장명 없이 이벤트를 대상으로 전달하거나 HTTP 요청 페이로드, 헤더 및 인증 메커니즘을 완벽하게 제어해야 하는 팀에 가장 적합합니다.**

**작동 방식:**

사용자 지정 Webhook 기반 이벤트 전달은 [!DNL Adobe Cloud Connector] 확장(기본적으로 포함됨)을 사용하여 임의의 끝점에 대해 임의의 HTTP 요청을 수행합니다. 구현자는 데이터 요소를 정의하여 들어오는 XDM 이벤트에서 값을 추출 및 변환한 다음 Cloud Connector의 &quot;가져오기 호출 만들기&quot; 작업 유형을 사용하여 규칙 작업을 구성합니다. 이 작업을 사용하면 HTTP 메서드, URL, 헤더 및 요청 본문을 완벽하게 제어할 수 있습니다.

요청 본문은 일반적으로 데이터 요소와 사용자 지정 코드를 사용하여 대상의 API 사양에 따라 페이로드 형식을 지정합니다. 이 접근 방식은 REST API, 웹후크, 클라우드 함수 또는 내부 서비스 등 HTTP 액세스 가능한 모든 끝점을 지원하므로 가장 유연한 옵션이 됩니다.

이러한 단점은 구현 노력 및 지속적인 유지 관리 수준을 높이는 것입니다. 구현자는 대상 API를 이해하고, 인증을 수동으로 처리(예: 인증 헤더 설정, 토큰 새로 고침 관리)해야 하며, 대상 API가 발전하는 경우 페이로드 형식을 유지해야 합니다.

**주요 고려 사항:**

- 대상 API 사양(HTTP 메서드, URL 구조, 페이로드 형식, 인증)에 대한 이해가 필요합니다.
- 인증 자격 증명은 데이터 요소 또는 비밀에서 수동으로 관리해야 합니다.
- 페이로드 변환(해시, 인코딩, 재구성)에 사용자 정의 코드가 필요할 수 있음
- 대상 API가 변경될 때 자동 업데이트가 없음 — 수동 유지 관리 필요
- 데이터 수집의 비밀 기능은 API 키 및 토큰을 안전하게 저장할 수 있습니다

**장점:**

- 모든 HTTP 액세스 가능 엔드포인트 지원 — 확장 종속성 없음
- 요청 페이로드, 헤더 및 인증에 대한 전체 제어
- 내부 서비스, 사용자 정의 API 또는 틈새 플랫폼으로 전달 가능
- 사용자 지정 코드를 사용하여 복잡한 페이로드 변환 사용
- 사용자 지정 코드 내에서 재시도 논리 및 오류 처리를 구현할 수 있음

**제한 사항:**

- 높은 초기 구현 노력
- 페이로드 형식 및 인증에 대한 지속적인 유지 관리 책임
- 사전 설치된 오류 처리 또는 자격 증명 회전 없음 — 수동으로 구현해야 함
- HTTP 프로토콜 및 대상 API 세부 사항에 대한 개발자 전문 지식 필요

**Experience League:**

- [Adobe Cloud Connector 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [이벤트 전달 비밀](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/secrets)

### 옵션 C: 하이브리드(확장 + 맞춤형 웹후크)

**최적의 용도:** 일부 조직에서는 확장이 미리 만들어져 있고 다른 조직에서는 사용자 지정 통합이 필요한 여러 대상으로 이벤트를 전달하는 조직입니다.

**작동 방식:**

하이브리드 접근 방식은 잘 지원되는 대상에 대한 확장 기반 전달과 확장이 부족한 대상에 대한 사용자 지정 웹후크 작업을 결합합니다. 단일 이벤트 전달 속성에는 여러 규칙이 포함됩니다. 일부는 확장 작업(예: 광고 전환 추적을 위해 [!DNL Meta] 전환 API 확장 사용)을 사용하고, 일부는 Cloud Connector 가져오기 작업(예: 내부 데이터 레이크 끝점으로 전달)을 사용합니다.

이 접근 방식은 불필요한 사용자 정의 개발을 최소화하면서 커버리지를 극대화합니다. 각 규칙은 독립적으로 작동하므로 확장 기반 규칙은 사전 설치된 페이로드 형식의 이점을 활용하며 사용자 지정 규칙은 유연성을 최대한 유지합니다.

**주요 고려 사항:**

- 규칙 및 대상 수가 증가하면 속성 복잡성이 증가합니다
- 테스트 및 디버깅에는 확장 기반 규칙과 사용자 지정 규칙에 대한 다양한 접근 방식이 필요할 수 있습니다
- 변경 사항 게시는 속성의 모든 규칙에 영향을 줍니다. 라이브러리와 환경을 사용하여 변경 사항을 안전하게 스테이징합니다
- 명확한 이름 지정 규칙을 사용하여 확장 기반과 사용자 지정 작업을 구별하는 규칙 구성을 고려해 보십시오

**장점:**

- 다양한 대상 유형에 대한 최상의 지원
- 사용 가능한 경우 사전 설치된 확장을 활용하여 수고 감소
- 사용자 지정 대상에 대한 유연성 유지
- 단일 이벤트 전달 속성이 모든 전달 논리를 관리합니다.

**제한 사항:**

- 여러 규칙 유형을 사용하는 경우 속성 복잡성 증가
- 혼합 유지 관리 모델 — 일부 규칙은 확장을 통해 자동 업데이트되고, 다른 규칙은 수동 유지 관리가 필요
- 디버깅을 사용하려면 확장 구성 및 사용자 지정 가져오기 호출 패턴 모두에 익숙해야 합니다

**Experience League:**

- [이벤트 전달 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/overview)
- [이벤트 전달 시작](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/getting-started)

### 옵션 비교

다음 표에서는 세 가지 구현 옵션을 비교합니다.

| 기준 | 옵션 A: 확장 기반 | 옵션 B: 사용자 지정 Webhook | 옵션 C: 하이브리드 |
| --- | --- | --- | --- |
| 다음에 최적 | 지원되는 대상([!DNL Meta], [!DNL Google], [!DNL AWS] 등) | 사용자 정의 엔드포인트, 틈새 플랫폼, 내부 서비스 | 혼합 지원을 사용하는 여러 대상 |
| 복잡성 | 낮음 | Medium 하이 | 중간 |
| 구현 시간 | 일 | 일-주 | 대상 혼합에 따라 다름 |
| 유연성 | 확장 기능으로 제한 | 전체 제어 | 필요한 경우 전체 제어 |
| 유지 관리 | 낮음(확장 관리) | 높음(수동 유지) | 혼합 |
| 필요 | 대상에 사용할 수 있는 확장 | 대상 API 설명서 | 두 가지 모두, 대상에 따라 다름 |
| 사용자 지정 코드 필요 | 최소 | 보통-중요 | 다양함 |

### 적절한 옵션 선택

먼저 대상 인벤토리를 작성하고 사전 빌드된 이벤트 전달 확장이 각각에 대해 존재하는지 확인합니다.

1. **모든 대상에 확장이 있는 경우** — 옵션 A를 선택합니다. 따라서 유지 관리 부담이 가장 적은 가장 빠른 구현이 가능합니다. 확장은 인증, 페이로드 서식 지정 및 API 버전 관리를 처리합니다.

2. **대상에 확장명이 없거나 전체 페이로드 제어가 필요한 경우** — 옵션 B를 선택합니다. Cloud Connector 확장을 사용하여 모든 끝점에 대한 사용자 지정 HTTP 요청을 만듭니다. 복잡한 변형, 사용자 지정 해싱 또는 내부 서비스로 전송해야 하는 경우에도 올바른 선택입니다.

3. **지원되는 대상과 지원되지 않는 대상을 혼합하여 사용하는 경우** — 옵션 C를 선택합니다. [!DNL Meta], [!DNL Google] 및 [!DNL AWS]과(와) 같은 플랫폼에 대한 확장 및 기타 모든 것에 대한 사용자 지정 웹후크를 사용합니다. 분석 및 광고 스택이 다양한 조직의 가장 일반적인 프로덕션 시나리오입니다.

## 구현 단계

다음 단계에서는 이벤트 전달을 위한 전체적인 구현 프로세스를 설명합니다.

### 1단계: 데이터스트림 구성

**응용 프로그램 함수:** AEP: 데이터 스트림 구성

**구성할 내용:** 웹 SDK, Mobile SDK 또는 Server API 구현에서 이벤트를 받고 이벤트 전달 규칙이 이벤트를 처리할 수 있는 Edge Network으로 라우팅하는 데이터 스트림입니다. 이벤트 전달이 기존 데이터 수집 배포에 추가되는 경우 기존 데이터 스트림에서 이벤트 전달을 활성화합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 새 데이터스트림과 기존 데이터스트림 비교**
>
>이벤트 전달을 위해 새 데이터스트림을 생성하거나 기존 데이터스트림에서 이벤트 전달을 활성화해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 기존 데이터 스트림 사용 | 데이터 스트림을 통해 이벤트를 전송하는 웹 SDK 또는 서버 API가 이미 있습니다. | 가장 일반적인 시나리오: 이벤트 전달은 데이터 스트림에서 추가 서비스로 간단히 활성화됩니다. 클라이언트측 변경이 필요하지 않습니다. |
>| 새 데이터 스트림 만들기 | 이는 기존 데이터 수집이 없는 녹색 필드 구현이거나 특정 이벤트 유형에 대해 별도의 데이터 흐름이 필요합니다 | 새 데이터 스트림 ID를 가리키도록 클라이언트측 SDK 구성이 필요합니다. 격리된 구성을 허용합니다. |

>[!NOTE]
>
>**결정: 이벤트 전달과 함께 활성화할 AEP 서비스**
>
>데이터스트림은 이벤트를 여러 AEP 서비스로 동시에 라우팅할 수 있습니다. 이벤트 전달은 하나의 서비스입니다. 다른 서비스(AEP 데이터 수집, [!DNL Target], [!DNL Analytics])는 동시에 실행할 수 있습니다.
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 이벤트 전달만 | 이벤트를 Adobe이 아닌 대상에만 전달하면 되며 AEP 데이터 세트의 데이터는 필요하지 않습니다 | 데이터 처리 비용 최소화 이벤트는 Edge Network을 통해 전달 규칙으로 이동하지만 AEP 데이터 레이크로 수집되지 않습니다. |
>| 이벤트 전달 + AEP 수집 | AEP(프로필, 대상자, 여정)에서 동일한 이벤트가 필요하며 외부 시스템으로 전달되어야 합니다 | 타사 분석과 함께 [!DNL RT-CDP] 또는 [!DNL AJO]을(를) 사용하는 조직에 가장 일반적입니다. 데이터스트림은 이벤트를 AEP 데이터 세트와 이벤트 전달 규칙 모두에 보냅니다. |
>| 이벤트 전달 + 여러 Adobe 서비스 | AEP, [!DNL Target], [!DNL Analytics] 및 외부 대상으로 동시에 라우팅되는 이벤트가 필요합니다. | 데이터 스트림에 필요한 모든 서비스를 사용하도록 설정합니다. 각 서비스는 개별적으로 이벤트를 수신합니다. |

**UI 탐색:** [!DNL Experience Platform] > 데이터 수집 > 데이터스트림 > 데이터스트림 선택 또는 만들기

**키 구성 세부 정보:**

- 데이터 스트림의 고급 설정 또는 서비스 구성에서 이벤트 전달이 활성화되어 있어야 합니다.
- 데이터 스트림에 이벤트 전달 속성(2단계에서 생성됨)을 연결합니다.
- 데이터 스트림에 할당된 XDM 스키마가 수집 메커니즘이 보내는 이벤트 구조와 일치하는지 확인합니다

**Experience League 설명서:**

- [데이터스트림 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/configure)
- [데이터스트림 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/overview)
- [이벤트 전달 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/overview)

### 2단계: 이벤트 전달 속성 및 확장

**응용 프로그램 함수:** AEP: 이벤트 전달 속성 설정

**구성할 내용:** 대상 대상에 필요한 확장과 함께 데이터 수집 UI의 이벤트 전달 속성입니다. 이벤트 전달 속성은 서버측 전달 논리를 정의하는 모든 규칙, 데이터 요소 및 확장에 대한 컨테이너입니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 단일 속성과 여러 속성 비교**
>
>모든 대상에 대해 하나의 이벤트 전달 속성을 사용해야 합니까, 아니면 별도의 속성을 사용해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 단일 속성 | 대부분의 구현, 모든 전달 규칙이 동일한 이벤트 스트림을 공유합니다. | 단일 게시 워크플로우로 간편하게 관리할 수 있으며 모든 규칙이 모든 이벤트에 대해 평가됩니다. 규칙 조건을 사용하여 대상으로 이동할 이벤트를 필터링합니다. |
>| 여러 속성 | 서로 다른 대상 통합을 독립적으로 관리하려면 서로 다른 팀이 필요하거나 엄격한 환경 격리 요구 사항이 있습니다 | 각 속성에는 자체 게시 워크플로우가 있으며 서로 다른 데이터스트림에 연결할 수 있습니다. 관리 오버헤드가 증가하지만 액세스 제어 경계가 개선됩니다. |

>[!NOTE]
>
>**결정: 설치할 확장**
>
>대상 및 선택한 구현 옵션 (위에서 A, B 또는 C)을 기반으로 확장을 선택합니다.
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 대상별 확장([!DNL Meta], [!DNL Google], [!DNL AWS] 등) | 대상에 사전 설치된 확장이 있으며 최소한의 사용자 지정 구성을 원하는 경우(옵션 A 또는 C) | 각 확장에는 대상별 자격 증명(API 토큰, 측정 ID, 계정 ID)이 필요합니다. 지원되는 이벤트 유형 및 필수 필드에 대해서는 확장 설명서를 검토하십시오. |
>| Cloud Connector 확장 전용 | 모든 대상은 사용자 지정 HTTP 요청을 사용합니다(옵션 B). | Cloud Connector 확장은 기본적으로 설치됩니다. 암호 기능을 사용하여 API 키 및 인증 토큰을 안전하게 저장합니다. |
>| 대상별 및 클라우드 커넥터 모두 | 지원되는 대상과 사용자 지정 대상을 혼합하여 사용할 수 있습니다(옵션 C). | 잘 지원되는 대상에 대해 특정 확장을 설치하고 나머지는 Cloud Connector를 사용합니다. |

**UI 탐색:** [!DNL Experience Platform] > 데이터 수집 > 이벤트 전달 > 속성 만들기(또는 기존 항목 선택)

**키 구성 세부 정보:**

- 명확한 규칙을 사용하여 속성에 이름을 지정합니다(예: &quot;Event Forwarding - Production&quot; 또는 &quot;EF - Analytics &amp; Advertising&quot;).
- [!DNL Adobe Cloud Connector] 확장 설치(사용자 지정 Webhook 작업의 경우 기본적으로 포함됨)
- 대상별 확장을 설치하고 자격 증명을 구성합니다.
- 보안 기능(데이터 수집 > 이벤트 전달 > 보안)을 사용하여 API 키, 토큰 및 자격 증명을 안전하게 저장합니다
- 안전한 게시 워크플로우를 위한 환경(개발, 스테이징, 프로덕션) 구성

**Experience League 설명서:**

- [이벤트 전달 시작](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/getting-started)
- [이벤트 전달 확장 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/overview)
- [이벤트 전달 비밀](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/secrets)
- [Adobe Cloud Connector 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/cloud-connector/overview)

### 3단계: 이벤트 규칙 정의

**응용 프로그램 함수:** AEP: 이벤트 규칙 정의, AEP: 대상 매핑

**구성할 규칙:** 들어오는 이벤트 데이터를 평가하고, 전달할 이벤트를 필터링하는 조건을 적용하고, 데이터를 대상 끝점으로 보내는 작업을 정의하는 규칙입니다. 각 규칙은 조건(실행 시기)과 작업(수행할 작업)으로 구성됩니다. 데이터 요소는 규칙 조건 및 작업 구성에 사용할 XDM 이벤트 페이로드에서 값을 추출하고 변환합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 이벤트 필터링 전략**
>
>각 대상에 전달되는 이벤트를 어떻게 결정해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 모든 이벤트 전달 | 대상에는 전체 이벤트 스트림(예: 원시 이벤트 저장을 위한 Data Warehouse)이 필요합니다 | 가장 간단한 구성 — 필요 없음. 대상의 높은 데이터 볼륨입니다. 대상 비용 및 요금 제한을 고려하십시오. |
>| 이벤트 유형별 필터링 | 대상마다 서로 다른 이벤트 유형(예: 구매 - 광고, 페이지 보기 - 분석)이 필요합니다. | `arc.event.xdm.eventType` 또는 유사한 XDM 필드를 기반으로 하는 조건을 사용합니다. 대상에서 불필요한 데이터를 줄입니다. |
>| 이벤트 속성으로 필터링 | 특정 기준을 충족하는 특정 이벤트만 전달해야 합니다(예: 임계값 이상의 구매, 특정 페이지 경로의 이벤트). | 규칙 조건에 데이터 요소 값을 사용합니다. 더 복잡하지만 목적지의 소음이 줄어듭니다. |

>[!NOTE]
>
>**결정: 데이터 변환 접근 방식**
>
>대상 페이로드에 대한 XDM 이벤트 데이터는 어떻게 변환해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 데이터 요소를 통한 직접 XDM 필드 매핑 | 대상 필드는 XDM 필드에 완전히 매핑됩니다(확장 기반 전달과 공통) | XDM 경로를 참조하는 데이터 요소를 만듭니다(예: `arc.event.xdm.commerce.order.priceTotal`). 확장은 종종 매핑 UI를 제공합니다. |
>| 사용자 지정 코드 변환 | 대상에 XDM과 상당히 다른 페이로드 형식이 필요하거나 필드에 해시, 연결 또는 재구성이 필요합니다 | 사용자 지정 코드 데이터 요소 또는 작업 수준 사용자 지정 코드를 사용하여 페이로드를 변환합니다. 유연성은 높지만 유지 관리가 어렵습니다. |
>| 데이터 요소와 사용자 지정 코드의 조합 | 일부 필드는 직접 매핑되지만 다른 필드는 변환이 필요합니다 | 단순 매핑에는 데이터 요소를 사용하고, 복잡한 변환에는 사용자 지정 코드 블록을 사용합니다. 유지 관리 기능과 유연성 간의 균형 유지 |

>[!NOTE]
>
>**결정: 전달된 데이터의 PII 처리**
>
>전달하기 전에 개인 식별 정보를 처리하려면 어떻게 해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 완전히 PII 필드 제외 | 대상은 PII가 필요하지 않으며 거버넌스 정책은 공유를 제한합니다 | 전달된 페이로드에서 PII 필드를 생략하도록 규칙을 구성합니다. 개인 정보 보호 규정 준수를 위한 가장 간단한 접근 방식. |
>| 전달하기 전에 PII 필드 해시 | 대상에 해시된 식별자가 필요합니다(예: [!DNL Meta]에는 전환 API용 SHA-256 해시된 이메일이 필요). | 사용자 지정 코드 데이터 요소를 사용하여 SHA-256 해시를 적용합니다. 일부 확장은 해싱을 자동으로 처리합니다. |
>| 계약상의 토대 PII 전달 | 대상에는 데이터 처리 계약이 있으며 PII를 공유할 수 있는 법적 기반이 있습니다 | 데이터 사용 레이블 및 거버넌스 정책(S3)이 공유를 허용하는지 확인합니다. 법적 근거를 문서화합니다. |

**UI 탐색:** [!DNL Experience Platform] > 데이터 수집 > 이벤트 전달 > 속성 선택 > 데이터 요소/규칙

**키 구성 세부 정보:**

- **데이터 요소**&#x200B;에서 경로 접두사 `arc.event.xdm.`(예: 페이지 URL의 경우 `arc.event.xdm.web.webPageDetails.URL`)을(를) 사용하여 들어오는 XDM 이벤트를 참조합니다
- **규칙 조건**&#x200B;은 데이터 요소 값을 평가하여 규칙을 실행할지 여부를 결정합니다.
- **규칙 작업** 확장 관련 작업(옵션 A의 경우) 또는 Cloud Connector &quot;Make Fetch Call&quot; 작업(옵션 B의 경우)을 사용하여 데이터를 대상으로 보냅니다.
- 각 규칙에는 여러 작업이 있을 수 있으므로, 단일 이벤트를 여러 대상에 전달할 수 있습니다
- 동일한 이벤트에 대해 여러 규칙이 실행될 수 있는 경우 규칙 순서 지정을 사용하여 평가 시퀀스를 제어합니다
- 프로덕션에 게시하기 전에 개발 환경에서 규칙을 철저하게 테스트합니다.

**옵션이 나뉘는 위치:**

**옵션 A(확장 기반)의 경우:**

대상 확장의 미리 작성된 작업 유형을 사용하여 규칙 작업을 구성합니다. 예를 들어 [!DNL Meta] 전환 API 확장은 XDM 필드를 [!DNL Meta] 이벤트 매개 변수(event_name, event_time, user_data, custom_data)에 매핑하는 &quot;이벤트 보내기&quot; 작업을 제공합니다. 확장은 페이로드 형식 지정, 해시 및 API 통신을 처리합니다.

**옵션 B(사용자 지정 Webhook)의 경우:**

Cloud Connector 확장의 &quot;Make Fetch Call&quot; 작업을 사용하여 규칙 작업을 구성합니다. 대상 URL, HTTP 메서드(일반적으로 POST), 요청 헤더(인증 포함)를 지정하고 데이터 요소 및/또는 사용자 지정 코드를 사용하여 요청 본문을 구성합니다. 대상 API의 예상 페이로드 형식을 정확하게 일치시켜야 합니다.

**옵션 C(하이브리드)의 경우:**

각 대상에 대해 별도의 규칙을 만듭니다. 확장 기반 규칙은 확장의 작업 유형을 사용하고, 사용자 지정 규칙은 Cloud Connector 가져오기 호출을 사용합니다. 모든 규칙은 동일한 속성에서 공존하며 들어오는 각 이벤트에 대해 독립적으로 평가됩니다.

**Experience League 설명서:**

- [이벤트 전달 규칙](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/overview)
- [이벤트 전달의 데이터 요소](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/ui/data-elements)
- [데이터 수집 규칙](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/ui/rules)
- [Adobe Cloud Connector 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/cloud-connector/overview)

### 4단계: 게시 및 활성화

**응용 프로그램 함수:** AEP: 실행 전달

**구성할 내용:** 이벤트 전달 규칙을 개발에서 스테이징을 통해 프로덕션으로 승격하는 게시 워크플로우입니다. 이벤트 전달에서는 Edge Network에서 활성화된 구성을 제어하는 환경 및 빌드 아티팩트와 함께 Tags와 동일한 라이브러리 기반 게시 모델을 사용합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 게시 작업 과정 엄격함**
>
>게시 프로세스는 얼마나 엄격해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 프로덕션으로 직접 연결(개발 > 프로덕션) | 소규모 팀, 위험이 적은 대상 또는 개념 입증 구현 | 배포는 빨라지지만 프로덕션 문제의 위험은 높아집니다. 중요하지 않은 대상을 사용한 초기 테스트에 적합합니다. |
>| 전체 환경 진행률(개발 > 스테이징 > 프로덕션) | 중요한 대상이 포함된 프로덕션 구현(광고 플랫폼, 데이터 웨어하우스) | 모든 프로덕션 사용 사례에 권장됩니다. 스테이징을 사용하면 프로덕션 배포 전에 실제 트래픽으로 확인할 수 있습니다. |

**UI 탐색:** [!DNL Experience Platform] > 데이터 수집 > 이벤트 전달 > 속성 선택 > 게시 흐름

**키 구성 세부 정보:**

- 게시할 모든 규칙, 데이터 요소 및 확장 구성이 포함된 라이브러리를 만듭니다
- 먼저 이벤트 전달 모니터링 도구를 사용하여 개발 환경에서 빌드하고 테스트하여 이벤트가 올바르게 전달되는지 확인합니다
- 라이브 트래픽을 사용한 사전 프로덕션 유효성 검사를 위해 스테이징으로 승격
- 스테이징에서 성공적인 이벤트 전달을 확인한 후에만 프로덕션에 게시
- 라이브러리 버전을 사용하여 변경 사항을 추적하고 필요한 경우 롤백을 활성화합니다

**Experience League 설명서:**

- [게시 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/publish/overview)
- [라이브러리](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/publish/libraries)
- [환경](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/environments)
- [빌드](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/publish/builds)

### 5단계: 모니터링 및 유효성 검사

**응용 프로그램 함수:** AEP: 모니터링

**구성할 내용:** 대시보드 및 유효성 검사 프로세스를 모니터링하여 이벤트가 정상적으로 전달되는지 확인하고, 오류를 진단하고, 이벤트 전달 배포의 작동 상태를 유지합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 모니터링 깊이**
>
>이벤트 전달을 얼마나 깊이 모니터링해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 이벤트 전달 모니터링 대시보드만 | 중요하지 않은 대상 또는 초기 배포에 대한 기본 모니터링 | 전달 성공률/실패율 및 대상 응답 코드에 대한 개요를 제공합니다. 대부분의 구현에 충분합니다. |
>| 이벤트 전달 모니터링 + 대상 측 유효성 검사 | 데이터 완전성이 비즈니스 결과에 직접 영향을 미치는 주요 대상(광고 전환 추적, 데이터 웨어하우스 무결성) | 대상 측 수신 확인을 통해 Adobe 측 전달 지표를 상호 참조합니다. 대상이 요청을 수락하지만 데이터를 처리하지 못하는 경계 사례를 catch합니다. |
>| 전체 가시성 스택(이벤트 전달 모니터링 + 대상 유효성 검사 + AEP 경고) | 데이터 게재에 대한 SLA 요구 사항을 갖춘 엔터프라이즈급 배포 | 이벤트 전달 모니터링을 AEP 플랫폼 경고와 결합하여 포괄적인 보기를 제공합니다. 전달 실패 임계값에 대한 경고 알림을 구성합니다. |

**UI 탐색:** [!DNL Experience Platform] > 데이터 수집 > 이벤트 전달 > 속성 선택 > 모니터링

**키 구성 세부 정보:**

- 이벤트 전달 모니터링 도구는 규칙 및 대상별로 이벤트 볼륨, 성공률 및 오류 세부 사항을 보여 줍니다
- 대상에서 HTTP 응답 코드 모니터링 — 2xx는 성공, 4xx는 클라이언트 오류(페이로드 또는 인증 문제 가능성), 5xx는 대상 측 오류를 나타냅니다.
- [!DNL Adobe Experience Platform Debugger] 브라우저 확장을 사용하여 클라이언트에서 Edge Network을 통해 이벤트 전달 규칙으로 이동하는 이벤트를 검사합니다.
- 전달된 이벤트가 대상 시스템에 표시되는지 확인하여 종단 간 유효성 검사(예: [!DNL Google Analytics]개의 실시간 보고서, [!DNL Meta]개의 이벤트 관리자 또는 데이터 웨어하우스 테이블 확인)
- 소스 및 데이터 흐름 실패에 대한 AEP 경고를 설정하여 이벤트가 이벤트 전달 규칙에 도달하지 못하도록 하는 업스트림 문제를 포착합니다

**Experience League 설명서:**

- [이벤트 전달 모니터링](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/monitoring)
- [Adobe Experience Platform Debugger](https://experienceleague.adobe.com/ko/docs/experience-platform/debugger/home)
- [경고 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/alerts/overview)

## 구현 시 고려 사항

이 섹션에서는 구현 전반에 걸쳐 염두에 두어야 할 보호 기능, 일반적인 위험, 모범 사례 및 상충 결정 등을 다룹니다.

### 보호 기능 및 제한 사항

- 이벤트 전달은 Edge Network에서 실시간으로 이벤트를 처리합니다. 기본적으로 실패한 게재에 대한 배치 모드 또는 재시도 큐가 없습니다
- Edge Network 속도 제한은 데이터스트림당 처리된 총 이벤트 볼륨에 적용됩니다. [Edge Network 보호](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/guardrails)
- 이벤트 전달 규칙은 서버측에서 실행되며 클라이언트측 리소스(DOM, 쿠키, localStorage)에 액세스할 수 없습니다.
- 이벤트 전달 규칙의 사용자 지정 코드는 샌드박스 환경에서 실행되며 일부 브라우저 JavaScript API는 사용할 수 없습니다
- Cloud Connector 가져오기 호출에 시간 제한 사항이 있습니다. 느리게 응답하는 대상으로 인해 시간 초과가 발생할 수 있습니다
- 이벤트 전달은 Edge Network 지리적 라우팅이 적용됩니다. 이벤트는 가장 가까운 Edge 위치에서 처리됩니다
- 전달된 요청에 대한 최대 페이로드 크기는 Edge Network 제한으로 제어됩니다.

### 일반적인 함정

- **모든 XDM 필드를 필터링하지 않고 전달:** 일부 필드만 필요한 대상으로 전체 XDM 이벤트 페이로드를 전송하면 대역폭이 낭비되고 대상 비용이 증가하며 실수로 PII를 공유할 수 있습니다. 항상 전달 규칙의 필수 필드만 매핑합니다.

- **암호를 사용하여 자격 증명을 보호하지 않음:** 데이터 요소 또는 규칙 작업에서 API 키 또는 토큰을 하드코딩하면 보안 위험이 발생합니다. 항상 데이터 수집 암호 기능을 사용하여 자격 증명을 안전하게 저장하고 규칙에서 참조합니다.

- **대상 속도 제한을 무시합니다.** 타사 대상에 API 속도 제한이 있는 경우가 많습니다. 이벤트 볼륨이 대상의 용량을 초과하면 이벤트가 삭제되거나 API 액세스가 제한될 수 있습니다. 대상 설명서에서 비율 제한을 검토하고 필요한 경우 이벤트 볼륨을 줄이기 위해 필터링을 구현합니다.

- **스테이징 없이 프로덕션에 직접 게시:** 스테이징 환경을 건너뛰면 프로덕션 환경에서만 오류가 검색되어 중요한 대상에서 데이터 손실이 발생할 수 있습니다. 항상 라이브 트래픽을 사용하여 스테이징에서 먼저 유효성을 검사하십시오.

- **HTTP 응답 코드를 모니터링하지 않음:** 오류 없이 실행되는 규칙은 대상이 데이터를 성공적으로 처리했음을 보장하지 않습니다. 대상 응답 코드(이벤트 전달 모니터링 도구에서 사용 가능)를 모니터링하고 2xx 이외의 응답을 조사합니다.

- **잘못 구성된 XDM 경로 참조:** 데이터 요소는 `arc.event.xdm.` 접두사를 사용하여 들어오는 이벤트 필드를 참조합니다. 잘못된 경로(예: 중첩 수준 누락)는 오류를 발생하는 대신 자동으로 null 값을 생성합니다. 디버거를 사용하여 데이터 요소 값의 유효성을 검사합니다.

### 우수 사례

- **단일 대상으로 시작하여 점진적으로 확장** - 추가 규칙 및 대상을 추가하기 전에 하나의 대상으로 종단간 이벤트 전달을 확인합니다. 이를 통해 디버깅을 간소화하고 인프라에 대한 신뢰도를 높일 수 있습니다.

- **일관된 명명 규칙 사용** — 대상, 이벤트 유형 및 환경을 식별하는 명확한 규칙을 사용하여 데이터 요소, 규칙 및 라이브러리의 이름을 지정합니다(예: &quot;규칙: Meta - 구매 이벤트&quot;, &quot;DE: 주문 총계&quot;).

- **개인 정보에 대한 필드 수준 필터링을 구현합니다** — 대상이 PII를 적절히 처리했다고 주장하는 경우에도 Edge Network에서 나가기 전에 중요한 필드를 삭제하거나 해시하도록 서버측 필터링을 적용하십시오. 이는 클라이언트측 태그에 대한 이벤트 전달의 주요 거버넌스 장점입니다.

- **구성 버전 지정** — 라이브러리 게시 워크플로를 사용하여 이벤트 전달 구성의 버전 지정된 스냅숏을 유지 관리합니다. 감사 및 롤백 목적으로 각 라이브러리 버전에 포함된 내용을 문서화합니다.

- **Platform Debugger를 사용하여 테스트** — [!DNL Adobe Experience Platform Debugger] 확장은 클라이언트측 SDK에서 Edge Network 처리를 통해 이벤트 라이프사이클에 대한 가시성을 제공합니다. 개발 및 문제 해결 중에 사용하십시오.

- **이벤트 전달 규칙을 XDM 스키마 디자인에 맞춥니다** — 이벤트 전달이 알려진 요구 사항인 경우 대상에 필요한 필드를 포함하도록 XDM 스키마 및 이벤트 분류법을 디자인합니다. 배포 후 스키마 변경 내용을 다시 맞춤화하면 더 번거로워집니다.

### 절충안 결정

>[!NOTE]
>
>**절충점: 확장 단순성과 웹후크 유연성 비교**
>
>사전 빌드된 확장은 구현 노력 및 유지 관리를 최소화하지만 확장의 지원되는 기능 및 페이로드 형식으로 제한됩니다. 사용자 지정 웹 후크는 전체 제어를 제공하지만 더 많은 개발과 지속적인 유지 관리가 필요합니다.
>
>- **확장 기반(옵션 A)은 다음과 같은 이점을 제공합니다.** 시장 출시 속도, 개발자 종속성 감소, 자동 자격 증명 관리, 유지 관리 감소
>- **Webhook 기반(옵션 B)은 다음을 지원합니다.** 전체 페이로드 제어, 모든 HTTP 끝점 지원, 사용자 지정 변환 논리, 확장 릴리스 주기와 독립성
>- **권장 사항:** 사용 가능하고 충분한 경우 확장을 사용합니다. 대상에 확장이 없거나 확장이 필요한 특정 API 기능을 지원하지 않는 경우에만 맞춤형 웹후크로 돌아갑니다. 하이브리드 접근법(옵션 C)은 대부분의 조직에 실용적인 선택이다.

>[!NOTE]
>
>**절충: 모든 이벤트와 선택적 필터링을 전달합니다**
>
>모든 이벤트를 대상으로 전달하면 완벽성은 보장되지만 데이터 양, 대상 비용 및 개인 정보 노출이 증가합니다. 선택적 필터링은 소음을 감소시키지만 유용한 이벤트를 누락할 위험이 있습니다.
>
>- **모든 이벤트를 전달합니다.** 데이터 완전성, 단순성, 향후 교정(나중에 필요한 경우 데이터가 있음)
>- **선택적 필터링 기능:** 비용 효율성, 개인 정보 보호 위험 감소, 대상 데이터 정리, 데이터 최소화 원칙 준수
>- **권장 사항:** 기본적으로 이벤트 유형 및 비즈니스 관련성에 따라 선택적 필터링이 적용됩니다. 각 대상에 실제로 필요한 이벤트와 필드만 전달합니다. 이는 데이터 최소화 원칙(GDPR 제5조)에 부합하고 운영 비용을 절감합니다.

>[!NOTE]
>
>**절충: 단일 속성과 여러 속성 비교**
>
>단일 이벤트 전달 속성은 관리가 더 간단하지만 모든 규칙이 하나의 게시 워크플로우를 공유함을 의미합니다. 여러 속성을 사용하면 격리 기능이 제공되지만 관리 오버헤드가 증가합니다.
>
>- **단일 속성 우대:** 단순성, 통합 게시, 공유 데이터 요소, 더 쉬운 디버깅
>- **여러 속성을 사용할 수 있습니다.** 팀 수준 액세스 제어, 독립 게시 케이던스, 대상 오류 격리
>- **권장 사항:** 대부분의 구현에 대해 단일 속성으로 시작합니다. 서로 다른 팀이 서로 다른 대상 통합을 소유하고 독립적인 릴리스 주기를 필요로 하거나 규제 요구 사항에 따라 데이터 흐름 간에 엄격한 격리가 필요한 경우에만 여러 속성으로 분할합니다.

## 관련 설명서

다음 리소스는 이 안내서에서 다루는 항목에 대한 추가 세부 정보를 제공합니다.

**이벤트 전달**

- [이벤트 전달 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/overview)
- [이벤트 전달 시작](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/getting-started)
- [이벤트 전달 모니터링](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/monitoring)
- [이벤트 전달 비밀](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/event-forwarding/secrets)

**이벤트 전달 확장**

- [서버측 확장 카탈로그](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/overview)
- [Adobe Cloud Connector 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Meta 전환 API 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/meta/overview)
- [Google Cloud Platform 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [AWS 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/aws/overview)
- [Snowflake 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/snowflake/overview)
- [Google Ads Enhanced Conversions 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/google-ads-enhanced-conversions/overview)
- [Mailchimp 확장](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/extensions/server/mailchimp/overview)

**데이터 수집 및 Edge Network**

- [데이터스트림 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/configure)
- [데이터스트림 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/overview)
- [웹 SDK 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/home)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/edge-network-server-api/overview)
- [태그 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/tags/home)
