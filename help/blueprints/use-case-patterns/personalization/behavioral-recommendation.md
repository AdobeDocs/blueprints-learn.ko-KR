---
title: 행동 추천
description: 선택 전략 및 순위 모델을 사용하여 항목 및 콘텐츠 권장 사항을 생성하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: db16e773-e0da-46c4-9fa5-d16f04feb46b
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7545'
ht-degree: 2%

---

# 행동 추천

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) Decisioning, [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP) 및 [!DNL Adobe Experience Platform]&#x200B;(AEP)을 사용하여 동작 제품 및 콘텐츠 권장 사항을 구현하는 방법을 다룹니다. 웹, 모바일 앱 및 이메일 채널 전반에 개인화된 추천 경험을 제공해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

실행 가능한 모든 구현 옵션, 각 단계의 결정 고려 사항 및 [!DNL Adobe Experience League] 설명서에 대한 링크를 제공합니다. 행동 권장 사항은 AJO Decisioning 선택 전략 및 등급 모델과 결합된 행동 신호(제품 보기, 구매, 콘텐츠 상호 작용, 검색 쿼리)를 사용하여 항목 수준 또는 콘텐츠 수준 권장 사항을 생성합니다. 자격 규칙 및 비즈니스 제한을 사용하여 제한된 오퍼, 프로모션 또는 인센티브 세트를 제어하는 Offer Decisioning과 달리, 이 패턴은 통제 대상 자격이 아닌 행동 친화성 신호에 의해 선택이 유도되는 크고 지속적으로 변경되는 항목 카탈로그(제품, 문서, 비디오)에서 작동합니다.

## 사용 사례 개요

제품 카탈로그, 콘텐츠 라이브러리 또는 미디어 라이브러리가 있는 조직은 행동 기록 및 세션 내 활동을 기반으로 각 방문자에게 가장 관련성이 높은 항목을 표시해야 합니다. 홈페이지의 &quot;권장&quot; 캐러셀, 제품 세부 사항 페이지의 교차 판매 위젯 또는 이메일 캠페인에 포함된 제품 권장 사항이든 기본 문제는 동일합니다. 각 방문자의 행동 프로필을 카탈로그의 가장 관련 있는 항목에 일치시킨 다음 적절한 시점에 적절한 채널에서 이러한 권장 사항을 제공합니다.

이 패턴은 [!DNL Web SDK] 또는 [!DNL Mobile SDK]을(를) 통해 동작 신호를 실시간으로 수집하고, 항목 특성을 동작 컨텍스트와 결합하는 AJO Decisioning 선택 전략을 통해 처리하고, 웹, 인앱 또는 이메일 채널을 통해 권장 항목을 제공함으로써 이러한 문제를 해결합니다. 순위 모델은 공식 기반(예: 카테고리 친화성 점수별로 정렬) 또는 AI 등급(예: 개인화된 추천 모델)일 수 있습니다. 이 패턴은 폴백 권장 사항을 구성하여 동작 기록이 없는 새 방문자에 대한 콜드 스타트 시나리오도 처리합니다.

이 패턴의 타겟 대상에는 전자 상거래 머천다이징 팀, 콘텐츠 개인화 팀 및 실제 사용자 행동을 통해 제공되는 개인화된 추천을 통해 참여, 전환 및 평균 주문 가치를 개선하려는 디지털 경험 팀이 포함됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### [교차 판매 및 상향 판매 매출 촉진](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)

행동 및 구매 내역을 기반으로 기존 고객에게 보완 및 프리미엄 제품 또는 서비스를 홍보합니다.

**KPI:** 상향 판매/교차 판매 %, 증분 수익, 고객 생애 가치

### [전환율 증가](../../business-objectives/revenue-monetization/increase-conversion-rates.md)

구매, 등록 또는 양식 제출과 같은 원하는 작업을 완료하는 방문자 및 잠재 고객의 비율을 향상시킵니다.

**KPI:** 전환율, 잠재 고객 전환, 잠재 고객당 비용

### [개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.

**KPI:** 참여, 전환율, 고객 만족도(CSAT)

## 예시 전술 사용 사례

다음은 이 패턴의 일반적인 전술적 구현입니다.

- 제품 세부 사항 페이지의 제품 교차 판매 위젯(&quot;고객이 구매함&quot;)
- 찾아보기 기록을 기반으로 한 홈 페이지 캐러셀 &quot;추천 항목&quot;
- 읽기 동작을 기반으로 한 미디어 사이트의 콘텐츠 권장 사항
- 유사한 항목 위젯과 결합된 &quot;최근에 본 항목&quot;
- 구매 후 보완 제품 권장 사항
- 행동 친화성을 기반으로 한 이메일 제품 권장 사항
- 세션 내 검색 동작을 기반으로 하는 카테고리별 권장 사항
- 동작 신호를 기반으로 검색 결과 재순위 지정

## 주요 성과 지표

다음 KPI는 행동 추천 구현의 효과를 측정하는 데 도움이 됩니다.

| KPI | 측정 접근 방식 |
| --- | --- |
| 권장 사항 클릭스루 비율(CTR) | 추천 항목을 추천 노출로 나눈 클릭 수 |
| 추천 전환율 | 추천 클릭을 총 추천 클릭으로 나눈 구매 또는 원하는 작업 |
| 권장 사항의 영향을 받는 매출 | 최소 한 개 이상의 추천 기반 제품이 포함된 주문의 총 수익 |
| AOV(평균 주문 가격) 상승도 | 권장 사항과 관련된 세션과 그렇지 않은 세션의 AOV 증가 |
| 주문당 항목 수 | 권장 사항 참여 세션의 주문당 항목 수 |
| 권장 사항 범위 | 개인화된(대체 아님) 권장 사항을 받은 적합한 페이지 보기 또는 세션의 비율 |
| 콜드-스타트 대체 비율 | 동작 기록 부족으로 인해 대체 로직에서 제공하는 추천 요청의 비율 |

## 사용 사례 패턴

**동작 권장 사항**

행동 신호를 기반으로 AJO Decisioning 선택 전략 및 등급 모델을 사용하여 컨텍스트 기반의 콘텐츠를 제공하는 항목 수준 또는 콘텐츠 수준 권장 사항을 생성합니다.

**함수 체인:** 동작 신호 수집 > 의사 결정 전략 평가 > 권장 사항 게재 > 보고

패턴 결합에 대한 지침은 구현 고려 사항 아래의 패턴 구성 섹션을 참조하십시오.

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Adobe Journey Optimizer](AJO) Decisioning** — 선택 전략, 순위 모델, 항목 카탈로그 및 동작 신호를 평가하고 각 방문자에 대해 가장 관련성이 높은 항목을 반환하는 결정 정책
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — 행동 프로필 데이터 누적, 추천 범위에 대한 대상 평가 및 행동 선호도 점수에 대한 계산된 특성
- **[!DNL Adobe Experience Platform](AEP)** — [!DNL Web SDK] 및 [!DNL Mobile SDK]을(를) 통한 동작 이벤트 수집, [!DNL Edge Network] 처리, 이벤트 및 카탈로그 데이터에 대한 XDM 스키마 관리

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 사항 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | Decisioning 권한이 활성화된 AJO 샌드박스 항목 카탈로그 관리, 선택 전략 구성 및 채널 표면 관리에 대한 액세스 권한을 통해 프로비저닝된 사용자 역할입니다. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 항목/제품 식별자로 동작 신호(제품 보기, 장바구니에 추가, 구매, 콘텐츠 상호 작용)를 캡처하는 경험 이벤트 스키마. 추천 항목 세트에 대한 항목 카탈로그 스키마(제품 속성, 카테고리, 이미지, 가격). ID 필드가 있는 프로필 스키마. [!DNL Real-Time Customer Profile]에 대해 모든 스키마가 활성화되었습니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [스키마 구성 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition), [데이터 집합 만들기](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create) |
| 데이터 소스 및 수집 | 필수 | [!DNL Web SDK] 또는 [!DNL Mobile SDK]을(를) 통한 실시간 동작 이벤트 스트리밍은 매우 중요합니다. 권장 사항 품질은 새로운 동작 신호에 따라 다릅니다. 항목 카탈로그 데이터는 수집(일괄 처리 또는 스트리밍)해야 합니다. Edge 의사 결정을 위해 활성화된 AJO 서비스로 구성된 데이터스트림. | [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview), [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure) |
| ID 및 프로필 구성 | 필수 | 행동 프로필을 만들려면 행동 신호를 ID(ECID를 통해 알려지거나 익명)와 연결해야 합니다. 알려진 방문자 권장 사항의 경우 인증된 ID(CRM ID, 이메일)를 구성해야 합니다. 실시간 권장 사항 전달을 위해 Edge에서 병합 정책이 활성화됩니다. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| 대상 정의 및 세분화 | 추천 | 대상은 권장 사항의 범위를 지정하거나(예: 프리미엄 구성원에게 프리미엄 제품을 권장) 필터링하는 데 사용할 수 있습니다. 권장 사항이 순전히 행동적인 경우에는 엄격히 필요하지 않습니다. 이메일 기반 권장 사항(옵션 C)이 타겟 대상자를 정의하는 데 필요합니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 기능 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 카테고리 친화성 점수, 제품 상호 작용 빈도, 최근 구매 및 총 지출과 같은 계산된 속성은 추천 순위 품질을 향상시킵니다. [!DNL Customer AI] 성향 점수는 구매 가능성을 예측하여 관련성을 더욱 높일 수 있다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview), [Customer AI 개요](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview) |
| 데이터 수명 주기 관리 | 추천 | 동작 이벤트 데이터에는 적절한 만료 정책이 있어야 합니다. 권장 사항 관련성은 오래된 데이터로 인해 저하됩니다. 동작 이벤트 데이터 세트에 데이터 세트 만료 정책을 설정하면 신선도가 보장되고 스토리지가 관리됩니다. 동의 적용은 행동 데이터의 규정 준수를 보장합니다. | [데이터 세트 만료](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration), [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 행동 데이터의 거버넌스 레이블은 권장 사항에 대한 상호 작용 기록을 준수하여 사용할 수 있도록 합니다. 행동 데이터가 탐색 패턴, 구매 내역 또는 건강/금융 제품 관심 신호를 포함하는 경우 특히 중요합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview) |
| 모니터링 및 가시성 | 추천 | 권장 사항 배달 지연, 대체 비율 및 항목 카탈로그 수집 상태가 모니터링되어야 합니다. 행동 이벤트 수집 실패 및 의사 결정 오류에 대한 경고는 권장 사항 품질을 유지하는 데 도움이 됩니다. | [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| 보고 및 분석 | 포함됨 | 권장 사항 성능 보고는 Function Chain 4단계의 일부입니다. [!DNL Customer Journey Analytics] 표면 및 세그먼트 전반에 걸친 추천 효율성, 매출 영향 및 항목 수준 성능의 분석은 최적화 통찰력을 제공합니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer]&#x200B;(AJO)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 결정 | 품목 카탈로그 및 선택 전략 설정 | 항목 카탈로그(의사 결정 항목), 행동 순위 모델을 통한 선택 전략, 필터링 규칙 및 대체 권장 사항 구성 |
| 채널 구성 | 채널 및 표면 구성 | 권장 사항이 렌더링될 웹(코드 기반 경험), 인앱, 콘텐츠 카드 또는 이메일 채널에 대한 게재 표면을 구성합니다 |
| 메시지 작성 | 콘텐츠 및 게재 구성 | 추천 렌더링 템플릿, 항목 표시 레이아웃 및 추천 항목에 대한 개인화 표현식 디자인 |
| 보고 및 성능 분석 | 보고 및 최적화 | AJO 기본 보고서 및 [!DNL Customer Journey Analytics] 통합을 통해 권장 사항 클릭스루, 전환 및 매출 지표 모니터링 |

### [!DNL Real-Time CDP]&#x200B;(RT-CDP)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 대상 범위 지정(옵션 C) | 권장 사항의 범위를 지정하거나 이메일 권장 사항 캠페인에 대한 대상 모집단을 정의하는 데 사용되는 대상 세그먼트를 평가합니다 |
| 프로필 보강 | 행동 신호 보강 | 추천 순위를 향상시키는 계산된 속성(카테고리 친화성 점수, 상호 작용 빈도)으로 프로필을 보강합니다 |

## 필요 조건

구현을 시작하기 전에 다음을 완료하십시오.

- [ ] AJO Decisioning이 프로비저닝되고 target 샌드박스에서 활성화됩니다
- [ ] [!DNL Web SDK] 또는 [!DNL Mobile SDK]이(가) 배포되고 제품/콘텐츠 식별자를 사용하여 동작 이벤트를 수집합니다.
- [ ] 제품 또는 콘텐츠 카탈로그 데이터를 수집할 수 있습니다(제품 이름, 카테고리, 가격, 이미지 URL, 사용 가능).
- [ ] 동작 이벤트 스키마에는 카탈로그 항목에 연결되는 항목/제품 식별자가 포함되어 있습니다.
- [ ] 데이터 스트림이 [!DNL Adobe Journey Optimizer] 서비스를 사용하도록 구성되어 있습니다(Edge 의사 결정에 필요).
- [ `isActiveOnEdge: true`과(와) ] 병합 정책이 구성되었습니다(실시간 웹/앱 권장 사항에 필요).
- [ ] 이메일 권장 사항(옵션 C)의 경우: 이메일 채널 표면이 구성되고 유효합니다.
- [ ] 이메일 권장 사항(옵션 C): 대상 대상을 정의하고 평가합니다.

## 구현 옵션

다음 옵션에서는 동작 권장 사항을 구현하기 위한 다양한 접근 방식을 설명합니다. 채널 요구 사항 및 기술 제한에 가장 적합한 옵션을 선택합니다.

### 옵션 A: 웹 실시간 추천

**웹 페이지의 제품 또는 콘텐츠 추천 항목:** 제품 세부 정보 페이지 크로스셀 위젯, 홈페이지 추천 캐러셀, 범주 페이지 개인화 목록 및 검색 결과 개인화 등.

**작동 방식:**

동작 신호는 방문자가 사이트를 탐색할 때 [!DNL Web SDK]을 통해 실시간으로 수집됩니다. 각 페이지 보기, 제품 상호 작용 또는 검색 쿼리는 AEP으로 스트리밍되고 방문자의 프로필과 연결됩니다(익명 방문자의 경우 ECID 또는 알려진 방문자의 경우 인증된 ID를 통해). 권장 사항 표면이 포함된 페이지가 로드되면 [!DNL Web SDK]은(는) [!DNL Edge Network]을(를) 통해 AJO에서 의사 결정 평가를 요청합니다. 의사 결정 엔진은 선택 전략에 대해 방문자의 행동 프로필을 평가하고 순위 논리를 적용하고 부적격 항목(이미 구매됨, 재고 부족)을 필터링한 다음 권장 항목을 반환합니다.

권장 사항은 코드 기반 경험 또는 웹 채널 표면을 통해 페이지에서 렌더링됩니다. 렌더링은 캐러셀, 그리드, 단일 항목 위젯 또는 권장 사항 템플릿에 정의된 사용자 지정 레이아웃일 수 있습니다. 노출 및 클릭 이벤트는 성능 보고를 위해 AEP으로 자동으로 다시 추적됩니다.

**주요 고려 사항:**

- Edge decisioning에서 병합 정책을 Edge에서 활성화해야 함
- 권장 사항 대기 시간은 [!DNL Edge Network] 응답 시간에 따라 다릅니다(단일 범위 요청의 경우 500ms 미만 SLA).
- 익명 방문자는 세션 내 동작을 기반으로 권장 사항을 받습니다. 알려진 방문자는 세션 간 동작 기록의 이점을 받습니다
- 동작 기록이 없는 콜드 스타트 방문자는 대체 권장 사항을 받습니다.

**장점:**

- 세션 내 동작을 기반으로 하는 실시간 개인화
- [!DNL Edge Network]을(를) 통한 1초 미만의 추천 게재
- 익명 방문자와 알려진 방문자 모두에 대해 작동합니다
- 자동 노출 및 클릭 추적
- 새로운 권장 사항에 필요한 페이지 재로드 없음

**제한 사항:**

- Edge 프로필 스토어에 전체 프로필 속성의 하위 집합이 포함되어 있습니다
- 프로필 속성이 많은 복잡한 순위 모델은 허브측 평가가 필요할 수 있습니다
- 동작 이벤트 추적을 사용하는 [!DNL Web SDK] 배포 필요

**Experience League:**

- [Edge Decisioning API를 사용하여 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)
- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)

### 옵션 B: 모바일 앱 권장 사항

**인앱 제품 추천, 개인화된 콘텐츠 피드, 알림 기반의 추천 및 모바일 상거래 경험에 대한 추천 항목:**.

**작동 방식:**

사용자가 앱과 상호 작용할 때 [!DNL Mobile SDK]을(를) 통해 동작 신호가 수집됩니다. 제품 보기, 콘텐츠 상호 작용, 검색 및 구매는 AEP으로 스트리밍됩니다. 권장 사항 표면이 포함된 화면이 로드되면 [!DNL Mobile SDK]에서 의사 결정 평가를 요청합니다. 권장 사항은 모바일 앱 내에서 인앱 메시지, 콘텐츠 카드 또는 코드 기반 경험을 통해 제공됩니다.

콘텐츠 카드는 사용자가 편리하게 검색할 수 있는 피드와 유사한 환경에서 지속되므로 모바일 앱의 권장 사용 사례에 특히 적합합니다. 인앱 메시지는 특정 동작(예: 장바구니에 항목 추가 후 보완 제품 표시)에 의해 트리거된 상황별 권장 사항에 사용할 수 있습니다.

**주요 고려 사항:**

- 관련 상호 작용에 대한 동작 이벤트 추적을 사용하여 [!DNL Mobile SDK]을(를) 구성해야 합니다.
- 콘텐츠 카드는 지속적인 추천 표면을 제공합니다. 인앱 메시지는 사용 후 삭제됨
- 오프라인 동작 추적을 사용하려면 지연된 이벤트 제출을 위한 SDK 큐 관리가 필요합니다
- 앱스토어 업데이트 주기는 권장 사항 렌더링 변경 사항을 배포하는 속도에 영향을 줍니다

**장점:**

- 매끄러운 앱 통합 권장 사항 렌더링이 포함된 기본 모바일 경험
- 콘텐츠 카드는 영구적이고 검색할 수 있는 추천 피드를 제공합니다
- 인앱 메시지를 통해 상황별, 비헤이비어 트리거 권장 사항 활성화
- 장치 수준 신호(위치, 앱 사용 패턴)를 활용하여 관련성 향상

**제한 사항:**

- [!DNL Mobile SDK] 통합 및 앱 개발 리소스 필요
- 렌더링 변경 사항을 사용하려면 앱 업데이트가 필요합니다(서버 기반 레이아웃으로 코드 기반 경험을 사용하는 경우 제외)
- 오프라인 기간은 동작 신호 수집에 간격을 만듭니다.

**Experience League:**

- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 옵션 C: 이메일 행동 권장 사항

**가장 적합한 대상:** 이메일 캠페인의 제품 추천 — 제품 추천이 표시된 구매하지 않은 이메일, 구매 후 교차 판매 이메일, 정기적인 &quot;추천&quot; 다이제스트 및 개인화된 제품 추천이 포함된 재참여 이메일.

**작동 방식:**

이전 세션에서 누적된 행동 프로필 데이터는 이메일 전송 시간 또는 렌더링 시간에 권장 사항 선택을 알려줍니다. 대상은 적절한 수신자(예: 찾아보았지만 구매하지 않은 방문자, 최근 구매한 고객)를 타겟팅하도록 정의됩니다. 캠페인이나 여정은 추천 배치를 포함하는 이메일을 보내도록 구성되어 있습니다. 전송 시 AJO Decisioning은 선택 전략에 대해 각 수신자의 행동 프로필을 평가하고 권장 항목을 이메일 콘텐츠에 주입합니다.

이 옵션은 세션 내 신호보다는 축적된 행동 이력에 의존합니다. 계산된 속성(카테고리 친화성 점수, 최근 제품 보기, 구매 빈도)은 행동 기록을 선택 전략이 효율적으로 평가할 수 있는 프로필 수준 신호로 증류하므로 이메일에 대한 권장 사항 품질을 크게 향상시킵니다.

**주요 고려 사항:**

- 이메일 권장 사항은 열기 시간이 아닌 전송 시간에 평가됩니다. 전송 시점의 행동 프로필 상태가 권장 사항을 결정합니다
- 계산된 속성은 순위 품질을 개선하는 데 적극 권장됩니다
- 이메일 렌더링 제한 사항(JavaScript 없음, 제한된 CSS)으로 추천 표시 형식이 제한됩니다
- 구성되고 검증된 이메일 채널 표면 필요

**장점:**

- 세션 간 전체 동작 내역을 활용하여 보다 심층적인 개인화
- 기존 캠페인 및 여정 워크플로우와 통합
- 웹/앱 터치포인트를 사용할 수 없는 재참여 및 전환 시나리오에 효과적입니다.
- 단일 이메일 내에 여러 개의 추천 배치를 포함할 수 있음

**제한 사항:**

- Recommendations는 전송 시 정적이며 이메일을 열 때 업데이트되지 않습니다
- 이메일 렌더링 제한으로 추천 표시 형식 제한
- 대상 평가 및 캠페인/여정 오케스트레이션 인프라 필요
- 추가적인 종속성(채널 구성, 대상 정의, 캠페인 실행)으로 인해 구현 복잡성 증가

**Experience League:**

- [이메일 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### 옵션 비교

다음 표에는 구현 옵션 간의 주요 차이점이 요약되어 있습니다.

| 기준 | 옵션 A: 웹 실시간 | 옵션 B: 모바일 앱 | 옵션 C: 이메일 동작 |
| --- | --- | --- | --- |
| 다음에 최적 | 웹 페이지 권장 사항(PDP, 홈 페이지, 카테고리) | 인앱 권장 사항 및 콘텐츠 피드 | 제품 추천이 포함된 이메일 캠페인 |
| 행동 신호 소스 | 세션 내 + 세션 간([!DNL Web SDK]) | 인앱 상호 작용([!DNL Mobile SDK]) | 누적 행동 기록(프로필) |
| 권장 사항 지연 | 매 초([!DNL Edge Network]) | 매 초([!DNL Edge Network]) | 전송 시(허브측 평가) |
| 방문자 유형 | 익명 및 알려짐 | 알려진 항목(앱 사용자) | 알려짐(이메일 수신자) |
| 복잡성 | 중간 | Medium 하이 | 높음 |
| 채널 종속성 | [!DNL Web SDK], 코드 기반 경험 표면 | [!DNL Mobile SDK], 인앱/콘텐츠 카드 표면 | 이메일 채널 표면, 대상자, 캠페인/여정 |
| 필요 | [!DNL Web SDK] 배포, Edge 병합 정책 | [!DNL Mobile SDK] 배포, Edge 병합 정책 | 이메일 표면, 대상자 정의, 캠페인 설정 |

### 적절한 옵션 선택

다음 지침을 사용하여 상황에 가장 적합한 옵션을 선택합니다.

- **기본 목표가 웹 사이트의 실시간 제품 추천인 경우 옵션 A로 시작**. 이는 가장 일반적인 시작점이며 구현 복잡성이 가장 낮은 즉각적인 가치를 제공합니다.
- 모바일 앱이 기본 참여 채널이고 인앱 권장 사항이 의미 있는 전환 향상도를 유도하는 경우 **옵션 B를 선택**&#x200B;합니다. 옵션 B는 동일한 선택 전략과 품목 카탈로그를 사용하여 옵션 A와 동시에 실행할 수 있습니다.
- 동작 권장 사항을 전자 메일 캠페인으로 확장하려면 **옵션 C**&#x200B;를 추가하십시오. 이는 일반적으로 동일한 항목 카탈로그 및 선택 전략을 사용하지만 이메일별 렌더링 템플릿 및 대상 기반 타깃팅과 함께 옵션 A 또는 B 위에 계층화됩니다.
- **활성 방문자를 위한 실시간 웹 권장 사항과 전환하지 않고 나가는 방문자를 위한 찾아보기 또는 구매 후 이메일 권장 사항을 결합하는 일반적인 패턴입니다. 옵션 A + C**.

## 구현 단계

다음 단계는 행동 권장 사항의 전체 구현을 안내합니다.

### 1단계: 동작 이벤트 스키마 및 데이터 수집 구성

**응용 프로그램 함수:** AEP: 데이터 모델링 및 준비(F2), AEP: 데이터 소스 및 수집(F3)

이 단계에서는 동작 신호 및 항목 카탈로그 데이터를 캡처하는 XDM 스키마, 데이터 세트 및 데이터 수집 메커니즘을 설정합니다. 이 데이터 기반은 모든 권장 사항 논리의 기반이 됩니다.

#### 의사 결정: 동작 이벤트 스키마 디자인

어떤 행동 신호가 권장 사항을 유도해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 제품 보기 전용 | 간단한 교차 판매/상향 판매 권장 사항 | 구현 노력 최소화, 제한된 신호 깊이 |
| 제품 보기 + 구매 | 구매 제외 및 교차 판매 논리가 있는 권장 사항 | 중재; &quot;이미 구매한 항목 제외&quot; 필터링을 활성화합니다. |
| 전체 행동 세트(보기, 구매, 장바구니에 추가, 검색, 콘텐츠 상호 작용) | 다중 신호 등급을 가진 정교한 추천 | 최고 신호 품질, 포괄적인 [!DNL Web SDK]/[!DNL Mobile SDK] 계측 필요 |

#### 결정: 항목 카탈로그 수집 방법

제품 또는 콘텐츠 카탈로그를 AEP에 수집하려면 어떻게 해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 소스 커넥터를 통한 일괄 처리 수집 | 카탈로그 업데이트는 주기적(일별/주별) | 간편한 설정, 카탈로그 변경 사항이 실시간으로 반영되지 않음 |
| 스트리밍 수집 | 카탈로그를 사용하려면 실시간에 가까운 업데이트(가격 변경, 가용성)가 필요합니다. | 보다 복잡하고, 권장 사항이 현재 인벤토리를 반영하는지 확인합니다. |
| 수동/API 업로드 | 자주 변경되지 않는 작은 카탈로그 | 가장 간단한 설정, 대규모 또는 동적 카탈로그에 대한 확장 불가 |

**UI 탐색:** 데이터 관리 > 스키마 > 스키마 만들기; 데이터 수집 > 데이터스트림 > 새 데이터스트림

**키 구성 세부 정보:**

- 경험 이벤트 스키마는 이벤트 페이로드에 제품/항목 식별자(SKU, 제품 ID, 콘텐츠 ID)를 포함해야 합니다.
- 항목 카탈로그 스키마에는 필터링 및 등급에 사용되는 범주, 가격, 이미지 URL, 가용성 상태, 태그 등의 속성이 포함되어야 합니다.
- 데이터 스트림에는 Edge 의사 결정에 대해 [!DNL Adobe Journey Optimizer] 서비스가 활성화되어 있어야 합니다.
- [!DNL Web SDK] `sendEvent` 호출에는 XDM 상거래 필드에 매핑된 제품 상호 작용 데이터가 포함되어야 합니다.

**Experience League 설명서:**

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [두 스키마 간의 관계 정의](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### 2단계: ID 및 프로필 구성

**응용 프로그램 함수:** AEP: ID 및 프로필 구성(F4)

이 단계에서는 동작 신호가 방문자 프로필과 올바르게 연결되고 실시간 추천 게재에 사용할 수 있도록 하는 ID 네임스페이스, 기본 ID 지정 및 병합 정책을 설정합니다.

#### 의사 결정: Edge 의사 결정을 위한 병합 정책

권장 사항 사용 사례에 실시간 Edge 평가가 필요합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| Edge 병합 정책에서 활성화 | 옵션 A 및 B(웹 및 모바일 실시간 권장 사항) | 1초 미만의 추천 게재에 필요, 샌드박스당 하나의 Edge 병합 정책만 필요 |
| 표준 병합 정책(Edge에 없음) | 옵션 C만(전송 시 평가된 이메일 권장 사항) | 허브측 평가에 충분함. Edge 병합 정책 슬롯을 사용하지 않음 |

#### 의사 결정: 익명과 알려진 방문자 ID 비교

익명 방문자의 행동 신호는 어떻게 처리되어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| ECID 전용(익명) | 세션 내 동작을 기반으로 하는 익명 방문자에 대한 권장 사항 | 간단한 설정, 방문자가 인증하지 않는 한 세션 간 연속성이 없음 |
| ECID + 인증된 ID(CRM ID, 이메일) | ID 결합을 사용하는 알려진 방문자에 대한 세션 간 권장 사항 | 더욱 풍부한 비헤이비어 프로필, 인증 흐름 필요 |
| 둘 다 ID 그래프 연결 사용 | ID 결합을 통한 전체 익명-알 수 있는 여정 | 가장 포괄적, ID 연결 규칙 구성 필요 |

**UI 탐색:** ID > ID 네임스페이스; 프로필 > 병합 정책

**키 구성 세부 정보:**

- ECID 네임스페이스는 미리 구성되어 [!DNL Web SDK] 및 [!DNL Mobile SDK]에 의해 자동으로 사용됩니다.
- 인증된 ID에 대해 사용자 정의 ID 네임스페이스(CRM ID, 로열티 ID)를 만들어야 합니다.
- 경험 이벤트 스키마의 기본 ID는 웹/모바일 동작 이벤트에 대한 ECID여야 합니다.
- 병합 정책은 장치 간 ID 결합에 대해 개인 장치 그래프를 사용해야 합니다.

**Experience League 설명서:**

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [아이덴티티 그래프 연결 규칙](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/identity-linking-logic)

### 단계 3: 품목 카탈로그 및 선택 전략 설정

**응용 프로그램 함수:** AJO: Decisioning

이 단계에서는 항목 카탈로그(결정 항목), 순위 지정을 위한 항목 속성과 동작 신호를 결합하는 선택 전략, 부적격 항목을 제외하는 필터링 규칙 및 콜드 스타트 프로필에 대한 대체 권장 사항을 구성합니다.

#### 결정: 항목 카탈로그 범위

추천에 사용할 수 있는 항목은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 제품 카탈로그(전자 상거래) | 실제 또는 디지털 제품을 구매하도록 추천 | 품목 속성에는 가격, 범주, 가용성, 이미지가 포함됩니다. |
| 콘텐츠 카탈로그(미디어/게시) | 기사, 비디오 또는 교육 콘텐츠 추천 | 항목 속성에는 주제, 작성자, 게시 날짜, 콘텐츠 유형이 포함됩니다. |
| 하이브리드 카탈로그 | 제품 및 콘텐츠 모두 추천 | 두 형식을 모두 포함하는 통합 항목 스키마 필요 |

#### 의사 결정: 등급 접근 방식

적합한 항목의 등급을 어떻게 지정하여 최상의 추천을 결정해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 공식 기반 순위 | 순위에 대한 비즈니스 논리 지우기(예: 카테고리 관심도 점수와 항목 관심도를 곱한 값 기준 정렬) | 투명하고 감사 가능한 등급. 정의된 등급 공식 필요 |
| AI 등급(자동 최적화) | 머신 러닝은 전환 데이터를 기반으로 최적의 순위를 결정해야 한다 | 모델 교육을 위해 최소 1,000개의 전환 이벤트가 필요하며 투명성이 낮음 |
| 우선 순위 기반(수동) | 간단하고 수동으로 큐레이트된 권장 사항 순서 | 가장 쉬운 구성, 개별 동작에 적응하지 않음 |

#### 의사 결정: 필터링 규칙

추천에서 제외해야 하는 항목은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이미 구매한 항목 제외 | 교차 판매 및 검색 권장 사항 | 행동 프로필에 구매 내역 필요 |
| 품절 항목 제외 | 동적 인벤토리를 사용한 전자 상거래 | 실시간 또는 실시간에 가까운 카탈로그 업데이트 필요 |
| 이전에 해제된 항목 제외 | 사용자가 제안을 거부할 수 있는 콘텐츠 권장 사항 | 행동 이벤트에서 해고 추적 필요 |
| 범주 범위 필터링 | 특정 범주로 제한된 권장 사항 | 필터링에 항목 속성 사용 |

#### 의사 결정: 콜드 스타트 전략

동작 기록이 없는 새 방문자에 대해 표시되는 것은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 인기 항목(글로벌 베스트셀러) | 범용 대체 | 간편한 유지 관리, 개인화되지 않음 |
| 카테고리별 인기 항목 | 방문자가 범주 페이지에 도달했습니다. | 컨텍스트에 따라 관련 폴백, 페이지 컨텍스트 필요 |
| 선별된 에디토리얼 선택 | 브랜드가 콜드 스타트 경험에 대한 에디토리얼 제어 필요 | 수동 큐레이션 및 업데이트 필요 |
| 트렌드 항목 (시간 가중 인기도) | 현재 트렌드를 반영하는 동적 폴백 | 트렌드 신호 계산 필요 |

**UI 탐색:** [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리 > 의사 결정; [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리 > 오퍼; [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리 > 배치

**키 구성 세부 정보:**

- 특성(범주, 가격, 이미지 URL, 태그)을 사용하여 카탈로그의 각 제품 또는 콘텐츠 항목을 나타내는 의사 결정 항목을 만듭니다
- 항목 카탈로그 필터링과 동작 순위 논리를 결합하는 선택 전략 정의
- 등급 모델 구성 - 공식 기반 표현식은 프로필 속성(예: 계산된 속성의 카테고리 친화성 점수)을 참조할 수 있습니다.
- 콜드 스타트 프로필에 대한 기본 권장 사항 역할을 하는 대체 오퍼/항목 만들기
- 논리적 그룹화에 컬렉션 한정자(태그)를 사용하여 항목을 컬렉션으로 구성합니다.
- 선택 전략 내에서 필터링 규칙을 설정하여 비즈니스 규칙 적용(구매 제외, 재고 전용)

**Experience League 설명서:**

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [의사 결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 4단계: 채널 및 표면 구성

**응용 프로그램 함수:** AJO: 채널 구성

이 단계는 권장 사항이 렌더링될 게재 표면을 구성합니다. 구성은 구현 옵션에 따라 크게 달라집니다.

#### 결정: 게재 표면 유형

추천은 어디에 표시됩니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 코드 기반 경험(웹) | 사용자 지정 렌더링으로 웹 페이지의 추천 위젯 | 렌더링에 대한 유연성 극대화, 프론트엔드 개발 필요 |
| 웹 채널 표면 | 표준 웹 개인화 표면 | AJO 웹 디자이너를 사용하므로 코드 기반보다 유연성이 낮음 |
| 인앱 메시지 | 앱 동작에 의해 트리거된 상황별 권장 사항 | 단기적, 상호 작용 또는 해고 후 사라짐 |
| 콘텐츠 카드(모바일) | 모바일 앱의 지속적인 추천 피드 | 사용자가 작동할 때까지 지속됩니다. 검색 가능한 피드 경험 |
| 이메일 | 이메일 캠페인에 임베드된 제품 추천 | 전송 시 정적(이메일 렌더링 제한에 따름) |

**옵션이 나뉘는 위치:**

**옵션 A의 경우(웹 실시간 권장 사항):**
코드 기반 경험 표면 또는 웹 채널 표면을 구성합니다. 코드 기반 경험은 사용자 지정 권장 사항 렌더링(회전 메뉴, 그리드, 항목 카드)에 가장 많은 유연성을 제공합니다. 표면 URI는 페이지에서 권장 사항이 나타나는 위치를 식별합니다.

**옵션 B(모바일 앱 권장 사항)의 경우:**
인앱 메시지 또는 콘텐츠 카드 표면을 구성합니다. 영구 추천 피드에 대해 컨텐츠 카드가 권장됩니다. 인앱 메시지는 상황별, 비헤이비어 트리거 권장 사항에 적합합니다.

**옵션 C의 경우(전자 메일 동작 권장 사항):**
하위 도메인 위임, IP 풀 할당 및 발신자 설정으로 이메일 채널 표면을 구성합니다. 표면이 전달성의 유효성을 검사하는지 확인합니다.

**UI 탐색:** 관리 > 채널 > 채널 표면 > 표면 만들기

**Experience League 설명서:**

- [채널 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 5단계: 콘텐츠 및 게재 구성

**응용 프로그램 함수:** AJO: 메시지 작성

이 단계는 권장 항목이 방문자에게 표시되는 방식을 제어하는 권장 렌더링 템플릿을 정의합니다. 여기에는 항목 레이아웃 디자인, 항목 속성(이름, 이미지, 가격, 링크)을 가져오는 개인화 표현식 및 전체 권장 사항 경험 디자인이 포함됩니다.

#### 결정: 권장 사항 표시 형식

추천 항목은 어떻게 렌더링해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 회전(가로 스크롤) | 세로 공간이 제한된 홈페이지 또는 범주 페이지 | 익숙한 UX 패턴, 컴팩트 공간에 여러 항목 표시 |
| 그리드(다중 행) | 충분한 공간이 있는 전용 추천 섹션 | 한 번에 더 많은 항목을 표시합니다. &quot;사용자에게 추천&quot; 섹션에 적합합니다. |
| 단일 항목 위젯 | 특정 페이지 위치(예: 사이드바)의 상황별 추천 | 설치 공간 최소화, 영향이 큰 배치 |
| 인라인 이메일 블록 | 이메일 본문에 포함된 권장 사항 | 이메일 HTML/CSS 제한에 따름. 일반적으로 2~4개 항목 |

#### 결정: 표시할 권장 사항 수

배치당 몇 개의 항목을 결정 반환해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 3-4개 항목 | 표준 추천 위젯 | 시각적 밀도와 관련성 균형 잡기 |
| 6-8개 항목 | 스크롤 또는 그리드 레이아웃이 포함된 회전 메뉴 | 방문자를 위한 추가 옵션, 충분한 카탈로그 깊이 필요 |
| 1개 항목 | 상황별 단일 제품 추천 | 가장 관련성이 높은 영향, 가장 간단한 렌더링 |
| 10개 이상의 항목 | 피드 스타일 추천 경험 | 콘텐츠가 많은 사용 사례(미디어, 게시) |

**옵션이 나뉘는 위치:**

**옵션 A의 경우(웹 실시간 권장 사항):**
코드 기반 경험 템플릿을 사용하여 권장 사항 렌더링을 디자인합니다. HTML/CSS/JavaScript을 사용하여 회전 메뉴, 그리드 또는 위젯 레이아웃을 만듭니다. Personalization 표현식은 의사 결정 응답 속성(항목 이름, 이미지 URL, 가격, 제품 URL)을 참조합니다. 노출 및 클릭 추적은 [!DNL Web SDK]에 의해 자동으로 처리됩니다.

**옵션 B(모바일 앱 권장 사항)의 경우:**
항목 표시 논리를 사용하여 콘텐츠 카드 또는 인앱 메시지 템플릿을 구성합니다. 모바일 앱이 기본적으로 렌더링하는 JSON 기반 콘텐츠 구조를 사용합니다. 각 권장 항목에 대한 딥링크를 포함합니다.

**옵션 C의 경우(전자 메일 동작 권장 사항):**
이메일 Designer을 사용하여 이메일 콘텐츠를 디자인합니다. 의사 결정 기반 콘텐츠 블록을 사용하여 추천 배치를 삽입합니다. 이메일 템플릿 내의 항목 속성에 대한 개인화 표현식을 구성합니다. 제목 줄 개인화는 상위 추천 항목을 참조할 수 있습니다.

**UI 탐색:** 콘텐츠 관리 > 콘텐츠 템플릿; 캠페인/여정 > 콘텐츠 편집 > 이메일 Designer

**키 구성 세부 정보:**

- 각 권장 사항 배치는 3단계에서 생성된 결정을 참조해야 합니다
- Personalization 표현식은 Handlebars 구문을 사용하여 항목 속성을 렌더링합니다
- 웹의 경우: 결정을 호출하고 응답을 렌더링하도록 코드 기반 경험 구성
- 이메일의 경우: 캠페인 또는 여정 내의 이메일 작업에 결정을 포함합니다
- 알려진 동작 내역이 있는 테스트 프로필을 사용하여 권장 사항 미리보기

**Experience League 설명서:**

- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### 6단계: 대상자 범위 지정 및 캠페인/여정 설정(옵션 C만 해당)

**응용 프로그램 함수:** RT-CDP: 대상 평가, AJO: Campaign 실행 또는 Journey Orchestration

이메일 기반 권장 사항(옵션 C)의 경우, 이 단계는 타겟 대상자를 정의하고 권장 사항 이메일을 제공하는 캠페인 또는 여정을 구성합니다. 권장 사항이 페이지/화면 로드 시 실시간으로 제공되므로 옵션 A 및 B는 이 단계를 건너뜁니다.

#### 의사 결정: 대상 평가 방법

추천 이메일에 대한 타겟 대상자는 어떻게 평가해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 배치 평가 | 예약된 추천 이메일 캠페인(일별, 주별 다이제스트) | 예측 가능한 전송 시간, 전송 전에 평가된 대상 |
| 스트리밍 평가 | 이벤트가 트리거된 추천 이메일(구매하지 않은 찾아보기, 구매 후) | 실시간에 가까운 대상 검증, 여정 오케스트레이션과 결합 |

#### 의사 결정: 게재 메커니즘

이메일이 캠페인을 통해 전달되어야 합니까, 아니면 여정을 통해 전달되어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 예약된 캠페인 | 정의된 대상에게 일회성 또는 반복 추천 이메일 발송 | 간단한 설정, 대상자 평가 일괄 처리 및 보내기 |
| 대상 항목을 포함한 여정 | 대상 자격에 의해 트리거된 진행 중인 추천 이메일 | 여러 단계 흐름(예: 추천 이메일, 미리 알림)을 활성화합니다. |
| 이벤트 트리거된 여정 | 특정 이벤트(찾아보기 포기, 구매)에 의해 트리거된 추천 이메일 | 실시간 트리거, 이벤트 기반 여정 입력 필요 |

**UI 탐색:** 고객 > 대상 > 대상 만들기 > 규칙 빌드; 캠페인 > 캠페인 만들기; 여정 > 여정 만들기

**키 구성 세부 정보:**

- 동작 기록을 참조하는 세그먼트 규칙 표현식(예: &quot;지난 7일 동안 제품을 보았으나 구매하지 않음&quot;)을 사용하여 타겟 대상을 정의합니다
- 4단계의 여정 표면을 참조하는 이메일 작업으로 캠페인 또는 채널 구성
- 3단계의 결정을 이메일 콘텐츠에 포함
- 과도한 메시지를 방지하기 위해 예약 및 빈도 규칙 설정

**Experience League 설명서:**

- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)

### 7단계: 보고 및 최적화 구성

**응용 프로그램 함수:** AJO: 보고 및 성능 분석, S5: 보고 및 분석

이 단계에서는 권장 사항 클릭스루, 전환 및 매출 지표에 대한 성능 모니터링을 설정합니다. 보고 인프라를 만들어 추천 효율성을 측정하고 최적화 기회를 식별합니다.

#### 결정: 보고 깊이

필요한 보고 분석 수준은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| AJO 기본 보고서만 | 기본 권장 사항 성능 모니터링 | 빠른 설정, AJO 추적 지표로 제한됨 |
| AJO + [!DNL Customer Journey Analytics] 통합 | 크로스 채널 추천 영향 분석 및 매출 기여도 분석 | [!DNL Customer Journey Analytics] 연결 및 데이터 보기가 필요합니다. 더 자세한 통찰력을 제공합니다. |
| 사용자 지정 대시보드가 있는 전체 [!DNL Customer Journey Analytics] 작업 영역 | 항목 수준, 세그먼트 수준 및 표면 수준 분석을 통한 지속적인 최적화 프로그램 | 가장 포괄적이며 [!DNL Customer Journey Analytics]개의 전문 지식과 설정이 필요합니다. |

**UI 탐색:** 캠페인 > 캠페인 선택 > 모든 시간 보고서; 여정 > 여정 선택 > 모든 시간 보고서; [!DNL Customer Journey Analytics] > 프로젝트 > 새 프로젝트 만들기

**키 구성 세부 정보:**

- 게재 및 참여 지표에 대한 AJO 캠페인 및 여정 보고서 검토
- [!DNL Customer Journey Analytics] 통합의 경우 AJO 경험 이벤트 데이터 세트(메시지 피드백, 이메일 추적, 의사 결정)를 포함하는 연결을 만드십시오.
- 권장 사항별 차원(항목 이름, 항목 카테고리, 권장 사항 표면)과 지표(노출 횟수, 클릭 수, 전환 수, 매출)를 사용하여 [!DNL Customer Journey Analytics] 데이터 보기를 만듭니다.
- 권장 사항 CTR, 전환율 및 노출당 매출에 대해 계산된 지표 작성
- 표면, 세그먼트 및 기간에 걸쳐 권장 사항 성능을 비교하는 [!DNL Customer Journey Analytics] 작업 영역 패널을 만듭니다.

**Experience League 설명서:**

- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [연결 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [계산된 지표 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

## 구현 시 고려 사항

구현 전후에 다음 보호, 위험, 모범 사례 및 장단점을 검토하십시오.

### 보호 기능 및 제한 사항

- 샌드박스당 최대 10,000개의 승인된 개인화된 오퍼(의사 결정 항목) — [의사 결정 관리 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 의사 결정당 최대 30개 배치
- 결정 요청당 최대 30개의 수집 범위
- 오퍼 게재 응답 시간 SLA: 단일 범위 Edge 요청의 경우 P95에서 500ms 미만
- AI 등급 모델은 교육을 위해 최소 1,000개의 전환 이벤트가 필요합니다
- 오퍼 한도 카운터는 처리량이 많은 시나리오에서 최대 몇 초의 지연 시간을 가질 수 있습니다
- Edge 의사 결정은 edge 프로필 스토어에서 사용할 수 있는 프로필 속성으로 제한됩니다
- 샌드박스당 Edge에서 병합 정책을 하나만 활성화할 수 있습니다. [프로필 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 샌드박스당 최대 25개의 활성 연산 속성 — [연산 속성 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- 샌드박스당 최대 4,000개의 세그먼트 정의 — [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 스트리밍 수집: HTTP 연결당 초당 최대 20,000개의 레코드 — [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### 일반적인 함정

- **의사 결정은 대체 항목만 반환합니다.** 개인화된 의사 결정 항목이 유효 날짜 범위 내에서 승인되고 자격 규칙이 방문자의 프로필 특성과 일치하는지 확인하십시오. 최대 한도에 도달하지 않았는지 확인하십시오.
- **Edge 게재에서 빈 개인 맞춤화를 반환합니다.** 데이터 스트림이 [!DNL Adobe Journey Optimizer] 서비스를 사용하도록 구성되어 있는지, [!DNL Web SDK] 요청에서 결정 범위의 형식이 올바른지 확인하십시오.
- **순위 수식이 적용되지 않음:** 수식이 구문적으로 유효하고 액세스 가능한 프로필 특성을 참조하는지 확인하십시오. 공식 오류는 자동으로 우선 순위 기반 순위로 대체됩니다.
- **오래된 권장 사항:** 동작 이벤트 데이터가 실시간으로 흐르지 않으면 권장 사항은 오래된 동작 프로필을 기반으로 합니다. [!DNL Web SDK] 또는 [!DNL Mobile SDK]이(가) 현재 이벤트를 스트리밍하고 있는지 확인하십시오.
- **콜드 스타트 대체 비율이 너무 높습니다.** 많은 방문자가 대체 권장 사항을 받는 경우 행동 기록에만 의존하지 않고 컨텍스트 신호(현재 페이지 카테고리, 참조 소스)를 사용하여 콜드 스타트 전략을 보강하는 것이 좋습니다.
- **페이지에서 렌더링하지 않는 권장 사항:** 코드 기반 경험 표면 URI가 페이지 URL 패턴과 일치하는지, [!DNL Web SDK]이(가) 결정 응답을 올바르게 요청하고 렌더링하는지 확인하십시오.
- **권장 사항에서 누락된 카탈로그 항목:** 모든 카탈로그 항목이 의사 결정 항목으로 수집되고 올바른 컬렉션 한정자로 태그가 지정되었으며 선택 전략에서 참조하는 해당 컬렉션에 포함되어 있는지 확인하십시오.

### 우수 사례

- AI 등급 모델에 투자하기 전에 계산된 속성(카테고리 친화성, 상호 작용 최신성)을 사용하여 공식 기반 순위 모델로 시작합니다. 공식 기반 모델은 투명하고 감사 가능하며, 비교를 위한 견고한 기준선을 제공합니다.
- 첫날부터 노출 및 클릭 추적을 구현합니다. 상호 작용 데이터가 없으면 AI 등급 모델이 교육할 수 없으며, 추천 효과를 측정할 수 없습니다.
- 모든 곳에서 단일 전략을 재사용하지 않고 다양한 권장 사항 표면(홈 페이지, PDP, 이메일)에 대한 별도의 선택 전략을 만듭니다. 서로 다른 표면이 서로 다른 사용자 의도를 제공합니다.
- 계산된 속성을 사용하여 행동 기록을 등급 신호로 증류합니다. 원시 이벤트 데이터는 효과적인 공식 기반 순위에 비해 너무 세분화되어 있습니다. &quot;카테고리 친화성 점수&quot; 및 &quot;마지막 구매 이후 일수&quot;와 같은 집계된 신호가 더 효과적입니다.
- 대체 권장 사항을 개인화된 권장 사항과 별도로 테스트합니다. 대체 항목이 새 방문자에게 적합한 경험을 제공하는 고품질의 브랜드에 적합한 기본값인지 확인하십시오.
- 콜드-스타트 대체 비율 을 주요 상태 지표로 모니터링합니다. 시간이 지남에 따라 대체 비율이 감소하는 것은 동작 범위가 증가하는 것을 나타냅니다.
- 이메일 권장 사항의 경우 일정은 행동 프로필이 가장 완료된 시간에 전송됩니다(예: 최대 탐색 시간 후가 아니라 검색 시간 후).

### 절충안 결정

특정 요구 사항을 기반으로 다음 상충관계를 평가해야 합니다.

#### 실시간 신호 대 누적 기록

세션 내 행동 신호는 즉각적인 관련성을 제공하지만 심도는 제한적입니다. 축적된 행동 이력은 깊이를 제공하지만 부실 할 수 있습니다. 이러한 소스 간의 균형은 추천 품질에 영향을 줍니다.

- **옵션 A는 다음과 같습니다.** 즉각적인 관련성을 위한 실시간 신호이며, 알려진 방문자에 대해 누적된 기록이 보완되었습니다.
- **옵션 C는 다음을 선호합니다.** 전자 메일이 비동기적으로 전송되기 때문에 누적된 기록
- **권장 사항:** 웹 및 모바일(옵션 A, B)의 경우 세션 내 신호와 이전 동작에서 파생된 계산된 특성을 결합하십시오. 이메일(옵션 C)의 경우, 행동 기록을 실행 가능한 프로필 수준 신호로 요약하는 계산된 속성에 크게 투자하십시오.

#### 공식 기반 및 AI 등급 모델

공식 기반 순위는 투명하고 즉각적인 것입니다. AI 등급 모델은 자동으로 조정되지만 교육 데이터가 필요하며 등급 결정에 대한 가시성이 적습니다.

- **수식 기반 지원:** 투명성, 감사 가능성, 즉시 배포 및 순위 논리에 대한 세분화된 비즈니스 제어
- **AI 등급 우대:** 자동화된 최적화, 명확하지 않은 패턴 검색 및 수동 조정 작업 감소
- **권장 사항:** 성능 기준을 설정하고 전환 데이터를 누적하려면 수식 기반 순위로 시작하십시오. 충분한 교육 데이터(1,000개 이상의 전환 이벤트)가 있고 수동 공식 튜닝을 통해 달성할 수 있는 것 이상을 최적화하려는 경우 AI 등급 모델로 전환합니다.

#### 추천 범위와 관련성 비교

항목 카탈로그를 확장하고 필터링 규칙을 완화하면 개인화된 추천을 받는 요청의 비율이 증가하지만 추천당 관련성은 감소할 수 있습니다.

- **적용 범위 우대:** 개인화된 추천을 보는 방문자 수를 최대화합니다. 기본 목표가 참여인 경우 유용합니다.
- **높은 관련성 선호도:** 더 많은 방문자에게 대체 권장 사항이 표시되더라도 관련성이 높은 항목만 표시합니다. 기본 목표가 전환인 경우 유용합니다.
- **권장 사항:** 보통 필터링(구매한 항목 제외, 재고 부족 항목)으로 시작하고 대체 속도와 전환율을 모두 모니터링합니다. 전환 데이터가 지원하는 경우에만 필터링 규칙을 강화합니다.

#### Personalization 깊이 대 구현 복잡성

더 풍부한 동작 신호와 더 정교한 순위 모델은 추천 품질을 향상시키지만 구현 복잡성과 유지 관리 부담을 증가시킵니다.

- **간단한 구현의 장점:** 가치 창출 시간 단축, 유지 관리 비용 절감, 디버그 및 반복하기 쉬움
- **더 심층적인 개인화 혜택:** 더 높은 전환 향상도, 더 나은 고객 경험, 경쟁사 차별화
- **권장 사항:** 단계적으로 구현. 제품 보기 신호 및 수식 기반 등급으로 시작합니다(1단계). 동작 강화를 위해 계산된 속성을 추가합니다(2단계). 기반이 성숙되고 충분한 교육 데이터를 사용할 수 있게 되면 AI 등급 모델을 평가합니다(3단계).

## 관련 설명서

다음 리소스는 이 패턴에 사용되는 기술 및 기능에 대한 추가 세부 정보를 제공합니다.

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
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [Edge Decisioning API를 사용하여 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/api/offer-delivery-api/edge-decisioning-api)

### 데이터 수집 및 웹/모바일 SDK

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)

### XDM 및 데이터 모델링

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [데이터 세트 만들기](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/create)
- [두 스키마 간의 관계 정의](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/relationship-api)

### ID 및 프로필

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### 계산된 속성 및 프로필 보강

- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [계산된 속성 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [Customer AI 개요](https://experienceleague.adobe.com/en/docs/experience-platform/intelligent-services/customer-ai/overview)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [채널 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)

### 메시지 작성 및 개인화

- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)

### 보고 및 분석

- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [계산된 지표 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)

### 데이터 거버넌스 및 라이프사이클

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [데이터 세트 만료](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration)

### 모니터링 및 가시성

- [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)

### 튜토리얼 및 안내서

- [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)
- [태그 개요](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
