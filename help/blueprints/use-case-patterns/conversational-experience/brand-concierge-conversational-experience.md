---
title: Brand Concierge 대화 경험
description: 디지털 속성을 고객 검색을 안내하는 AI 기반의 브랜드 안전 대화 경험으로 변환하는 방법에 대해 알아봅니다.
solution: Experience Platform, Real-Time Customer Data Platform
exl-id: a9545328-316d-446a-9308-18af61c58d1c
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '7239'
ht-degree: 0%

---

# Brand Concierge 대화 경험

이 안내서에서는 [!DNL Adobe Experience Platform]&#x200B;(AEP) 및 [!DNL Real-Time Customer Data Platform]&#x200B;([!DNL RT-CDP])과(와) 통합된 [!DNL Adobe Brand Concierge]을(를) 사용하여 AI 기반 대화 경험에 대한 포괄적인 구현 참조를 제공합니다. 디지털 자산 전반에 브랜드 안전 대화 에이전트를 배포해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

각 옵션을 선택할 시기에 대한 지침과 함께 제품 자문 챗봇에서 전체 사이트 탐색 도우미에 이르기까지 대화 경험을 배포하기 위한 모든 실행 가능한 접근 방식을 다룹니다. 이 계획에서는 에이전트 구성, 브랜드 거버넌스, 콘텐츠 통합, 배포 전략, 대화 신호로부터 프로필 강화 및 분석 최적화를 다룹니다.

[!DNL Brand Concierge]을(를) 통해 브랜드는 브랜드 음성을 이해하고 승인된 제품 카탈로그 및 콘텐츠에 액세스하며 실시간 프로필 데이터를 기반으로 개인화된 추천을 제공하고 의도 및 감정 신호를 통합 고객 프로필로 다시 캡처하는 지능형 대화 에이전트를 배포할 수 있습니다. 그 결과, 각 고객에 대한 조직의 이해를 풍부하게 하면서 자연스럽게 브랜드에 맞는 대화식 경험을 할 수 있습니다.

## 사용 사례 개요

조직에서는 정적 디지털 경험을 검색, 제품 선택 및 구매 결정을 통해 고객을 안내하는 역동적이고 AI가 지원하는 대화로 전환하고자 하는 경우가 점점 늘어나고 있습니다. [!DNL Adobe Brand Concierge] AEP Agent Orchestrator에서 제공하는 기존 디지털 속성 위에 있는 오케스트레이션된 대화형 AI 레이어를 제공하여 이러한 문제를 해결합니다.

이 패턴은 AEP의 통합 프로필과 기본적으로 통합되고, 브랜드 거버넌스 가드레일을 사용하여 모든 응답이 브랜드 표준에 부합하도록 하며, 다운스트림 개인화 및 활성화를 위해 대화 신호를 고객 데이터 플랫폼에 다시 공급하기 때문에 기존 챗봇 구현과 구별됩니다.

타겟 대상에는 디지털 경험 팀, 전자 상거래 관리자, 콘텐츠 전략가 및 마케팅 기술자가 참여도, 전환율 및 프로필 강화를 유도하는 지능형 대화 경험을 배포해야 합니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 개인화된 고객 경험 전달

콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.

**KPI:** 참여, 전환율, 고객 만족도(CSAT)

[개인화된 고객 경험을 제공하는 방법에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/deliver-personalized-customer-experiences.md)

### 고객 참여 개선

모든 디지털 및 물리적 터치포인트에서 상호 작용 빈도와 깊이를 높입니다.

**KPI:** 참여, Time On(웹) 페이지, 열람율

[고객 참여도 향상에 대해 자세히 알아보기](/help/blueprints/business-objectives/qualification-sales-b2b/improve-customer-engagement.md)

### 전환율 향상

구매, 등록 또는 양식 제출과 같은 원하는 작업을 완료하는 방문자 및 잠재 고객의 비율을 향상시킵니다.

**KPI:** 전환율, 잠재 고객 전환, 잠재 고객당 비용

[전환율 증가에 대해 자세히 알아보기](/help/blueprints/business-objectives/revenue-monetization/increase-conversion-rates.md)

### 신규 고객 확보

타겟팅 획득 캠페인, 유사 대상 및 유료 미디어 최적화를 통해 고객 기반을 확장합니다.

**KPI:**&#x200B;개의 신규 고객, 고객 확보 비용, 잠재 고객/잠재 고객 전환

[신규 고객 확보에 대해 자세히 알아보기](/help/blueprints/business-objectives/acquisition-growth/acquire-new-customers.md)

## 예시 전술 사용 사례

다음 시나리오에서는 이 패턴을 실제로 적용하는 방법을 보여 줍니다.

- **제품 검색 도우미** — 자격을 갖춘 질문을 묻고 고객의 요구 사항, 환경 설정 및 예산에 따라 제품 권장 사항을 좁히는 대화 에이전트를 제품 목록 페이지에 배포합니다.
- **안내식 비교 관리자** - 고객이 자연스러운 대화를 통해 제품을 나란히 비교하도록 지원하여 명시된 우선 순위와 관련된 차이점을 강조 표시합니다.
- **크기 및 맞춤 컨시어지** — 의류나 신발 구매자에게 대화형 Q&amp;A를 사용하여 크기 선택을 안내하여 수익률을 줄이고 구매 신뢰도를 높입니다.
- **구독 또는 플랜 선택기** - 사용 패턴 및 명시된 필요에 따라 개인화된 권장 사항을 통해 서비스 계층 또는 구독 플랜 옵션을 고객에게 안내합니다.
- **사이트 탐색 도우미** - 방문자가 지정한 의도를 기반으로 관련 콘텐츠, 지원 리소스 또는 제품 범주를 찾을 수 있도록 지원하여 복잡한 사이트의 바운스 비율을 줄입니다.
- **사전 구매 상담** — 추천을 위해 쌓이는 다중 전환 대화를 통해 높은 가치의 구매 지침(예: 전자 제품, 금융 제품, 보험)을 제공합니다.
- **충성도 프로그램 컨시어지** - 충성도 멤버가 대화형 상호 작용을 통해 보상을 찾고 계층 혜택을 이해하며 상환 기회를 찾을 수 있도록 지원합니다.
- **다시 참여 대화** — 이전 검색 기록 또는 포기한 장바구니 항목을 기반으로 재방문자에게 사전 대화 전달을 시작합니다.
- **컨텍스트와 함께 라이브 에이전트 에스컬레이션** — 전체 대화 컨텍스트와 고객 프로필 데이터를 유지하면서 라이브 영업 또는 지원 에이전트에게 복잡한 문의 사항을 원활하게 전달합니다.
- **구매 후 지원 및 상향 판매** - 구매 후 대화 채널을 통해 설정 지원, 보완 제품 제안 및 만족도 체크인으로 고객을 참여시킵니다.

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 성공을 측정하는 데 도움이 됩니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 대화 참여율 | 대화를 시작하고 지속하는 방문자의 비율 | 대화 시작됨/적격 페이지 보기 |
| 대화 완료율 | 의미 있는 해결에 도달하는 대화 비율 | 완료된 대화/대화 시작됨 |
| 전환 전환율 | 원하는 작업(구매, 등록, 리드 양식)으로 이어지는 대화의 백분율 | 대화 전환 / 총 대화 |
| 평균 대화 깊이 | 대화당 회전 수, 참여 품질 표시 | 세션당 평균 메시지 수 |
| 고객 만족도(CSAT) | 경험 내 피드백의 대화 후 만족도 점수 | 설문 조사 응답 또는 상향/하향 평점 |
| 권장 사항 수락율 | 수락되거나 클릭된 제품 추천의 비율 | 실행된 권장 사항 / 제공된 권장 사항 |
| 라이브 에이전트 핸드오프 비율 | 라이브 에이전트로 에스컬레이션된 대화의 비율 | Handoffs / 전체 대화 |
| 프로필 보강 비율 | 새로운 의도 또는 환경 설정 신호를 생성하는 대화 비율 | 보강된 프로필 / 총 대화 |
| 대화의 영향을 받은 매출 | 전환 전 [!DNL Brand Concierge] 대화가 있었던 구매의 매출 | 대화-구매 여정에 대한 속성 분석 |
| 해결 시간 | 대화 시작부터 해결 또는 핸드오프까지의 평균 기간 | 대화 이벤트 간 타임스탬프 분석 |

## 사용 사례 패턴

**Brand Concierge 대화 경험**

디지털 속성을 자연스러운 대화 상자를 통해 고객 검색을 안내하고 의도 및 감정 신호로 프로필을 보강하며 개인화된 제품 추천을 제공하는 AI 기반의 브랜드 안전 대화 경험으로 전환합니다.

**기능 체인:** 에이전트 구성 > 브랜드 거버넌스 설정 > 콘텐츠 통합 > 대화형 경험 배포 > 프로필 강화 > 분석 및 최적화

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Brand Concierge]** — 에이전트 orchestrator, Product Advisor Agent, 사이트 자문 에이전트, 브랜드 거버넌스 및 대화형 분석을 제공하는 AI 기반 대화형 경험 애플리케이션
- **[!DNL Adobe Experience Platform] (AEP)** — XDM 스키마, ID 확인, 실시간 고객 프로필 및 대화 신호를 위한 데이터 수집 인프라를 제공하는 통합 데이터 기반
- **[!DNL Real-Time CDP] ([!DNL RT-CDP])** — 개인화된 대화에 대한 실시간 프로필 조회, 대화 신호의 대상자 세분화 및 의도 및 감정 데이터를 통한 프로필 강화를 제공하는 고객 데이터 플랫폼

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 필수 | [!DNL Brand Concierge] 권한이 활성화된 샌드박스, 대화형 경험 관리자, 콘텐츠 관리자 및 분석 사용자에 대해 구성된 역할, PII 또는 중요한 고객 신호가 포함된 대화형 데이터에 대해 ABAC 정책 배치 | [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 대화 이벤트에 대한 XDM 스키마(의도, 감정, 제품 상호 작용 및 전달 이벤트를 캡처하는 대화별 필드 그룹이 있는 ExperienceEvent 클래스), 대화 환경 설정 및 의도 속성으로 확장된 프로필 스키마, 권장 사항 접지를 위한 제품 카탈로그 조회 스키마 | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| 데이터 소스 및 수집 | 필수 | 대화형 이벤트 데이터를 AEP 데이터 세트로 라우팅하는 데이터 스트림으로 구성된 [!DNL Web SDK] 또는 [!DNL Mobile SDK], 대화 중 실시간 이벤트 캡처를 위한 [!DNL Edge Network] 통합, 소스 커넥터 또는 일괄 처리 수집을 통해 수집된 제품 카탈로그 데이터 | [Web SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) |
| ID 및 프로필 구성 | 필수 | 방문자 식별을 위해 구성된 ID 네임스페이스(익명의 경우 ECID, 인증된 경우 CRM ID 또는 이메일), 대화 중 실시간 프로필 조회를 위해 Edge 활성화로 구성된 병합 정책, 장치 간 대화 연속성을 위한 ID 연결 규칙 | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) |
| 대상 정의 및 세분화 | 가정 위치 | 핵심 대화 배포에는 필요하지 않지만 개인화된 대화 전략에 필요한 대상(예: 고가치 고객 세그먼트는 다양한 대화 흐름을 받음), 실시간 대화 개인화에 권장되는 스트리밍 또는 에지 평가 | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 다운스트림 세그먼테이션 및 개인화에 사용할 수 있도록 대화 신호를 프로필 수준 속성(예: 총 대화, 주요 제품 관심, 평균 감정 점수)으로 집계 | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | 대화 이벤트 데이터에 대한 보존 정책을 구성하고, 대화 기록 및 프로파일링에 대한 동의를 관리하며, 대화 기록에 대한 개인 정보 삭제 요청을 지원합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | PII, 감정 또는 의도 신호가 포함된 대화 데이터 필드에 레이블을 지정하고 중요한 대화 데이터가 승인되지 않은 대상에 도달하지 못하도록 거버넌스 정책을 적용합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| 모니터링 및 가시성 | 추천 | 대화 이벤트 수집 파이프라인을 모니터링하고, 프로필 보강 성공률을 추적하고, 대화 개인화 품질에 영향을 줄 수 있는 데이터 흐름 실패에 대해 경고합니다 | [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | 크로스 채널 대화 영향 분석을 위해 [!DNL Brand Concierge] 기본 제공 분석 및 [!DNL CJA]을(를) 사용하여 대화 성과, 고객 피드백, 전환 속성 및 에이전트 효과를 분석합니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Brand Concierge]

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 에이전트 구성 | 1단계: 에이전트 구성 | 에이전트 전문 기술(제품 관리자, 사이트 자문) 및 기본 동작 설정을 사용하여 [!DNL Brand Concierge] 에이전트 Orchestrator 구성 |
| 브랜드 거버넌스 설정 | 2단계: 브랜드 거버넌스 설정 | 브랜드 음성, 톤, 메시징 가드레일, 승인된 콘텐츠 경계 및 모든 대화 상호 작용을 형성하는 금지된 주제를 정의합니다 |
| 컨텐츠 통합 | 3단계: 컨텐츠 통합 | AEM 컨텐츠, 제품 카탈로그, 기술 자료 및 기타 신뢰할 수 있는 데이터를 비롯한 브랜드에서 승인한 컨텐츠 소스를 연결하여 기본적인 응답 제공 |
| 제품 관리자 구성 | 3단계: 컨텐츠 통합 | 개인화된 제품 권장 사항, 안내식 비교 및 브랜드 맞춤형 응답 전달을 위한 Product Advisor Agent 구성 |
| 사이트 자문 구성 | 3단계: 컨텐츠 통합 | 방문자 행동 및 의도 신호에 따라 상호 작용을 조정하여 탐색을 향상시키도록 사이트 자문 에이전트를 구성합니다 |
| 대화형 경험 배포 | 4단계: 대화형 경험 배포 | 텍스트 및 음성 상호 작용 지원을 통해 지원되는 채널(웹, 모바일 앱, 사용자 지정 SDK)에 걸쳐 대화 경험을 배포할 수 있습니다 |
| 로우 코드 흐름 관리 | 4단계: 대화형 경험 배포 | 마케팅 팀이 로우 코드 구성 도구를 사용하여 대화 톤, 흐름 및 콘텐츠를 업데이트할 수 있도록 활성화 |
| 대화형 프로필 보강 | 5단계: 프로필 보강 | 대화 중에 캡처한 의도, 감정, 제품 친화성 및 행동 신호로 AEP 고객 프로필을 보강합니다 |
| 대화형 분석 | 6단계: 분석 및 최적화 | 내장된 분석 대시보드를 통해 참여 지표, 고객 피드백, 전환 데이터 및 대화 품질 모니터링 |
| 라이브 에이전트 제출 | 4단계: 대화형 경험 배포 | 전체 대화 컨텍스트를 유지하면서 라이브 영업 또는 지원 에이전트에 대한 원활한 전달 구성 |

### [!DNL Real-Time CDP]

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 실시간 프로필 조회 | 4단계: 대화형 경험 배포 | 실시간 고객 프로필 속성 및 세그먼트 멤버십에 액세스하여 알려진 고객 데이터를 기반으로 대화 응답을 개인화합니다 |
| 프로필 보강 | 5단계: 프로필 보강 | 대화 행동 이벤트(의도 점수, 감정 트렌드, 제품 선호도)에서 파생된 계산된 속성으로 프로필을 보강합니다. |
| 대상 평가 | 5단계: 프로필 보강 | 대화 신호를 기반으로 대상 멤버십을 평가하여 참여 대화 세그먼트의 다운스트림 타겟팅을 활성화합니다 |

## 필요 조건

구현이 시작되기 전에 다음 항목이 있어야 합니다.

- [ ] [!DNL Adobe Brand Concierge] 권한이 조직에 대해 활성화되었습니다.
- [ ] AEP 및 [!DNL RT-CDP] 라이선스에 충분한 프로필 및 이벤트 볼륨 권한이 제공됨
- [ 음성, 톤, 승인된 메시지 및 금지된 주제를 정의하는 사용 가능한 ] 브랜드 지침 문서
- [ ] 통합을 위해 준비된 제품 카탈로그 또는 콘텐츠 저장소(AEM 자산, PIM 데이터 또는 구조화된 제품 피드)
- [ SDK 통합에 대한 기술 액세스 권한으로 대화형 경험 배포에 대해 식별된 ] 웹 속성
- [ 핸드오프가 필요한 경우 사용 가능한 ] 라이브 에이전트 인프라(연락처 센터 플랫폼, CRM 통합)
- [ 대화형 데이터 캡처 및 프로파일링을 위해 ] 동의 관리 프레임워크 사용
- [ ] [!DNL Web SDK] 또는 [!DNL Mobile SDK]이(가) 대상 속성에 이미 배포되었거나 동시 배포에 예정되어 있습니다.
- [ 대화 범위에 대한 ] 관련자 정렬(제품 설명서만, 사이트 탐색 또는 둘 다)
- [ AI 기반 대화 데이터 캡처 및 사용에 대한 ] 개인 정보 및 법률 검토 완료됨

## 구현 옵션

다음 섹션에서는 이러한 사용 사례 패턴을 구현하기 위한 다양한 접근 방식을 설명합니다.

### 옵션 A: 제품 관리자 배포

**가장 적합한 대상:** 전자 상거래 및 소매 조직은 전환율과 평균 주문 가격을 유도하는 안내식 제품 검색, 비교 및 권장 사항 경험에 중점을 둡니다.

**작동 방식:**

Product Advisor Agent은 기본 대화 특수화로 구성됩니다. 제품 카탈로그에 연결하고 제품 속성 및 관계를 이해하며 고객이 개인화된 추천을 받을 수 있도록 자연스러운 대화 상자를 통해 안내합니다. 에이전트는 브랜드 거버넌스 가드레일을 사용하여 권장 사항이 비즈니스 우선 순위에 부합하도록 합니다(예: 재고 내 항목 홍보, 마진 기반 제품 강조).

Product Advisor는 실시간 고객 프로필과 통합되어 구매 내역, 검색 동작 및 환경 설정 데이터에 액세스하므로 고객이 이미 소유하고 있거나, 이전에 고려했거나, 필요할 것 같은 항목을 설명하는 권장 사항을 프로필을 기반으로 활성화할 수 있습니다. 대화는 경험 이벤트 및 의도 신호가 다운스트림 사용을 위해 프로필로 다시 이동할 때 캡처됩니다.

**주요 고려 사항:**

- 효과적인 추천을 위해 풍부한 특성 데이터가 포함된 잘 구성된 제품 카탈로그 필요
- 품절 또는 단종 품목을 추천하지 않도록 제품 데이터를 최신 상태로 유지해야 합니다
- 브랜드 거버넌스에서는 에이전트가 경쟁 제품 언급 및 가격 비교를 처리하는 방법을 정의해야 합니다

**장점:**

- 가이드 구매 전환을 통해 측정 가능한 매출 효과를 직접 유도
- 정보에 입각한 구매 결정을 통해 제품 반품 비율 감소
- 다운스트림 개인화를 위해 고가치 제품 선호도 및 의도 신호를 캡처합니다.
- 기존 전자 상거래 경험의 자연스런 확장

**제한 사항:**

- 지속적인 제품 카탈로그 유지 관리 및 동기화 필요
- 제품 중심 대화로 제한되어 있어 사이트 탐색 질문이 해결되지 않을 수 있음
- 카탈로그 데이터 품질과 완성도에 따라 효율성 향상

**Experience League:**

- [Brand Concierge 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Brand Concierge 제품 관리자](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)

### 옵션 B: 사이트 자문 배포

**가장 적합한 대상:** 방문자가 관련 콘텐츠, 리소스 또는 셀프서비스 도구를 찾기 위해 탐색 지원이 필요한 복잡한 디지털 속성(미디어, 금융 서비스, 의료, 기술)이 있는 조직입니다.

**작동 방식:**

사이트 자문 에이전트는 기본 대화 전문으로 구성됩니다. 사이트 콘텐츠 구조를 인덱싱하고, 페이지 관계 및 콘텐츠 범주를 파악하며, 방문자 행동 신호 및 명시된 의도를 기반으로 지침을 조정합니다. 방문자가 참여하면 에이전트는 방문자의 요구 사항을 해석하고 가장 관련성이 높은 콘텐츠, 도구 또는 리소스로 안내합니다.

사이트 자문은 프로필 데이터(이전 방문, 콘텐츠 환경 설정, 고객 계층)와 결합된 실시간 행동 신호(현재 페이지, 참조 소스, 탐색 경로)를 사용하여 컨텍스트에 맞는 탐색 지원을 제공합니다. 이는 깊은 콘텐츠 계층, 여러 제품 라인 또는 복잡한 셀프서비스 워크플로가 있는 사이트에서 특히 유용합니다.

**주요 고려 사항:**

- 사이트 콘텐츠 변경에 따라 포괄적인 콘텐츠 인덱싱 및 일반 re-크롤링 필요
- 방문자가 일반적으로 필요한 것을 찾기 위해 애쓰는 상당한 콘텐츠 너비를 가진 사이트에서 가장 효과적입니다
- 브랜드 거버넌스는 범위 경계(에이전트가 이동할 수 있는 사이트 영역)를 정의해야 합니다.

**장점:**

- 복잡한 사이트에서 바운스 비율 감소 및 콘텐츠 검색 기능 향상
- 콘텐츠 간격 및 사용자 경험 문제를 표시하는 탐색 의도 신호를 캡처합니다.
- Product Advisor보다 구현 복잡성 감소(제품 카탈로그 통합 불필요)
- 방문자가 찾고 있지만 찾을 수 없는 항목에 대한 분석 통찰력을 제공합니다

**제한 사항:**

- 제품 중심의 대화보다 매출 전환에 덜 직접적으로 연결됨
- 정확한 지침을 위해 콘텐츠를 잘 구성하고 정기적으로 업데이트해야 함
- 사이트 구조가 발전함에 따라 빈번한 재교육이 필요할 수 있음

**Experience League:**

- [Brand Concierge 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Brand Concierge 사이트 관리자](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)

### 옵션 C: 통합 제품 관리자 + 사이트 자문 배포

**최적의 대상:** 광범위한 디지털 속성 및 다양한 방문자 의도를 가진 대규모 소매 또는 B2C 브랜드에서 제품 검색 및 사이트 탐색을 모두 다루는 포괄적인 대화 환경을 원하는 조직입니다.

**작동 방식:**

Product Advisor Agent 및 Site Advisory Agent가 모두 [!DNL Brand Concierge] Orchestrator 내에 구성되어 있습니다. Agent Orchestrator는 인텐트 검색을 사용하여 대화를 적절한 전문 분야로 라우팅합니다. 제품 관련 쿼리는 Product Advisor로, 탐색 및 콘텐츠 검색 쿼리는 Site Advisory로 이동합니다. Orchestrator는 한 번의 대화로 전문 분야 간의 원활한 전환을 관리합니다.

이 접근 방식은 &quot;제품 찾기 도움말&quot;에서 &quot;내 주문 상태를 확인할 수 있는 위치&quot;까지 방문자의 모든 요구 사항을 처리하는 가장 완벽한 대화 경험을 제공합니다. 브랜드 거버넌스 가드레일은 두 전문 분야에 균일하게 적용되어 대화 주제에 관계없이 일관된 브랜드 목소리를 보장합니다.

**주요 고려 사항:**

- 제품 카탈로그와 컨텐츠 통합이 모두 필요한 구현 복잡성 증가
- 전문성 간의 의도 라우팅은 잘못된 대화를 방지하기 위해 잘 조정되어야 합니다
- 브랜드 거버넌스 설정은 제품 및 탐색 컨텍스트 모두를 포괄하기에 더 광범위합니다

**장점:**

- 방문자에게 가장 포괄적인 대화 환경 제공
- 단일 진입점이 별도의 인터페이스 없이 다양한 방문자 의도를 처리합니다
- 교차 전문화 대화(예: 탐색 지원을 유도하는 제품 질문)가 자연스럽게 처리됨
- 다양한 대화 신호를 통한 풍부한 프로필 보강

**제한 사항:**

- 최고의 구현 노력과 지속적인 유지 관리
- 제품 카탈로그와 콘텐츠 팀 간의 조정 필요
- 더욱 복잡한 테스트 및 품질 보증 요구 사항
- 브랜드 거버넌스 구성이 더 많이 포함됩니다.

**Experience League:**

- [Brand Concierge 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)

### 옵션 비교

| 기준 | 옵션 A: 제품 관리자 | 옵션 B: 사이트 자문 | 옵션 C: 결합 |
| --- | --- | --- | --- |
| 다음에 최적 | 전자 상거래, 제품 중심 전환 | 컨텐츠가 많은 사이트, 셀프서비스 탐색 | 전체 범위 디지털 환경 |
| 복잡성 | 중간 | Low-Medium | 높음 |
| 가치 창출 시간 | 4-6주 | 3-5주 | 6-10주 |
| 매출에 미치는 영향 | 높음(직접 전환 영향) | Medium(참여를 통한 간접) | 가장 높음(전환과 참여 모두) |
| 콘텐츠 요구 사항 | 풍부한 특성을 가진 제품 카탈로그 | 사이트 콘텐츠 인덱스 | 제품 카탈로그 및 컨텐츠 색인 |
| 프로필 보강 | 제품 관심도, 구매 의도 | 탐색 의도, 컨텐츠 환경 설정 | 전체 신호 스펙트럼 |
| 유지 관리 노력 | 제품 카탈로그 동기화 | 콘텐츠 리인덱싱 | 둘 다 진행 중 |

### 적절한 옵션 선택

먼저 주요 비즈니스 목표 및 디지털 속성 특성을 평가합니다.

1. **기본 목표가 제품 전환을 유도하는 것이고** 디지털 속성이 상업에 중점을 둔 경우 **옵션 A(제품 관리자)**&#x200B;를 선택하십시오. 소매 및 전자 상거래 브랜드의 가장 일반적인 시작점입니다.

2. **콘텐츠 검색 기능을 개선하는 것이 기본 목표이고** 사이트에 깊은 콘텐츠 계층 또는 복잡한 셀프 서비스 워크플로가 있는 경우 **옵션 B(사이트 자문)**&#x200B;를 선택하세요. 미디어, 금융 서비스, 의료 및 기술 회사에 이상적입니다.

3. **포괄적인 적용 범위가 필요한 경우** 제품 상거래와 콘텐츠 탐색이 모두 필요한 경우 **옵션 C(결합)**&#x200B;을(를) 선택하십시오. 하나의 전문화에서 시작하여 첫 번째 다음에 두 번째 를 추가하는 것이 안정적이고 최적화되었다고 생각해 보십시오.

대부분의 조직에는 단계별 접근 방식이 권장됩니다. 먼저 한 가지 전문 기술을 배포하고, 성능을 검증하고, 학습을 수집한 다음 결합된 배포로 확장하십시오.

## 구현 단계

다음 단계에서는 권장 구현 순서를 간략하게 설명합니다.

### 1단계: 에이전트 구성

**응용 프로그램 함수:** [!DNL Brand Concierge]: 에이전트 구성

에이전트 전문 기술(제품 관리자, 사이트 자문 또는 둘 다)을 선택하고, 기본 에이전트 동작을 구성하고, 프로필 액세스 및 이벤트 캡처를 위해 [!DNL Brand Concierge]과(와) AEP 간의 연결을 설정하는 등 핵심 [!DNL Brand Concierge] 에이전트 Orchestrator를 구성합니다.

#### 의사 결정: 에이전트 특수화 선택

이 배포에 대해 활성화할 에이전트 특수화를 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 제품 관리자만 | Commerce 중심의 배포 타깃팅 제품 검색 및 전환 | 제품 카탈로그 통합 필요, 매출에 미치는 영향의 가장 빠른 경로 |
| 사이트 자문만 | 컨텐츠 및 탐색 중심 배포 | 통합 복잡성 감소, 비커머스 사이트에 적합 |
| 두 가지 전문 | 제품 및 콘텐츠 전반의 포괄적인 대화 범위 | 복잡성 증가, 1단계부터 단계적 롤아웃 고려 |

#### 의사 결정: 대화 시작 모델

디지털 속성에서 대화를 시작하는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 방문자 시작(수동) | 채팅 위젯을 사용할 수 있지만 사전 예방적으로 관여하지 않는 기본 접근 방식 | 중단 위험 감소, 채팅 옵션에 대한 방문자의 인지도에 의존 |
| 사전 예방적 참여(트리거됨) | 상담원은 행동 신호(예: 장시간 유지, 반복된 페이지 방문, 장바구니 망설임)를 기반으로 대화를 시작합니다. | 참여도는 높아지지만 트리거가 너무 공격적일 경우 방문자 불편이 발생할 수 있습니다. 행동적 트리거 조정이 필요합니다. |
| 하이브리드(상황에 맞는 프롬프트가 있는 수동) | 채팅 위젯은 수동적이지만 페이지 콘텐츠나 방문자 행동을 기반으로 상황별 프롬프트를 표시합니다 | 균형 잡힌 접근 방식, 강제 참여 없이 안내 |

#### 에이전트 구성

**UI 탐색:** [!DNL Experience Platform] > AI Assistant > [!DNL Brand Concierge] > 에이전트 구성

주요 구성 세부 정보:

- 대화 인터페이스에 나타날 에이전트 이름과 설명을 정의합니다.
- 에이전트가 액세스해야 하는 고객 프로필 및 이벤트 데이터가 포함된 AEP 샌드박스를 선택합니다
- 의도 탐지를 기반으로 전문화 간에 쿼리를 라우팅하도록 에이전트 오케스트레이터를 구성합니다.
- 대화 세션 매개 변수 설정(시간 제한 기간, 최대 대화 길이, 동시 세션 제한)
- 에이전트가 대화 중에 방문자 프로필 데이터에 액세스할 수 있도록 실시간 프로필 조회 통합을 활성화합니다

**옵션이 나뉘는 위치:**

**옵션 A(제품 관리자)의 경우:**
제품 관리자 전문화를 활성화하고 제품 카탈로그 데이터 소스에 대한 연결을 구성합니다. 응답당 최대 권장 사항 수, 제품 속성 표시 환경 설정 및 비교 처리 규칙을 포함하여 제품 권장 사항 매개 변수를 설정합니다.

옵션 B의 **사이트 자문:**
사이트 자문 전문화를 활성화하고 사이트 콘텐츠 인덱스에 대한 연결을 구성합니다. 콘텐츠 범위 경계, 페이지 카테고리 처리 및 딥링크 생성 환경 설정을 포함한 탐색 매개 변수를 설정합니다.

옵션 C의 **(결합):**
전문화를 모두 활성화하고 Orchestrator의 인텐트 라우팅 논리를 구성합니다. 제품 관리자 와 사이트 자문 간에 대화를 처리해야 하는 시기와 단일 대화 내에서 전문 분야 간 전환을 관리하는 방법을 결정하는 라우팅 규칙을 정의합니다.

**Experience League 설명서:**

- [Brand Concierge 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [AI Assistant 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/home)
- [AEP Agent Orchestrator](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)

### 2단계: 브랜드 거버넌스 설정

**응용 프로그램 함수:** [!DNL Brand Concierge]: Brand Governance 설정

모든 대화 상호 작용을 형성하는 브랜드 거버넌스 가드레일을 구성합니다. 여기에는 브랜드 음성 및 색조 정의, 승인된 콘텐츠 경계, 금지된 주제, 응답 스타일 지침 및 에스컬레이션 규칙이 포함됩니다. 브랜드 거버넌스는 모든 AI 생성 응답이 브랜드 표준에 부합하도록 보장합니다.

#### 의사 결정: 거버넌스 엄격성 수준

브랜드 거버넌스 가드레일이 대화 응답을 얼마나 엄격하게 제한해야 하는지 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 엄격한 거버넌스 | 엄격한 규제 수준이 요구되는 산업(금융 서비스, 의료, 보험) 또는 프리미엄 브랜드 | 대화 유연성의 한계. &quot;I cannot help with that&quot; 응답 빈도가 높아질 수 있음, 최고의 브랜드 안전성 |
| 관리 중재 | 브랜드 음성 일관성이 중요하지만 일부 대화 유연성이 허용 가능한 대부분의 소비자 브랜드 | 브랜드 안전성과 대화 자연성의 적절한 조화, 대부분의 구현에 권장되는 시작점 |
| 유연한 관리 | 대화적 성격과 참여가 우선시되는 캐주얼 또는 라이프스타일 브랜드 | 대부분의 자연스러운 대화 느낌; 브랜드 외 응답에 대한 지속적인 모니터링이 필요합니다. |

#### 의사 결정: 주제에서 벗어난 처리 전략

에이전트가 구성된 범위를 벗어나는 질문을 처리하는 방법을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 범위로 리디렉션 | 상담원은 질문을 인식하고 이 질문에 대한 도움을 줄 수 있는 주제로 리디렉션합니다 | 참여를 유지하지만 적절한 오프토픽 요구 사항으로 방문자를 좌절시킬 수 있습니다. |
| 라이브 에이전트에 전달 | 에이전트는 주제에서 벗어난 질문을 위해 방문자를 인간 에이전트와 연결하도록 제공합니다 | 최상의 고객 경험을 제공하지만 라이브 에이전트 인프라 및 인력 배치 필요 |
| 리소스를 통한 점진적 감소 | 상담원은 해당 항목에 대해서는 도움을 줄 수 없다고 설명하고 관련 리소스 또는 지원 채널에 대한 링크를 제공합니다 | 마찰이 적은 폴백(Fallback), 라이브 에이전트 가용성이 필요 없음 |

#### 브랜드 거버넌스 구성

**UI 탐색:** [!DNL Experience Platform] > AI Assistant > [!DNL Brand Concierge] > 브랜드 거버넌스

주요 구성 세부 정보:

- 브랜드 속성(브랜드 이름, 태그, 임무, 가치 및 대화 톤을 알려주는 성격 특성)을 정의합니다.
- 톤 매개 변수 설정: 형식 수준, 유머 내성, 공감 수준 및 제품 추천에 대한 적극성
- 승인된 콘텐츠 경계 구성: 에이전트가 논의할 권한이 있는 주제 및 명시적으로 금지되는 주제
- 응답 형식 지침 정의: 최대 응답 길이, 목록 및 산문 사용, 이모지 정책 및 링크 형식
- 에스컬레이션 트리거 설정: 라이브 에이전트에게 자동으로 대화를 라우팅해야 하는 조건(예: 고객 불만 탐지, 반복되는 불만 신호, 높은 가치의 고객 식별)
- 경쟁 언급 처리 구성: 방문자가 경쟁업체 제품에 대해 질문할 때 에이전트가 어떻게 대응해야 하는지 설명합니다.
- 면책조항 및 법적 고지 요구 사항 정의: 규제 대상 산업에 대한 필수 공개

**Experience League 설명서:**

- [Brand Concierge 브랜드 거버넌스](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [AI Assistant 작동 인사이트](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/home)

### 3단계: 컨텐츠 통합

**응용 프로그램 함수:** [!DNL Brand Concierge]: 콘텐츠 통합, 제품 관리자 구성, 사이트 자문 구성

브랜드에서 승인한 정확한 정보로 대화 응답을 기반으로 하는 콘텐츠 소스를 구성합니다. 여기에는 제품 카탈로그 통합, AEM 컨텐츠 연결, 기술 자료 가져오기 및 컨텐츠 새로 고침 일정이 포함됩니다.

#### 의사 결정: 제품 카탈로그 통합 방법

제품 데이터를 Product Advisor Agent에 제공하는 방법을 결정합니다. (옵션 A 및 C만 해당)

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| AEP 데이터 세트 통합 | 제품 카탈로그는 이미 소스 커넥터를 통해 조회 데이터 세트로 AEP에 수집되었습니다 | 기존 데이터 인프라 활용, 제품 데이터를 프로필 데이터와 동기화 유지, 제품 카탈로그를 포함하기 위한 기본 데이터 모델링 및 수집 필요 |
| 직접 피드 통합 | 제품 카탈로그는 구조화된 피드를 제공할 수 있는 PIM 또는 상거래 플랫폼에 있습니다. | 더 많은 실시간 인벤토리 및 가격 데이터를 제공할 수 있습니다. 피드 구성 및 일정 조정 필요 |
| AEM 컨텐츠 통합 | 제품 콘텐츠는 AEM에서 관리되며 신뢰할 수 있는 제품 데이터 소스 역할을 해야 합니다 | AEM이 콘텐츠 허브인 브랜드에 가장 적합하며, 웹 콘텐츠와 대화 응답 간의 일관성을 보장합니다 |

#### 의사 결정: 컨텐츠 새로 고침 빈도

에이전트의 콘텐츠 기술 자료를 얼마나 자주 업데이트해야 하는지 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 실시간 / 거의 실시간으로 | 제품 가용성, 가격 또는 콘텐츠 변경 빈도가 높음(예: 플래시 판매, 재고 구분 소매) | 정확성이 가장 높지만 인프라 로드가 높음. 재고에 민감한 권장 사항에 중요 |
| 일별 새로 고침 | 콘텐츠 변경 사항이 계획 및 예약됩니다(예: 편집 캘린더, 주간 프로모션) | 정확성과 성능의 적절한 조화, 대부분의 구현에 적합 |
| 온디맨드 새로 고침 | 콘텐츠 변경은 빈번하지 않으며 업데이트 시 수동으로 트리거할 수 있습니다 | 낮은 오버헤드. 정적 제품 카탈로그 또는 안정적인 컨텐츠 사이트에 적합 |

#### 콘텐츠 소스 구성

**UI 탐색:** [!DNL Experience Platform] > AI Assistant > [!DNL Brand Concierge] > 콘텐츠 소스

주요 구성 세부 정보:

- 제품 이름, 설명, 속성, 가격 책정, 가용성, 이미지 및 범주 계층에 대한 필드 매핑과 제품 카탈로그 데이터 원본 연결
- 사이트 페이지, 기술 자료 문서, FAQ 콘텐츠 및 지원 설명서에 대한 콘텐츠 색인화를 구성합니다.
- 에이전트가 참조할 수 있고 제외될 콘텐츠를 정의하는 콘텐츠 범위 경계 설정
- 에이전트가 질문에 답변할 관련 컨텐츠를 찾을 수 없는 경우 컨텐츠 대체 동작을 구성합니다.
- 응답, 인용 요구 사항 및 소스 속성에 포함하기 위한 최소 콘텐츠 신뢰 임계값과 같은 콘텐츠 품질 규칙 설정

**옵션이 나뉘는 위치:**

**옵션 A(제품 관리자)의 경우:**
풍부한 제품 속성 매핑을 통한 제품 카탈로그 통합에 주력하십시오. 제안할 제품 수, 재고 부족 항목을 처리하는 방법, 제품 비교를 제공하는 방법, 고객 프로필 데이터(구매 내역, 검색 동작)를 추천 순위에 통합하는 방법 등을 포함하여 Product Advisor Agent의 추천 로직을 구성합니다.

옵션 B의 **사이트 자문:**
페이지 계층 구조 매핑을 사용한 사이트 콘텐츠 색인화에 중점을 둡니다. 방문자 의도를 해석하는 방법, 우선 순위를 지정할 콘텐츠 카테고리, 모호한 탐색 요청을 처리하는 방법, 방문자의 현재 페이지 컨텍스트 및 세션 동작을 기반으로 제안을 조정하는 방법을 포함하여 사이트 자문 에이전트의 탐색 논리를 구성합니다.

옵션 C의 **(결합):**
제품 카탈로그 및 사이트 콘텐츠 소스를 모두 구성합니다. 콘텐츠 라우팅 로직이 콘텐츠를 적절한 특수화에 올바르게 할당하고 제품 콘텐츠와 사이트 탐색 콘텐츠 간의 상호 참조가 올바르게 매핑되는지 확인하십시오.

**Experience League 설명서:**

- [Brand Concierge 콘텐츠 구성](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Brand Concierge 제품 관리자](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)
- [Brand Concierge 사이트 관리자](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)
- [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)

### 4단계: 대화형 경험 배포

**응용 프로그램 함수:** [!DNL Brand Concierge]: 대화형 경험 배포, 로우 코드 흐름 관리, 라이브 에이전트 핸드오프; [!DNL RT-CDP]: 실시간 프로필 조회

채널 구성, 위젯 사용자 정의, 개인화를 위한 프로필 조회 통합, 라이브 에이전트 핸드오프 규칙 및 지속적인 콘텐츠 관리를 위한 로우 코드 도구를 포함하여 대상 디지털 속성에 대한 대화 경험을 배포합니다.

#### 의사 결정: 배포 채널

대화 경험을 배포할 채널을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 웹(임베드된 위젯) | 기본 웹 속성은 주요 고객 접점 | 가장 일반적인 시작점으로, [!DNL Web SDK] 통합이 필요합니다. 익명 방문자와 인증된 방문자를 모두 지원합니다. |
| 모바일 앱(SDK 통합) | 모바일 앱은 중요한 고객 참여 채널입니다 | [!DNL Mobile SDK] 통합이 필요합니다. 대화 UI에 화면 실제 제한을 고려하십시오. |
| 사용자 지정 SDK 배포 | 사용자 지정 애플리케이션, 키오스크 또는 비표준 디지털 속성에 대화 환경이 포함되어야 합니다 | 최대 유연성, 더 많은 개발 노력 필요, 매장 내 키오스크 또는 독점 플랫폼에 적합 |
| 다중 채널 배포 | 웹, 모바일 및 기타 채널에서 동시에 필요한 대화 경험 | 최고 도달 범위, 채널 간 일관된 브랜드 거버넌스 필요, 가능한 경우 채널 간에 대화 컨텍스트를 지속해야 함 |

#### 의사 결정: 대화를 위한 Personalization 깊이

에이전트가 대화를 개인화하는 데 사용해야 하는 고객 프로필 데이터의 양을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 익명 전용(세션 컨텍스트) | 개인 정보 우선 접근 방식 또는 대부분의 방문자가 미확인된 경우 | 세션 내 동작 신호만 사용합니다. 프로필 조회가 필요하지 않으며 익명 제품 검색에 적합합니다. |
| 프로필 인식(인증된 방문자) | 방문자는 일반적으로 로그인하며 기록 추가 값에 따라 개인화된 권장 사항입니다 | [!DNL RT-CDP]을(를) 통한 실시간 프로필 조회가 필요합니다. 알려진 고객의 추천 품질이 크게 향상되었습니다. |
| 점진적 개인화 | 대화 중 점진적 프로필 작성으로 익명 및 인증 혼합 | 세션 컨텍스트로 시작, 방문자가 정보를 제공하거나 인증을 받을 때 강화, 개인 정보와 개인화의 균형 유지 |

#### 결정: 라이브 에이전트 핸드오프 구성

살아있는 인간 에이전트에게 대화를 에스컬레이션해야 하는지 여부를 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 핸드오프 없음(셀프서비스만 해당) | AI 에이전트가 모든 예상 대화 유형을 처리할 수 있거나 라이브 에이전트를 사용할 수 없습니다 | 가장 간단한 배포. 복잡한 요구 사항으로 방문자를 좌절시킬 수 있으며, 위험도가 낮은 제품 검색 시나리오에 적합합니다. |
| 규칙 기반 제출 | 특정 트리거는 라이브 에이전트로 에스컬레이션해야 합니다(예: 컴플레인 감지, 고가치 고객, 복잡한 조회) | 예측 가능한 에스컬레이션 동작, 에스컬레이션 규칙 및 트리거 정의 필요, 라이브 에이전트 플랫폼 통합 필요 |
| 방문자 요청 핸드오프 | 방문자는 대화의 어느 시점에서든 라이브 에이전트를 요청할 수 있습니다 | 최상의 고객 경험, 항상 사용 가능한 에이전트 인력 또는 대기열 관리 필요, 대화 컨텍스트를 전송해야 함 |

#### 대화 경험 배포

**UI 탐색:** [!DNL Experience Platform] > AI Assistant > [!DNL Brand Concierge] > 배포

주요 구성 세부 정보:

- 위치, 색 구성표, 아바타, 환영 메시지 및 상호 작용 스타일(텍스트, 음성 또는 둘 다)과 같은 대화 위젯 모양을 구성합니다.
- 이벤트 캡처 및 프로필 확인을 위해 [!DNL Web SDK] 또는 [!DNL Mobile SDK]과(와) 통합
- 실시간 프로필 조회를 구성하여 고객 속성, 세그먼트 멤버십 및 대화 중 최근 활동에 액세스합니다
- 컨텍스트 전송 프로토콜, 큐 라우팅 및 에이전트 알림을 포함하여 Contact Center 플랫폼과 라이브 에이전트 핸드오프 통합을 설정합니다.
- 마케팅 팀이 개발자의 개입 없이 대화 시작자, 프로모션 메시지, 시즌 콘텐츠 및 플로우 변형을 업데이트할 수 있는 로우 코드 플로우 관리 도구를 활성화합니다
- 대화 세션 지속성 규칙 구성: 대화 기록이 유지되는 기간, 세션 간에 대화가 재개될 수 있는지 여부, 디바이스 간 대화 지속성

**Experience League 설명서:**

- [Brand Concierge 배포](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [프로필 API 엔티티 엔드포인트](https://experienceleague.adobe.com/en/docs/experience-platform/profile/api/entities)
- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### 5단계: 프로필 보강

**응용 프로그램 함수:** [!DNL Brand Concierge]: 대화형 프로필 보강, [!DNL RT-CDP]: 프로필 보강, 대상 평가

대화형 신호를 AEP 통합 고객 프로필에 다시 제공하는 캡처 및 보강 파이프라인을 구성합니다. 여기에는 대화 이벤트를 XDM에 매핑, 의도 및 감정 신호 추출, 대화 데이터에서 계산된 속성 생성, 대화 동작을 기반으로 대상 구축 등이 포함됩니다.

#### 결정: 대화 신호 캡처 범위

고객 프로필에 캡처 및 기록해야 하는 대화 신호를 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 핵심 참여 신호만 | 최소한의 프로필 보강, 캡처 대화 시작, 종료, 기간 및 완료 상태 | 가장 낮은 데이터 볼륨, 기본 분석에 충분함, 제한된 개인화 값 |
| 의도 및 환경 설정 신호 | 유추된 제품 관심 분야, 명시된 환경 설정 및 논의된 주제 카테고리 캡처 | 높은 개인화 값, 중간 데이터 볼륨, 가장 일반적으로 권장됨 |
| 전체 신호 캡처 | 의도, 감정, 제품 상호 작용, 추천 응답, 전달 이벤트 및 피드백 점수 캡처 | 풍부한 프로필 보강, 최고 데이터 볼륨, 고급 분석 및 ML 기반 개인화 활성화 |

#### 의사 결정: 대화 데이터에서 대상자 만들기

다운스트림 활성화에 대한 대화 동작을 기반으로 대상자를 만들어야 하는지 여부를 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 대화형 대상자 없음 | 대상 활성화가 아닌 분석에만 사용되는 대화 데이터 | 가장 간단한 접근 방식, 대화가 기존 참여 채널에 보충적인 경우에 적합 |
| 의도 기반 대상 | 대화에서 언급된 제품 관심사 또는 탐색 의도를 기반으로 대상자 만들기 | 관심을 표시했지만 전환되지 않은 방문자를 재타겟팅할 수 있습니다. 상업에 높은 가치를 제공합니다. |
| 행동 대상자 | 대화 참여 패턴(예: 높은 참여, 포기한 대화, 반복된 방문)을 기반으로 대상을 만듭니다 | 대화 정보에 기반한 여정 오케스트레이션 및 크로스 채널 후속 조치 활성화 |

#### 프로필 보강 구성

**UI 탐색:** [!DNL Experience Platform] > 고객 > 프로필 > 계산된 특성(파생 신호용); 고객 > 대상 > 대상 만들기(대화 대상용)

주요 구성 세부 정보:

- 대화 ID, 메시지 수, 논의된 주제, 참조된 제품, 감정 점수 및 해결 상태를 캡처하는 대화 이벤트를 XDM ExperienceEvent 스키마 필드에 매핑
- 통합 프로필에 대한 WIL(Write Intent) 및 환경 설정 신호를 사용하도록 [!DNL Brand Concierge] 프로필 데이터 보강 구성
- 대화 이벤트 데이터에서 총 대화(라이프타임), 주요 제품 범주 관심(30일), 평균 감정 점수(90일), 대화-구매 전환율과 같은 계산된 속성을 만듭니다
- 다운스트림 활성화에 대한 대화 신호를 기반으로 스트리밍 또는 일괄 대상 세그먼트 정의(예: &quot;지난 7일 동안 제품 카테고리 X에 대해 논의했지만 구매하지 않은 방문자&quot;)
- 샘플 프로필을 조회하여 대화 속성이 채워졌는지 확인하여 프로필 강화를 확인합니다.

**Experience League 설명서:**

- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- [계산된 속성 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/ui)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

### 6단계: 분석 및 최적화

**응용 프로그램 함수:** [!DNL Brand Concierge]: 대화형 분석

Analytics 대시보드 및 보고를 설정하여 대화 경험 성과를 측정하고, 최적화 기회를 식별하고, KPI를 추적합니다. 여기에는 [!DNL Brand Concierge]개의 기본 제공 분석, 크로스 채널 대화 영향 분석을 위한 선택적 [!DNL CJA] 통합 및 지속적인 최적화 워크플로가 포함됩니다.

#### 의사 결정: 분석 깊이

필요한 대화 분석 수준을 결정합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기본 제공 [!DNL Brand Concierge] 분석 | 대화량, 참여, 만족도, 전환에 대한 표준 보고로도 충분하다 | 가장 빠른 활성화, 핵심 KPI 포함, 제한된 크로스 채널 상관 관계 |
| [!DNL Brand Concierge] + [!DNL CJA] 통합 | 크로스 채널 분석은 대화가 더 광범위한 고객 여정에 미치는 영향을 이해하는 데 필요합니다. | [!DNL CJA] 연결 및 데이터 보기 설정이 필요합니다. 대화 및 다른 채널에서 속성 분석을 사용할 수 있습니다. |
| 전체 분석 스택([!DNL Brand Concierge] + [!DNL CJA] + 사용자 지정 대시보드) | 분석 통찰력을 통한 경영진 수준 보고, 고급 속성 모델링 및 사용자 지정 대상 만들기 | 최고의 분석 기능, [!DNL CJA]개의 전문 지식 필요, 데이터 중심의 대화 최적화 지원 |

#### 분석 및 최적화 구성

**UI 탐색:** [!DNL Experience Platform] > AI Assistant > [!DNL Brand Concierge] > Analytics; [!DNL Analytics Platform] > Workspace([!DNL CJA]의 경우)

주요 구성 세부 정보:

- 대화 볼륨 트렌드, 참여율, 완료율, CSAT 점수, 추천 수락율 및 핸드오프 빈도 등 [!DNL Brand Concierge]개의 기본 제공 분석 대시보드를 검토하십시오.
- 채널 간 분석을 위해 대화형 이벤트 데이터 세트를 포함하도록 [!DNL CJA] 연결을 구성하십시오([!DNL CJA] 통합을 선택하는 경우).
- 대화-전환 속성을 위한 [!DNL CJA] 작업 영역 분석을 빌드하여 어느 대화 주제가 구매 동작과 상호 연관되는지 식별합니다
- 대화 품질 모니터링 설정: 에이전트가 힘들어하는 주제, 답변하지 못하는 일반적인 질문 및 시간이 지남에 따른 감정 트렌드를 추적합니다.
- 최적화 워크플로 정의: 브랜드 거버넌스 업데이트에 대한 정기적인 검토 케이던스, 콘텐츠 새로 고침 트리거 및 분석 통찰력을 기반으로 한 대화 흐름 개선

**Experience League 설명서:**

- [Brand Concierge analytics](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [CJA Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [CJA 연결 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [CJA 데이터 보기 만들기 또는 편집](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)

## 구현 시 고려 사항

다음 섹션에서는 구현 중에 기억해야 할 보호 기능, 일반적인 위험, 모범 사례 및 상충 결정을 다룹니다.

### 보호 기능 및 제한 사항

- [!DNL Brand Concierge] 대화 경험은 AI 응답 생성률 제한을 받습니다. 동시 대화 용량은 권한 계층에 따라 다릅니다.
- 대화 중 실시간 프로필 조회는 샌드박스당 프로필 API 속도 제한을 받습니다. [실시간 고객 프로필 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 대화형 이벤트 데이터 수집은 표준 AEP 스트리밍 수집 제한을 따릅니다. — [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- 제품 카탈로그 크기 및 콘텐츠 인덱스 볼륨에 [!DNL Brand Concierge] 콘텐츠 통합 제한이 적용됩니다.
- 샌드박스당 최대 25개의 연산 속성이 대화 신호 집계에 적용됩니다. — [연산 속성 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
- 샌드박스당 최대 4,000개의 세그먼트 정의가 대화 대상에 적용됩니다. — [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)

### 일반적인 함정

- **브랜드 거버넌스 정의가 충분하지 않음:** 브랜드 거버넌스 구성을 완료하지 않고 배포하면 브랜드 외 응답이 발생하여 고객의 신뢰가 손상됩니다. 구축 전에 톤, 경계 및 에스컬레이션 규칙을 정의하는 2단계에 상당한 시간을 투자하십시오.
- **오래된 제품 카탈로그 데이터:** 오래된 재고, 가격 또는 가용성 데이터를 기반으로 한 제품 관리자 권장 사항이 고객을 좌절시키고 신뢰도를 손상시킵니다. 유효성 검사를 사용하여 자동화된 콘텐츠 새로 고침 파이프라인을 설정합니다.
- **적극적인 사전 유도 참여 트리거:** 동작 트리거를 너무 적극적으로 설정(예: 페이지에서 3초 후에 대화 트리거)하면 방문자가 불쾌해지고 바운스 비율이 증가합니다. 유지 트리거로 시작하고 참여 데이터를 기반으로 튜닝합니다.
- **익명 방문자 환경을 무시하는 중:** 인증된 방문자에게만 개인화를 집중하면 대부분의 트래픽이 무시됩니다. 세션 내 동작 신호를 사용하여 익명 방문자에게 값을 제공하는 대화 흐름을 디자인합니다.
- **프로필 보강 구성을 건너뛰는 중:** 신호를 다시 프로필에 캡처하지 않고 대화 내용을 배포하면 중요한 의도와 기본 설정 데이터가 낭비됩니다. 나중에 생각하는 것이 아니라 배포와 동시에 프로필 강화를 구성합니다.
- **라이브 에이전트 전달 환경을 무시합니다.** 잘못된 전달 환경(컨텍스트 손실, 반복된 질문, 긴 대기 시간)은 전달을 전혀 제공하지 않는 것보다 전체 대화 환경에 영향을 줍니다. 시작하기 전에 전체 전달 흐름을 처음부터 끝까지 테스트합니다.

### 우수 사례

- 단일 에이전트 전문화(제품 자문 또는 사이트 자문)로 시작하고 기준 성능을 설정한 후 확장하십시오.
- 가드레일을 구성하기 전에 마케팅, 법률 및 고객 경험 이해 당사자와 브랜드 거버넌스 워크샵을 진행합니다.
- 점진적 개인화 사용: 세션 컨텍스트 기반 응답으로 대화를 시작하고 방문자가 정보를 제공하거나 인증을 받으면 개인화를 심화합니다.
- 로우 코드 흐름 관리 도구를 사용하여 대화 시작, 프롬프트 및 추천 프레젠테이션 형식의 A/B 테스트를 구현합니다.
- 대화 분석을 정기적으로(주별 또는 격주로) 검토하여 콘텐츠 격차, 일반적인 장애 지점 및 최적화 기회를 파악합니다.
- 대화 분석 및 브랜드 거버넌스 업데이트 간의 피드백 루프 만들기 - 대화 데이터를 사용하여 색조를 조정하고, 새로운 승인된 주제를 추가하고, 에스컬레이션 규칙을 조정합니다.
- 제품 문제, 사이트 문제 또는 브랜드 인식 변화에 대한 조기 경고 시스템으로 대화 감정 트렌드를 모니터링합니다.
- 상호 작용을 심문처럼 느끼게 하지 않고 프로필을 보강하는 신호를 자연스럽게 포착하는 디자인 대화 흐름입니다.

### 절충안 결정

>[!NOTE]
>다음의 상충 결정은 조직의 특정 요구 사항과 제약 조건을 기반으로 평가되어야 합니다.

**대화 개인화 깊이와 개인 정보 보호 간소화 비교**

더 심층적인 프로필 통합을 통해 보다 개인화되고 효과적인 대화가 가능하지만 데이터 수집 복잡성, 동의 요구 사항 및 개인 정보 보호 규정 준수 부담이 증가합니다.

- **심층적인 개인화 혜택:** 전환율 향상, 추천 품질 향상, 풍부한 프로필 강화, 재방문 고객을 위한 보다 매력적인 대화
- **개인 정보 보호 간소화 우대:** 배포 시간 단축, 동의 관리 간소화, 규제 위험 완화 및 개인 정보 보호 우선 브랜드 포지셔닝
- **권장 사항:** 익명 방문자에게 잘 작동하고 인증된 세션에 대해 프로필 기반 개인화를 추가하는 점진적 개인화로 시작합니다. 따라서 개인 정보 보호 규정 준수를 관리하는 동시에 모든 식별 수준에서 가치를 제공합니다. 기존 동의 프레임워크에 정렬된 대화 프로파일링에 대한 동의 캡처를 구현합니다.

**브랜드 거버넌스 엄격성 대 대화 자연성**

엄격한 브랜드 거버넌스 가드레일을 통해 모든 응답이 브랜드 표준에 부합하도록 할 수 있지만 지나치게 엄격한 제약은 대화가 로봇처럼 느껴지게 하고 참여를 줄일 수 있게 합니다.

- **엄격한 거버넌스 혜택:** 브랜드 안전, 규정 준수, 일관된 메시징 및 예측 가능한 에이전트 동작
- **유연한 거버넌스 지원:** 자연스러운 대화 흐름, 참여도 향상, 고객 만족도 향상 및 광범위한 쿼리 처리 기능
- **권장 사항:** 보통 거버넌스로 시작하고 대화 분석을 기반으로 조이거나 해제합니다. 과한 제약의 지표로 &quot;어쩔 수 없다&quot;는 응답 비율을 모니터링한다. 로우 코드 흐름 관리 도구를 사용하여 개발자의 개입 없이 거버넌스 설정을 빠르게 반복할 수 있습니다.

**실시간 콘텐츠 새로 고침과 시스템 성능 비교**

실시간 컨텐츠 동기화를 통해 에이전트에는 항상 현재 제품 및 컨텐츠 데이터가 있지만, 지속적인 새로 고침을 통해 인프라 리소스를 더 많이 소비하고 지연 시간을 초래할 수 있습니다.

- **실시간 새로 고침 우선:** 인벤토리에 민감한 권장 사항, 시간에 민감한 프로모션 및 빠르게 변화하는 콘텐츠에 대한 정확성
- **예정된 새로 고침 필요:** 시스템 안정성, 예측 가능한 리소스 사용량 및 인프라 비용 절감
- **권장 사항:** 일일 콘텐츠 새로 고침을 기본값으로 사용하며, 고객 경험에 실질적으로 영향을 미치는 인벤토리 가용성 및 가격 책정 데이터에 대해서만 실시간에 가까운 새로 고침을 사용합니다. 컨텐츠 정확도 지표를 모니터링하여 새로 고침 빈도가 적절한지 확인합니다.

**포괄적인 신호 캡처와 데이터 관리 오버헤드**

모든 대화 신호를 캡처하면 풍부한 프로필 보강 및 분석이 가능하지만 데이터 양, 스토리지 비용 및 거버넌스 복잡성이 증가합니다.

- **전체 신호 캡처 지원:** 고급 분석, ML 모델 교육, 포괄적인 프로필 강화 및 최대 다운스트림 개인화 값
- **선택적 캡처 지원:** 스토리지 비용 절감, 데이터 거버넌스 간소화, 프로필 조회 성능 향상, 데이터 최소화 원칙 준수 용이
- **권장 사항:** 의도 및 환경 설정 신호 캡처(가운데)로 시작하여 추가 데이터가 측정 가능한 다운스트림 값을 생성하는지 확인한 후에만 전체 신호 캡처로 확장합니다. 데이터 세트 만료 정책을 대화형 이벤트 데이터에 적용하여 스토리지 증가를 관리합니다.

## 관련 설명서

다음 리소스는 이 사용 사례 패턴을 구현하기 위한 추가 정보를 제공합니다.

**[!DNL Brand Concierge]**

- [Brand Concierge 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/overview)
- [Brand Concierge 제품 관리자](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/product-advisor)
- [Brand Concierge 사이트 관리자](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/brand-concierge/site-advisor)
- [AI Assistant 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ai-assistant/home)

**[!DNL Adobe Experience Platform]**

- [AEP 개요](https://experienceleague.adobe.com/en/docs/experience-platform/landing/home)
- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

**데이터 수집 및 통합**

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [모바일 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/mobile-sdk/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home)

**ID 및 프로필**

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)

**대상 및 세분화**

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

**데이터 거버넌스 및 개인 정보 보호**

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Privacy Service 개요](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/home)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)

**모니터링 및 관찰 가능성**

- [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home)
- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)

**분석 및 보고**

- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [CJA 연결 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/overview)
- [CJA 데이터 보기 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)

**보호 기능**

- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)
- [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
