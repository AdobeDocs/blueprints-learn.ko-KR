---
title: 알려진 방문자 웹/앱 Personalization
description: 실시간 프로필 및 세그먼트 멤버십을 기반으로 식별된 방문자에게 개인화된 콘텐츠, 오퍼 또는 프로모션을 제공하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '7957'
ht-degree: 2%

---


# 알려진 방문자 웹/앱 개인화

이 참조 플랜은 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) 및 [!DNL Adobe Real-Time Customer Data Platform]&#x200B;(RT-CDP)을 사용하여 디지털 표면에 걸쳐 식별된 방문자에게 개인화된 콘텐츠를 제공하기 위한 전체 구현 안내서를 제공합니다. 실행 가능한 모든 구현 접근 방식, 각 단계에서 수행해야 하는 결정 및 구성을 지원하는 Experience League 설명서를 이해해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

알려진 방문자 웹/앱 개인화는 인증된 디지털 경험에 대한 기본 개인화 패턴입니다. 세션 내 동작 신호에만 의존하는 익명 방문자 개인화와 달리, 이 패턴은 이전 동작 데이터, 세그먼트 멤버십, 충성도 계층, 구매 기록, 라이프사이클 단계, 계산된 속성 및 성향 점수와 같은 전체 통합 프로필을 활용합니다. AJO 웹 채널을 통한 웹 페이지, 모바일 인앱 메시지 및 콘텐츠 카드 전반에서 개인화를 지원합니다.

이 안내서에서는 상충 관계, 의사 결정 지침 및 [!DNL Adobe Experience League] 설명서에 대한 참조와 함께 실행 가능한 모든 구현 옵션(세그먼트 기반, 의사 결정 기반 및 다중 표면)을 제공합니다.

## 사용 사례 개요

전자 상거래 사이트, 뱅킹 포털, 구독 서비스, 로열티 프로그램, 모바일 앱과 같은 인증된 디지털 속성을 보유한 조직은 브랜드와 각 고객의 관계를 반영하는 개인화된 경험을 제공해야 합니다. 방문자가 로그인하거나 ID 확인을 통해 인식되면 플랫폼은 전체 통합 프로필에 액세스하여 특정 속성, 동작 및 환경 설정에 따른 콘텐츠를 제공할 수 있습니다.

이 패턴은 식별된 방문자가 웹 속성에 도달하거나 모바일 앱을 여는 시나리오를 해결하며, 시스템은 실시간 프로필 데이터 및 대상 멤버십을 기반으로 표시할 최적의 콘텐츠, 오퍼 또는 프로모션을 결정해야 합니다. 개인화 결정은 에지(밀리초)에서 발생하며 가시 지연 없이 초 미만의 콘텐츠 전달을 활성화합니다.

이 패턴은 결정론적 개인화(특정 콘텐츠가 특정 대상 세그먼트에 매핑되는 경우)와 동적 의사 결정(AJO Decisioning이 자격 규칙 및 등급 전략을 평가하여 프로필별로 최적의 콘텐츠를 선택하는 경우)을 모두 지원합니다. 웹 페이지, 모바일 인앱 메시지 및 컨텐츠 카드 등 여러 디지털 표면에 걸쳐 있으므로 고객의 디지털 여정 전반에 걸쳐 일관된 개인화가 가능합니다.

## 주요 비즈니스 목표

다음 비즈니스 목표는 이 사용 사례 패턴을 통해 해결됩니다.

### 개인화된 고객 경험 전달

콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다. 자세한 내용은 [개인화된 고객 경험 전달](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)을 참조하십시오.

| KPI | 설명 |
| --- | --- |
| 참여 | 디지털 표면 전반에 걸쳐 개인화된 콘텐츠와 상호 작용 빈도 및 깊이 |
| 전환율 | 개인화된 콘텐츠를 받은 후 원하는 작업을 완료하는 방문자의 비율 |
| 고객 만족도(CSAT) | 개인화된 적절한 디지털 경험을 통해 전반적인 만족도 향상 |

### 웹 사이트 참여 늘리기

관련 경험을 통해 사이트에서 보낸 시간, 세션당 페이지 수 및 웹 콘텐츠와의 상호 작용을 개선합니다. 자세한 내용은 [웹 사이트 참여 늘리기](../../business-objectives/acquisition-growth/increase-website-engagement.md)를 참조하십시오.

| KPI | 설명 |
| --- | --- |
| Time On (웹) 페이지 | 개인화된 콘텐츠 영역에 대한 체류 시간 증가 |
| 참여 | 개인화된 요소와의 상호 작용 비율(클릭, 스크롤, 상호 작용) |
| 전환율 | 맞춤형 콘텐츠와 기본 콘텐츠의 전환 개선 |

### 모바일 앱 참여 늘리기

개인화된 인앱 경험을 통해 일일 활성 사용량, 기능 채택 및 인앱 전환을 유도합니다.

| KPI | 설명 |
| --- | --- |
| 참여 | 개인화된 메시지 및 콘텐츠 카드를 통한 인앱 상호 작용 비율 |
| 유지 | 개인화된 경험을 통해 앱 보존 기능 향상 |
| 전환율 | 개인화된 오퍼 및 권장 사항에서 인앱 전환 개선 |

## 예시 전술 사용 사례

다음은 이 패턴의 일반적인 전술적 구현입니다.

- 충성도 계층 또는 라이프사이클 단계에 의한 홈 페이지 영웅 개인화 - 고객이 신규 고객인지, 활성 고객인지, 위험 고객인지 또는 VIP 고객인지에 따라 다른 영웅 배너를 표시합니다
- 구매 내역을 기반으로 한 제품 추천 캐러셀 - 과거 구매 데이터 및 제품 선호도 점수를 사용하여 관련 제품 제안을 표시합니다
- 고객 세그먼트별로 개인화된 프로모션 배너 - 고가치, 위험 및 새로운 고객 세그먼트에 대한 다양한 프로모션 표시
- 기능 채택을 기반으로 하는 모바일 사용자를 위한 인앱 메시지 - 사용 패턴에 따라 활용도가 낮은 기능을 안내합니다
- 계정 대시보드에 개인화된 오퍼가 있는 컨텐츠 카드 - 고객의 프로필에 맞게 맞춤화된 영구적이고 판매 불가능한 오퍼
- 고객 계층을 기반으로 한 맞춤형 가격 또는 할인 표시 - 등급별 가격 또는 고객 충성도 프로그램 회원에 대한 단독 할인 표시
- 소유 제품 기반 교차 판매 추천 위젯 — 현재 포트폴리오를 기반으로 보완 제품 또는 서비스 제안
- 관심 영역을 기반으로 개인화된 탐색 또는 콘텐츠 정렬 — 표시된 환경 설정을 기반으로 콘텐츠 모듈 또는 탐색 요소 재정렬

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 효과를 측정하는 데 도움이 됩니다.

| KPI | 측정 접근 방식 | 벤치마크 지침 |
| --- | --- | --- |
| Personalization 참여율 | 노출에 따라 구분된 개인화된 콘텐츠 요소와의 클릭 및 상호 작용 | 개인화된 컨텐츠는 기본 컨텐츠보다 20~50% 더 뛰어난 성과를 보여야 합니다. |
| 전환율 상승도 | 맞춤형 경험 대 제어/기본 경험에 대한 전환율 | 개인화되지 않은 경험에 대해 10~30% 상승도를 Target으로 지정 |
| 클릭스루 비율(CTR) | 개인화된 CTA, 오퍼 및 권장 사항을 노출로 나눈 클릭 | 표면(웹, 인앱, 콘텐츠 카드) 및 세그먼트당 모니터링 |
| 방문당 매출 | 개인화된 경험이 있는 세션에 따른 매출 | 개인화된 방문자 집단과 개인화되지 않은 방문자 집단 비교 |
| 컨텐츠 카드 상호 작용률 | 노출 횟수에 따른 컨텐츠 카드 클릭 및 해제 | 카드 유형 및 대상 세그먼트당 추적 |
| 인앱 메시지 참여 | 노출 횟수에 따른 인앱 메시지 상호 작용(CTA 클릭, 해제) | 대상 세그먼트 및 메시지 유형 간 비교 |
| 페이지에서 시간 | 개인화된 콘텐츠가 있는 페이지에서 보낸 평균 시간과 기본값 | 개인화된 페이지에 체류 시간이 늘어남 |
| 오퍼 수락율 | 전환 이벤트를 발생시키는 의사 결정 선택 오퍼의 비율 | 오퍼당, 배치당 및 순위 전략당 추적 |

## 사용 사례 패턴

이 섹션에서는 핵심 패턴과 해당 기능 체인에 대해 설명합니다.

**알려진 방문자 웹/앱 개인화**

웹, 모바일 인앱 및 콘텐츠 카드 표면 전반의 실시간 프로필 및 세그먼트 멤버십을 기반으로 식별된 방문자에게 개인화된 콘텐츠, 오퍼 또는 프로모션을 제공합니다.

**함수 체인:** 대상 평가 > Personalization Decisioning > 표면/채널 구성 > 콘텐츠 게재 > 노출 추적 > 보고

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Adobe Journey Optimizer](AJO)** — 웹 채널 구성, 인앱 채널 구성, 콘텐츠 카드 채널 구성, 의사 결정(오퍼 선택 및 등급), 메시지 작성(개인화된 콘텐츠 만들기), 캠페인 실행, 콘텐츠 실험 및 보고
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — 대상 평가(에지, 스트리밍 및 일괄 처리), Edge Network을 통한 실시간 프로필 조회, 계산된 특성 및 성향 점수를 통한 프로필 보강
- **[!DNL Adobe Experience Platform](AEP)** — 프로필 저장소, ID 서비스, Web SDK, Mobile SDK, 데이터스트림 구성, Edge Network Delivery

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 사항 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | 웹 채널, 인앱 채널 및 의사 결정 권한이 구성된 AJO 샌드박스 . 마케터 및 콘텐츠 작성자 역할로 프로비저닝된 사용자. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 프로필 스키마에는 개인화 및 세분화에 사용되는 속성(예: 충성도 계층, 구매 내역, 제품 관심 분야, 라이프사이클 단계)이 포함되어야 합니다. 웹/앱 상호 작용 추적 및 전환 이벤트에 대한 경험 이벤트 스키마. [!DNL Real-Time Customer Profile]에 대해 데이터 세트를 사용할 수 있습니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [스키마 구성 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| 데이터 소스 및 수집 | 필수 | 웹 SDK은 경험 전달 및 노출 추적을 위해 웹 속성에 구현되었습니다. 모바일 SDK은 인앱 및 콘텐츠 카드 전달을 위해 모바일 앱에 구현되었습니다. 에지 개인화에 대해 활성화된 AJO 서비스로 구성된 데이터스트림. 실시간 프로필 데이터를 엣지에서 1초 이내에 개인화할 수 있습니다. | [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview), [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| ID 및 프로필 구성 | 필수 | 알려진 ID 네임스페이스(CRM ID, 이메일, 인증된 사용자 ID)가 구성되었습니다. 익명에서 알려진 방문자 개인화로 원활하게 전환하기 위해 작동하는 익명 세션과 인증된 세션 간의 ID 결합. 가장자리에서 인증된 프로필을 해결하기 위해 `isActiveOnEdge: true`(으)로 구성된 Edge 병합 정책입니다. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| 대상 정의 및 세분화 | 필수 | 프로필 속성, 행동 데이터 및 계산된 속성을 사용하여 정의된 대상입니다. Edge 또는 스트리밍 평가를 통한 실시간 개인화 자격 부여. 세그먼트 기반 개인화에 사용되는 대상은 에지 평가의 대상이어야 합니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [Edge 세그먼테이션](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 기능 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 계산된 특성(예: [!DNL Customer AI] 성향 점수, 라이프타임 값, 참여 점수, 제품 선호도, 마지막 구매 이후 일 수)은 대상 정의 및 콘텐츠 선택에 더 풍부한 신호를 제공하여 개인화 품질을 크게 향상시킵니다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Customer AI 개요](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| 데이터 수명 주기 관리 | 추천 | 프로필 및 이벤트 데이터 보존 정책을 통해 새롭고 관련 있는 데이터를 통해 개인화 결정을 내릴 수 있습니다. 동의 적용은 사용자 환경 설정을 준수하도록 개인화를 보장합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 개인화에 사용되는 프로필 속성(특히 구매 내역, 위치, 재무 데이터와 같은 PII 인접 속성)의 거버넌스 레이블은 데이터 사용 정책을 준수하도록 합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview) |
| 모니터링 및 가시성 | 추천 | Edge 게재 및 개인화 성능 모니터링은 개인화된 경험을 저하시키는 지연 문제, 게재 실패 또는 데이터 신선도 문제를 탐지하는 데 도움이 됩니다. | [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| 보고 및 분석 | 포함됨 | Personalization 성능 보고는 Function Chain 6단계의 일부입니다. [!DNL Customer Journey Analytics] 분석을 사용하면 방문자 세그먼트 간 전환, 참여 및 매출에 미치는 개인화 영향을 심층적으로 조사할 수 있습니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer]&#x200B;(AJO)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 채널 구성 | 표면 및 채널 구성 | 개인화 게재를 위한 웹, 인앱 및 콘텐츠 카드 채널 표면 구성 |
| 메시지 작성 | 컨텐츠 작성 | 각 표면에 대한 동적 콘텐츠, 개인화 표현식 및 조건부 블록을 사용하여 개인화된 콘텐츠 변형을 작성합니다 |
| 캠페인 실행 | Campaign 설정 및 활성화 | 대상자, 표면 및 콘텐츠를 바인딩하는 웹 캠페인(예약됨 또는 API 트리거됨)을 만들고 활성화합니다 |
| 결정 | 의사 결정 설정(옵션 B/C) | 동적 개인화를 위한 자격 규칙, 등급 전략 및 오퍼/콘텐츠 항목을 사용하여 의사 결정 정책 구성 |
| 콘텐츠 실험 | 최적화(선택 사항) | 성능을 최적화하기 위해 개인화된 콘텐츠 변형에 대해 A/B 테스트 실행 |
| 빈도 및 비즈니스 규칙 | Campaign 설정 및 활성화 | 노출 빈도 상한을 적용하여 과도한 개인화 피로도 방지 |
| 보고 및 성능 분석 | 보고 및 최적화 | 표면 및 세그먼트당 개인화 게재, 참여 및 전환 지표 모니터링 |

### [!DNL Real-Time CDP]&#x200B;(RT-CDP)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 대상 정의 및 평가 | 프로필 속성, 행동 데이터 및 에지 또는 스트리밍 평가와 함께 계산된 속성을 사용하여 대상자를 정의하고 평가합니다 |
| 실시간 프로필 조회 | 컨텐츠 전달(런타임) | Edge Network을 통해 1초 미만의 개인화 결정을 위해 실시간 프로필 속성 및 세그먼트 멤버십에 액세스합니다 |
| 프로필 보강 | 사전 구현(지원) | 개인화 품질을 개선하는 계산된 특성, [!DNL Customer AI] 점수 및 집계된 행동 신호로 프로필을 보강합니다. |

## 필요 조건

이 사용 사례 패턴을 구현하기 전에 다음 사항이 적용되었는지 확인하십시오.

- [ ] 웹 SDK이 페이지 보기 및 상호 작용 추적에 대해 구성된 `alloy("sendEvent")`을(를) 사용하여 대상 웹 속성에 구현되었습니다.
- [ 대상 모바일 앱에 ] Mobile SDK이 구현되었습니다(인앱 또는 콘텐츠 카드 표면이 사용되는 경우)
- [ [!DNL Adobe Journey Optimizer] 서비스를 사용하도록 설정한 ] 데이터 스트림
- [ ] 프로필 스키마에는 개인화에 사용되는 특성(충성도 계층, 구매 내역, 제품 관심 분야, 라이프사이클 단계)이 포함되어 있습니다.
- [ 노출 및 전환 추적을 위해 구성된 ] 경험 이벤트 스키마
- [ ] 알려진 ID 네임스페이스가 만들어지고 ECID(익명 ID)와 인증된 ID 간에 ID 연결이 작동합니다
- [ `isActiveOnEdge: true`(으)로 구성된 ] Edge 병합 정책
- [ 실시간 개인화를 위해 Edge 적격 평가로 정의된 대상 ]개
- [ 각 개인화 변형에 대해 준비된 ]개의 콘텐츠 에셋(이미지, 복사본, CTA)
- [ ] Personalization 전략 문서화됨: 어떤 특성이 어떤 콘텐츠, 어떤 표면에 영향을 주는지

## 구현 옵션

이 섹션에서는 이 사용 사례 패턴에 사용할 수 있는 구현 접근 방식에 대해 설명합니다.

### 옵션 A: 세그먼트 기반 웹 개인화

**최적의 용도:** 특정 콘텐츠 변형이 충성도 계층별 히어로 배너, 라이프사이클 단계 메시징, 고객 세그먼트 홍보 콘텐츠 등 대상 세그먼트에 직접 매핑되는 결정론적 개인화 콘텐츠-세그먼트 매핑이 잘 정의되어 있고 동적 순위 또는 최적화가 필요하지 않은 경우에 이상적입니다.

**작동 방식:**

세그먼트 기반 개인화는 콘텐츠 변형을 대상 세그먼트에 직접 매핑합니다. 페이지 로드 시 알려진 방문자의 프로필이 Edge 적격 대상자에 대해 평가되면 시스템은 방문자가 속한 세그먼트를 결정하고 해당 콘텐츠 변형을 표시합니다. 선택은 세그먼트 멤버십 우선 순위를 기반으로 합니다. 방문자가 여러 세그먼트에 적격인 경우 가장 높은 우선 순위 세그먼트의 컨텐츠가 표시됩니다.

이 방법에서는 조건부 콘텐츠 규칙 또는 여러 치료 타기팅 구성이 있는 AJO 웹 채널 캠페인(또는 인앱/콘텐츠 카드 캠페인)을 사용합니다. 각 대상 세그먼트는 특정 콘텐츠 경험과 연결되어 있습니다. 의사 결정 엔진이 포함되지 않습니다. 컨텐츠 선택 로직은 전적으로 세그먼트에 의존합니다.

콘텐츠는 대상 멤버십 또는 프로필 속성에 따라 다른 콘텐츠를 렌더링하는 다이내믹 콘텐츠 블록과 AJO 메시지 작성 인터페이스를 사용하여 작성됩니다. 웹 SDK 또는 모바일 SDK은 Edge Network을 통해 실시간으로 개인화된 경험을 제공합니다.

**주요 고려 사항:**

- 각 세그먼트에 대해 컨텐츠 변형을 미리 작성해야 합니다.
- 세그먼트 정의는 실시간 자격에 적합한 간선이어야 합니다.
- 새 세그먼트 또는 콘텐츠 변형을 추가하려면 캠페인 구성을 업데이트해야 합니다
- 컨텐츠 선택은 결정적입니다. 즉, 동일한 세그먼트에 항상 동일한 컨텐츠가 표시됩니다

**장점:**

- 명확한 컨텐츠-세그먼트 매핑 기능을 통한 간편한 구현 및 유지 관리
- 이해 당사자에게 개인화 논리를 쉽게 이해하고 설명할 수 있습니다.
- 의사 결정 부담 없음 — 컨텐츠 해결 속도 향상
- 각 세그먼트가 수신하는 콘텐츠를 완벽하게 제어

**제한 사항:**

- 세그먼트 및 콘텐츠 변형의 수가 증가할 때 유연성 제한
- 세그먼트 멤버십 범위를 넘어 프로필 수준 신호를 기반으로 콘텐츠 선택을 동적으로 최적화할 수 없음
- 새 콘텐츠 변형을 추가하려면 수동 캠페인 업데이트가 필요합니다.
- 은 여러 오퍼가 동일한 배치를 위해 경쟁하는 다음 최상의 오퍼 시나리오를 지원하지 않습니다

**Experience League:**

- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [웹 경험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### 옵션 B: 의사 결정 기반 개인화

**가장 적합한 대상:** 자격 규칙 및 등급 전략(홈 페이지의 차선책 오퍼, 개인화된 제품 추천, 동적 홍보 배너 선택)을 사용하여 프로필별로 최적의 콘텐츠 또는 오퍼를 선택해야 하는 동적 개인화. 여러 오퍼 또는 컨텐츠 항목이 동일한 배치를 위해 경쟁하고 시스템에서 가장 적합한 오퍼를 선택해야 하는 경우에 이상적입니다.

**작동 방식:**

Decisioning 기반 개인화는 AJO Decisioning을 사용하여 콘텐츠 항목 또는 오퍼 카탈로그에 대해 각 방문자의 프로필을 평가하고, 자격 규칙을 적용하여 적합한 항목을 결정한 다음, 등급 전략(우선 순위 기반, 공식 기반 또는 AI 등급)을 적용하여 각 배치에 대한 최적 항목을 선택합니다.

구현에는 배치 생성(컨텐츠가 나타나는 위치), 자격 규칙 및 컨텐츠 표현이 있는 오퍼 정의, 오퍼를 컬렉션으로 구성 및 등급 전략이 있는 컬렉션에 배치를 바인딩하는 의사 결정 정책 생성이 포함됩니다. 런타임 시, 방문자가 페이지를 로드할 때 Edge Network은 방문자의 프로필에 대해 의사 결정 정책을 평가하고 선택한 오퍼 콘텐츠를 반환합니다.

이 접근 방식은 차선책, 최대 가치의 개인화된 프로모션 및 AI에 최적화된 콘텐츠 선택을 비롯한 정교한 개인화 시나리오를 지원합니다. 오퍼에는 프로필별 및 글로벌 제한, 유효 날짜 범위 및 프로필 속성과 대상 멤버십을 결합한 복잡한 자격 기준이 있을 수 있습니다.

**주요 고려 사항:**

- 추가 사전 구성 필요(배치, 오퍼, 자격 규칙, 컬렉션, 의사 결정)
- 순위 전략은 우선 순위 기반(수동), 공식 기반(사용자 지정 표현식) 또는 AI 등급(자동 최적화)일 수 있습니다
- AI 등급은 모델 교육에 최소 1,000개의 전환 이벤트가 필요합니다
- 오퍼 한도 카운터는 높은 처리량 시나리오에서 약간 지연될 수 있습니다.
- 개인화된 오퍼가 적격하지 않은 경우에 대해 대체 오퍼를 구성해야 합니다.

**장점:**

- 하드코딩된 세그먼트-콘텐츠 간 매핑 없이 프로필별 콘텐츠를 동적으로 선택
- 복잡한 자격 기준과 순위 논리를 지원합니다.
- AI 등급 옵션을 통해 수동 개입 없이 자동 최적화 가능
- 오퍼 한도 제한으로 특정 콘텐츠 과다 노출 방지
- 중앙 집중식 오퍼 관리 — 오퍼를 캠페인 및 채널에서 재사용할 수 있습니다.

**제한 사항:**

- 세그먼트 기반 개인화보다 높은 구현 복잡성
- AI 등급은 교육을 위해 충분한 전환 이벤트 볼륨이 필요합니다.
- 의사 결정 평가는 직접 세그먼트 기반 콘텐츠 전달에 비해 한계 지연 시간을 추가합니다
- 수식 기반 순위를 사용하려면 의도하지 않은 우선 순위 지정을 방지하기 위해 세심한 디자인이 필요합니다

**Experience League:**

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 옵션 C: 다중 표면 개인화(웹 + 인앱 + 콘텐츠 카드)

**최적의 용도:** 여러 디지털 표면에 걸쳐 일관적인 개인화를 통해 웹 페이지, 모바일 인앱 메시지 및 콘텐츠 카드에 개인화된 통합 환경을 제공할 수 있습니다. 조직이 웹 및 모바일 앱 속성을 모두 가지고 있고 모든 디지털 접점에 통합 개인화 논리를 원하는 경우에 이상적입니다.

**작동 방식:**

다중 표면 개인화는 옵션 A(세그먼트 기반) 또는 옵션 B(의사 결정 기반)를 확장하여 여러 AJO 표면 유형에 개인화된 콘텐츠를 제공합니다. 각 표면 유형(웹, 인앱, 콘텐츠 카드)은 콘텐츠 형식과 게재 메커니즘이 다를 수 있지만 기본 개인화 논리(대상자 멤버십 또는 의사 결정)가 공유됩니다.

구현에는 각 표면 유형에 대한 채널 표면 구성, 표면별 콘텐츠 작성(웹 표면에 대한 웹 HTML/CSS, 인앱에 대한 구조화된 메시지, 콘텐츠 카드에 대한 카드 레이아웃) 및 적절한 표면을 타깃팅하는 캠페인 생성이 포함됩니다. 웹 SDK은 웹 표면 전달을 처리하는 반면, 모바일 SDK은 인앱 및 콘텐츠 카드 전달을 처리합니다.

콘텐츠 카드는 계정 대시보드 또는 앱 홈 화면에서 영구적이고 사용이 불가능한 개인화된 메시지에 특히 유용합니다. 인앱 메시지는 상황별 세션별 통신에 이상적입니다. 웹 개인화는 영웅 배너, 추천 위젯 및 홍보 콘텐츠를 처리합니다.

**주요 고려 사항:**

- 각 표면 유형에는 자체 채널 표면 구성 및 콘텐츠 작성이 필요합니다
- Web SDK 및 Mobile SDK을 모두 구현하고 구성해야 합니다
- 내용은 각 표면 형식(다양한 치수, 레이아웃, 상호 작용 패턴)에 맞게 디자인되어야 합니다
- 공유 대상자 및 의사 결정 논리를 통해 표면 간 일관성 보장
- 테스트는 장치 전체의 모든 표면 유형을 포함해야 합니다.

**장점:**

- 모든 디지털 접점에서 일관된 개인화 경험
- 공유 대상자 및 의사 결정 로직이 중복을 줄임
- 콘텐츠 카드는 영구적이고 비간섭적인 개인화 환경을 제공합니다
- 인앱 메시지를 통해 모바일에서 상황에 맞는 세션별 개인화가 가능합니다

**제한 사항:**

- 최고의 구현 복잡성 — 각 표면 유형에 대한 구성이 필요합니다.
- 웹 SDK 및 모바일 SDK 구현 모두 필요
- 각 표면 형식에 맞게 콘텐츠를 디자인하고 유지해야 합니다.
- 검사 범위는 각 추가 표면 유형에 따라 증가합니다.

**Experience League:**

- [인앱 채널 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [콘텐츠 카드 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)

### 옵션 비교

다음 표에서는 세 가지 구현 옵션을 비교합니다.

| 기준 | 옵션 A: 세그먼트 기반 | 옵션 B: 의사 결정 기반 | 옵션 C: 다중 서피스 |
| --- | --- | --- | --- |
| 다음에 최적 | 알려진 세그먼트-콘텐츠 매핑 | 프로필당 동적 콘텐츠 선택 | 웹 + 모바일에서 일관된 개인화 |
| 복잡성 | 낮음 | Medium 하이 | 높음(A 또는 B에서 빌드) |
| 지연 | 가장 빠름(직접 세그먼트 해상도) | 약간 높음(의사 결정 평가) | 기본 옵션(A 또는 B)에 따라 다름 |
| 유연성 | 사전 정의된 세그먼트-콘텐츠 쌍으로 제한 | 높음 — 동적 순위 및 자격 요건 | 가장 높음 — 공유 논리를 사용하는 다중 표면 |
| 콘텐츠 관리 | 수동 세그먼트-콘텐츠 매핑 | 자격 규칙이 있는 중앙 집중식 오퍼 라이브러리 | 공유 개인화 논리를 사용하는 표면별 콘텐츠 |
| 최적화 | 수동 A/B 테스트 | AI 등급 자동 최적화 사용 가능 | 표면별 최적화 |
| 필요 | Edge 지원 대상, Web SDK | 배치, 오퍼, 자격 규칙, 의사 결정 | 웹 SDK + 모바일 SDK, 다중 표면 구성 |
| 지원되는 표면 | 웹(기본) | 웹(기본) | 웹 + 인앱 + 콘텐츠 카드 |

### 적절한 옵션 선택

올바른 구현 접근 방식을 선택하기 위해 다음 질문을 시작합니다.

1. **표면 개수** 웹과 모바일 앱 모두에서 개인화가 필요한 경우 옵션 C(기본 논리의 경우 A 또는 B 중 하나를 기반으로 함)를 선택합니다. 웹 전용인 경우 A와 B 중에서 선택합니다.

2. **콘텐츠 선택이 얼마나 동적입니까?** 세그먼트를 콘텐츠 변형에 잘 정의한 매핑(예: 각각 특정 히어로 배너를 포함하는 3~5개의 충성도 계층)이 있는 경우 옵션 A를 선택합니다. 복잡한 자격 및 순위가 있는 오퍼 카탈로그에서 선택해야 하는 경우 옵션 B를 선택합니다.

3. **AI에 최적화된 선택이 필요하십니까?** 시스템이 각 프로필에 대해 가장 성과가 좋은 콘텐츠를 자동으로 학습하고 최적화하도록 하려면 AI 등급 의사 결정으로 옵션 B를 선택하십시오.

4. **콘텐츠 변형의 개수** 세그먼트 매핑이 명확한 콘텐츠 변형이 10개 미만인 경우 옵션 A가 더 간단합니다. 자격 필터링 및 순위가 필요한 오퍼가 수십 개 있는 경우 옵션 B가 더 잘 확장됩니다.

5. **다른 채널로 확장하시겠습니까?** 의사 결정 논리가 결국 이메일, 웹 및 기타 채널 전반에서 오퍼를 제공해야 하는 경우, 옵션 B는 채널 간 오퍼 의사 결정이 확장되는 중앙 집중식 의사 결정 기반을 제공합니다.

## 구현 단계

이 섹션에서는 구현의 각 단계를 자세히 설명합니다.

### 1단계: 대상자 정의 및 평가 구성

**응용 프로그램 함수:** RT-CDP: 대상 평가

**구성할 내용:** 개인화 콘텐츠 선택을 유도하는 대상을 정의합니다. 이러한 대상은 개인화된 경험(충성도 계층, 라이프사이클 단계, 행동 집단 또는 제품 선호도 그룹)을 수신하는 방문자 세그먼트를 나타냅니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 대상 평가 방법**
>
>개인화를 위해 대상자 멤버십을 얼마나 빨리 해결해야 합니까? 이는 페이지 로드 시 개인화가 발생할 수 있는지 또는 지연이 필요한지 여부에 직접적으로 영향을 줍니다.
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 에지 평가 | 1초 미만의 자격이 필요한 실시간 웹/앱 개인화 | 단순 프로필 속성 확인 및 세그먼트 멤버십으로 제한됩니다. 시계열 쿼리나 복잡한 집계가 없습니다. 알려진 방문자 개인화에 필요합니다. |
>| 스트리밍 평가 | 프로필이 행동 이벤트를 기반으로 대상자를 입장/종료할 때의 거의 실시간 자격 조건 | 단일 이벤트 및 제한된 기간 쿼리를 지원합니다. 대상 변경 사항이 몇 분 내에 반영됩니다. 약간의 지연이 허용되는 인앱 및 콘텐츠 카드 표면에 적합합니다. |
>| 배치 평가 | 복잡한 집계 또는 이전 패턴을 기반으로 한 세그먼트에 대해 일일 대상 새로 고침 | 전체 세그먼트 규칙 기능 지원. 실시간 개인화에 적합하지 않지만 복잡한 사전 계산된 세그먼트로 Edge Audiences를 보완할 수 있습니다. |

>[!NOTE]
>**결정: Personalization 특성**
>
>대상 정의 및 콘텐츠 선택을 유도하는 프로필 속성은 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 프로필 속성(충성도 계층, 라이프사이클 단계) | 알려진 고객 속성을 기반으로 한 결정론적 개인화 | 안정적이고 잘 정의된 속성. 콘텐츠 변형에 매핑하기 쉽습니다. 프로파일이 제대로 구성된 경우 에지에서 사용할 수 있습니다. |
>| 행동 신호(구매 내역, 탐색 패턴) | 최근 행동 및 참여 패턴을 기반으로 한 Personalization | 계산된 속성 또는 스트리밍 세그먼트가 필요합니다. 더 동적이지만 유지 관리가 더 복잡합니다. |
>| 성향 점수([!DNL Customer AI]) | 전환, 이탈 또는 구매 가능성을 기반으로 한 예측 개인화 | 계산된 속성이 필요합니다. 정교한 개인화를 가능하게 하지만 ML 모델 교육 데이터가 필요합니다. |
>| 결합된 접근 방식 | 대부분의 프로덕션 구현 | 세분화를 위해 행동 신호 및 성향 점수와 함께 기본 세분화를 위해 프로필 속성을 사용합니다. |

**UI 탐색:** 고객 > 대상 > 대상 만들기 > 규칙 빌드

**키 구성 세부 정보:**

- 프로필 속성을 참조하는 세그먼트 규칙 표현식과 함께 세그먼트 빌더를 사용하여 대상자 정의
- 세그먼트 규칙 표현식이 에지 평가(단순 속성 확인, 세그먼트 멤버십)에 적합한지 확인
- 실시간 개인화 사용 사례를 위한 Edge 적격 대상 구성
- 최근에 전환되거나 옵트아웃된 방문자를 제외하려면 제외 대상을 고려하십시오

**Experience League 설명서:**

- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### 2단계: 의사 결정 설정(옵션 B 및 C만 해당)

**응용 프로그램 함수:** AJO: Decisioning

**구성할 내용:** 각 방문자에 대해 최적의 콘텐츠 또는 오퍼를 동적으로 선택하는 의사 결정 인프라를 설정합니다. 여기에는 배치(오퍼가 표시되는 위치), 오퍼(사용 가능한 컨텐츠), 자격 규칙(적격 사용자), 등급 전략(최상의 선택 방법) 및 의사 결정 정책(모든 것이 연결되는 방법)이 포함됩니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 순위 전략**
>
>각 방문자에 대해 가장 적합한 오퍼를 선택하기 위해 적격 오퍼의 등급을 어떻게 지정해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 우선 순위 기반(수동) | 명확한 오퍼 계층 구조를 가진 간단한 사용 사례 | 각 오퍼에는 수동 우선 순위 값이 있습니다. 우선 순위가 가장 높은 적격 오퍼가 승리합니다. 쉽게 이해하고 제어할 수 있습니다. |
>| 공식 기반(사용자 정의 표현식) | 순위에서 프로필 속성을 고려해야 하는 경우 | 사용자 지정 등급 공식은 프로필 데이터(예: 충성도 계층 + 최신성별 점수)를 참조합니다. 유연하지만 공식 설계 및 테스트가 필요합니다. |
>| AI 등급(자동 최적화) | 시스템이 오퍼 선택을 자동으로 최적화하도록 하려는 경우 | ML 모델은 어떤 오퍼가 어떤 프로필에 가장 잘 수행되는지 학습합니다. 교육을 위해 최소 1,000개의 전환 이벤트가 필요합니다. 트래픽이 많은 배치에 가장 적합합니다. |

>[!NOTE]
>**결정: 오퍼 한도**
>
>방문자 또는 모든 방문자에게 오퍼가 표시되는 횟수를 제한해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 프로필별 상한 | 동일한 오퍼를 반복적으로 표시하지 않도록 피로도 방지 | 일정 기간 동안 방문자당 노출 횟수를 제한합니다. 개인화된 경험에서 다양성을 보장합니다. |
>| 글로벌 상한 | 프로모션 또는 제한된 가용성 오퍼에 대한 총 노출 횟수 제한 | 모든 방문자에 대한 총 노출 횟수를 제한합니다. 수량 제한 판촉에 유용합니다. |
>| 상한 없음 | 항상 관련성이 높은 콘텐츠 또는 오퍼 | 노출 제한 없음. 충성도 계층 배너와 같은 지속적인 콘텐츠에 적합합니다. |

**UI 탐색:** [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리

**키 구성 세부 정보:**

- 오퍼가 표시될 각 표면(웹 배너, 인앱 메시지 영역, 콘텐츠 카드 슬롯)에 대한 배치를 만듭니다
- 프로필 속성 및 대상자 멤버십을 참조하는 세그먼트 규칙 표현식을 사용하여 자격 규칙 정의
- 각 배치에 대한 콘텐츠 표시를 사용하여 개인화된 오퍼 만들기
- 모든 배치를 포함하는 대체 오퍼를 만듭니다(개인화된 오퍼가 적격하지 않을 때 표시됨).
- 컬렉션 한정자(태그)를 사용하여 오퍼를 구성하고 컬렉션으로 그룹화
- 선택한 순위 전략을 사용하여 컬렉션에 배치 정책 바인딩 결정 만들기

**Experience League 설명서:**

- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [의사 결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 3단계: 표면 및 채널 구성

**응용 프로그램 함수:** AJO: 채널 구성

**구성할 내용:** 개인화된 콘텐츠가 전달될 위치를 정의하는 채널 표면을 구성합니다. 각 표면 유형(웹, 인앱, 콘텐츠 카드)에는 표면 URI, 콘텐츠 형식 및 게재 매개 변수를 지정하는 자체 구성이 필요합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 대상 표면**
>
>어떤 디지털 표면이 개인화된 콘텐츠를 수신합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 웹 채널만 | 웹 속성에 중점을 둔 Personalization | 웹 SDK이 필요합니다. 가장 간단한 구현입니다. 영웅 배너, 프로모션 영역, 추천 위젯을 다룹니다. |
>| 인앱 채널만 | 모바일 앱 경험에 중점을 둔 Personalization | Mobile SDK이 필요합니다. 앱 내의 상황에 맞는 세션별 메시지를 다룹니다. |
>| 컨텐츠 카드 채널만 | 영구적이고 허용되지 않는 개인화된 메시지 | Mobile SDK 또는 Web SDK이 필요합니다. 카드는 해제될 때까지 지속됩니다. 대시보드 및 홈 화면에 이상적입니다. |
>| 여러 서피스(옵션 C) | 웹 및 모바일에서 일관된 개인화 | Web SDK과 Mobile SDK이 모두 필요합니다. 각 표면에는 별도의 구성과 콘텐츠가 필요합니다. |

>[!NOTE]
>**결정: 웹 표면 구성 접근 방식**
>
>컨텐츠 전달을 위해 웹 표면을 어떻게 구성해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 단일 페이지 애플리케이션(SPA) | 클라이언트측 라우팅을 사용하는 최신 웹 앱 | 웹 SDK `sendEvent` 호출에서 `renderDecisions: true`을(를) 사용합니다. SDK에서 자동으로 렌더링하는 컨텐츠입니다. |
>| 다중 페이지 애플리케이션(MPA) | 기존 서버에서 렌더링된 웹 페이지 | Edge Network 응답을 통해 페이지 로드 시 전달된 콘텐츠. 페이지 수준 표면 URI 구성이 필요할 수 있습니다. |

**UI 탐색:** [!DNL Journey Optimizer] > 관리 > 채널 > 채널 표면

**키 구성 세부 정보:**

- 웹 표면: 대상 페이지와 일치하는 웹 표면 URI를 구성합니다.
- 인앱 표면: 앱 ID 및 표면 유형으로 모바일 앱 표면 구성
- 컨텐츠 카드 표면의 경우: 앱 ID 또는 웹 컨텍스트로 컨텐츠 카드 표면을 구성합니다
- 데이터 스트림에 에지 개인화 전달을 위한 AJO 서비스가 활성화되었는지 확인합니다.

**Experience League 설명서:**

- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [웹 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)
- [인앱 채널 사전 요구 사항](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [콘텐츠 카드 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)

### 4단계: 콘텐츠 작성

**응용 프로그램 함수:** AJO: 메시지 작성

**구성할 내용:** 각 표면, 세그먼트 또는 오퍼에 대해 개인화된 콘텐츠 변형을 작성합니다. 여기에는 시각적 레이아웃 디자인, 프로필 속성을 참조하는 개인화 표현식 추가, 조건부 콘텐츠 블록 구성 및 재사용 가능한 콘텐츠 조각 만들기가 포함됩니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 콘텐츠 접근 방식**
>
>이 사용 사례에 맞게 개인화된 콘텐츠를 어떻게 구성해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 조건부 콘텐츠 블록 | 동일한 레이아웃 내의 다른 콘텐츠 섹션은 대상자에 따라 다릅니다 | 조건부 규칙이 있는 단일 콘텐츠 에셋. 작은 변형(헤드라인, CTA 텍스트, 이미지 교체)에 대해 효율적입니다. |
>| 처리당 개별 콘텐츠 변형 | 대상자별로 근본적으로 다른 레이아웃 또는 디자인 | 여러 전체 콘텐츠 자산. 유연성은 높지만 유지 보수는 더욱 향상됩니다. 콘텐츠 실험에 필요합니다. |
>| 의사 결정 기반 콘텐츠 | 오퍼 카탈로그에서 동적으로 선택된 콘텐츠 | 오퍼 표시는 콘텐츠를 정의합니다. 컨텐츠 관리는 오퍼 라이브러리에서 중앙 집중화됩니다. |

>[!NOTE]
>**결정: Personalization 깊이**
>
>얼마나 많은 콘텐츠를 개인화해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 표면 수준 개인화 | 특정 요소만 개인화됨 (영웅 이미지, CTA, 오퍼 배너) | 복잡성 감소. 영향력이 큰 영역에 집중 개인화. 가장 일반적인 시작점. |
>| 전체 페이지 개인화 | 전체 페이지 레이아웃 또는 콘텐츠 순서 지정이 개인화됨 | 복잡성 증가. 광범위한 콘텐츠 제작이 필요합니다. 가장 적합한 경험을 제공합니다. |
>| 토큰 수준 개인화 | 인라인 개인화 토큰(이름, 계층, 포인트 균형) | 가장 단순한 형태입니다. 프로필 속성 값을 정적 콘텐츠에 삽입합니다. |

**UI 탐색:** [!DNL Journey Optimizer] > 캠페인 > 캠페인 만들기 > 콘텐츠 편집

**옵션이 나뉘는 위치:**

**옵션 A의 경우(세그먼트 기반):**

- 웹 디자이너 또는 코드 편집기를 사용하여 각 대상 세그먼트에 대한 콘텐츠 변형을 작성합니다
- 대상자 멤버십을 기반으로 한 조건과 함께 다이내믹 콘텐츠 블록 사용
- 프로필 특성(예: `{{profile.person.name.firstName}}`, `{{profile.loyalty.tier}}`)을 참조하는 개인화 표현식 구성
- 세그먼트 멤버십을 기반으로 다른 콘텐츠를 표시하도록 조건부 규칙 설정

**옵션 B(의사 결정 기반)의 경우:**

- 2단계에서 정의된 각 배치에 대한 오퍼 콘텐츠 표현 작성
- 각 오퍼에는 배치와 일치하는 하나 이상의 표시(HTML, 이미지, JSON)가 있습니다
- 의사 결정 배치를 포함하여 의사 결정 출력을 웹 페이지 또는 앱에 통합
- 콘텐츠는 런타임 시 동적으로 선택됩니다. 작성은 개별 오퍼 항목에 중점을 둡니다

**옵션 C의 경우(다중 표면):**

- 각 타겟 표면에 대한 표면별 콘텐츠 작성(웹 HTML/CSS, 인앱 구조 메시지, 콘텐츠 카드 레이아웃)
- 각 서피스의 형식 제약 조건에 맞게 조정하면서 서피스 간에 일관된 개인화 논리를 유지합니다.
- 각 표면 유형에서 컨텐츠 렌더링 테스트

**Experience League 설명서:**

- [웹 경험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [인앱 메시지 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [콘텐츠 카드 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### 5단계: 캠페인 설정 및 활성화

**응용 프로그램 함수:** AJO: 캠페인 실행

**구성할 내용:** 전달을 위해 대상, 표면 및 콘텐츠를 함께 바인딩하는 AJO 캠페인을 만들고 활성화합니다. 웹 개인화의 경우, 캠페인은 일반적으로 일회성으로 예약된 전송이 아니라 즉각적인 또는 지속적인 활성화를 위해 구성됩니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 캠페인 유형**
>
>개인화 캠페인은 어떻게 트리거해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 예약된 캠페인(항상 켜짐) | 자격을 갖춘 모든 방문자에 대해 지속적으로 실행되는 개인화 | 시작 날짜를 즉시 로 설정하고 종료 날짜를 지정하지 않습니다. 캠페인은 수동으로 중지될 때까지 활성 상태로 유지됩니다. 웹 개인화에 가장 일반적입니다. |
>| 예약된 캠페인(시간 제한) | 특정 프로모션 기간과 연결된 Personalization | 시작 및 종료 날짜를 설정합니다. Campaign은 종료 날짜 이후 자동으로 중단됩니다. 계절 프로모션 또는 한정 기간 오퍼에 적합합니다. |
>| API 트리거된 캠페인 | 특정 애플리케이션 이벤트에 의해 트리거된 Personalization | 프로그래밍 방식으로 트리거됩니다. 특정 시스템 이벤트에 대한 응답에만 개인화가 표시되어야 하는 경우에 유용합니다. |

>[!NOTE]
>**결정: 빈도 제한**
>
>이 개인화에 대해 노출 빈도를 제한해야 합니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| 빈도 규칙 적용 | 방문자를 피로하게 만들 수 있는 프로모션 또는 오퍼 기반 개인화 | 동일한 개인화가 너무 많이 표시되지 않도록 합니다. AJO 비즈니스 규칙을 통해 구성됩니다. |
>| 빈도 제한 없음 | 항상 사용되는 콘텐츠 개인화(충성도 계층 배너, 대시보드 콘텐츠) | 피로를 유발하지 않는 항상 관련성이 있는 콘텐츠. 노출 제한이 필요하지 않습니다. |

**UI 탐색:** [!DNL Journey Optimizer] > 캠페인 > 캠페인 만들기

**키 구성 세부 정보:**

- 웹, 인앱 또는 콘텐츠 카드 채널과 3단계에서 구성한 표면을 선택합니다
- 1단계에서 정의된 대상 바인딩
- 4단계에서 작성된 콘텐츠 연결
- 캠페인 일정(즉시, 날짜 범위 또는 API 트리거) 구성
- 캠페인 검토 및 활성화
- 콘텐츠 실험의 경우: 실험 토글을 활성화하고, 처리를 정의하고, 활성화하기 전에 트래픽 할당 및 성공 지표를 설정합니다.

**Experience League 설명서:**

- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)

### 6단계: 노출 추적 및 데이터 수집

**응용 프로그램 함수:** AEP: 데이터 원본 및 컬렉션

**구성할 내용:** 개인화된 경험의 노출, 상호 작용 및 전환을 플랫폼으로 다시 추적하여 보고, 대상 재평가 및 의사 결정 최적화를 수행할 수 있도록 합니다.

**키 구성 세부 정보:**

- 개인화된 콘텐츠가 렌더링될 때 웹 SDK에서 `decisioning.propositionDisplay`개의 이벤트를 보내고 있는지 확인
- 방문자가 개인화된 콘텐츠(클릭, 해제)와 상호 작용할 때 웹 SDK에서 `decisioning.propositionInteract`개의 이벤트를 보내는지 확인
- 모바일 SDK의 경우: 인앱 메시지 및 컨텐츠 카드 상호 작용 이벤트가 캡처되는지 확인
- 다운스트림 성공 지표(구매, 등록, 기능 채택)에 대한 전환 이벤트 추적 구성
- 이벤트에 특정 개인화 결정에 대한 속성을 위한 제안 ID가 포함되어 있는지 확인합니다.

**Experience League 설명서:**

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [웹 SDK으로 이벤트 추적](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)
- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)

### 7단계: 보고 및 최적화

**응용 프로그램 함수:** AJO: 보고 및 성능 분석, 보고 및 분석

**구성할 내용:** 성능 모니터링 및 분석을 설정하여 표면, 세그먼트 및 콘텐츠 변형에 대한 개인화 효율성을 측정합니다. 운영 지표에 대해서는 AJO 기본 보고서를 사용하고, 크로스 채널 비즈니스 영향 분석에 대해서는 [!DNL Customer Journey Analytics]을(를) 사용합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 보고 범위**
>
>이 개인화 사용 사례에 필요한 분석 수준은 무엇입니까?
>
>| 옵션 | 선택 시기 | 고려 사항 |
>| --- | --- | --- |
>| AJO 기본 보고서만 | 게재 및 참여 지표에 대한 운영 모니터링 | 노출, 클릭 및 전환 데이터가 포함된 기본 제공 캠페인 보고서. 설정하는 것이 가장 빠릅니다. |
>| CJA 크로스 채널 분석 | 개인화가 비즈니스 결과에 미치는 영향에 대한 심층적인 분석 | CJA 연결 및 데이터 보기가 필요합니다. 채널 전반에서 funnel 분석, 집단 비교 및 속성 모델링을 활성화합니다. |
>| AJO + CJA | 완벽한 운영 및 분석 가시성 | 일상적인 모니터링에는 AJO을 사용하고 전략적 분석에는 CJA을 사용합니다. 프로덕션 구현에 권장됩니다. |

**UI 탐색:**

- AJO 보고서: 캠페인 > 캠페인 선택 > 보고서 보기
- CJA: 프로젝트 > 새 프로젝트 만들기

**키 구성 세부 정보:**

- 활성 개인화 게재 중 캠페인 라이브 보고서에 액세스
- 완료된 캠페인 또는 정기 분석에 대한 내역 보고서 검토
- CJA의 경우: AJO 경험 이벤트 데이터 세트를 포함하는 연결을 구성하고 개인화 지표를 사용하여 데이터 보기를 만듭니다
- 개인화 참여율, 전환 상승도, 오퍼 수락율 및 방문당 매출을 추적하는 대시보드 구축
- 의사 결정 기반 개인화의 경우(옵션 B): 배치 및 순위 전략 효과별로 오퍼 성과 모니터링

**Experience League 설명서:**

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## 구현 시 고려 사항

이 섹션에서는 이 사용 사례 패턴과 관련된 보호, 일반적인 위험, 모범 사례 및 보상 결정을 다룹니다.

### 보호 기능 및 제한 사항

- Edge Network 조회에 에지 평가 세그먼트에 대한 응답 시간 SLA이 200ms 미만입니다. [실시간 고객 프로필 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 샌드박스당 최대 4,000개의 세그먼트 정의 — [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- Edge 세그먼트는 단순 속성 확인 및 세그먼트 멤버십 쿼리(시계열 쿼리 없음)로 제한됩니다. [Edge 세그멘테이션](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- 샌드박스당 Edge에서 하나의 병합 정책만 활성화할 수 있습니다. [병합 정책](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- 샌드박스당 최대 10,000개의 승인된 맞춤형 오퍼 — [의사 결정 관리 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 결정당 최대 30개의 배치 — [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- AI 등급 모델은 교육을 위해 최소 1,000개의 전환 이벤트가 필요합니다
- 단일 범위 요청에 대한 SLA의 오퍼 게재 응답 시간은 P95에서 500ms 미만입니다.
- 샌드박스당 최대 500개의 활성 라이브 캠페인 — [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 샌드박스당 최대 25개의 활성 연산 속성 — [연산 속성 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)

### 일반적인 함정

- **Edge 병합 정책이 구성되지 않음:** 에지 활성 병합 정책이 없으면 Edge Network에서 인증된 프로필을 확인할 수 없으므로 개인화가 실패하거나 익명 동작으로 대체됩니다. 샌드박스에 정확히 하나의 병합 정책에 `isActiveOnEdge: true`이(가) 있는지 확인하십시오.
- **대상이 Edge에 적합하지 않음:** 대상 세그먼트 규칙 식에서 시계열 쿼리, 복잡한 집계 또는 일괄 처리 전용 세그먼트에 대한 `inSegment()` 참조를 사용하는 경우 Edge 평가에 적합하지 않으며 실시간 개인화를 실행할 수 없습니다. 대상 정의 중에 에지 적격성을 확인합니다.
- **인증 중 ID 결합 간격:** 방문자가 익명에서 인증으로 전환할 때 프로필이 아직 확인되지 않은 순간이 있을 수 있습니다. ID 결합이 올바르게 구성되어 있고 웹 SDK이 로그인 즉시 `identityMap`을(를) 통해 인증된 ID를 전송하는지 확인하십시오.
- **의사 결정에 대체 오퍼가 없음:** 대체 오퍼가 구성되어 있지 않고 방문자에게 적합한 개인화된 오퍼가 없으면 의사 결정에서 빈 콘텐츠를 반환하여 끊어진 경험을 만듭니다. 항상 모든 배치를 포함하는 대체 오퍼를 구성합니다.
- **Web SDK에서 제안 표시 이벤트를 보내지 않음:** `renderDecisions`이(가) `true`(으)로 설정되어 있지만 표시 이벤트가 전송되지 않는 경우 보고는 실제 노출을 반영하지 않습니다. 브라우저 개발자 도구에서 네트워크 요청을 검사하여 이벤트 추적을 확인합니다.
- **페이지 로드 시 콘텐츠 깜박임:** 의사 결정 호출 동안 개인화된 콘텐츠가 미리 숨겨지지 않은 경우 방문자에게 기본 콘텐츠가 교체되기 전에 잠깐 볼 수 있습니다. 플리커를 제거하려면 사전 숨김 코드 조각 또는 CSS 기반 사전 숨김을 사용하십시오.

### 우수 사례

- 초기 구현을 위해 세그먼트 기반 개인화(옵션 A)로 시작한 다음, 오퍼 카탈로그가 증가하고 최적화 요구 사항이 증가함에 따라 의사 결정 기반(옵션 B)으로 진화합니다
- 실시간 개인화를 위해 가능하면 항상 에지 평가 대상을 사용하고, 보완 사용 사례를 위해 스트리밍 및 배치 대상을 예약하십시오
- 개인화된 경험에 대한 콘텐츠 실험을 구현하여 개인화가 기본 콘텐츠에 대해 측정 가능한 상승도를 유도하는지 확인
- 점진적 저하 전략으로 개인화 디자인 — 에지에서 프로필을 해결할 수 없는 경우 손상된 경험이 아닌 잘 디자인된 기본 콘텐츠를 표시합니다
- 계산된 속성을 사용하여 참여 점수, 제품 친화성 및 마지막 구매 이후 일 수와 같은 고가치 개인화 신호를 생성하여 세그먼트 기반 및 의사 결정 기반 개인화 품질을 모두 향상시킵니다
- 콘텐츠 거버넌스 프로세스를 유지 관리하여 개인화된 콘텐츠가 모든 표면에 걸쳐 최신, 브랜드 내 및 규정을 준수하도록 합니다.
- 세그먼트별 개인화 성과를 모니터링하여 어떤 대상자가 개인화의 이점을 가장 많이 누리며 상승도가 가장 강한지 식별합니다

### 절충안 결정

>[!NOTE]
>**절충점: Personalization 세부기간 대 콘텐츠 관리 복잡성**
>
>더 세분화된 개인화(더 많은 세그먼트, 더 많은 콘텐츠 변형, 더 많은 표면)는 점점 더 맞춤화되는 경험을 제공하지만 그에 따라 더 많은 콘텐츠 생성, 유지 관리 및 거버넌스 노력이 필요합니다.
>
>- **세부 기간 우대:** 향상된 고객 경험, 높은 참여, 강력한 전환 향상도
>- **세부 기간 우대 낮음:** 구현 속도 향상, 콘텐츠 유지 관리 부담 감소, 간단한 거버넌스
>- **권장 사항:** 콘텐츠 차별화가 명확한 3~5개의 영향력이 큰 세그먼트(예: 충성도 계층 또는 라이프사이클 단계)로 시작합니다. 측정된 성능 향상도에 따라 세부 기간을 확장합니다. 의사 결정(옵션 B)을 사용하여 컨텐츠 관리 증가 정도에 비례하지 않고 세부기간을 확장할 수 있습니다.

>[!NOTE]
>**절충: 실시간 의사 결정과 결정론적 콘텐츠 제어 비교**
>
>의사 결정 기반 개인화(옵션 B)는 동적 최적화를 제공하지만 각 방문자가 보는 콘텐츠에 대한 직접 제어를 줄입니다. 세그먼트 기반 개인화(옵션 A)는 모든 결정론적 제어를 제공하지만 동적 최적화를 제한합니다.
>
>- **의사 결정 제안:** 확장성, 자동 최적화, 복잡한 자격 조건 시나리오
>- **세그먼트 기반 이점:** 예측 가능성, 준수 제어, 관련자 투명성
>- **권장 사항:** 정확한 제어가 필요한 규정 준수 관련 콘텐츠(규제 메시지, 계층별 가격 책정)에 세그먼트 기반 개인화를 사용합니다. 동적 최적화가 가치를 더하는 프로모션 콘텐츠, 오퍼 및 권장 사항에 의사 결정을 사용합니다.

>[!NOTE]
>**절충: Edge 데이터 가용성과 개인화 풍부성 비교**
>
>Edge 평가 개인화는 edge 프로필 스토어에서 사용할 수 있는 특성으로 제한됩니다. 더 풍부한 개인화 신호(전체 동작 내역, 복잡한 계산된 속성)는 서버측 조회 또는 사전 계산이 필요할 수 있습니다.
>
>- **Edge 전용 지원:** 초 미만 지연, 가장 간단한 아키텍처
>- **미리 계산된 데이터 보강 혜택:** 더 풍부한 개인화 신호, 더 정교한 대상 정의
>- **권장 사항:** 계산 특성을 사용하여 리치 동작 신호를 에지 사용 가능한 프로필 특성으로 미리 집계합니다. 이것은 에지 평가의 속도를 가진 행동 데이터의 풍부함을 제공한다.

## 관련 설명서

다음 리소스는 이 안내서에서 참조하는 기술 및 구성에 대한 추가 세부 정보를 제공합니다.

### 웹 채널 개인화

- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [웹 경험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [웹 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/web-configuration)

### 인앱 및 콘텐츠 카드 채널

- [인앱 채널 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/get-started-in-app)
- [인앱 채널 사전 요구 사항](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/inapp-configuration)
- [인앱 메시지 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/in-app/create-in-app)
- [콘텐츠 카드 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/get-started-content-card)
- [콘텐츠 카드 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/content-card-configuration)
- [콘텐츠 카드 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/content-card/create-content-card)

### 의사 결정 관리

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [의사 결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### Personalization 및 콘텐츠

- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### ID 및 프로필

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [아이덴티티 그래프 연결 규칙](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)
- [프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### 데이터 수집 및 SDK

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### 캠페인 및 실험

- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### 계산된 속성 및 데이터 보강

- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [계산된 속성 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Customer AI 개요](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### 보고 및 분석

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

### 거버넌스 및 개인 정보 보호

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
