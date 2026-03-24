---
title: 이벤트 트리거된 메시징
description: 행동 또는 시스템 이벤트에 대한 응답으로 상황에 맞는 실시간 메시지를 전달하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 75137990-9848-40c0-abf3-adbd21d2de52
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '9040'
ht-degree: 1%

---

# 이벤트 트리거된 메시징

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO), [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP) 및 [!DNL Adobe Experience Platform]&#x200B;(AEP)을 사용하여 이벤트가 트리거된 메시지에 대한 포괄적인 구현 블루프린트를 제공합니다. 행동 또는 시스템 이벤트에 대한 응답으로 상황에 맞는 실시간 메시지를 전달해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

이 안내서를 사용하여 구성할 내용, 구현 선택 사항이 있는 위치 및 각 의사 결정을 유도하는 장단점을 이해합니다.

이 안내서에서는 이벤트 수집 및 여정 생성에서부터 메시지 전달 및 성능 보고에 이르기까지 전체 라이프사이클을 다루며, 세 가지 고유한 구현 옵션에 대한 자세한 결정 지침을 제공합니다.

## 사용 사례 개요

이벤트 트리거 메시징은 실시간 행동 또는 시스템 이벤트에 대한 응답으로 컨텍스트 메시지를 제공합니다. 예약된 미리 평가된 대상자에게 보내는 배치 아웃바운드 메시지 활성화와 달리 이 패턴은 장바구니 포기, 찾아보기 세션, 양식 제출 또는 시스템 상태 변경과 같은 자격을 갖춘 이벤트를 수신하고 조건을 평가하고 메시지를 전달하는 여정에 즉시 트리거 프로필을 입력합니다.

이 패턴은 AEP(웹 SDK, 모바일 SDK 또는 서버측 API를 통해)로의 실시간 이벤트 스트리밍, AJO에 단일 이벤트 항목이 있는 여정 및 전송 여부와 내용을 결정하는 조건 평가 논리에 의존합니다. 메시지는 일반적으로 트리거 이벤트가 발생한 후 몇 분 내에 전송되므로 이 패턴은 시간에 민감하고 컨텍스트에 따라 적절한 통신에 이상적입니다.

조직은 이 패턴을 사용하여 고객 작업에 실시간으로 응답함으로써 관련성을 높이고 예약된 일괄 처리 통신에 비해 높은 참여도 및 전환율을 제공합니다. 일반적인 시나리오에는 포기한 장바구니 복구, 구매 후 후속 조치, 등록 후 환영 메시지, 결제 실패 또는 가격 하락 경고와 같은 시간에 민감한 알림이 포함됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

**[포기한 장바구니 및 여정 복구](../../business-objectives/customer-experience/recover-abandoned-carts-journeys.md)**

구매, 애플리케이션 또는 등록 중에 중단한 사용자를 적시에 개인화된 후속 조치와 함께 다시 참여시킵니다.

| KPI |
| --- |
| 전환율, 증분 수익, 참여 |

**[전환율 증가](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

구매, 등록 또는 양식 제출과 같은 원하는 작업을 완료하는 방문자 및 잠재 고객의 비율을 향상시킵니다.

| KPI |
| --- |
| 전환율, 가망 고객 전환, 가망 고객당 비용 |

**[개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.

| KPI |
| --- |
| 참여, 전환율, 고객 만족도(CSAT) |

**[고객 온보딩 개선](../../business-objectives/customer-experience/improve-customer-onboarding.md)**

능률적이고 개인화된 환영 경험과 활성화 여정을 통해 신규 고객의 가치 실현 시간을 단축합니다.

| KPI |
| --- |
| 참여, 유지, 전환율 |

## 예시 전술 사용 사례

다음 시나리오는 이벤트 트리거 메시징이 다양한 비즈니스 컨텍스트에 적용될 수 있는 방법을 보여줍니다.

- **장바구니 포기 전자 메일 또는 SMS** — 고객이 장바구니에 항목을 추가하지만 정의된 기간 내에 구매를 완료하지 않으면 알림 메시지를 보냅니다.
- **찾아보기 포기 후속 작업** - 제품이나 콘텐츠를 보았지만 전환 작업을 수행하지 않은 방문자를 다시 참여시킵니다.
- **구매 후 감사 또는 크로스셀** — 구매 이벤트 직후 확인 및 크로스셀 권장 사항을 제공합니다.
- **평가판 만료 알림** — 갱신 또는 전환 메시지를 통해 무료 평가판 종료에 가까워지는 사용자에게 알립니다.
- **등록 후 환영 메시지** — 새 사용자가 등록하거나 계정을 만들 때 즉시 온보딩 메시지를 보냅니다.
- **양식 제출 확인** — 상황별 확인을 통해 양식 제출(연락처 요청, 애플리케이션, 등록)을 확인합니다
- **결제 실패 알림** — 반복 결제가 실패하면 고객에게 경고하여 결제 정보를 업데이트하도록 합니다
- **앱 제거 win-back 푸시 알림** - 사용자가 모바일 응용 프로그램을 제거할 때 win-back 메시지를 트리거합니다.
- **예약 또는 약속 확인** — 예약, 예약 또는 약속이 예약된 후 즉시 확인을 보냅니다.
- **위시리스트 항목에 대한 가격 하락 경고** — 위시리스트에 있는 제품의 가격이 하락하면 고객에게 알립니다.

## 주요 성과 지표

다음 KPI는 이벤트가 트리거된 메시징 구현의 효과를 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 전환율 | 원하는 작업(구매, 등록, 갱신)을 완료하는 트리거된 메시지 수신자의 백분율 | 전환/게재된 메시지 * 100 |
| 증분 수익 | 전송 안 함 제어 그룹에 비해 이벤트가 트리거된 메시지로 인한 추가 매출 | 트리거된 전송에서의 수익 - 컨트롤 그룹 기준선 |
| 열람률 | 수신자가 연 게재된 메시지 비율 | 열기/게재됨 * 100 |
| 클릭스루 비율(CTR) | 최소 한 번의 클릭을 생성하는 게재된 메시지 비율 | 클릭 수 / 게재됨 * 100 |
| 전환 시간 | 메시지 게재와 전환 이벤트 사이의 평균 경과 시간 | 평균(전환 타임스탬프 - 게재 타임스탬프) |
| 여정 완료율 | 여정에 들어가서 메시지 게재 단계에 도달하는 프로필의 비율 (조건 또는 종료에 의해 삭제되지 않음) | 게재 중인 프로필 / 여정 중인 프로필 * 100 |
| 메시지 비표시 비율 | 빈도 제한, 동의 또는 상태 평가로 인해 제외된 적격 프로필의 비율 | 제외된 프로필 / 총 적격 프로필 * 100 |
| 바운스 비율 | 하드 바운스 또는 소프트 바운스로 인해 배달되지 못한 메시지 비율 | 바운스 수 / 전송됨 * 100 |

## 사용 사례 패턴

이 섹션에서는 이벤트가 트리거된 메시징을 유도하는 핵심 패턴과 기능 체인에 대해 설명합니다.

**이벤트 트리거된 메시징**

실시간 행동 또는 시스템 이벤트를 수신한 다음 상황별 메시지를 트리거하는 프로필에 전달합니다.

**함수 체인:** 이벤트 수집 > 여정 항목 > 조건 평가 > 메시지 게재 > 보고

## 애플리케이션

이 사용 사례 패턴에는 다음 Adobe 애플리케이션이 사용됩니다.

- **[!DNL Adobe Journey Optimizer](AJO)** — 단일 이벤트 항목, 조건 평가, 대기 단계, 메시지 작성, 채널 구성, 빈도 거버넌스 및 게재 보고와 함께 여정 오케스트레이션
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** - 여정, 동의 및 거버넌스 적용, 프로필 강화 내에서의 조건 기반 필터링에 대한 대상 평가
- **[!DNL Adobe Experience Platform](AEP)** — 웹 SDK, Mobile SDK 또는 서버측 API를 통한 실시간 이벤트 수집, 데이터 모델링, ID 확인, Edge Network

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 사항 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | AJO 샌드박스가 활성 채널 구성으로 프로비저닝되었습니다. 여정 작성 및 구현 팀에 할당된 게시 권한. 여정 관리, 콘텐츠 작성 및 채널 관리를 위해 구성된 사용자 역할. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | XDM ExperienceEvent 스키마는 조건 평가 및 메시지 개인화에 필요한 모든 컨텍스트 필드(예: 장바구니 이벤트, 제품 세부 정보, 장바구니 값의 경우 `commerce.productListAdds`)를 사용하여 트리거 이벤트를 캡처해야 합니다. 실시간 고객 프로필에 대해 스키마를 활성화해야 합니다. 해당 데이터 세트를 만들고 프로필이 활성화되어야 합니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [스키마 구성 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| 데이터 소스 및 수집 | 필수 | 실시간 이벤트 스트리밍을 구성해야 합니다. 웹 이벤트의 경우 Web SDK, 앱 이벤트의 경우 Mobile SDK 또는 시스템 이벤트의 경우 Edge Network Server API입니다. AEP 및 AJO 서비스가 활성화된 상태에서 데이터 스트림을 구성하여 이벤트를 올바른 데이터 세트로 라우팅해야 합니다. 패턴은 실시간 이벤트 수집에 따라 달라지므로 이는 중요한 종속성입니다. | [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| ID 및 프로필 구성 | 필수 | 트리거링 이벤트는 알려진 ID(이메일, CRM ID 또는 인증된 세션)와 연결되어 있어야 여정이 프로필을 확인하고 메시지를 전달할 수 있습니다. 트리거링 이벤트에 사용되는 식별자에 대해 ID 네임스페이스가 있어야 합니다. 메시지를 전달하려면 익명 이벤트에는 ID 그래프를 통한 ID 결합이 필요합니다. 병합 정책을 구성해야 합니다. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| 대상 정의 및 세분화 | 추천 | 이벤트 트리거 여정(시작은 이벤트 기반이며 대상 기반이 아님)에 대해서는 엄격히 필요하지 않지만, 대상 세그먼트는 여정 내의 조건 평가에 사용될 수 있습니다(예: 프로필이 &quot;고가치 고객&quot; 세그먼트에 있는 경우에만 전송하거나 프로필이 &quot;최근에 연락한&quot; 세그먼트에 있는 경우에는 표시하지 않음). 스트리밍 평가는 여정 내 실시간 세그먼트 멤버십 확인에 권장됩니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [스트리밍 세그먼테이션](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 기능 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 장바구니 포기 수, 마지막 구매 이후 일 수, 평균 주문 가격 및 라이프타임 구매 합계와 같은 계산된 속성은 트리거된 여정 내에서 조건 평가 및 개인화를 향상시킵니다. 이러한 행동 집계는 보다 정확한 타깃팅 결정을 가능하게 합니다(예: 처음 포기자와 반복 포기자를 구별합니다). | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | 스토리지 비용 및 규정 준수를 관리하려면 일시적인 동작 이벤트(페이지 보기, 검색, 클릭 수)에 대해 이벤트 데이터 만료를 구성해야 합니다. 메시지 게재 중 채널별 옵트인/옵트아웃 적용을 위해 동의 스키마 필드가 있어야 합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [데이터 세트 만료](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 이벤트 및 프로필 필드의 거버넌스 레이블은 규정 준수 개인화를 보장합니다. 트리거된 메시지에 PII 또는 행동 데이터를 사용하는 개인화된 콘텐츠가 포함된 경우 메시지 콘텐츠에서 허가되지 않은 데이터 사용을 방지하기 위해 데이터 사용 레이블 및 거버넌스 정책을 검토해야 합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview) |
| 모니터링 및 가시성 | 포함됨 | 여정 실행 모니터링은 보고 단계의 일부입니다. 또한 이벤트 수집 실패 또는 여정 처리 지연에 대한 경고를 구성하여 트리거된 메시지가 전송되지 않도록 하는 파이프라인 문제를 감지합니다. | [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [가시성 통찰력 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | 여정 성능 보고서는 보고 단계에서 다룹니다. 채널 간 및 시간에 따른 트리거된 메시징 효과를 보다 심층적으로 분석하려면 CJA 연결 및 작업 영역을 구성하여 전환 속성, 전환 시간 및 채널 성능을 분석하십시오. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer]&#x200B;(AJO)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| Journey Orchestration | 여정 생성 및 구성 | 단일 이벤트 항목으로 여정 만들기, 자격 이벤트 구성, 조건 노드 추가, 대기 단계, 메시지 작업, 종료 기준 및 재입력 규칙 |
| 채널 구성 | 채널 표면 설정 | 하위 도메인 위임, IP 풀, 발신자 설정 및 제외 목록 관리를 포함하여 채널 표면(이메일, SMS, 푸시)을 구성하거나 확인합니다 |
| 메시지 작성 | 메시지 콘텐츠 만들기 | 이벤트 기반 개인화, 조건부 콘텐츠 블록 및 재사용 가능한 조각을 사용하여 컨텍스트 기반 메시지 콘텐츠 작성 |
| 빈도 및 비즈니스 규칙 | 여정 생성 및 구성(옵션 C) | 빈도가 높은 이벤트 소스에서 과도한 메시지를 보내지 않도록 빈도 제한 및 중복 제거 규칙을 구성합니다. |
| 충돌 및 우선 순위 관리 | 여정 생성 및 구성 | 동일한 프로필에 대해 경쟁하는 여정에 대해 우선 순위 점수를 할당하고 충돌 검색을 구성합니다. |
| 보고 및 성능 분석 | 보고 및 모니터링 | 라이브 및 내역 보고서를 통해 여정 전달 지표를 모니터링하고 CJA을 통해 프로그래밍 방식 성능 데이터에 액세스합니다 |

### [!DNL Real-Time CDP]&#x200B;(RT-CDP)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 기본 설정(F5) | 여정 내에서 조건 기반 필터링에 사용되는 대상 세그먼트(예: 고가치 고객 세그먼트, 제외 세그먼트)를 평가합니다 |
| 동의 및 거버넌스 적용 | 기본 설정(S2/S3) | 메시지 게재 중 동의 환경 설정 및 데이터 사용 거버넌스 정책을 적용하여 규정 준수 커뮤니케이션을 보장 |

## 필요 조건

구현을 시작하기 전에 다음을 완료하십시오.

- [ ] AJO 샌드박스가 여정 만들기 및 게시 권한으로 프로비저닝됨(F1)
- [ 컨텍스트 필드를 사용하여 트리거 이벤트를 캡처하는 ] XDM ExperienceEvent 스키마가 실시간 고객 프로필(F2)에 대해 활성화되었습니다.
- [ 올바른 AEP 데이터 집합에 대한 데이터 스트림 라우팅 이벤트를 사용하여 웹 SDK, Mobile SDK 또는 Edge Network Server API를 통해 구성된 ] 실시간 이벤트 스트리밍(F3)
- [ 트리거링 이벤트의 식별자에 대해 구성된 ] ID 네임스페이스, ID 연결 규칙(F4)
- [ ] 채널 표면(이메일, SMS 또는 푸시)이 구성되고 테스트 전송이 정상적으로 완료되어 유효성이 확인되었습니다.
- [ ] 메시지 콘텐츠를 샘플 프로필로 작성, 검토 및 테스트했습니다.
- [ 대상 채널의 프로필에 채워진 ] 동의 필드(예: `consents.marketing.email.val`)
- [ ] 조건 기반 대상 필터링(옵션 B/C)을 사용하는 경우 스트리밍 평가된 대상 세그먼트가 정의되어 있으며 현재 평가 중입니다.

## 구현 옵션

이 섹션에서는 이벤트 트리거 메시징에 대한 세 가지 구현 옵션에 대해 설명합니다. 각 옵션은 이전 옵션을 기반으로 하며 추가 기능을 추가합니다.

### 옵션 A: 간단한 이벤트 트리거 메시지

**최적의 용도:** 지연 또는 조건부 논리가 필요하지 않은 즉각적인 단일 메시지 응답(주문 확인, 환영 이메일, 양식 제출 승인, 예약 확인).

**작동 방식:**

여정은 단일 이벤트 입력 노드를 통해 자격 부여 이벤트를 수신합니다. 이벤트가 수신되면, 프로필이 여정에 진입하고, 최소 조건 평가(동의 확인, 프로필 존재 확인)를 거친 후 구성된 채널 액션 노드를 통해 즉시 단일 메시지를 수신하게 된다.

가장 간단한 구현 변형입니다. 여정 캔버스에는 이벤트 항목 노드, 기본 자격 확인을 위한 선택적 조건 노드, 단일 메시지 작업 노드 및 종료 노드가 포함됩니다. 대기 단계, 복잡한 분기 및 전환 확인이 없습니다. 이 메시지는 일반적으로 트리거 이벤트가 발생한 후 몇 초에서 몇 분 내에 전달됩니다.

트리거 이벤트의 이벤트 데이터(제품 이름, 주문 총액, 양식 세부 정보)는 개인화 편집기에서 컨텍스트 속성을 통해 메시지 개인화에 사용할 수 있습니다. 이 접근 방식은 게재 속도를 극대화하고 여정 복잡성을 최소화합니다.

**주요 고려 사항:**

- 이벤트 후 고객이 자체 전환하는지 여부에 관계없이 메시지가 전송됩니다(전환 확인 없음)
- 기본적으로 즉각적인 응답을 보장하는 이벤트에 적합(확인, 승인)
- 재입력 규칙은 신중하게 구성해야 합니다. 확인 스타일 메시지의 경우 각 이벤트가 메시지를 생성하도록 재입력을 허용하고 환영 스타일 메시지의 경우 재입력을 금지합니다

**장점:**

- 가장 빠른 게재 시간(이벤트 후 초~분)
- 움직이는 부품을 최소화하면서 가장 간단한 여정 구성
- 여정 실패 또는 중단 프로필의 위험이 가장 낮음
- 간편한 테스트 및 유지 관리

**제한 사항:**

- 보내기 전에 고객이 자체 전환했는지 여부를 확인할 수 없음
- 시간 지연된 조건부 논리를 통합할 수 없음
- 이벤트가 빈도 거버넌스 없이 자주 발생하는 경우 불필요한 메시지를 생성할 수 있음

**Experience League:**

- [여정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [일반 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)

### 옵션 B: 대기가 있는 조건부 이벤트 트리거 메시지

**최적의 대상:** 메시지를 받기 전에 고객이 자체 변환할 시간이 있어야 하는 지연된 조건부 응답, 즉 장바구니 포기(1~4시간 기다린 후 장바구니가 포기 상태인지 확인), 찾아보기 포기(24시간 기다린 후 구매했는지 확인), 평가판 만료(만료 날짜가 가까워질 때까지 대기).

**작동 방식:**

여정은 자격 이벤트를 수신하고, 프로필에 입장하고, 조건을 평가하기 전에 대기 기간을 지정합니다. 대기 후 조건 노드는 고객이 자체 전환되었는지(예: 구매를 완료했는지, 구독을 갱신했는지) 또는 원래 컨텍스트가 여전히 유효한지 여부를 확인합니다. 조건이 충족되는 경우(예: 장바구니가 여전히 중단되는 경우)에만 여정이 메시지 게재로 진행됩니다.

여정 캔버스에는 이벤트 시작 노드, 대기 노드(구성 가능한 기간 또는 특정 날짜/시간), 전환 이벤트 또는 프로필 상태 변경을 확인하는 조건 노드, 분기 경로(메시지를 보내거나 보내지 않고 종료), 자격 있는 경로의 메시지 작업 노드 및 각 분기의 종료 노드가 포함됩니다. 대기 기간 동안 전환 이벤트가 발생하는 경우 여정에서 프로필을 자동으로 제거하도록 종료 기준을 구성할 수 있으므로 명시적 조건 확인이 필요하지 않습니다.

이 접근 방식은 고객이 자체 변환할 시간을 제공하여 고객 경험을 개선하고 전송된 메시지의 인지된 관련성을 높임으로써 불필요한 메시지를 줄입니다.

**주요 고려 사항:**

- 대기 시간은 전환율에 큰 영향을 미칩니다. 대기 시간이 짧을수록(1~2시간) 긴급도는 높아지지만 불필요한 전송이 더 많아집니다. 대기 시간이 길수록(24~48시간) 볼륨은 줄어들지만 관련성 창을 놓칠 수 있습니다.
- 조건 평가를 수행하려면 전환 이벤트를 AEP에서 캡처하고 동일한 프로필 ID와 연결해야 합니다
- 종료 기준은 전환 확인을 위해 명시적 조건 노드에 대한 보다 명확한 대안을 제공합니다
- 재입력 규칙은 대기 기간 동안 고려되어야 합니다. 즉, 이미 대기하고 있는 동안 프로필이 여정을 재입력해서는 안 됩니다.

**장점:**

- 자동 전환 확인을 통해 불필요한 메시지 감소
- 고품질, 관련성 높은 커뮤니케이션 생성
- 구성 가능한 지연 시간으로 시간에 민감한 사용 사례 지원
- 종료 기준 전환 시 자동 여정 제거 사용

**제한 사항:**

- 대기 및 조건 노드를 통한 여정 복잡성 증가
- 프로필이 대기 기간 동안 여정 슬롯을 차지함(91일 여정 시간 초과에 따름)
- 정확한 상태 평가를 위해 대기 기간 내에 전환 이벤트를 AEP에 수집해야 합니다.
- 옵션 A에 비해 더 긴 제공 시간

**Experience League:**

- [대기 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [조건 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### 옵션 C: 빈도 거버넌스를 사용하여 이벤트가 트리거됨

**가장 적합한 대상:** 메시지 피로가 우려되는 빈도가 높은 이벤트 소스(페이지 보기, 제품 보기, 검색 쿼리, 장바구니 추가 반복). 옵션 A 또는 옵션 B 위에 오버레이로 적용할 수 있습니다.

**작동 방식:**

이 옵션은 옵션 A 또는 옵션 B에 주파수 거버넌스를 추가하여 과대 메시지를 방지합니다. 빈도가 높은 행동 이벤트(예: 제품 보기 또는 반복된 장바구니 추가)는 짧은 기간 내에 여정을 여러 번 트리거할 수 있습니다. 빈도 거버넌스가 없으면 프로필에서 중복 또는 과도한 메시지를 받을 수 있습니다.

빈도 거버넌스는 프로필이 기간당 채널당 수신하는 메시지 수를 제한하는 AJO 비즈니스 규칙(빈도 제한)과 프로필이 동일한 여정에 다시 입력하기 전에 쿨다운 기간을 정의하는 여정 수준 다시 입력 규칙의 두 가지 보완 메커니즘을 통해 구현됩니다. 비즈니스 규칙은 조직 수준에서 작동하고 모든 캠페인과 여정에 상한선을 적용합니다(예: 일주일에 최대 3개의 이메일), 재입력 콜다운은 개별 여정 수준에서 작동합니다(예: 프로필은 마지막 입력 후 72시간 이내에 이 특정 여정에 다시 입력할 수 없음).

또한 트리거된 여정에 우선 순위 점수를 할당하도록 충돌 및 우선 순위 관리를 구성할 수 있으므로 여러 여정 또는 캠페인이 동일한 프로필에서 경쟁할 때 우선 순위가 가장 높은 커뮤니케이션이 이기도록 할 수 있습니다.

**주요 고려 사항:**

- 빈도 상한은 피로를 방지하고 중요한 트리거 메시지가 전달되도록 하는 것 사이에서 균형을 이루어야 합니다
- 채널별 최대 용량 권장 - 이메일, SMS 및 푸시에 서로 다른 피로도 임계값이 있음
- 여정 재입력 쿨다운 및 조직 수준 빈도 상한은 함께 작동하며, 둘 다 구성해야 합니다
- 우선 순위 점수는 최대 한도에 도달했을 때 통신 승수를 결정합니다. 우선 순위가 높은 여정에게 더 높은 점수를 할당해야 합니다

**장점:**

- 빈도가 높은 이벤트 소스에서 메시지 피로도 방지
- 브랜드 평판 및 구독자 만족도 유지
- 조직 수준의 상한선은 모든 캠페인과 여정에 안전망을 제공합니다.
- 우선 순위 점수는 최대 한도에 도달할 때 가장 중요한 메시지가 전달되도록 합니다

**제한 사항:**

- 일부 자격 있는 프로필은 표시되지 않으며 관련 메시지가 누락될 수 있습니다
- 주파수 상한 구성으로 관리 복잡성 증가
- Caps는 동일한 채널을 공유하는 다른 활성 캠페인 및 여정과 예기치 않게 상호 작용할 수 있습니다
- 메시징 포트폴리오 변화에 따라 지속적인 모니터링 및 조정 필요

**Experience League:**

- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [비즈니스 규칙 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)

### 옵션 비교

다음 표에서는 주요 기준에서 세 가지 구현 옵션을 비교합니다.

| 기준 | 옵션 A: 간단한 이벤트 트리거됨 | 옵션 B: 대기가 있는 조건부 | 옵션 C: 빈도 거버넌스 |
| --- | --- | --- | --- |
| 다음에 최적 | 즉각적인 확인, 승인 | 포기 복구, 지연된 조건부 응답 | 고주파 이벤트 소스, 다중 여정 환경 |
| 복잡성 | 낮음 | 중간 | Medium-High (A 또는 B에 추가) |
| 메시지 지연 | 초 ~ 분 | 분 ~ 시간/일(구성 가능한 대기 시간) | 기본 옵션과 동일(A 또는 B) |
| 자동 전환 확인 | 아니요 | 예(조건 또는 종료 기준을 통해) | 기본 옵션에 따라 다름 |
| 주파수 보호 | 없음(C와 결합되지 않은 경우) | 없음(C와 결합되지 않은 경우) | 예 — 채널 캡 및 재입력 쿨다운 |
| 여정 캔버스 노드 | 3-4(이벤트, 선택적 조건, 작업, 종료) | 5-7(이벤트, 대기, 조건, 분기, 작업, 종료) | A 또는 B와 동일하며 비즈니스 규칙 구성 |
| 필요 | 이벤트 스키마, 채널 표면, 메시지 콘텐츠 | 모든 옵션 A + 전환 이벤트 수집 | 옵션 A 또는 B + 빈도 규칙 구성 모두 |

### 적절한 옵션 선택

다음 의사 결정 지침을 사용하여 올바른 구현 옵션을 선택합니다.

1. **지연 없이 메시지를 즉시 보내야 합니까?** 그렇다면 **옵션 A**(으)로 시작하십시오. 확인 메시지, 시작 이메일 및 승인은 일반적으로 대기 기간이 필요하지 않습니다.

2. **메시지를 받기 전에 고객이 직접 전환할 수 있어야 합니까?** 그렇다면 **옵션 B**&#x200B;을 선택하세요. 장바구니 포기, 찾아보기 포기 및 체험판 만료 사용 사례는 고객이 직접 작업을 완료할 수 있는 대기 기간을 제공합니다.

3. **트리거 이벤트가 빈도가 높습니까?(동일한 프로필에 대해 세션당 또는 일별로 여러 번 발생)** 그렇다면 옵션 A 또는 B 위에 **옵션 C**&#x200B;을(를) 오버레이로 추가하십시오. 제품 보기, 페이지 보기 및 검색 이벤트는 주파수 보호가 필요한 많은 양의 트리거를 생성할 수 있습니다.

4. **샌드박스에서 여러 개의 트리거된 여정 및 캠페인이 활성화되어 있습니까?** 그렇다면 이벤트 빈도에 관계없이 **옵션 C**&#x200B;을(를) 추가하여 여정 간 통신 부하를 관리하고 채널 피로를 방지하십시오.

실제로 대부분의 프로덕션 구현은 포기 스타일 사용 사례에 옵션 B + C를 사용하고(빈도 거버넌스로 조건부 대기) 확인 스타일 사용 사례에 옵션 A + C를 사용합니다(빈도 거버넌스를 안전 네트워크로 즉시 전송).

## 구현 단계

다음 단계에서는 이벤트 트리거 메시지의 전체적인 구현을 살펴봅니다.

### 1단계: 이벤트 스키마 및 데이터 수집 구성

**응용 프로그램 함수:** AEP: 데이터 모델링(F2), AEP: 데이터 소스 및 수집(F3)

**구성할 내용:** 트리거 이벤트를 캡처하는 XDM ExperienceEvent 스키마, 이러한 이벤트를 저장하는 데이터 세트, 이벤트를 AEP으로 스트리밍하는 실시간 데이터 수집 파이프라인(Web SDK, Mobile SDK 또는 Server API). 이 단계는 여정이 수신할 데이터 기반을 확립합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 이벤트 유형을 트리거하는 중**
>
>메시지를 트리거하는 이벤트 이벤트 유형은 필요한 스키마 필드와 수집 방법을 결정합니다.
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| Commerce 이벤트(장바구니 추가, 구매, 체크아웃) | 전자 상거래 사용 사례 — 장바구니 포기, 구매 후 | `productListItems`, `cart`, `order` 필드가 있는 Commerce 필드 그룹이 필요합니다. |
>| 웹 인터랙션 이벤트(페이지 보기, 제품 보기) | 찾아보기 포기, 콘텐츠 참여 트리거 | `webPageDetails`, `webInteraction` 필드가 있는 웹 세부 정보 필드 그룹이 필요합니다. |
>| 애플리케이션 이벤트(앱 설치, 제거, 인앱 작업) | 모바일 참여 트리거 | 모바일 SDK 구현 및 애플리케이션 필드 그룹 필요 |
>| 시스템 이벤트(결제 실패, 가입 변경, 상태 업데이트) | 운영 알림 | 시스템 이벤트를 수집하려면 서버측 API 또는 소스 커넥터 필요 |
>| 양식 제출 이벤트 | 리드 생성, 등록 확인 | 양식 데이터 필드를 캡처하는 사용자 정의 필드 그룹 필요 |

>[!NOTE]
>
>**결정: 컬렉션 메서드**
>
>트리거 이벤트는 어떻게 캡처되어 AEP으로 스트리밍됩니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 웹 SDK | 웹 기반 행동 이벤트(장바구니 추가, 페이지 보기, 양식 제출) | 웹 사이트에 웹 SDK 설치 필요. 이벤트는 Edge Network을 통해 실시간으로 스트리밍됩니다. |
>| Mobile SDK | 모바일 앱 이벤트(앱 열기, 인앱 작업, 푸시 토큰 등록) | 기본 앱 또는 React Native 래퍼에서 Mobile SDK 통합 필요 |
>| Edge Network 서버 API | 서버측 시스템 이벤트(결제 처리, 구독 관리, 백엔드 트리거) | 클라이언트측 종속성 없음. 조직의 백엔드 시스템에서 전송된 이벤트 |
>| Source 커넥터 | 외부 시스템(CRM, 마케팅 자동화, 레거시 플랫폼)의 이벤트 | 일반적으로 일괄 처리 기반, 스트리밍이 가능하지 않은 한 실시간 트리거를 지원하지 않을 수 있음 |

**UI 탐색:** 데이터 수집 > 데이터스트림 > 새 데이터스트림(데이터스트림 설정용), 스키마 > 스키마 만들기(이벤트 스키마용), 데이터 세트 > 스키마에서 데이터 세트 만들기(데이터 세트 생성용)

**키 구성 세부 정보:**

- 이벤트 스키마에는 여정 조건 평가 및 메시지 개인화에 필요한 모든 필드가 포함되어야 합니다
- 데이터 스트림에는 [!DNL Adobe Experience Platform] 및 [!DNL Adobe Journey Optimizer] 서비스가 모두 활성화되어 있어야 합니다.
- 이벤트가 통합 프로필과 연결되도록 실시간 고객 프로필에 대해 데이터 세트를 활성화해야 합니다
- 이벤트 데이터에는 알려진 프로필로 확인할 수 있는 ID 필드(이메일, CRM ID, ECID)가 포함되어야 합니다

**Experience League 설명서:**

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [스트리밍 수집 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### 2단계: ID 및 프로필 구성

**응용 프로그램 함수:** AEP: ID 및 프로필 구성(F4)

**구성할 내용:** 트리거 이벤트의 식별자에 대한 ID 네임스페이스, 이벤트 스키마에 대한 기본 ID 지정, 장치 간 확인을 위한 ID 연결 규칙 및 프로필 통합을 위한 병합 정책. 이렇게 하면 트리거 이벤트가 통합 고객 프로필과 연결되어 여정이 연락처 정보를 해결하고 메시지를 전달할 수 있습니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 이벤트 스키마에 대한 기본 ID**
>
>트리거 이벤트의 어떤 ID 필드가 프로필 확인을 위한 기본 ID로 사용되어야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 이메일 주소 | 이메일이 캡처되는 인증된 웹 세션 또는 양식의 이벤트 | 연결 가능한 ID에 대한 직접 해결. 이메일 게재에 대한 가장 간단한 경로 |
>| CRM ID | CRM ID가 기본 식별자인 인증된 시스템의 이벤트 | CRM ID 네임스페이스 만들기 필요, 프로필에 메시지 전달을 위해 연결된 이메일 또는 전화가 있어야 함 |
>| ECID (Experience Cloud ID) | 인증된 ID를 사용할 수 없는 익명 웹 또는 앱 이벤트 | ECID를 알려진 ID에 연결하려면 ID 결합이 필요합니다. 메시지는 ECID로만 보낼 수 없습니다. |
>| 전화번호 | 모바일 또는 콜 센터 상호 작용의 이벤트 | SMS 게재 지원, 전화 네임스페이스 필요 |

**UI 탐색:** ID > ID 네임스페이스 만들기; 스키마 > 스키마 선택 > 필드 선택 > ID > 기본 ID로 설정; 프로필 > 병합 정책

**키 구성 세부 정보:**

- 익명 이벤트(ECID 전용)는 ECID가 ID 그래프를 통해 알려진 연결 가능한 ID(이메일, 전화)에 연결될 때까지 메시지 게재를 트리거할 수 없습니다
- AJO에서 사용하는 병합 정책은 대상 평가에 사용되는 병합 정책과 일치해야 합니다
- 웹 기반 트리거 메시지의 경우, ID 그래프가 로그인 이벤트를 통해 ECID를 인증된 ID에 연결하는지 확인합니다

**Experience League 설명서:**

- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [아이덴티티 그래프 연결 규칙](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### 3단계: 채널 표면 설정

**응용 프로그램 함수:** AJO: 채널 구성

**구성할 내용:** 트리거된 메시지의 전송 인프라(하위 도메인 위임, IP 풀, 보낸 사람 ID, 회신 주소, 구독 취소 처리 및 채널별 자격 증명(SMS 공급자, 푸시 인증서)을 정의하는 채널 표면(사전 설정). 메시지 콘텐츠를 만들거나 여정을 게시하려면 유효한 채널 표면이 있어야 합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 메시지 채널**
>
>트리거된 메시지는 어느 채널을 사용합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 이메일 | 가장 많이 트리거된 메시징 사용 사례 — 중단 복구, 확인, 온보딩 | 하위 도메인 위임, IP 풀, 발신자 구성 필요, 풍부한 HTML 콘텐츠 및 개인화 지원 |
>| SMS | 시간에 민감한 알림, 간결한 경고, SMS 참여도가 높은 대상자 | SMS 공급자 통합(Sinch, Twilio, Infobip) 필요, 문자 제한 및 보다 엄격한 동의 요구 사항 적용 |
>| 푸시 알림 | 모바일 앱 참여, 앱 사용자의 재참여 | 푸시 자격 증명 구성(iOS용 APNs, Android용 FCM)이 필요합니다. 사용자에게 푸시 기능이 활성화된 앱이 설치되어 있어야 합니다. |
>| 여러 채널 | 채널 환경 설정 또는 폴백 논리를 사용한 포괄적인 참여 전략 | 여러 채널 표면 필요, 여정 조건 노드를 통해 채널 선택 관리 가능 |

>[!NOTE]
>
>**결정: 하위 도메인 위임 방법(이메일)**
>
>이메일 전송 하위 도메인을 Adobe에 위임하는 방법은 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 전체 위임 | 조직은 Adobe이 보내는 하위 도메인에 대한 모든 DNS 레코드를 관리하도록 합니다. | 가장 간단한 설정: Adobe이 SPF, DKIM, DMARC 레코드를 자동으로 관리 |
>| CNAME 위임 | 조직에서 Adobe 인프라를 가리키는 동안 DNS 제어를 유지하고자 함 | 수동 DNS 레코드 관리 필요, DNS에 대한 보다 조직적인 제어 제공 |

**UI 탐색:** 관리 > 채널 > 하위 도메인(하위 도메인 설정용), 관리 > 채널 > IP 풀(IP 풀 구성용), 관리 > 채널 > 채널 표면 > 표면 만들기(표면 생성용)

**키 구성 세부 정보:**

- 하위 도메인 확인 및 DNS 전파는 최대 48시간이 소요될 수 있습니다
- 새로운 IP 풀에는 준비 계획(2~4주 간의 점진적 볼륨 증가)이 필요합니다.
- 이메일 규정 준수를 위해 원클릭 목록 구독 취소 헤더 구성
- SMS의 경우 SMS 채널 표면을 만들기 전에 공급자 자격 증명을 구성합니다
- 푸시의 경우 푸시 채널 표면을 만들기 전에 APNs 및 FCM 자격 증명을 구성합니다

**Experience League 설명서:**

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [채널 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 4단계: 메시지 콘텐츠 만들기

**응용 프로그램 함수:** AJO: 메시지 작성

**구성할 내용:** 레이아웃 디자인, 프로필 및 이벤트 특성을 사용한 개인화 토큰, 조건부 콘텐츠 블록, 재사용 가능한 조각(머리글, 바닥글, 법적 고지 사항), 콘텐츠 미리 보기 및 테스트를 포함하여 여정이 제공할 메시지 콘텐츠입니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 콘텐츠 접근 방식**
>
>메시지 콘텐츠는 어떻게 생성해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 기존 템플릿에서 시작 | 조직 템플릿이 존재하며 브랜드 일관성이 필요합니다. | 컨텐츠 작성에 대한 가장 빠른 경로, 브랜드 규정 준수 보장, 템플릿 변경 사항이 새 메시지로 전달 |
>| 이메일 Designer에서 처음부터 디자인 | 이 특정 트리거 메시지에 필요한 사용자 지정 레이아웃 | 완벽한 크리에이티브 제어, 드래그 앤 드롭 시각적 편집기, 느리지만 보다 유연한 |
>| HTML 가져오기 | 콘텐츠는 외부 팀이나 에이전시가 디자인하며 HTML으로 제공됩니다 | HTML 코딩 전문 지식 필요, 일부 이메일 Designer 기능을 완전히 지원하지 않을 수 있음 |

>[!NOTE]
>
>**결정: 이벤트 개인화**
>
>메시지 콘텐츠에서 어떤 이벤트 데이터를 사용해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 이벤트 컨텍스트 속성 | 메시지에는 트리거 이벤트의 세부 사항(제품 이름, 장바구니 값, 양식 필드)이 포함되어야 합니다 | 개인화 편집기에서 컨텍스트 기반 이벤트 속성 을 사용합니다. 데이터는 트리거 이벤트 페이로드에서 가져옵니다. |
>| 프로필 속성 | 메시지에는 프로필 수준 데이터(이름, 충성도 계층, 위치)가 포함되어야 합니다 | XDM 경로(예: `profile.person.name.firstName`)를 통해 프로필 속성을 사용합니다. 데이터는 통합 프로필에서 가져옵니다. |
>| 이벤트 및 프로필 속성 모두 | 이 메시지는 이벤트 컨텍스트를 프로필 개인화와 결합해야 합니다 | 트리거된 메시지에 대한 가장 일반적인 접근 방식, 관련성(이벤트) 및 개인화(프로필) 모두 보장 |

**UI 탐색:** 콘텐츠 관리 > 콘텐츠 템플릿 > 찾아보기(템플릿 선택), Campaign 또는 여정 작업 > 콘텐츠 편집 > 이메일 Designer(콘텐츠 디자인), 텍스트 구성 요소 > Personalization 아이콘(개인화 추가) 선택

**키 구성 세부 정보:**

- 컨텍스트 속성을 사용하여 트리거 이벤트의 데이터(예: 제품 이름, 장바구니 값)로 개인화합니다
- 이름, 환경 설정 및 충성도 데이터에 프로필 속성 사용
- 프로필 세그먼트 또는 속성에 따라 컨텐츠를 달리하도록 조건부 컨텐츠 블록을 구성합니다(예: 충성도 멤버의 경우 다른 CTA).
- 트리거된 메시지 간에 공유되는 머리글, 바닥글 및 법적 고지 사항에 대해 재사용 가능한 조각 만들기
- 개인화가 올바르게 렌더링되는지 확인하기 위해 여러 테스트 프로필로 미리 보기
- 여정을 게시하기 전에 내부 이해 당사자에게 증명 보내기

**Experience League 설명서:**

- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 5단계: 여정 만들기 및 구성

**응용 프로그램 기능:** AJO: Journey Orchestration, AJO: 빈도 및 비즈니스 규칙(옵션 C), AJO: 충돌 및 우선 순위 관리

**구성할 내용:** 트리거 이벤트를 수신하고 메시지 배달을 조정하는 여정. 여정 항목 노드, 조건 노드, 대기 단계(옵션 B의 경우), 메시지 작업 노드 및 종료 기준을 사용하여 이벤트 캔버스를 디자인하는 핵심 구현 단계입니다. 이 단계에서는 빈도 거버넌스(옵션 C) 및 충돌/우선 순위 구성도 다룹니다.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 다시 입력 규칙**
>
>트리거링 이벤트가 다시 발생하는 경우 프로필이 이 여정으로 다시 들어갈 수 있습니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 다시 입력 허용(쿨다운 포함) | 이벤트는 합법적으로 다시 발생할 수 있으며 각 발생에 메시지가 표시됩니다(예: 각 장바구니 포기는 복구 메시지를 트리거해야 함) | 쿨다운 기간(최소 5분)을 설정하여 중복 이벤트가 신속하게 재입력되지 않도록 합니다. 일반적인 쿨다운 시간은 1시간에서 72시간입니다. |
>| 재입력 없음 | 메시지는 이벤트 반복에 관계없이 프로필당 한 번만 전송되어야 합니다(예: 첫 번째 등록 후 환영 메시지) | 프로필은 첫 번째 여정 완료 후 영구적으로 제외됩니다. 일회성 라이프사이클 메시지에 적합합니다 |

>[!NOTE]
>
>**결정: 대기 기간(옵션 B만 해당)**
>
>여정이 조건을 평가하고 메시지를 보내기 전에 얼마나 기다려야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 짧은 대기 시간(1~4시간) | 즉각적인 후속 조치가 효과적인 장바구니 포기와 같은 긴급도가 높은 사용 사례 | 메시지 볼륨이 높을수록 일부 자체 변환기를 사용할 수 있으며, 장바구니 복구 비용이 높음 |
>| Medium 대기 시간(12~24시간) | 찾아보기 포기 또는 콘텐츠 참여와 같은 보통-긴급도 사용 사례 | 균형 잡힌 접근 방식, 관련성을 유지하면서 불필요한 전송을 줄임 |
>| 긴 대기 시간(2~7일) | 체험판 만료 알림 또는 정기 체크인과 같은 긴급도가 낮은 사용 사례 | 메시지 양 감소, 상황별 연관성 손실 위험 증가 |
>| 사용자 정의 날짜/시간 | 특정 날짜에 연결된 사용 사례(예: 체험판 만료일 3일 전 보내기) | 계산된 날짜/시간까지 대기; 사용자 정의 표현식 편집기를 사용합니다. |

>[!NOTE]
>
>**결정: 종료 기준**
>
>메시지 작업에 도달하기 전에 어떤 조건에서 여정을 제거해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 전환 이벤트(예: 구매 완료) | 목표가 전환인 장바구니 또는 찾아보기 포기 | 전환 이벤트가 감지되면 프로필이 자동으로 종료됩니다. 옵션 B에 대한 가장 깨끗한 접근 방식 |
>| 대상자 멤버십 변경 | 자격 있는 세그먼트를 벗어나는 경우 프로필이 종료되어야 합니다. | 거의 실시간으로 업데이트되는 스트리밍 평가 대상 필요 |
>| 여정 시간 초과(최대 91일) | 기본 비헤이비어 - 프로필이 최대 여정 기간 후에 종료됩니다. | 안전 망입니다. 단기간 트리거된 여정의 주요 종료 메커니즘이 되어서는 안 됩니다. |
>| 명시적 종료 기준 없음 | 자격을 갖춘 모든 프로필에서 메시지를 수신해야 하는 간단한 확인(옵션 A) | 메시지 작업 및 종료 노드 후 프로필이 자연적으로 종료됨 |

>[!NOTE]
>
>**결정: 빈도 거버넌스(옵션 C)**
>
>프로필은 기간당 몇 개의 트리거된 메시지를 수신해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 채널별 상한(예: 이메일/주 3개, SMS/일 1개) | 채널마다 피로도 임계값이 다름 | 권장 접근 방식, 각 채널의 침입 수준을 고려 |
>| 글로벌 상한(예: 모든 채널에서 매주 5개의 메시지) | 모든 커뮤니케이션 유형에 대한 거버넌스 단순화 | 관리가 쉬워지지만 미묘한 차이를 줄이며, 방해가 적은 채널을 과도하게 제한할 수 있음 |
>| 여정 수준 재입력 쿨다운만 | 이 특정 여정에 필요한 빈도 거버넌스이지만 조직 전체에는 필요하지 않음 | 가장 간단한 구현으로 여정 간 피로로부터 보호되지 않음 |

**UI 탐색:** 여정 > 여정 만들기(여정 만들기), 여정 캔버스 > 이벤트 활동 드래그(이벤트 입력), 여정 캔버스 > 드래그 &quot;대기&quot; 활동(대기 구성), 여정 캔버스 > 드래그 &quot;조건&quot; 활동(조건 분기), 여정 속성 > 종료 기준(종료 구성), 관리 > 비즈니스 규칙 > 규칙 만들기(빈도 제한)

**키 구성 세부 정보:**

- 이벤트 스키마를 선택하고 자격 조건을 정의하여 여정 이벤트를 구성합니다
- 옵션 B의 경우 이벤트 항목 바로 뒤에 조건 평가 앞에 대기 노드를 추가합니다
- 프로필 속성, 이벤트 데이터 또는 대상 멤버십 검사를 사용하여 조건 노드 구성
- 메시지 작업 노드를 채널 표면에 연결하고 3단계 및 4단계에서 작성된 콘텐츠
- 여정 시간 제한을 적절한 기간(트리거된 여정의 경우 91일 미만)으로 설정합니다.
- 옵션 C의 경우 여정을 게시하기 전에 관리 > 비즈니스 규칙을 통해 빈도 규칙을 만듭니다
- 다른 캠페인이나 여정이 겹치는 대상을 타겟팅하는 경우 여정에 우선 순위 점수를 할당합니다

**옵션이 나뉘는 위치:**

**옵션 A의 경우(간단한 이벤트가 트리거됨):**
여정 캔버스는 최소입니다. 이벤트 항목 > 선택적 동의/자격 조건 > 메시지 작업 > 끝. 대기 단계 또는 전환 확인이 없습니다. 이벤트가 발생할 때마다 메시지를 생성해야 하는지에 따라 재입력 규칙을 설정합니다.

옵션 B의 **조건(대기 시간 포함):**
이벤트 항목 뒤에 대기 노드를 추가합니다. 대기 후 전환을 확인할 조건 노드(예: 여정 입력 후 `commerce.purchases` 이벤트가 발생했는지 확인)를 추가하거나 종료 기준을 사용하여 전환된 프로필을 자동으로 제거합니다. &quot;변환되지 않음&quot; 경로의 메시지 작업과 &quot;변환된&quot; 경로의 끝 노드로 분기합니다.

**옵션 C의 경우(빈도 거버넌스):**
게시하기 전에 관리 > 비즈니스 규칙을 통해 조직 수준 빈도 상한을 구성합니다. 여정 속성에서 여정 수준 재입력 쿨다운을 설정합니다. 필요한 경우 여정 속성을 통해 우선 순위 점수를 할당하여 최대 한도에 도달할 때 성공하는 커뮤니케이션을 제어합니다. 옵션 A 또는 옵션 B 위에 적용할 수 있습니다.

**Experience League 설명서:**

- [여정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [일반 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [조건 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [여정에 메시지 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### 6단계: 여정 테스트 및 배포

**응용 프로그램 함수:** AJO: Journey Orchestration

**구성할 내용:** 테스트 모드 유효성 검사로 여정이 테스트 프로필에서 예상대로 작동하는지 확인한 다음 게시를 게시하여 실시간으로 만듭니다.

**UI 탐색:** 여정 캔버스 > 테스트 모드 전환(테스트용), 여정 캔버스 > 게시(배포용)

**키 구성 세부 정보:**

- 여정 캔버스에서 테스트 모드를 활성화하여 테스트 프로필로 이벤트 트리거를 시뮬레이션합니다.
- 유효한 채널 연락처 정보(이메일 주소, 전화번호)가 있는 테스트 프로필 선택
- 테스트 이벤트를 트리거하고 테스트 프로필이 예상 경로를 통과하는지 확인합니다.
- 옵션 B의 경우 대기 단계가 올바르게 작동하고 조건 평가가 예상 분기를 생성하는지 확인합니다
- 테스트 메시지에서 개인화 토큰이 올바르게 렌더링되는지 확인
- 테스트가 성공하면 여정을 게시하여 라이브로 만듭니다
- 게시 후 여정 상태 및 초기 프로필 항목 지표 모니터링

**Experience League 설명서:**

- [여정 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### 7단계: 성능 모니터링 및 보고

**응용 프로그램 함수:** AJO: 보고 및 성능 분석, S4: 모니터링 및 관찰, S5: 보고 및 분석

**구성할 내용:** 게재 및 참여 모니터링을 위한 실시간 및 내역 여정 보고서, 이벤트 수집 및 여정 처리 실패를 위한 플랫폼 알림, 트리거된 메시지 효과에 대한 심층적인 크로스 채널 분석을 위한 선택적 CJA 작업 공간.

이 단계의 **결정 지점:**

>[!NOTE]
>
>**결정: 보고 깊이**
>
>이 사용 사례에 필요한 보고 분석은 얼마입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| AJO 기본 보고서만 | 게재 지표의 운영 모니터링으로 충분함 | 즉시 사용 가능, 전송, 배송, 반송, 열기, 클릭, 추가 구성 필요 없음 |
>| AJO 기본 + CJA 통합 | 크로스 채널 분석, 전환 속성 및 추세 분석이 필요합니다 | CJA 데이터 세트에 연결된 AJO 연결 및 데이터 보기가 필요하고 심층적인 분석 기능을 제공합니다. |

**UI 탐색:** 여정 > 여정 선택 > 라이브 보고서(라이브 모니터링용), 여정 > 여정 선택 > 모든 시간 보고서(내역 분석용), 경고 > 경고 규칙 > 가입(경고 구성용)

**키 구성 세부 정보:**

- 활성 실행 중에 여정 라이브 보고서에 액세스하여 프로필 항목, 종료 및 게재 지표를 모니터링합니다
- 의미 있는 데이터를 축적하기 위해 여정이 충분한 시간 동안 활성화된 후 내역 보고서를 검토합니다
- 소스 플로우 실행 실패(이벤트 수집) 및 여정 처리 지연에 대한 경고 구성
- CJA 통합의 경우 CJA 연결에 AJO 경험 이벤트 데이터 세트(메시지 피드백 이벤트 데이터 세트, 이메일 추적 경험 이벤트 데이터 세트)가 포함되어 있는지 확인합니다

**Experience League 설명서:**

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## 구현 시 고려 사항

이 섹션에서는 이벤트 트리거 메시징 구현에 대한 보호, 일반적인 위험, 우수 사례 및 절충 결정을 다룹니다.

### 보호 기능 및 제한 사항

이벤트가 트리거된 메시징 구현에는 다음과 같은 플랫폼 보호 및 제한이 적용됩니다.

- **단일 이벤트 처리량:** 단일 이벤트 여정에 대한 샌드박스당 초당 최대 5,000개 이벤트 — [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- **실시간 여정 제한:** 샌드박스당 최대 500개의 실시간 여정 — [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- **여정 캔버스 제한:** 여정 캔버스당 최대 50개 활동
- **여정 시간 제한:** 최대 여정 기간은 91일입니다(전역 시간 제한)
- **다시 시작 쿨다운:** 최소 다시 시작 쿨다운은 5분입니다
- **빈도 제한 구성:** 샌드박스당 최대 10개의 제한 구성
- **채널 표면:** 샌드박스당 채널 유형당 최대 10개 채널 표면
- **스트리밍 수집:** HTTP 연결당 초당 최대 20,000개의 레코드 — [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- **연산 속성:** 샌드박스당 최대 25개의 연산 속성 — [연산 속성 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview#guardrails)
- **콘텐츠 조각:** 메시지당 최대 30개의 콘텐츠 조각
- **실시간 보고서 새로 고침:** 실시간 보고서는 60초마다 새로 고침되며 지난 24시간 동안의 데이터를 표시합니다
- **이전 보고서 대기 시간:** 이전(항상) 보고서는 실행이 끝난 후 완전히 채워지는 데 최대 2시간이 걸릴 수 있습니다

### 일반적인 함정

이벤트가 트리거된 메시징을 구현할 때 다음과 같은 일반적인 문제를 알고 있어야 합니다.

- **ID 확인이 없는 익명 이벤트:** ECID(익명 쿠키 ID)만 전달하는 이벤트를 트리거하면 메시지 배달을 위해 연결 가능한 프로필로 확인할 수 없습니다. 트리거 이벤트에 인증된 ID가 포함되어 있는지 또는 ID 그래프가 ECID를 알려진 연락처에 연결하는지 확인합니다. ID를 확인하지 않으면 프로필이 여정을 입력하지만 메시지 게재 단계에서 실패합니다.

- **옵션 B 조건 검사에 대한 전환 이벤트 누락:** 전환 이벤트(예: 구매)가 AEP에 수집되지 않았거나 트리거 이벤트와 동일한 프로필 ID와 연결되어 있지 않으면 조건 검사가 &quot;전환되지 않음&quot;으로 잘못 평가되어 불필요한 메시지를 보냅니다. 전환 이벤트가 실시간으로 AEP으로 유입되는지 확인하고 트리거 이벤트와 ID를 공유합니다.

- **너무 허용 재입력 규칙:** 빈도가 높은 이벤트 원본에서 쿨다운 기간 없이 재입력을 허용하면 동일한 프로필에서 몇 분 안에 여러 메시지를 받을 수 있습니다. 항상 비즈니스 컨텍스트와 일치하는 재입력 쿨다운(예: 장바구니 포기의 경우 4시간 쿨다운, 찾아보기 포기의 경우 24시간 쿨다운)을 설정하십시오.

- **대기 단계 표준 시간대 오정렬:** 대기 단계가 기본적으로 UTC로 처리됩니다. 여정이 여러 시간대에 걸쳐 프로필을 타겟팅하고 대기 시간이 수신자의 현지 시간과 일치해야 하는 경우 그에 따라 여정에서 시간대 설정을 구성합니다.

- **다른 캠페인과 충돌하는 빈도 상한:** 조직 수준의 빈도 상한은 모든 캠페인과 여정에 적용됩니다. 프로필이 다른 활성 캠페인에서 이미 상한에 도달한 경우 새 트리거된 여정이 표시되지 않을 수 있습니다. 제외 비율을 모니터링하고 우선 순위 점수를 조정하여 중요한 트리거 메시지가 우선 순위를 갖도록 합니다.

- 종속성 누락으로 인해 **여정 게시가 실패했습니다.** 여정 캔버스의 모든 분기는 종료 활동으로 종료되어야 합니다. 모든 작업 노드는 활성 메시지 콘텐츠가 있는 유효한 채널 표면을 참조해야 합니다. 게시하기 전에 모든 종속성을 확인하십시오.

### 우수 사례

성공적인 이벤트 트리거 메시징 구현을 위해 다음 권장 사항을 따르십시오.

- **단순하게 시작한 다음 반복:** 옵션 A로 시작하여 새로 트리거된 메시징 사용 사례를 확인합니다. 이벤트 파이프라인 및 메시지 게재의 유효성을 검사한 후에만 대기 및 조건 논리(옵션 B)를 추가합니다. 여러 트리거된 여정이 활성 상태일 때 빈도 거버넌스(옵션 C)를 추가합니다.

- **전환 확인을 위해 조건 노드 대신 종료 기준을 사용합니다.** 종료 기준은 자격 있는 이벤트(예: 구매)가 발생하면 여정에서 프로필을 자동으로 제거하여 대기 단계 후 명시적 조건 노드가 필요하지 않습니다. 이렇게 하면 더 깨끗한 여정 캔버스와 더 반응형 전환 감지가 만들어집니다.

- **개발 샌드박스에서 실제 이벤트 데이터를 사용하여 테스트:** 테스트 모드를 실제 이벤트 페이로드(테스트 프로필뿐만 아니라)와 함께 사용하여 이벤트 스키마 필드, 개인화 토큰 및 조건 식이 프로덕션 유사 데이터에 올바르게 작동하는지 확인하십시오.

- **이벤트별 재입력 쿨다운 설정:** 쿨다운 기간을 트리거링 이벤트의 비즈니스 컨텍스트와 일치시킵니다. 장바구니 포기 여정은 일반적으로 4~24시간 콜다운을 사용하며, 확인 여정을 통해 즉시 다시 시작할 수 있습니다. 온보딩 여정은 다시 시작할 수 없도록 해야 합니다.

- **상태 지표로 제외율을 모니터링합니다.** 제외율(빈도 제한 또는 조건으로 인해 프로필에 자격이 있지만 메시지를 받지 못함)이 30-40%를 초과하는 경우 제한 수가 너무 제한적인지 또는 트리거링 이벤트가 너무 광범위하게 정의되어 있는지 검토하십시오.

- **실시간 여정을 편집하는 대신 버전 여정:** 실시간 버전을 직접 편집할 수 없습니다. 여정을 복제하고 변경한 다음, 이전 버전을 중지하고 새 버전을 게시하여 새 버전을 만듭니다. 이렇게 하면 현재 여정에 있는 프로필이 중단되는 것을 방지할 수 있습니다.

- **조건 노드에 대체/기본 경로 포함:** 예기치 않은 프로필 상태를 처리할 수 있도록 항상 조건 노드에 기본(기타) 경로를 구성하십시오. 조건 분기와 일치하지 않는 프로필은 중단된 상태를 유지하는 대신 정상적으로 종료되어야 합니다.

### 절충안 결정

이벤트가 트리거되는 메시징 구현을 디자인할 때는 다음 장단점을 고려하십시오.

>[!NOTE]
>
>**절충: 메시지 속도와 메시지 관련성 비교**
>
>즉시 메시지 게재(옵션 A)는 속도를 최대화하지만 자체 전환한 고객에게 메시지를 보낼 수 있습니다. 지연된 조건부 게재(옵션 B)는 자체 변환기를 필터링하여 관련성을 향상시키지만 긴급성을 줄일 수 있는 지연을 제공합니다.
>
>- **옵션 A는 다음과 같습니다.** 모든 이벤트가 메시지를 보증하는 속도, 단순성, 확인 스타일 사용 사례
>- **옵션 B는 다음과 같습니다.** 관련성, 메시지 피로도 감소, 자동 전환이 일반적인 포기 스타일 사용 사례
>- **권장 사항:** 속도가 기본 값인 트랜잭션 및 확인 메시지에 옵션 A를 사용합니다. 관련성이 속도를 능가하는 복구 및 재참여 메시지에 옵션 B를 사용합니다. 대기 기간을 실험하여 각 사용 사례에 대한 최적의 균형을 찾습니다.

>[!NOTE]
>
>**절충점: 주파수 보호와 메시지 범위 비교**
>
>엄격한 빈도 상한(옵션 C)은 피로를 방지하지만 프로필이 상한 근처에 있을 때 중요한 트리거된 메시지를 표시하지 않을 수 있습니다. 허용 또는 제한 없음은 적용 범위를 최대화하지만 과도한 메시징 및 채널 피로도가 발생할 수 있습니다.
>
>- **엄격한 제한 적용:** 고객 경험, 브랜드 신뢰도, 전달성(스팸 불만 감소)
>- **허용 한도 선호:** 메시지 범위, 전환 기회, 누락된 트리거 방지
>- **권장 사항:** 업계 표준 상한(3-5개의 이메일/주, 1-2개의 SMS/주, 2-3개의 푸시/일)으로 시작하고 참여 지표 및 구독 취소 비율에 따라 조정합니다. 최대 한도에 도달했을 때 일괄 처리 캠페인보다 우세하도록 트리거된 메시지에 우선 순위 점수가 높게 할당됩니다.

>[!NOTE]
>
>**절충점: 여정 단순성과 여정 정교성 비교**
>
>간단한 여정(몇 개의 노드, 분기 없음)는 구축, 테스트 및 유지 관리가 더 쉽지만 제한적인 컨텍스트 적응을 제공합니다. 정교한 여정(여러 조건, 분기 경로, 세그먼트 확인)을 통해 보다 정밀한 응답을 사용할 수 있지만 복잡성과 오류 위험이 높아집니다.
>
>- **간단한 여정 사용:** 더 빠른 구현, 더 쉬운 디버깅, 낮은 유지 관리 부담
>- **정교한 여정 선호:** 더 정밀한 타깃팅, 더 나은 개인화, 불필요한 전송 감소
>- **권장 사항:** 비즈니스 요구 사항을 충족하는 가장 간단한 여정으로 시작합니다. 성능 데이터를 기반으로 복잡성을 점진적으로 증가시킵니다. 안정적으로 작동하는 간단한 여정은 감지되지 않은 오류가 있는 복잡한 여정보다 더 중요합니다.

## 관련 설명서

다음 리소스는 이 구현에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

### 여정 편성

- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [여정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [일반 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [대상자 선별 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [조건 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [여정에 메시지 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [여정 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [이메일 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [제외 목록 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### 메시지 작성 및 개인화

- [이메일 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [SMS 메시지 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [푸시 알림 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### 빈도 및 비즈니스 규칙

- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [비즈니스 규칙 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [최대 가용량 API](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/channel-surfaces/capping)

### 충돌 및 우선 순위 관리

- [충돌 및 우선 순위 관리 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [여정 한도 및 중재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### 보고 및 성능

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### 데이터 수집 및 수집

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [스트리밍 수집 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview)

### 데이터 모델링 및 스키마

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

### ID 및 프로필

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [아이덴티티 그래프 연결 규칙](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### 세분화 및 대상자

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### 데이터 거버넌스 및 동의

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### 계산된 속성

- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [계산된 속성 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)

### 모니터링 및 가시성

- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### 튜토리얼 및 안내서

- [여정 자습서 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
