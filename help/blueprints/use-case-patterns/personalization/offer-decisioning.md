---
title: Offer Decisioning
description: 중앙 집중식 의사 결정 논리를 사용하여 여러 채널에서 프로필에 대한 차선책 오퍼 또는 콘텐츠를 선택하는 방법에 대해 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 8fd511b3-0200-41bf-aff1-e3f2a00a578e
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8026'
ht-degree: 2%

---

# Offer Decisioning

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) Decisioning 및 [!DNL Adobe Real-Time Customer Data Platform]&#x200B;(RT-CDP)을 사용하는 Offer Decisioning에 대한 포괄적인 구현 참조를 제공합니다. 채널 전반의 각 고객 프로필에 대한 차선책을 결정하는 중앙 집중식 오퍼 선택 로직을 구현해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

이 안내서를 사용하여 구성해야 하는 사항, 선택 사항이 있는 위치 및 각 의사 결정에 적용되는 상충관계를 파악합니다.

패턴은 &quot;표시할 위치&quot; 채널 논리에서 &quot;표시할 항목&quot; 결정을 분리하여 이메일, 웹, 모바일 앱 및 기타 모든 터치포인트에서 일관되고 최적화된 오퍼 선택을 활성화합니다. AJO Decisioning은 오퍼 생성 및 카탈로그 관리, 자격 규칙(각 오퍼를 볼 수 있는 사용자), 순위 전략(적격 오퍼 중에서 선택하는 방법), 배치(오퍼가 표시되는 위치) 및 의사 결정 정책(모든 것을 결합하는)과 같은 전체 오퍼 라이프사이클을 관리합니다.

## 사용 사례 개요

조직은 상호 작용 시 각 고객에게 가장 관련성이 높은 오퍼, 프로모션 또는 인센티브를 제공해야 하는 경우가 많습니다. 상호 작용이 이메일 여정, 웹 사이트 홈페이지, 모바일 앱 내에서 또는 여러 단계 캠페인의 결정 지점에서 발생하든지 상관없이, 당면 과제는 동일합니다. 고객이 누구이고, 고객이 무엇을 검증하고, 어떤 오퍼가 원하는 결과를 도출할 수 있는지에 따라 사용 가능한 옵션 카탈로그에서 최적 오퍼를 선택합니다.

Offer Decisioning은 AJO의 의사 결정 관리 엔진에서 모든 오퍼 선택 논리를 중앙 집중화하여 이를 해결합니다. 의사 결정 엔진은 오퍼 할당을 개별 캠페인이나 채널로 하드코딩하는 대신 각 프로필의 속성, 대상 멤버십 및 컨텍스트 신호를 평가하여 실시간으로 최상의 오퍼를 결정합니다. 이러한 중앙 집중화를 통해 동일한 고객이 어떤 채널을 통해 접속하는지에 관계없이 일관되고 최적화된 오퍼를 받을 수 있습니다.

이 패턴은 범위가 알려진 방문자 웹/앱 개인화와는 다릅니다. offer decisioning은 채널과 관계없고 중앙 집중화된 반면, 알려진 방문자 개인화는 디지털 표면 개인화에 중점을 둡니다. 이것은 카탈로그 모델의 행동 권장 사항과 다릅니다. 적격 항목 세트가 비즈니스 규칙, 자격 제한 또는 규제 요구 사항(프로모션, 금융 제품, 인센티브)에 의해 제어되는 경우 Offer Decisioning을 사용합니다. 항목 세트가 크고 지속적으로 변경되며 선택 사항이 행동 유사성 또는 선호도 신호(제품 카탈로그, 콘텐츠 라이브러리)에 의해 주도되는 경우 행동 권장 사항을 사용하십시오.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

**[개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.
**KPI:**&#x200B;개 참여, 전환율, 고객 만족도(CSAT)

**[교차 판매 및 상향 판매 매출 촉진](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
행동 및 구매 내역을 기반으로 기존 고객에게 보완 및 프리미엄 제품 또는 서비스를 홍보합니다.
**KPI:** 상향 판매/교차 판매 %, 증분 수익, 고객 생애 가치

**[고객 충성도 및 라이프타임 값 증가](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
고객 관계를 심화하고 충성도 프로그램, 보상 및 개인화된 참여를 통해 장기적인 가치를 극대화합니다.
**KPI:** 고객 생애 가치, 유지, 상향 판매/교차 판매 %

## 예시 전술 사용 사례

다음 시나리오에서는 offer decisioning 을 실제로 적용하는 방법을 보여 줍니다.

- 이메일 캠페인의 다음 베스트 오퍼 — 전송 시 수신자별로 가장 관련성이 높은 프로모션을 선택합니다.
- 웹 사이트의 실시간 프로모션 배너 — 의사 결정은 방문자의 프로필을 기반으로 페이지 로드 시 오퍼를 선택합니다.
- 사용자의 라이프사이클 단계에 가장 좋은 인센티브를 제공하는 개인화된 인앱 카드
- 크로스 채널 오퍼 일관성 — 동일한 의사 결정 로직이 이메일, 웹 및 푸시를 제공하므로 고객은 통합된 오퍼 경험을 볼 수 있습니다.
- 고객 가치 계층에 따라 동적 쿠폰 또는 할인 선택(예: 고가치 고객은 프리미엄 오퍼를 받음)
- 현재 구독 수준에 따라 제품 업그레이드 또는 상향 판매 오퍼 선택
- 계층 및 활동 내역을 기반으로 한 충성도 보상 오퍼 개인화

## 주요 성과 지표

다음 KPI는 Offer Decisioning 구현의 효과를 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 오퍼 수락율 | 클릭, 상환 또는 전환을 초래하는 게재된 오퍼의 비율 | 오퍼 클릭 수 또는 상환 횟수/게재된 총 오퍼 수 |
| 오퍼 선택 배포 | 모든 의사 결정에서 선택한 각 오퍼의 비율 | 오퍼당 카운트 / 렌더링된 총 의사 결정 |
| 대체 비율 | 자격이 있는 개인화된 오퍼와 대체 항목이 제공된 의사 결정의 비율 | 대체 노출 횟수 / 총 결정 수 |
| 전환율 | 원하는 작업(구매, 등록, 상환)을 완료한 오퍼 수신자의 비율 | 전환/오퍼 노출 횟수 |
| 증분 수익 | 선택한 오퍼와 컨트롤 그룹 또는 대체 오퍼를 비교하여 발생하는 수익 | 개인화된 오퍼의 수익 - 대체/제어의 수익 |
| 크로스 채널 일관성 점수 | 정의된 기간 내의 여러 채널에서 동일한 오퍼를 받는 프로필의 비율 | 일관된 오퍼 / 총 멀티채널 노출 횟수 |
| 오퍼 클릭스루 비율 | 클릭을 발생시키는 오퍼 노출 비율입니다. | 오퍼 클릭수 / 오퍼 노출 횟수 |

## 사용 사례 패턴

이 섹션에서는 offer decisioning에 대한 함수 체인 및 패턴 정의에 대해 설명합니다.

**Offer Decisioning**

중앙 집중식 의사 결정 논리를 사용하여 여러 채널에서 프로필에 대한 차선책 오퍼 또는 콘텐츠를 선택합니다.

**함수 체인:** 대상 평가 > 오퍼 자격 > 순위 전략 > 의사 결정 실행 > 게재 > 보고

각 컴포지션이 어떻게 표시되는지 알아보려면 [구현 옵션](#implementation-options) 섹션을 참조하십시오.

## 애플리케이션

이 사용 사례 패턴에는 다음 Adobe 애플리케이션이 사용됩니다.

- **[!DNL Adobe Journey Optimizer] (AJO)** — 오퍼 만들기, 자격 규칙, 순위 전략, 배치 및 의사 결정 정책을 위한 의사 결정 관리 엔진, 오퍼 게재를 위한 채널 구성 및 메시지 작성, 캠페인 및 여정 실행
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** — 오퍼 자격 세그먼트에 대한 대상 평가, 자격 및 순위에 사용되는 프로필 데이터 및 계산된 속성
- **[!DNL Adobe Experience Platform] (AEP)** - AJO과 RT-CDP를 모두 지원하는 통합 프로필 저장소, ID 확인 및 데이터 파운데이션

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | Decisioning 권한이 활성화된 AJO 샌드박스 구현 팀에 할당된 오퍼 관리 역할(의사 결정 관리자, 오퍼 승인자). | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 프로필 스키마에는 오퍼 자격 규칙에 사용되는 특성(예: 충성도 계층, 구매 내역, 구독 유형)이 포함되어야 합니다. 오퍼 노출 횟수, 클릭 수 및 전환을 추적하기 위한 오퍼 응답/상호 작용 스키마가 제자리에 있어야 합니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [스키마 구성 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| 데이터 소스 및 수집 | 가정 위치 | 자격 규칙에 사용되는 프로필 속성은 최신 상태여야 합니다. 웹 게재의 경우(옵션 B), 데이터 스트림에 AJO 서비스를 활성화한 상태로 웹 SDK을 구현해야 합니다. 이메일 게재의 경우 전송 시 프로필 속성을 확인할 수 있어야 합니다. | [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| ID 및 프로필 구성 | 가정 위치 | 오퍼가 게재되는 모든 채널에서 프로필을 확인할 수 있어야 합니다. 크로스 채널 오퍼의 일관성을 위해서는 통합 ID가 중요합니다. 이메일, 웹 및 모바일 컨텍스트에서 동일한 프로필을 인식해야 합니다. 실시간 웹/앱 게재를 위해서는 에지 활성 병합 정책이 필요합니다. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| 대상 정의 및 세분화 | 필수 | 오퍼 자격 기준으로 사용되는 대상을 정의하고 평가해야 합니다(예: &quot;고가치 고객&quot;, &quot;평가판 사용자&quot;, &quot;충성도 골드 계층&quot;). 평가 방법은 게재 지연 시간(실시간 웹/앱에 대한 에지 평가, 이메일 캠페인에 대한 일괄 처리 또는 스트리밍)과 일치해야 합니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 고객 AI 성향 점수, 라이프타임 값 계산 및 참여 지표는 순위 전략 효율성을 크게 향상시킵니다. &quot;마지막 구매 이후 일 수&quot; 또는 &quot;90일 동안의 총 지출&quot;과 같은 계산된 속성을 사용하면 보다 정확한 자격 규칙 및 공식 기반 순위를 사용할 수 있습니다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Customer AI 개요](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| 데이터 수명 주기 관리 | 추천 | 오퍼 내역 및 의사 결정 이벤트 데이터는 시간이 지남에 따라 누적됩니다. 스토리지를 관리하고 데이터 보존 요구 사항을 준수하기 위해 오퍼 상호 작용 이벤트 데이터 세트에 대해 보존 정책(만료)을 구성해야 합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [데이터 세트 만료](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 거버넌스 레이블은 중요한 타겟팅 기준(예: 재무 상태, 상태)이 있는 오퍼가 데이터 사용 정책을 준수하도록 합니다. 자격 규칙에 사용된 필드의 레이블은 호환되지 않는 오퍼 타깃팅을 방지합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview) |
| 모니터링 및 가시성 | 추천 | 의사 결정 엔진 성능, 대체 비율 및 오퍼 게재 상태를 모니터링해야 합니다. 높은 대체 비율에 대한 경고는 자격 규칙 오구성 또는 데이터 새로 고침 문제를 나타낼 수 있습니다. | [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [가시성 통찰력 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | 오퍼 성능 보고는 기능 체인의 일부입니다(7단계). CJA 분석을 통해 크로스 채널 오퍼 효율성 측정, 매출 영향 속성 및 최적화 기회를 식별할 수 있습니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer]&#x200B;(AJO)

다음 표에는 AJO 함수와 해당 함수가 구성된 구현 단계가 나열되어 있습니다.

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 결정 | 3단계: 의사 결정 설정 | 오퍼 항목 만들기, 자격 규칙 정의, 등급 전략 구성, 대체 오퍼 만들기, 배치 정의 및 의사 결정 정책 빌드 |
| 채널 구성 | 4단계: 채널 및 표면 구성 | 오퍼 게재를 위한 이메일, 웹, 인앱 또는 코드 기반 채널 표면 구성 |
| 메시지 작성 | 5단계: 콘텐츠 및 게재 구성 | 오퍼 배치 영역을 사용하여 메시지 템플릿 디자인, 웹/앱 전달을 위한 코드 기반 경험 구성 |
| 캠페인 실행 | 5단계: 콘텐츠 및 게재 구성 | 의사 결정 정책을 호출하는 예약되거나 API 트리거된 캠페인 실행(옵션 A) |
| 콘텐츠 실험 | 5단계: 콘텐츠 및 게재 구성 | 선택적으로 A/B는 다양한 순위 전략을 테스트하거나 창의적인 변형을 제공합니다 |
| 보고 및 성능 분석 | 7단계: 보고 및 성능 모니터링 | 오퍼 선택 분포, 수락율, 대체 비율 및 채널 수준 성과 모니터링 |

### [!DNL Real-Time CDP]&#x200B;(RT-CDP)

다음 표에는 RT-CDP 함수와 이러한 함수가 구성된 구현 단계가 나와 있습니다.

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 2단계: 대상 평가 | 오퍼 자격 규칙에 사용되는 대상을 정의하고 평가합니다. 적절한 평가 방법(일괄 처리, 스트리밍 또는 에지)을 선택합니다. |
| 프로필 보강 | 1단계(지원): 계산된 속성 | 순위 전략 효율성을 개선하는 계산된 속성 및 성향 점수로 프로필을 보강합니다 |

## 필요 조건

구현을 시작하기 전에 다음 전제 조건을 완료하십시오.

- [ 의사 결정 관리 기능이 활성화된 ] AJO 샌드박스
- [ 의사 결정 관리 권한(오퍼 만들기/편집, 배치, 의사 결정)이 있는 ] 사용자 역할
- [ ] 프로필 스키마에는 오퍼 자격 요건(예: 충성도 계층, 고객 세그먼트, 구독 수준)에 필요한 특성이 포함되어 있습니다.
- [ ] 프로필 데이터가 현재 자격 특성 새로 고침에 대해 수집되고 있습니다.
- [ 옵션 A의 ] (이메일): 확인된 하위 도메인과 웜된 IP 풀로 구성된 이메일 채널 표면
- [ 옵션 B(웹/앱)의 ]: 데이터 스트림에 AJO 서비스를 사용하도록 설정한 웹 SDK이 구현되었습니다. 에지 활성 병합 정책이 구성되었습니다.
- [ 옵션 C의 ] (여정): 여정 캔버스 권한 및 하나 이상의 여정 항목 이벤트 또는 대상이 구성되었습니다.
- [ ] 각 오퍼 및 배치 조합에 대해 준비된 오퍼 크리에이티브 자산(이미지, 복사본, CTA)
- [ 각 배치에 대해 준비된 대체 오퍼 콘텐츠 ]
- [ RT-CDP에서 정의되고 평가된 오퍼 자격 규칙에 대한 ]개 대상

## 구현 옵션

이 섹션에서는 offer decisioning에 사용할 수 있는 구현 옵션에 대해 설명합니다. 각 옵션은 다른 게재 채널 및 사용 사례 컨텍스트를 제공합니다.

### 옵션 A: 이메일 offer decisioning

이 옵션은 아웃바운드 이메일 캠페인(프로모션 이메일, 뉴스레터 개인화, 동적 오퍼 콘텐츠가 포함된 라이프사이클 이메일)에 포함할 최상의 오퍼를 선택하는 데 가장 적합합니다. 각 수신자의 메시지 렌더링 시간에 결정합니다.

#### 작동 방식

이메일 메시지 렌더링 중에 의사 결정 정책을 호출하여 각 수신자에게 가장 적합한 오퍼를 선택합니다. 이메일 템플릿에는 의사 결정 엔진이 선택한 오퍼의 컨텐츠 표시(이미지, HTML 또는 텍스트)를 삽입하는 오퍼 배치 영역이 포함되어 있습니다. 전송 시 엔진은 오퍼 자격 규칙에 대해 각 수신자의 프로필을 평가하고 등급 전략을 적용하며 우승 오퍼의 콘텐츠를 이메일에 임베드합니다.

이 접근 방식은 예약된 캠페인(캠페인 실행 시간에 평가됨)과 여정이 포함된 이메일(프로필이 메시지 작업 노드에 도달하면 평가됨) 모두에서 작동합니다. 오퍼 콘텐츠(이미지, 헤드라인, 본문 사본 및 CTA)는 의사 결정 결과에 따라 수신자별로 개인화됩니다.

#### 주요 고려 사항

- 오퍼 자격은 프로필의 현재 상태를 사용하여 전송 시 평가됩니다.
- 메시지 렌더링 중에 결정이 발생하므로 일괄 대상 평가로 충분합니다
- 각 오퍼에는 이메일 배치에 대한 HTML 또는 이미지 컨텐츠 표현이 필요합니다
- 대체 오퍼에는 사용된 모든 이메일 배치에 대한 컨텐츠가 있어야 합니다.

#### 장점

- 가장 간단한 구현 경로 - 표준 캠페인 또는 여정 이메일 게재를 사용합니다.
- 클라이언트측 SDK 요구 사항 없음
- 기존 이메일 인프라 및 채널 표면 사용
- 일괄 캠페인 실행을 통해 대규모 대상자 볼륨 지원

#### 제한 사항

- 전송 시간에 결정을 내립니다. 전송 후 동작에 적응할 수 없습니다.
- 이메일이 전달되면 오퍼 컨텐츠가 정적입니다(실시간 업데이트 없음)
- 허브 프로필 저장소에서 사용할 수 있는 프로필 특성으로 제한됨(에지 아님)

#### Experience League 리소스

- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### 옵션 B: 웹/앱 실시간 오퍼 의사 결정

이 옵션은 웹 페이지 또는 모바일 앱(홈 페이지 홍보 배너, 계정 대시보드 오퍼 위젯, 인앱 오퍼 카드 또는 페이지가 로드되거나 화면이 렌더링될 때 오퍼를 선택해야 하는 디지털 표면)에서 실시간 오퍼를 선택하는 데 가장 적합합니다.

#### 작동 방식

의사 결정 정책은 Edge Decisioning 네트워크 또는 코드 기반 경험을 통해 페이지 로드 또는 앱 화면 렌더링 시 호출됩니다. 방문자가 페이지를 로드할 때 웹 SDK은 Edge Network에 요청을 보내어 오퍼 자격 규칙 및 등급 전략에 대해 방문자의 Edge 프로필을 평가합니다. 선택한 오퍼가 응답에서 반환되고 디지털 표면에 구성된 배치에서 렌더링됩니다.

코드 기반 경험의 경우 애플리케이션은 의사 결정 응답을 검색하고 사용자 지정 프론트엔드 논리를 사용하여 오퍼 콘텐츠를 렌더링합니다. 웹 채널 경험의 경우 AJO 웹 채널은 시각적 또는 코드 기반 작성을 사용하여 페이지에 오퍼 콘텐츠를 직접 삽입할 수 있습니다.

#### 주요 고려 사항

- 데이터 스트림에서 AJO 서비스가 활성화된 Web SDK 또는 Mobile SDK 구현이 필요합니다.
- 실시간 프로필 조회에 Edge 활성 병합 정책이 필요합니다.
- 적격성에 사용되는 대상은 에지 평가(단순 속성 확인 및 세그먼트 멤버십)를 지원해야 합니다.
- 오퍼 콘텐츠 표현은 클라이언트측 렌더링에 JSON 또는 이미지 URL 형식을 사용해야 합니다
- 노출 추적은 오퍼 보기 및 클릭을 캡처하도록 구현해야 합니다.

#### 장점

- 방문자의 현재 프로필 상태를 기반으로 하는 실시간 세션 내 오퍼 선택
- Edge Network을 통한 1초 미만의 결정 지연
- 오퍼는 에지에서 사용할 수 있는 최신 프로필 데이터에 맞게 조정됩니다
- 콘텐츠 실험을 통해 오퍼 전략의 A/B 테스트 지원

#### 제한 사항

- 클라이언트측 SDK 구현 필요(웹 SDK 또는 모바일 SDK)
- Edge 프로필에 전체 허브 프로필 속성의 하위 집합이 있습니다. 복잡한 자격 규칙이 올바르게 평가되지 않을 수 있습니다
- Edge 세그먼트에는 세그먼트 규칙 복잡성 제한 사항이 있습니다(시계열 쿼리 없음)
- 코드 기반 경험에서 사용자 지정 렌더링을 위한 프론트엔드 개발 필요

#### Experience League 리소스

- [Edge Decisioning API를 사용하여 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [코드 기반 경험 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/get-started-code-based)

**알려진 방문자 웹/앱 개인화 옵션 B와 차이점:**

인프라는 동일합니다. 두 가지 모두 Web SDK과 Edge에서 AJO Decisioning을 사용하고 Edge-Active 병합 정책을 사용합니다. 차이점은 카탈로그 거버넌스 모델입니다. 이 옵션은 자격 규칙, 최대 가용량 카운터 및 유효성 검사 날짜가 포함된 경계 오퍼 카탈로그를 제어합니다. 비즈니스 또는 규제 제한에 따라 표시할 수 있는 오퍼와 빈도가 결정될 때 이 옵션을 사용하십시오. [알려진 방문자 웹/앱 개인화](known-visitor-web-app-personalization.md) 옵션 B는 오퍼 라이프사이클 관리 없이 세그먼트 멤버십 또는 순위 전략을 사용하여 콘텐츠 항목에서 선택합니다. 항목 세트가 크고 지속적으로 변경되며 최대 가용량 또는 자격 거버넌스가 필요하지 않은 경우 알려진 방문자 옵션 B를 대신 사용하십시오.

### 옵션 C: 여정 결정 노드

이 옵션은 여러 단계 여정 내에서 오퍼를 선택하는 데 가장 적합합니다. 즉, 고객 여정의 의사 결정 지점에서 최상의 오퍼를 선택한 다음 다음 다음 작업 노드를 통해 오퍼를 제공합니다. 오퍼 결정이 대기, 조건 및 여러 메시지 작업을 포함하는 광범위한 오케스트레이션 흐름의 일부인 경우 이 옵션을 사용합니다.

#### 작동 방식

결정 정책은 AJO 여정 캔버스 내의 결정 노드에서 호출됩니다. 프로필이 의사 결정 노드에 도달하면 엔진이 오퍼 자격 및 순위를 평가하여 최적의 오퍼를 선택합니다. 선택한 오퍼는 다음 메시지 작업(포함할 오퍼 컨텐츠, 사용할 채널 또는 오퍼 결과를 기반으로 수행할 여정 분기)을 알려줍니다.

이 접근 방식을 사용하면 여정 결정이 후속 여정 단계에 영향을 주는 적응형 오퍼를 사용할 수 있습니다. 예를 들어 여정은 최상의 오퍼를 선택하고, 이메일을 통해 이를 전달하고, 참여를 기다린 다음, 오퍼가 열리지 않은 경우 푸시 알림을 수행할 수 있습니다.

#### 주요 고려 사항

- 여정은 의사 결정 노드 다음에 하나 이상의 메시지 작업 노드가 오도록 설계되어야 합니다
- 오퍼 자격은 프로필이 의사 결정 노드에 도달하는 순간 프로필의 상태를 사용하여 평가됩니다
- 결정과 게재 사이의 여정 대기 단계로 인해 프로필의 상태가 변경될 수 있습니다
- 오퍼를 여정 분기와 결합하여 오퍼를 선택한 기반으로 다른 경로를 취할 수 있습니다.

#### 장점

- 오퍼 선택을 여러 단계 오케스트레이션 흐름으로 통합
- 오퍼 선택이 후속 단계에 영향을 미치는 적응형 여정을 활성화합니다.
- 동일한 여정(이메일, 푸시, SMS) 내에서 채널 간 게재 지원
- 오퍼 후 참여 추적을 위해 여정 조건과 결합할 수 있음

#### 제한 사항

- 독립 실행형 Campaign Decisioning보다 설정하기 복잡함
- 여정 처리량 제한 적용(초당 5,000개의 프로필)
- 의사 결정은 여정 컨텍스트에 연결되어 있습니다. 변경 내용을 적용하려면 여정 버전 관리가 필요합니다.
- 여정 카탈로그 또는 의사 결정 정책 업데이트를 적용하려면 오퍼를 다시 게시해야 합니다.

#### Experience League 리소스

- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### 옵션 비교

다음 표에서는 주요 기준에서 세 가지 구현 옵션을 비교합니다.

| 기준 | 옵션 A: 이메일 의사 결정 | 옵션 B: 웹/앱 실시간 | 옵션 C: 여정 결정 노드 |
| --- | --- | --- | --- |
| 다음에 최적 | 수신자별 오퍼 선택을 사용한 일괄 이메일 캠페인 | 웹/앱 표면의 실시간 오퍼 배너 | 여러 단계로 구성된 오케스트레이션된 여정 내에서 오퍼 선택 |
| 결정 지연 | 전송 시(일괄 렌더링 중 수신자 당 초) | Sub-second(Edge Network) | 여정 노드 실행 시(초) |
| 채널 | 이메일 | 웹, 모바일 앱, 코드 기반 표면 | 여정 내 모든 채널(이메일, 푸시, SMS) |
| SDK 필요 | 아니요 | 예(웹 SDK 또는 모바일 SDK) | 아니요(이메일/푸시용), 예(웹 채널이 여정 작업인 경우) |
| 대상 평가 | 일괄 처리 또는 스트리밍 | Edge | 일괄 처리, 스트리밍 또는 에지(여정 항목에 따라 다름) |
| 프로필 데이터 범위 | 전체 허브 프로필 | Edge 프로필(하위 집합) | 전체 허브 프로필 |
| 복잡성 | 낮음 | Medium 하이 | 중간 |
| 처리량 | 높음(일괄 캠페인 볼륨) | 높음(Edge Network 규모) | Medium(여정 처리량 제한 적용) |

### 적절한 옵션 선택

사용 사례에 가장 적합한 구현 옵션을 선택하려면 다음 지침을 사용하십시오.

- 기본 사용 사례가 아웃바운드 이메일 캠페인에서 수신자별로 최상의 오퍼를 선택하고 클라이언트측 SDK을 사용할 수 없는 경우 **옵션 A**&#x200B;을(를) 선택합니다. 이는 가장 간단한 구현 경로이며 프로모션 이메일, 뉴스레터 및 라이프사이클 캠페인에 적합합니다.
- **방문자가 웹 페이지를 로드하거나 모바일 앱을 여는 동안 실시간으로 오퍼를 선택해야 하는 경우 옵션 B**&#x200B;를 선택합니다. 이를 위해서는 Web SDK 또는 Mobile SDK 및 에지 활성 병합 정책이 필요하지만 가장 빠르고 상황에 맞는 오퍼를 선택할 수 있습니다.
- 오퍼 결정이 여러 단계, 대기 및 조건부 분기를 사용하는 광범위한 고객 여정의 일부인 경우 **옵션 C**&#x200B;을 선택합니다. 선택한 오퍼가 다운스트림 여정 작업에 영향을 주거나 오퍼 참여를 기반으로 한 다중 채널 후속 조치가 필요한 경우 올바른 선택입니다.
- 채널 간에 오퍼를 일관되게 전달해야 하는 경우 **옵션을 결합**&#x200B;합니다. 고객이 이메일(옵션 A), 웹 사이트(옵션 B) 및 여정 후속 조치(옵션 C)에서 동일한 오퍼를 볼 수 있도록 세 가지 옵션 모두에 대해 동일한 결정 정책을 사용합니다.

## 구현 단계

다음 단계에서는 Offer Decisioning의 전체 구현 시퀀스를 간략히 설명합니다.

### 1단계: 기본 사전 요구 사항 확인

**응용 프로그램 기능:** AEP: 데이터 모델링 및 준비, AEP: ID 및 프로필 구성

이 단계에서는 기본 데이터 레이어가 Offer Decisioning을 지원하는지 확인합니다. 프로필 스키마에는 오퍼 자격 규칙에 사용된 속성이 포함되어야 하며 ID 구성은 채널 간 프로필 확인을 활성화해야 합니다.

#### 의사 결정: 자격에 대한 프로필 속성

오퍼 자격 규칙에 사용할 프로필 속성을 결정합니다.

>[!NOTE]
>프로필 속성 선택은 자격 규칙 디자인과 순위 전략 효율성 모두에 영향을 줍니다. 의사 결정 품질을 높이기 위해 계산된 속성 및 성향 점수를 고려합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 표준 프로필 속성(충성도 계층, 구매 내역) | 프로필 스키마에 속성이 이미 있음 | 스키마 변경이 필요하지 않습니다. 데이터 새로 고침 확인 |
| 계산된 속성(라이프타임 값, 참여 점수) | 자격 또는 순위는 집계된 행동 데이터에 따라 다릅니다 | S1 구성 필요, 계산된 속성 새로 고침 케이던스에 종속성 추가 |
| 고객 AI 성향 점수 | 순위는 ML 기반 예측을 활용해야 합니다. | 충분한 교육 데이터 필요(대상 이벤트를 포함한 10,000개 이상의 프로필), 모델 교육 시간 |

#### 주요 구성 세부 정보

- 프로필 스키마에 자격 규칙에 참조된 필드가 포함되어 있는지 확인합니다(예: `_tenantId.loyaltyTier`, `_tenantId.subscriptionType`).
- 노출, 클릭 및 전환 이벤트에 대한 오퍼 상호 작용 추적 스키마가 존재하는지 확인
- 옵션 B의 경우: 에지 활성 병합 정책이 구성되어 있고 웹 SDK 데이터 스트림에 AJO 서비스가 활성화되었는지 확인

#### Experience League 설명서

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [프로필용으로 스키마 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/union-schema)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### 2단계: 대상 평가 구성

**응용 프로그램 함수:** RT-CDP: 대상 평가

이 단계에서는 오퍼 자격 기준으로 사용되는 대상을 정의하고 평가합니다. 이러한 대상은 특정 오퍼에 적합한 고객 세그먼트를 결정합니다(예: &quot;고가치 고객&quot;은 프리미엄 오퍼에 적합한 고객, &quot;체험판 사용자&quot;는 전환 오퍼에 적합한 고객).

#### 의사 결정: 대상 평가 방법

오퍼 자격 요건에 대해 대상자 멤버십을 얼마나 빨리 업데이트해야 하는지 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 배치 평가 | 전송 시 적격성이 평가되는 옵션 A(이메일 캠페인) | 가장 간단함, 모든 세그먼트 규칙 표현식 지원됨, 일별 또는 온디맨드 새로 고침 |
| 스트리밍 평가 | 일괄 처리 사이에 실시간에 가까운 대상 업데이트가 필요한 경우 옵션 A 또는 C | 적격 세그먼트에 대한 자동, 제한된 세그먼트 규칙 지원(단일 이벤트, 속성 비교) |
| 에지 평가 | 페이지 로드 시 자격 조건을 평가해야 하는 옵션 B(웹/앱 실시간) | 1초 이내, 실시간 웹/앱 오퍼에 필요, 간단한 속성 확인 및 세그먼트 멤버십으로 제한 |

**UI 탐색:** 고객 > 대상 > 대상 만들기 > 규칙 빌드

#### 주요 구성 세부 정보

- 오퍼 적격성에 대한 타깃팅 대상 정의(예: &quot;충성도 골드 계층&quot;, &quot;고가치 고객&quot;, &quot;평가판 사용자&quot;)
- 필요한 경우 제외 대상 정의(예: &quot;최근 수신한 오퍼 X&quot;)
- 옵션 B의 경우: 자격 대상이 에지 평가에 적합한지 확인 - 세그먼트 규칙 표현식에서 시계열 쿼리 및 복잡한 집계를 피하십시오

#### 옵션 분기 위치

**옵션 A(Email Decisioning)의 경우:**
일괄 처리 또는 스트리밍 평가로 충분합니다. 대상자는 캠페인 실행 전 또는 실행 중에 평가됩니다. 시간 기반 조건 및 이벤트 집계를 포함한 복잡한 세그먼트 규칙 표현식이 완전히 지원됩니다.

**옵션 B의 경우(웹/앱 실시간):**
Edge 평가가 필요합니다. 대상자는 간단한 속성 확인 또는 세그먼트 멤버십 조건을 사용해야 합니다. 세그먼트 규칙 표현식이 에지 세분화에 적합한지 확인하여 에지 적격성을 테스트합니다.

옵션 C의 **여정 결정 노드:**
모든 평가 방법은 여정 입력 기준에 따라 작동합니다. 여정이 대상 기반 항목을 사용하는 경우 대상 평가 방법은 여정의 요구 사항과 일치합니다.

#### Experience League 설명서

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### 3단계: 의사 결정 설정

**응용 프로그램 함수:** AJO: Decisioning

이 단계는 오퍼 카탈로그, 자격 규칙, 등급 전략 및 의사 결정 정책을 작성하는 핵심 단계입니다. 이 단계는 모든 게재 옵션(A, B, C)이 공유하는 의사 결정 엔진 구성을 만듭니다.

#### 의사 결정: 배치 채널 및 컨텐츠 형식

오퍼가 표시되는 위치와 형식을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이메일(HTML) | 옵션 A — 이메일 본문 내에서 HTML으로 렌더링된 오퍼 컨텐츠 | 다양한 형식을 지원합니다. 이메일 클라이언트와 호환되어야 합니다. |
| 이메일(이미지 URL) | 옵션 A — 이메일에서 호스팅된 이미지로 렌더링된 오퍼 | 단순성, 이미지를 호스팅하고 액세스할 수 있어야 함, 동적 텍스트 없음 |
| 웹(HTML) | 옵션 B - 웹 페이지에서 HTML으로 렌더링된 오퍼 | 전체 레이아웃 제어, 대화형 요소 지원 |
| 웹/모바일(JSON) | 옵션 B - 사용자 지정 렌더링을 위해 JSON으로 반환되는 오퍼 데이터 | 유연성 극대화, 렌더링하려면 프론트엔드 개발 필요 |
| 코드 기반 (JSON) | 옵션 B - 코드 기반 경험 표면에 대한 데이터 제공 | 애플리케이션 제어 렌더링, 가장 유연한 |

#### 의사 결정: 순위 전략

적격 오퍼에서 최상의 오퍼를 선택하는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 우선 순위 기반(수동) | 소규모 오퍼 카탈로그, 오퍼 주문에 대한 명시적 비즈니스 규칙 | 구성 간소화, 오퍼당 우선 순위 값 수동 할당, 결정적 |
| 공식 기반(사용자 정의 표현식) | 순위는 프로필 속성(예: 충성도 계층, 최신성)을 고려해야 합니다. | 유연성, 프로필 데이터를 사용하여 순위 점수 계산, 세그먼트 규칙 표현식 디자인 필요 |
| AI 등급(자동 최적화) | 대규모 오퍼 카탈로그, 시간이 지남에 따라 ML에서 선택 최적화 필요 | 모델 교육을 위해 최소 1,000개의 전환 이벤트 필요, 오퍼 성능 데이터에서 학습 |

#### 결정: 오퍼 한도

오퍼가 표시되는 횟수를 제한해야 하는지 여부를 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 프로필별 상한 | 동일한 오퍼가 한 고객에게 너무 많이 표시되지 않도록 합니다. | 오퍼 피로도 방지, 처리량이 많은 시나리오에서 몇 초의 카운터 지연 |
| 글로벌 상한 | 모든 프로필에서 오퍼에 대한 총 노출 횟수 제한(예: 제한된 인벤토리) | 오퍼 공급을 제어합니다. 상한에 도달하면 오퍼가 의사 결정에서 제외됩니다. |
| 상한 없음 | 오퍼의 가용성은 무제한입니다. | 가장 간단함, 상시 승급에 적합 |

**UI 탐색:** 구성 요소 > 의사 결정 관리 > 배치/규칙/오퍼/의사 결정

#### 주요 구성 세부 정보

1. **배치 만들기** — 각 배치에 대한 채널 유형 및 콘텐츠 형식을 지정하여 오퍼가 표시되는 위치를 정의합니다.
   - UI: 구성 요소 > 의사 결정 관리 > 배치
   - 채널/형식 조합당 하나의 배치를 만듭니다(예: &quot;Email Hero Banner - HTML&quot;, &quot;웹 홈 페이지 - JSON&quot;, &quot;모바일 앱 카드 - JSON&quot;).

2. **자격 규칙 정의** — 프로필 특성이나 대상 멤버십을 참조하는 세그먼트 규칙 표현식을 사용하여 규칙을 만듭니다.
   - UI: 구성 요소 > 의사 결정 관리 > 규칙
   - 규칙은 대상 멤버십, 프로필 속성(충성도 계층, 구독 유형), 날짜 제한 또는 컨텍스트 데이터를 참조할 수 있습니다

3. **개인화된 오퍼 만들기** - 모든 배치에 대해 콘텐츠 표시를 사용하여 각 오퍼를 빌드하고, 자격 규칙을 지정하고, 우선 순위를 설정하고, 선택적 한도 설정을 구성합니다.
   - UI: 구성 요소 > 의사 결정 관리 > 오퍼 > 오퍼 만들기
   - 각 오퍼에는 배치당 컨텐츠 표현이 필요합니다(예: 이메일용 HTML, 웹용 JSON).
   - 각 오퍼를 볼 수 있는 프로필을 제어하는 자격 규칙 할당
   - 오퍼 유효 날짜(시작/종료) 및 선택적 빈도 설정
   - 의사 결정에 적격한 오퍼를 승인합니다.

4. **대체 오퍼 만들기** - 개인화된 오퍼가 적격하지 않을 때 표시되는 각 배치에 대한 기본 오퍼를 빌드합니다.
   - UI: 구성 요소 > 의사 결정 관리 > 오퍼 > 대체 오퍼 만들기
   - 대체 에는 결정에 사용되는 모든 배치에 대한 표현이 있어야 합니다.

5. **컬렉션 한정자 및 컬렉션 만들기** - 한정자 태그를 사용하여 오퍼를 컬렉션으로 구성합니다.
   - UI: 구성품 > 의사 결정 관리 > 수집 구분자
   - 결정 범위에 사용할 그룹 관련 오퍼(예: &quot;여름 프로모션&quot;, &quot;충성도 보상&quot;)

6. **의사 결정 정책 만들기** - 배치, 컬렉션, 순위 전략 및 대체 오퍼를 실행 가능한 의사 결정에 바인딩합니다.
   - UI: 구성 요소 > 의사 결정 관리 > 의사 결정 > 의사 결정 만들기
   - 각 결정 범위는 배치를 컬렉션에 연결하고 등급 지정 방법을 지정합니다

#### Experience League 설명서

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [의사 결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [컬렉션 수식어 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 4단계: 채널 및 표면 구성

**응용 프로그램 함수:** AJO: 채널 구성

이 단계는 오퍼가 게재될 채널 표면을 구성합니다. 구성은 사용 중인 구현 옵션에 따라 다릅니다.

#### 결정: 채널 유형

사용 사례에 필요한 메시징 채널을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이메일 | 이메일 게재가 포함된 옵션 A 또는 옵션 C | 하위 도메인 위임, IP 풀, 발신자 설정 필요 |
| 웹 | 웹 표면 게재용 옵션 B | 웹 SDK 및 데이터스트림 구성 필요 |
| 인앱 | 모바일 앱 게재를 위한 옵션 B | 모바일 SDK 및 푸시 자격 증명 필요 |
| 코드 기반 경험 | 사용자 정의 렌더링 표면 옵션 B | 가장 유연한 애플리케이션, 렌더링 처리 |

#### 옵션 분기 위치

**옵션 A(Email Decisioning)의 경우:**
- UI: 관리 > 채널 > 채널 표면 > 표면 만들기(이메일)
- 하위 도메인, IP 풀, 보낸 사람 이름/이메일, 회신, 구독 취소 설정 구성
- 보내는 하위 도메인에 대한 SPF, DKIM 및 DMARC 레코드 확인

**옵션 B의 경우(웹/앱 실시간):**
- UI: 관리 > 채널 > 채널 표면 > 표면 만들기(웹 또는 인앱)
- 웹: 웹 표면 URL 패턴 구성
- 코드 기반 경험의 경우: 애플리케이션에 대한 표면 URI를 정의합니다
- 데이터 스트림에 AJO 서비스가 활성화되었는지 확인

옵션 C의 **여정 결정 노드:**
- 여정에 사용된 각 채널(이메일, 푸시, SMS 또는 웹)에 대한 채널 표면 구성
- 각 여정 메시지 작업은 해당 활성 채널 표면을 필요로 합니다

#### Experience League 설명서

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [이메일 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 5단계: 콘텐츠 및 게재 구성

**응용 프로그램 함수:** AJO: 메시지 작성, AJO: 캠페인 실행

이 단계는 선택한 오퍼를 표시하는 메시지 템플릿 또는 경험 표면을 디자인한 다음 게재 메커니즘(캠페인, 여정 또는 코드 기반 경험)을 구성합니다.

#### 의사 결정: 오퍼 렌더링을 위한 콘텐츠 접근 방식

오퍼 콘텐츠를 메시지 또는 경험에 통합하는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이메일 Designer의 오퍼 결정 구성 요소 | 옵션 A — 이메일 템플릿에 오퍼 배치 포함 | 드래그 앤 드롭, 오퍼 콘텐츠는 의사 결정 결과에 따라 자동으로 렌더링됩니다. |
| 의사 결정 정책을 사용한 코드 기반 경험 | 옵션 B — 응용 프로그램이 오퍼 데이터를 검색하고 렌더링합니다. | 렌더링에 대한 최대 제어, 프론트엔드 개발 필요 |
| 포함된 결정이 있는 메시지 작업 여정 | 옵션 C - 의사 결정 노드가 오퍼 컨텐츠를 여정 메시지에 제공 | 오퍼 선택 및 게재는 여정 플로우 내에서 조정됩니다 |

#### 의사 결정: 캠페인 유형(옵션 A만 해당)

예약된 마케팅 캠페인인지, API 트리거 캠페인인지 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 예약된 캠페인 | 일회성 또는 반복 배치가 정의된 대상자에게 전송됨 | 실행 시 평가된 대상, 날짜/시간 설정 또는 반복 |
| API 트리거된 캠페인 | 이벤트 기반 또는 시스템 트리거된 가 지정된 프로필에 전송됨 | 트리거 페이로드에 지정된 프로필. 요청당 최대 20명의 수신자를 지원합니다. |

#### 옵션 분기 위치

**옵션 A(Email Decisioning)의 경우:**

1. 이메일 Designer을 사용하여 이메일 메시지 작성
   - UI: 캠페인 > 캠페인 만들기 > 이메일 선택 > 콘텐츠 편집
   - 오퍼 결정 구성 요소를 이메일 레이아웃에 삽입하여 배치 영역 정의
   - 프로필 수준 콘텐츠(이름, 충성도 계층)에 대한 개인화 토큰 추가
   - 선택적 개인화로 제목 줄 및 사전 머리글 구성
2. 캠페인 만들기 및 구성
   - UI: 캠페인 > 캠페인 만들기 > 예약됨 또는 API 트리거됨
   - 타겟 대상자 바인딩 및 채널 표면 선택
   - 실행 일정 또는 API 트리거 구성 설정
   - 캠페인 검토 및 활성화

**옵션 B의 경우(웹/앱 실시간):**

1. 코드 기반 경험 또는 웹 채널 구성
   - UI: 캠페인 > 캠페인 만들기 > 코드 기반 경험(또는 웹)
   - 의사 결정 정책을 경험 표면에 연결합니다.
   - 렌더링 형식 정의(코드 기반용 JSON 응답, 웹 채널용 비주얼 편집기)
2. 클라이언트측 렌더링 구현
   - 웹 SDK `sendEvent` 응답을 사용하여 선택한 오퍼를 검색합니다.
   - 페이지의 지정된 위치에 오퍼 콘텐츠 렌더링
   - 노출 및 클릭 추적 구현

옵션 C의 **여정 결정 노드:**

1. 의사 결정 노드로 여정 디자인
   - UI: 여정 > 여정 만들기 > 결정 노드 추가
   - 3단계에서 결정 정책을 호출하도록 결정 노드 구성
2. 결정 후 메시지 작업 노드 추가
   - 선택한 오퍼를 참조하는 이메일, 푸시 또는 SMS 작업 구성
   - 오퍼 참여를 기반으로 대기 단계, 조건 또는 분기 추가
3. 여정 게시

#### Experience League 설명서

- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 6단계: 테스트 및 유효성 검사

**응용 프로그램 함수:** AJO: Decisioning, AJO: 메시지 작성

이 단계에서는 의사 결정 엔진이 테스트 프로필에 대해 올바른 오퍼를 반환하고 오퍼 콘텐츠가 각 게재 채널에서 제대로 렌더링되는지 확인합니다.

#### 테스트 의사 결정 논리

알려진 특성이 있는 테스트 프로필을 사용하여 자격 조건 및 순위를 기준으로 올바른 오퍼가 선택되었는지 확인합니다.

- 다른 자격 기준과 일치하는 테스트 프로필(예: 골드 계층, 실버 계층, 평가판 사용자)을 만듭니다.
- 각 테스트 프로필이 예상 오퍼를 수신하는지 확인
- 자격 규칙과 일치하는 프로필이 대체 오퍼를 수신하는지 확인합니다.

#### 콘텐츠 렌더링 테스트

각 게재 채널에서 오퍼 컨텐츠를 미리 봅니다.

- 옵션 A의 경우: 테스트 프로필과 함께 이메일 미리 보기를 사용하여 오퍼 콘텐츠가 올바르게 렌더링되는지 확인
- 옵션 B의 경우: 스테이징 환경에서 Edge Decisioning 응답 테스트
- 옵션 C의 경우: 여정 테스트 모드를 사용하여 결정 노드가 올바로 선택되는지 확인합니다.

#### 노출 추적 유효성 검사

오퍼 노출 횟수, 클릭 수 및 전환 수가 추적되고 있는지 확인합니다.

- 오퍼 상호 작용 이벤트가 추적 데이터 세트에 표시되는지 확인
- 오퍼 노출 횟수와 다운스트림 전환 간 속성 확인

#### Experience League 설명서

- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [이메일 증명 보내기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)

### 7단계: 보고 및 성능 모니터링 구성

**응용 프로그램 함수:** AJO: 보고 및 성능 분석

이 단계에서는 오퍼 선택 분포, 수락율, 전환 영향 및 대체 비율을 추적하는 보고를 설정합니다. 이 단계에서는 AJO 기본 보고서와 CJA 기반 크로스 채널 분석을 모두 다룹니다.

#### 결정: 보고 방법

오퍼 성능 분석에 필요한 보고 도구를 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| AJO 기본 보고서만 | 개별 캠페인 또는 여정에 대한 운영 모니터링 | 빠른 액세스, 내장 게재 및 참여 지표, 제한된 교차 엔티티 분석 |
| CJA 작업 공간 분석 | 크로스 채널 오퍼 효율성, 매출 기여도 분석, funnel 분석 | CJA 연결 및 데이터 보기 필요, 심층적인 분석 기능 |
| AJO 및 CJA 모두 | 전체 운영 및 분석 범위 | 프로덕션 구현에 권장, 실시간 모니터링에 AJO, 전략적 분석에 CJA |

#### 주요 구성 세부 정보

1. **AJO 기본 보고** - 기본 제공 보고서를 사용하여 캠페인 또는 여정 성과를 모니터링합니다.
   - UI: 캠페인 > 캠페인 선택 > 모든 시간 보고서(또는 라이브 보고서)
   - 오퍼별 지표 검토: 오퍼당 노출 횟수, 오퍼당 클릭스루 비율, 대체 비율
   - 게재 모니터링 funnel: 타겟팅됨 > 전송됨 > 게재됨 > 열기 > 클릭 수

2. **CJA 분석(권장)** - 크로스 채널 오퍼 성능 대시보드를 빌드합니다.
   - AJO 오퍼 상호 작용 데이터 세트를 포함한 CJA 연결 구성
   - 오퍼별 차원(오퍼 이름, 배치, 의사 결정)과 지표(노출 횟수, 클릭 수, 전환)를 사용하여 데이터 보기를 만듭니다
   - 작업 공간 분석 작성 대상: 오퍼 선택 분포, 세그먼트별 수락율, 매출 영향, 크로스 채널 오퍼 일관성

#### Experience League 설명서

- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

## 구현 시 고려 사항

이 섹션에서는 Offer Decisioning 구현을 위한 보호, 일반적인 위험, 모범 사례 및 거래 사례를 다룹니다.

### 보호 기능 및 제한 사항

구현을 계획할 때 다음 플랫폼 보호 기능 및 제한 사항에 유의하십시오.

- 샌드박스당 최대 10,000개의 승인된 맞춤형 오퍼 — [의사 결정 관리 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 의사 결정당 최대 30개 배치
- 결정 요청당 최대 30개의 수집 범위
- AI 등급 모델은 교육을 위해 최소 1,000개의 전환 이벤트가 필요합니다
- 오퍼 한도 카운터는 처리량이 많은 시나리오에서 최대 몇 초의 지연 시간을 가질 수 있습니다
- Edge 의사 결정은 edge 프로필 스토어에서 사용할 수 있는 프로필 속성으로 제한됩니다
- 샌드박스당 최대 4,000개의 세그먼트 정의 — [플랫폼 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 샌드박스당 Edge에서 하나의 병합 정책만 활성화할 수 있습니다.
- 샌드박스당 최대 500개의 활성 라이브 캠페인
- 여정 진입률 제한: 초당 5,000개 프로필
- 샌드박스당 채널 유형당 최대 10개 채널 표면

### 일반적인 함정

구현 중에 자주 발생하는 이러한 문제를 방지하십시오.

- **결정은 항상 대체 오퍼를 반환합니다.** 이는 일반적으로 개인화된 오퍼가 승인되지 않았거나, 유효 날짜 범위를 벗어나거나, 자격 규칙이 테스트 프로필의 특성과 일치하지 않음을 의미합니다. 승인 상태, 날짜 범위 및 세그먼트 규칙 표현식 정확도 등 각 조건을 확인합니다. 또한 최대 가용량 한도에 도달하지 않았는지 확인하십시오.
- **오퍼가 컬렉션에 표시되지 않음:** 오퍼에 올바른 컬렉션 한정자로 태그가 지정되었고 컬렉션 필터가 일치하는지 확인하십시오. 오퍼가 컬렉션 기반 결정 범위에 표시되도록 하려면 태그 지정과 승인을 모두 받아야 합니다.
- **순위 수식이 적용되지 않음:** 수식이 구문적으로 유효하고 액세스 가능한 프로필 특성을 참조하는지 확인하십시오. 공식 오류는 눈에 보이는 오류 없이 자동으로 우선순위 기반 순위로 돌아갑니다.
- **Edge 게재에서 빈 개인 맞춤화를 반환합니다.** 데이터 스트림이 [!DNL Adobe Journey Optimizer] 서비스를 사용하도록 구성되어 있고 결정 범위의 형식이 올바른지 확인하십시오. 에지 활성 병합 정책이 있는지 확인합니다.
- **채널 간에 일관되지 않은 오퍼:** 채널별로 별도의 의사 결정 정책을 사용하는 경우 동일한 프로필에서 다른 오퍼를 받을 수 있습니다. 일관성을 위해 채널 간 단일 결정 정책을 사용하거나 채널별 배치에 따라 의도적인 분산을 수락합니다.
- **오퍼 콘텐츠가 전자 메일에서 렌더링되지 않습니다.** 오퍼에 전자 메일 배치 형식(HTML 또는 이미지 URL)과 일치하는 콘텐츠 표현이 있는지 확인하십시오. 표시가 없으면 빈 배치 영역이 생깁니다.

### 우수 사례

성공적인 Offer Decisioning 구현을 위해서는 다음 권장 사항을 따르십시오.

- **작은 오퍼 카탈로그로 시작하여 반복** — 5~10개의 오퍼로 시작하고 의사 결정 프레임워크의 유효성을 검사할 때 확장하십시오. 이렇게 하면 문제 해결을 단순화하고 비율을 조정하기 전에 자격 규칙이 올바르게 작동하는지 확인할 수 있습니다.
- **수집 한정자를 전략적으로 사용** - 캠페인 및 여정에서 재사용할 수 있는 유연한 수집 기반 결정 범위를 사용하도록 설정하려면 범주별 오퍼(예: &quot;획득&quot;, &quot;유지&quot;, &quot;업셀&quot;)에 태그를 지정합니다.
- **항상 의미 있는 대체 오퍼를 만드십시오** — 대체 오퍼는 안전망일 뿐만 아니라 자격 규칙과 일치하지 않는 프로필의 기본 경험입니다. 개인화 없이도 가치를 제공하는 대체 콘텐츠에 투자하십시오.
- **가능한 경우 함께 사용할 수 없는 자격 규칙을 디자인합니다** — 여러 오퍼에 겹치는 자격 조건이 있는 경우 순위 전략이 중요해집니다. 비즈니스 요구 사항이 특정 세그먼트에 대한 특정 오퍼를 지정하는 경우 등급에만 의존하지 않고 자격 규칙을 상호 배타적으로 만듭니다.
- **옵션 B에 대해 에지 대표 프로필을 사용하여 테스트** - Edge 프로필에 허브 프로필 특성의 하위 집합이 포함되어 있습니다. 프로덕션에서 적격성이 올바르게 평가되는지 확인하기 위해 에지 사용 가능한 특성이 있는 프로필로 테스트합니다.
- **대체 비율을 상태 지표로 모니터링** — 대체 비율이 높으면(20-30% 이상) 오퍼 카탈로그가 충분한 고객 세그먼트를 포함하지 않음을 나타냅니다. 오퍼 카탈로그를 확장하거나 자격 규칙을 확장합니다.
- **실시간 결정 정책을 편집하지 않고 버전 결정 정책** — 활성 결정 정책을 수정하지 않고 새 결정 정책 버전을 만듭니다. 이를 통해 라이브 캠페인이 중단되는 것을 방지하고 의사 결정 전략을 A/B에서 비교할 수 있습니다.

### 절충안 결정

아키텍처 및 구성 결정 시 다음과 같은 장단점을 고려하십시오.

#### 자격 정밀도와 오퍼 범위 비교

엄격한 자격 규칙은 각 오퍼가 가장 관련성이 높은 프로필에만 도달하도록 보장하지만, 프로필이 오퍼와 일치하지 않을 때 높은 대체 비율이 발생할 수 있습니다. 광범위한 자격 규칙은 오퍼 범위를 극대화하지만 개인화 정밀도를 감소시킵니다.

- **빠듯한 자격 조건 우대:** 높은 수락률, 더 나은 개인화, 더 낮은 오퍼 피로도
- **폭넓은 자격 조건 우대:** 대체 비율이 낮고 더 많은 프로필이 개인화된 오퍼를 받고 규칙 관리가 단순합니다.
- **권장 사항:** 더 광범위한 자격 규칙으로 시작하고 성능 데이터를 기준으로 규칙을 강화합니다. 대체 비율 및 수락 비율을 모니터링하여 적절한 균형을 찾습니다. 등급 전략을 사용하여 광범위하게 적격한 오퍼를 구별합니다.

#### 우선 순위 기반 및 AI 등급 비교

우선 순위 기반 등급은 표시되는 오퍼에 대한 모든 권한을 비즈니스에 제공하는 반면, AI 등급 등급은 전환을 위해 최적화되지만 오퍼 선택에 대한 사람의 제어를 줄입니다.

- **우선 순위 기반 지원:** 비즈니스 제어, 예측 가능성, 교육 데이터 요구 사항 없음, 즉시 배포
- **AI 등급 선호도:** 전환 최적화, 예기치 않은 패턴 검색, 변화하는 고객 행동에 대한 자동 적응
- **권장 사항:** 비즈니스 제어가 가장 중요한 초기 시작 및 규정에 따른 오퍼에 우선 순위 기반 순위를 사용합니다. 충분한 전환 데이터(1,000개 이상의 이벤트)를 사용할 수 있게 되면 볼륨에 따라 성능이 최적화된 사용 사례를 위해 AI 등급으로 전환합니다.

#### 단일 결정 정책과 채널별 결정 정책 비교

단일 결정 정책은 모든 채널에서 오퍼 일관성을 보장하지만 채널별 최적화를 제한합니다. 채널별 정책은 채널별 순위 및 자격 조건을 허용하지만 일관되지 않은 고객 경험을 초래할 수 있습니다.

- **단일 정책 지원:** 크로스 채널 일관성, 간편한 관리, 통합 보고
- **채널별 정책 선호도:** 채널에 최적화된 순위, 채널별 자격(예: 웹 전용 오퍼), 독립 반복
- **권장 사항:** 채널 간 일관성을 위한 단일 결정 정책으로 시작합니다. 비즈니스 요구 사항이 채널별 오퍼 전략(예: 웹 전용 플래시 판매)을 요구할 때만 채널별 정책을 수립합니다.

#### Hub 의사 결정 (옵션 A/C)과 Edge 의사 결정 (옵션 B)

Hub Decisioning 은 전체 프로필에 액세스할 수 있지만 전송 시간에 작동합니다. Edge decisioning은 1초 미만의 지연 시간으로 실시간으로 작동하지만 에지 사용 가능한 프로필 속성으로 제한됩니다.

- **Hub 의사 결정 지원:** 전체 프로필 데이터, 복잡한 자격 규칙, 일괄 캠페인 볼륨에 액세스
- **Edge 의사 결정 지원:** 실시간 컨텍스트, 세션 내 개인화, 1초 미만 응답
- **권장 사항:** 전체 프로필 데이터가 오퍼 관련성을 개선하는 아웃바운드 채널(이메일, 푸시)에 대해 허브 의사 결정을 사용합니다. 실시간 응답이 중요한 인바운드 채널(웹, 앱)에 대해 Edge Decisioning을 사용합니다. Edge에 대한 적격성 규칙이 Edge 사용 가능한 속성만 사용하는지 확인합니다.

## 관련 설명서

다음 리소스는 이 사용 사례 패턴에 사용되는 구성 요소에 대한 추가 세부 정보를 제공합니다.

### 의사 결정 관리

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [의사 결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [컬렉션 수식어 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 오퍼 게재

- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning API를 사용하여 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [Decisioning API를 사용하여 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/decisioning-api)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [이메일 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)

### 메시지 작성 및 개인화

- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 캠페인 및 여정

- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

### 콘텐츠 실험

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### 프로필 및 ID

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [Customer AI 개요](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### 데이터 모델링 및 수집

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)

### 보고 및 분석

- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### 데이터 거버넌스 및 라이프사이클

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

### 튜토리얼

- [의사 결정 관리 API 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/getting-started)
