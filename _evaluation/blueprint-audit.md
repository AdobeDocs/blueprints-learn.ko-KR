---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 6%

---
# 블루프린트 감사 및 권장 사항

이 감사는 [평가 규칙](rubric.md)을(를) 아래 모든 문서에 적용합니다.
[TOC.md](../help/blueprints/TOC.md)의 &quot;아키텍처 다이어그램 및 블루프린트&quot; 섹션(76-133행) 및
은(는) 각 블루프린트가 아키텍처, 사용 사례 **패턴**&#x200B;이(가) 되어야 하는지 여부를 권장합니다.
**다이어그램**, 둘 다(**분할**) 또는 기존 패턴의 **복제**(으)로 플래그가 지정되었습니다.

이는 감사 전용입니다. 컨텐츠가 이동되지 않았습니다. 마이그레이션 백로그(일괄 A-D 작업)
권장 사항이 검토되면 별도의 후속 계획으로 작성됩니다.

## 요약

**감사된 총 문서 수:** 43

| 추천 | 계수 | 액션 |
| --- | --- | --- |
| 패턴 | 8 | 새로운 사용 사례 패턴을 작성합니다. 다이어그램으로 원본을 트리밍합니다. |
| 복제 | 9 | 기존 패턴은 범위를 다룹니다. 다이어그램 및 교차 링크에 대한 블루프린트를 단순화합니다. |
| 분할 | 2 | 패턴 컨텐츠를 추출합니다. 원본을 다이어그램으로 줄이고, 두 내용을 모두 교차 연결합니다. |
| 다이어그램 | 16 | 아키텍처 다이어그램으로 유지하고, 필요한 경우 이야기를 다듬습니다. |
| 탐색 | 8 | 섹션 랜딩 페이지(overview.md 또는 links 전용), 마이그레이션 후 다시 방문. |

### 컨트롤 그룹 보정

6개의 `experience-platform/` 파일이 모두 Pattern=0, Diagram=3→ 만장일치로 **Diagram**&#x200B;되었습니다.
루브릭이 교정되고; 다른 하위 영역으로부터의 결과는 점수로 신뢰될 수 있다.

### 새로운 사용 사례 패턴 카테고리: B2B 활성화 및 마케팅

새 범주 `use-case-patterns/b2b/`(표시 레이블 **B2B 활성화 및 마케팅**, 목차 앵커)
제안된 `{#b2b-patterns}`)은(는) 모든 B2B 관련 패턴을 포함합니다. 레이블은 기존 을 미러링합니다
[TOC.md](../help/blueprints/TOC.md)의 아키텍처 다이어그램 영역에서 &quot;B2B 활성화 및 마케팅&quot; 하위 섹션,
독자에게 두 섹션 간의 시각적 대칭성을 제공합니다.

완전히 채워지면 범주에 **7개의 패턴**&#x200B;이 포함됩니다.

| 원본 | 액션 | 대상 경로 |
| --- | --- | --- |
| `use-case-patterns/audience-building-activation/b2b-audience-activation.md` | 기존 패턴 **재배치** | `use-case-patterns/b2b/account-audience-activation.md` |
| `use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md` | 기존 패턴 **재배치** | `use-case-patterns/b2b/buying-group-marketing.md` |
| `use-case-patterns/analysis/b2b-analytics.md` | 기존 패턴 **재배치** | `use-case-patterns/b2b/account-analytics.md` |
| `b2b/b2b-journeys-with-marketo.md` | **새로 작성**(감사 패턴 행) | `use-case-patterns/b2b/marketo-data-journeys.md` |
| `b2b/ajo-b2b-paid-media-controller.md` | **새로 작성**(감사 패턴 행) | `use-case-patterns/b2b/paid-media-orchestration.md` |
| `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | **새로 작성** | `use-case-patterns/b2b/campaign-intake-and-creation.md` |
| `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | **새로 작성** | `use-case-patterns/b2b/campaign-review-and-approval.md` |

> **초기 전환 상태 — writer-coordination 게이트** 기존 &quot;B2B 활성화 및 마케팅&quot;> [TOC.md](../help/blueprints/TOC.md)의 아키텍처 다이어그램 영역에서 하위 섹션(95~106행) **그대로 유지> 전환 중**. 각 블루프린트 전환 및 기존 패턴 재배치에는 다음이 필요합니다.> 콘텐츠가 마이그레이션되기 전에 소유 작성기에서 사인오프합니다. 새로운 `b2b/` 사용 사례 패턴> 섹션은 를 사용하여 페이지별로 마이그레이션이 발생하는 동안 기존 블루프린트 섹션과 공존합니다.> 두 페이지 사이를 상호 연결합니다.

위치 변경 및 새 패턴이 모두 도착한 경우:

- [TOC.md](../help/blueprints/TOC.md) `Use Case Patterns` 섹션이 `B2B Activation & Marketing{#b2b-patterns}`
하위 섹션(작성자와 TBD 배치).
- [use-case-patterns/overview.md](../help/blueprints/use-case-patterns/overview.md)에서 B2B 범주 테이블을 가져옵니다.
- 재배치된 패턴은 `audience-building-activation`에서 제거됩니다.
  `campaign-management-orchestration` 및 `analysis` 개요 테이블입니다. 이전 URL은 유지됩니다.
[migration-redirects.csv](migration-redirects.csv)에서 리디렉션을 통해 활성 상태입니다.

### 식별된 중복 항목 (9)

블루프린트 범위는 이미 기존 사용 사례 패턴에 의해 다루어지고 있습니다. 마이그레이션 작업:
**아키텍처 다이어그램으로 단순화 + 교차 링크**.

| 블루프린트 | 기존 패턴 |
| --- | --- |
| `audience-activation/advertising-activation.md` | `use-case-patterns/audience-building-activation/audience-activation-to-destinations.md` |
| `audience-activation/segment-match.md` | `use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md` |
| `b2b/b2bactivation.md` | `use-case-patterns/audience-building-activation/b2b-audience-activation.md` |
| `b2b/b2b-buying-group-journeys.md` | `use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md` |
| `customer-journey-analytics/b2b-cja.md` | `use-case-patterns/analysis/b2b-analytics.md` |
| `customer-journeys/journey-optimizer/journey-optimizer-journeys.md` | `use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md` |
| `customer-journeys/journey-optimizer/journey-optimizer-campaigns.md` | `use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md` |
| `customer-journeys/decision-management/decision-management-edge.md` | `use-case-patterns/personalization/offer-decisioning.md` |
| `customer-journeys/decision-management/decision-management-hub.md` | `use-case-patterns/personalization/offer-decisioning.md` |

> 참고: `decision-management-edge.md`과(와) `decision-management-hub.md`이(가) 모두 같은 항목에 매핑됩니다.> 기존 `offer-decisioning.md` 패턴입니다. 두 블루프린트를 하나로 통합하는 것이 좋습니다.> deployment-options 다이어그램 또는 edge-vs-hub 배포로 기존 패턴 확대> 변형입니다. 작성기 검토를 위한 플래그입니다.

### 작성자 패턴(신규 8개 + 분할에서 2개 = 총 10개)

| Source 블루프린트 | 제안된 범주 | 제안된 패턴 제목 |
| --- | --- | --- |
| `audience-activation/customer-activity.md` | 대상자 구축 활성화 | 지원 및 판매를 위한 실시간 프로필 조회 |
| `audience-activation/data-science.md` | 대상자 구축 활성화 | 프로필 강화를 위한 데이터 과학 모델 수집 |
| `audience-activation/real-time-lookup.md` | 개인화 | 웹/모바일 Personalization용 Edge 프로필 액세스 |
| `b2b/b2b-journeys-with-marketo.md` | **b2b**(신규) | Marketo 데이터 통합을 통한 B2B 계정 여정 |
| `b2b/ajo-b2b-paid-media-controller.md` | **b2b**(신규) | Waterfall 분할 경로 논리를 통한 B2B 유료 미디어 오케스트레이션 |
| `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | **b2b**(신규) | Campaign 요청 접수 및 자동화된 프로그램 만들기 |
| `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | **b2b**(신규) | 캠페인 자산 검토 및 승인 워크플로 |
| `customer-journeys/campaign-v8/campaign-v8-overview.md` | campaign-management-오케스트레이션 | Campaign v8 일괄 오케스트레이션 및 트랜잭션 메시지 |
| `audience-activation/rtcdp-target.md` *(분할)* | 개인화 | Adobe Target과 실시간 대상 공유 |
| `customer-journeys/journey-optimizer/3rd-party-messaging.md` *(분할)* | campaign-management-오케스트레이션 | Journey Optimizer과 서드파티 메시징 통합 |

### 제안된 새 패턴 범주

- **`b2b/`**(표시 레이블 **B2B 활성화 및 마케팅**) — 위의 전용 섹션을 참조하십시오. 다음
Marketo + Workfront 패턴(`intake-and-create`, `review-and-approve-blueprint`)이 라우팅됩니다.
`marketing-resource-management` 범주가 아니라 여기에 있습니다. 해당 범주는 다음을 나타내므로
실제 B2B 마케팅 운영. 새 카테고리는 총 7개 패턴 집계: 3개 재배치됨
기존 범주 및 블루프린트에서 새로 작성된 4개.

### 마이그레이션 리디렉션

이 마이그레이션에 의해 도입된 모든 URL 변경 사항은 정식 행에 행을 추가합니다.
저장소 루트의 [`redirects.csv`](../redirects.csv)(형식: `source,dest`). 확인됨
리디렉션은 [migration-redirects.csv](migration-redirects.csv)에서 준비되고
각 해당 이동이 실제로 발생할 때 표준 파일입니다.

**확인됨(3개 항목, 스테이징됨):** 기존 패턴이 `b2b/`(으)로 재배치되었습니다. 다음을 참조하십시오
[migration-redirects.csv](migration-redirects.csv).

**보류 중 — 블루프린트가 *삭제*일 때 추가됨(제대로 된 다이어그램으로 축소되지 않음):**
패턴, 분할 또는 중복 행의 블루프린트가 나중에 완전히 제거되면에서 리디렉션을 추가합니다.
블루프린트 URL을 표준 패턴 URL로 복사합니다. 기본 마이그레이션 접근 방식(다이어그램 작성 간소화)
블루프린트 URL을 그대로 유지하며 **이러한 리디렉션이 필요하지 않습니다**. 다음에 대해 아래에 나열됨:
블루프린트가 완전히 폐기된 경우 완성도:

```
# Pattern blueprints — if deleted, redirect to the new pattern URL
# (slugs are placeholders; finalize when each pattern is authored)
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/customer-activity → use-case-patterns/audience-building-activation/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/data-science → use-case-patterns/audience-building-activation/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/real-time-lookup → use-case-patterns/personalization-patterns/<new-pattern-slug>
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2b-journeys-with-marketo → use-case-patterns/b2b-patterns/marketo-data-journeys
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/ajo-b2b-paid-media-controller → use-case-patterns/b2b-patterns/paid-media-orchestration
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/marketo-engage-and-workfront-integration-blueprint/intake-and-create → use-case-patterns/b2b-patterns/campaign-intake-and-creation
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint → use-case-patterns/b2b-patterns/campaign-review-and-approval
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/campaign-v8/campaign-v8-overview → use-case-patterns/campaign-orchestration-patterns/<new-pattern-slug>

# Duplicate blueprints — if deleted, redirect to the existing pattern URL
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/advertising-activation → use-case-patterns/audience-building-activation/audience-activation-to-destinations
/en/docs/blueprints-learn/architecture/architecture-diagrams/audience-activation/known-customer-audience-activation/segment-match → use-case-patterns/audience-building-activation/audience-collaboration-segment-match
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2bactivation → use-case-patterns/b2b-patterns/account-audience-activation  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/b2b-activation/b2b-buying-group-journeys → use-case-patterns/b2b-patterns/buying-group-marketing  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journey-analytics/b2b-cja → use-case-patterns/b2b-patterns/account-analytics  (after b2b/ relocation)
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/journey-optimizer/journey-optimizer-journeys → use-case-patterns/campaign-orchestration-patterns/event-triggered-messaging
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/journey-optimizer/journey-optimizer-campaigns → use-case-patterns/campaign-orchestration-patterns/batch-outbound-message-activation
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/decision-management/decision-management-edge → use-case-patterns/personalization-patterns/offer-decisioning
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journeys/decision-management/decision-management-hub → use-case-patterns/personalization-patterns/offer-decisioning

# Optional one-off — if customer-journey-analytics/analysis.md is relocated to experience-platform/
/en/docs/blueprints-learn/architecture/architecture-diagrams/customer-journey-analytics/analysis → architecture-diagrams/architecture-overview/analysis
```

위의 행 중 하나를 활성 리디렉션으로 변환할 때 쉼표로 구분된 형식으로 변환 `source,dest`
전체 `/en/docs/...`개 경로(`.html` 접미사 없음) 사용, 의 기존 패턴과 일치
[`redirects.csv`](../redirects.csv).

### 리디렉션 생성 정책(지속 규칙)

모든 마이그레이션 단계에 대해 다음 규칙을 따르십시오.

1. **파일이 이동되었거나 이름이 변경됨**→ 이전 URL에서 새 URL로 리디렉션을 추가합니다.
2. **파일이 삭제됨**(블루프린트가 대체됨, 다이어그램이 유지되지 않음) → 삭제된 URL에서 리디렉션을 추가할 위치
표준 대체 URL.
3. **파일 간소화**(URL이 변경되지 않음) → 리디렉션이 없습니다.
4. **TOC 앵커 이름이 변경됨**(예: 섹션 제목 변경)→ 모든 페이지의 리디렉션을 추가합니다.
해당 앵커입니다. URL이 변경되기 때문입니다.

### 작성자를 위한 미해결 질문

1. **의사 결정 관리 에지와 허브** — 둘 다 동일한 기존 에지에 매핑됩니다. `offer-decisioning.md`
패턴. 배포 변형이 있는 단일 다이어그램으로 통합하거나 별도로 처리
같은 패턴으로 상호 연결되는 다이어그램
2. **Journey Optimizer 여정과 이벤트 트리거 메시지 비교** — 에이전트가 이 복제본에 플래그를 지정했습니다.
불확실한 분류. 블루프린트를 줄이기 전에 범위 정렬을 확인하십시오.
3. **`customer-journey-analytics/analysis.md`** — 콘텐츠는 실제로 Experience Platform에 대한 것입니다.
CJA이 아닌 쿼리 서비스. `experience-platform/` 폴더로 재배치하는 것이 좋습니다. (리디렉션 1개
추가되면 [migration-redirects.csv](migration-redirects.csv)을 참조하십시오.
4. **Campaign v7(더 이상 사용되지 않음)** — 더 이상 사용되지 않는 3개의 v7 파일이 다이어그램 /
탐색. 전혀 마이그레이션할지, 그대로 유지할지 또는 TOC에서 완전히 제거할지를 확인합니다.
5. **`customer-success-stories.md`** — 링크 전용 참조 페이지(`overview.md` 아님).
탐색으로 분류됩니다. 확인하거나 재분류합니다.
6. **B2B 섹션 TOC 앵커** — 제안된 `{#b2b-patterns}`. 다른 패턴 하위 섹션은
   `-patterns` 접미사(`{#personalization-patterns}`, `{#analysis-patterns}`,
   `{#campaign-orchestration-patterns}`). 리디렉션을 작성하기 전에 다른 앵커를 확인하거나 선택합니다.
7. TOC의 **B2B 섹션 배치** — `+ Use Case Patterns{#use-case-patterns}`에서 제안됩니다.
동위 멤버 간의 순서(대상 구축 및 활성화, Personalization, 캠페인 관리)
&amp; Orchestration, Analysis, B2B 활성화 및 마케팅, 대화 경험)은
작가님이 결정하셨어
8. **소유-작성기 조정** — 각 블루프린트 전환 및 기존 패턴 재배치
콘텐츠를 이동하기 전에 작성기 로그오프가 필요합니다. 감사 테이블은 대상 상태이지
시퀀싱 계획: 시퀀싱은 조정 후 후속 마이그레이션 계획에서 수행됩니다.

## 감사 테이블

| 경로 | 제목 | 요약 | dominant_type | 추천 | proposed_pattern_category | proposed_pattern_title | proposed_diagram_title | duplicate_of | pattern_score | diagram_score | 참고 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| help/blueprints/experience-platform/experience-cloud.md | Adobe Experience Cloud 아키텍처 다이어그램 | Experience Cloud 애플리케이션 및 서비스가 AEP 기반에 통합되는 방식을 보여 주는 엔터프라이즈 아키텍처. | 다이어그램 | 다이어그램 |  |  | Experience Cloud 아키텍처 개요 |  | 0 | 3 | 재정의 3(비즈니스 목표 없음). 세 가지 상호 보완적인 다이어그램(마케팅 구조, 통합, 기업 환경). 컨트롤 그룹: 예상대로 |
| help/blueprints/experience-platform/platform-applications.md | Adobe Experience Platform 및 애플리케이션 아키텍처 다이어그램 | Experience Platform이 다른 Experience Cloud 애플리케이션과 어떻게 관련되는지를 보여 주는 아키텍처 다이어그램입니다. | 다이어그램 | 다이어그램 |  |  | AEP 및 애플리케이션 아키텍처 |  | 0 | 3 | 재정의 3. 두 개의 개요/세부 다이어그램, 구현 지침 없음. 통합-학습 문서에 대한 교차 링크입니다. 컨트롤 그룹: 예상대로 |
| help/blueprints/experience-platform/platform-data-flow.md | Adobe Experience Platform 데이터 흐름 아키텍처 다이어그램 | Experience Platform 내부 및 외부 수집 및 이그레스 경로를 보여 주는 데이터 흐름 아키텍처 다이어그램입니다. | 다이어그램 | 다이어그램 |  |  | AEP 데이터 흐름 아키텍처 |  | 0 | 3 | 재정의 3. 데이터 수집 문서에 대한 단일 데이터 흐름 다이어그램. 순수 아키텍처 아티팩트. 컨트롤 그룹: 예상대로 |
| help/blueprints/experience-platform/guardrails.md | Experience Platform 및 애플리케이션 가드레일 | AEP 및 애플리케이션에 대한 시스템 제한, 성능 기대치 및 지연 보호 기능. | 다이어그램 | 다이어그램 |  |  | AEP 및 애플리케이션 보호 및 지연 |  | 0 | 3 | 재정의 3. 지연 다이어그램과 참조 테이블. 설계 중심(Edge와 Hub). 제한 설명서(방법 아님). 컨트롤 그룹: 예상대로 |
| help/blueprints/experience-platform/deployment/websdk.md | Experience Platform 웹 SDK 및 Edge Network 아키텍처 다이어그램 | 데이터 수집 흐름을 보여주는 웹 SDK 및 Edge Network 배포 아키텍처. | 다이어그램 | 다이어그램 |  |  | 웹 SDK 및 Edge Network 배포 |  | 0 | 3 | 재정의 3. 두 다이어그램(흐름 및 시퀀스). 는 튜토리얼을 참조하지만 문서 내 방법은 참조하지 않습니다. 설계 중심. 컨트롤 그룹: 예상대로 |
| help/blueprints/experience-platform/deployment/appsdk.md | 애플리케이션별 SDK 배포 아키텍처 다이어그램 | 애플리케이션별 SDK 통합 경로 및 데이터 수집 아키텍처 다이어그램. | 다이어그램 | 다이어그램 |  |  | 애플리케이션별 SDK 배포 |  | 0 | 3 | 재정의 3. 최소한의 서술로 단일 배포 다이어그램. 순수 아키텍처 아티팩트. 컨트롤 그룹: 예상대로 |
| help/blueprints/audience-activation/advertising-activation.md | Social 및 Advertising 대상으로 Audience Activation | ID 구성 및 대상 설정을 통해 RTCDP을 통해 Facebook 및 Google 광고 네트워크에 대상을 활성화합니다. | 패턴 | 복제 |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md | 4 | 1 | 기존 패턴은 이 범위를 포함합니다. 중복 재정의. 작업: 간단한 다이어그램 작성 및 교차 링크. |
| help/blueprints/audience-activation/audience-manager.md | 장치 기반 - Audience Manager을 사용한 익명 대상 타깃팅 | 채널 전반에서 디바이스 기반 타깃팅을 위해 Audience Manager 또는 RTCDP을 사용하는 익명 대상 활성화. | 다이어그램 | 다이어그램 |  |  | 익명 장치 기반 대상 타기팅 |  | 1 | 2 | 최소한의 이야기. 아키텍처 다이어그램이 있고 시스템 토폴로지가 표시됩니다. 비즈니스 목표 프레임 없음, 배포 SDK 및 허브/에지 개념 |
| help/blueprints/audience-activation/customer-activity.md | 지원 및 판매 시나리오를 위한 실시간 프로필 액세스 | 프로필 조회 API를 통해 지원 및 영업 상담원의 실시간 고객 컨텍스트를 활성화합니다. | 패턴 | 패턴 | 대상자 구축 활성화 | 지원 및 판매를 위한 실시간 프로필 조회 |  |  | 3 | 1 | 비즈니스 결과 프레임(에이전트 컨텍스트). 사전 요구 사항 체크리스트, 구현 단계 >30개 라인 포함. 고유 사용 사례: 허브 프로필 액세스(에지 개인화 아님). 기존 개인화 패턴과는 다릅니다. |
| help/blueprints/audience-activation/data-science.md | 사용자 정의 데이터 과학을 통한 프로필 강화 블루프린트 | 머신 러닝 모델 점수를 RTCDP에 수집하여 개인화 및 세그멘테이션을 위한 프로필을 보강합니다. | 패턴 | 패턴 | 대상자 구축 활성화 | 프로필 강화를 위한 데이터 과학 모델 수집 |  |  | 3 | 1 | 비즈니스 성과 프레임(개인화를 위한 데이터 보강). 사용 사례 및 고려 사항, 구현 고려 사항이 30줄 이상입니다. 메시징/활성화가 아닌 데이터 과학 워크플로에 중점을 둡니다. |
| help/blueprints/audience-activation/enterprise-destinations.md | 엔터프라이즈 대상에 대한 대상자 및 프로필 활성화 | 판매, 지원, 분석용 클라우드 스토리지 및 엔터프라이즈 앱에 대한 프로필 및 대상자 변경 사항을 스트리밍 또는 일괄 처리할 수 있습니다. | 다이어그램 | 다이어그램 |  |  | Enterprise 대상자 및 프로필 활성화 |  | 1 | 2 | 비즈니스 목표 프레임 없음. 스파스 구현 지침. 아키텍처 다이어그램 + 클라우드 스토리지/엔터프라이즈 앱의 시스템 토폴로지. 시력에 지배적입니다. |
| help/blueprints/audience-activation/real-time-lookup.md | 웹 및 모바일 Personalization용 실시간 Edge 프로필 액세스 | 실시간 웹 및 모바일 개인화를 위해 에지(밀리초)에서 통합 프로필에 액세스합니다. | 패턴 | 패턴 | 개인화 | 웹/모바일 Personalization용 Edge 프로필 액세스 |  |  | 5 | 2 | 강력한 비즈니스 프레임 구성(짧은 지연 시간 개인화). 두 가지 구현 패턴(웹 SDK과 Edge API). 광범위한 사전 요구 사항 및 단계(>30줄). KPI에 지연 시간, 처리량이 포함됩니다. |
| help/blueprints/audience-activation/rtcdp-target.md | Target을 사용하는 알려진 고객 Personalization | 알려진 방문자 웹 및 모바일 개인화를 위해 RTCDP 대상 및 프로필을 Adobe Target과 공유합니다. | 혼합 | 분할 | 개인화 | Adobe Target과 실시간 대상 공유 | Target 통합 아키텍처 | help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md | 3 | 2 | 기존의 알려진 방문자 패턴과 겹치지만 범위가 좁습니다(Target에만 해당). 세 가지 통합 패턴. 아키텍처 다이어그램 + Edge 배포 고려. 패턴 컨텐츠 + 다이어그램 모두 →. |
| help/blueprints/audience-activation/segment-match.md | 세그먼트가 일치하는 Audience Collaboration | 개인 정보 보호 컨트롤을 통한 세그먼트 일치 기능을 통해 보안 파트너 대상 공동 작업을 활성화합니다. | 패턴 | 복제 |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/audience-collaboration-segment-match.md | 4 | 1 | 기존 패턴은 이를 정확하게 다룹니다. 중복 재정의. 다이어그램에 보존할 고유한 콘텐츠: 자세한 RBAC/동의/거버넌스 구성 및 프로그래밍 광고 워크플로. |
| help/blueprints/b2b/overview.md | B2B Analytics, 활성화 및 마케팅 블루프린트 | B2B 분석, 대상 활성화, 구매 그룹, Marketo 및 Workfront 블루프린트를 나열하는 탐색 페이지. | 탐색 | 탐색 |  |  |  |  |  |  | 재정의 1: overview.md라는 파일. 마이그레이션에서 제외됩니다. |
| help/blueprints/b2b/b2bactivation.md | B2B 대상자 및 프로필 활성화 블루프린트 | 계정 및 프로필 데이터를 사용하여 웹, 이메일 및 광고 채널에서 계정 기반 B2B 대상을 활성화합니다. | 패턴 | 복제 |  |  |  | help/blueprints/use-case-patterns/audience-building-activation/b2b-audience-activation.md | 3 | 1 | 재정의 2: 동등한 패턴이 존재합니다. 블루프린트는 더 좁은 아키텍처 중심의 하위 집합입니다. |
| help/blueprints/b2b/b2b-account-activation.md | Advertising 대상 및 파일 대상에 대한 B2B 계정 활성화 | 계정 대상자 만들기 및 활성화를 사용하여 LinkedIn 및 클라우드 스토리지 대상을 통해 B2B 계정을 타깃팅합니다. | 다이어그램 | 다이어그램 |  |  | B2B 계정 Audience Activation |  | 1 | 2 | 최소한의 비즈니스 프레임, KPI 없음, 최소한의 이야기. 아키텍처 다이어그램이 있고 LinkedIn/클라우드 스토리지 토폴로지가 설명되어 있습니다. 다이어그램으로 유지 |
| help/blueprints/b2b/b2b-buying-group-journeys.md | 구매 그룹 기반 마케팅 및 여정 관리 블루프린트 | 정의된 역할과 솔루션 관심사를 가진 구매 그룹으로 이어질 수 있는 계정 여정을 설계합니다. | 패턴 | 복제 |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/buying-group-based-marketing.md | 5 | 2 | 재정의 2: 동등한 패턴이 존재합니다. 블루프린트에는 풍부한 패턴 콘텐츠가 있지만 기존 패턴이 더 포괄적입니다. |
| help/blueprints/b2b/b2b-journeys-with-marketo.md | Marketo 데이터 블루프린트를 사용하는 B2B 여정 | 구매 그룹 여정 및 계정 참여를 조정하기 위해 Journey Optimizer B2B edition과 Marketo 데이터를 배포합니다. | 패턴 | 패턴 | b2b | Marketo 데이터 통합을 통한 B2B 계정 여정 |  |  | 4 | 1 | 강력한 비즈니스 프레임. 나열된 KPI, 여러 구현 옵션, 광범위한 고려 사항(>30개 라인). Marketo 데이터 통합 깊이 (XDM 구성, ID 결합, 필드 차단)에 의해 기존 패턴과 구별됩니다. 새 b2b/ 카테고리로 이동합니다. |
| help/blueprints/b2b/ajo-b2b-paid-media-controller.md | AJO B2B - 계정 Journey Orchestration - 유료 미디어 컨트롤러 | waterfall 논리를 사용하여 B2B 유료 미디어 캠페인을 오케스트레이션하여 캠페인에 계정을 할당하고 대상에 활성화합니다. | 패턴 | 패턴 | b2b | Waterfall 분할 경로 논리를 통한 B2B 유료 미디어 오케스트레이션 |  |  | 4 | 2 | 강력한 비즈니스 프레임. 명시적 KPI, 여러 구현 옵션, 사전 요구 사항, 30줄 이상의 서술형 기존 구매 그룹 패턴과는 다릅니다(양육이 아닌 유료 미디어 우선 순위에 중점). 새 b2b/ 카테고리로 이동합니다. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/overview.md | Marketo Engage와 Workfront 통합 블루프린트 개요 | Marketo Engage 및 Workfront을 Fusion과 함께 사용하여 캠페인 계획에서 실행 자동화에 대한 개요입니다. | 탐색 | 탐색 |  |  |  |  |  |  | 재정의 1: overview.md라는 파일. 마이그레이션에서 제외됩니다. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md | 가져오기 및 만들기 블루프린트 | Workfront Forms 및 Marketo Engage 프로그램 템플릿을 사용하여 B2B 마케팅 캠페인 요청 수신 생성을 자동화합니다. | 패턴 | 패턴 | b2b | Campaign 요청 접수 및 자동화된 프로그램 만들기 |  |  | 4 | 1 | 캠페인 속도에 대한 강력한 비즈니스 프레임. 암시적 KPI(오류/재작업 감소), 워크플로우 단계 >30라인, 준비 체크리스트. 새 b2b/ 카테고리로 이동하는 경로(Marketo+Workfront 운영 체제는 주로 B2B임). |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md | 검토 및 승인 블루프린트 | Fusion Automation을 사용하여 Workfront 증명 및 승인 워크플로를 Marketo Engage 이메일 에셋과 통합합니다. | 패턴 | 패턴 | b2b | 캠페인 자산 검토 및 승인 워크플로 |  |  | 3 | 2 | 규정 준수 및 정확성에 대한 강력한 비즈니스 프레임, 암시적 KPI(승인 속도), 30개 이상의 설명 라인, 워크플로우 계획 섹션. 새 b2b/ 카테고리로 이동합니다. |
| help/blueprints/b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md | 고객 성공 사례 | Marketo 및 Workfront 통합 결과를 보여주는 고객 사례 연구 및 웨비나에 대한 링크입니다. | 탐색 | 탐색 |  |  |  |  |  |  | 최소 컨텐츠(6개의 하이퍼링크). 비즈니스 프레임, KPI, 아키텍처 또는 이야기 없음. 탐색으로 처리됩니다. 작성자가 확인해야 합니다. |
| help/blueprints/customer-journey-analytics/overview.md | Customer Journey Analytics 블루프린트 | 다양한 채널에서 고객 데이터와 행동을 통합 및 분석하여 여정 기반 보기를 만듭니다. | 탐색 | 탐색 |  |  |  |  |  |  | 재정의 1: overview.md. 목차 스타일 랜딩 페이지입니다. 마이그레이션에서 제외됩니다. |
| help/blueprints/customer-journey-analytics/b2b-cja.md | B2B Customer Journey Analytics 블루프린트 | 계정을 기본 데이터 모델로 사용하는 B2B 조직을 위한 계정 기반 CJA 보고 및 분석입니다. | 패턴 | 복제 |  |  |  | help/blueprints/use-case-patterns/analysis/b2b-analytics.md | 4 | 2 | 재정의 2: 동등한 패턴은 CJA B2B edition의 B2B 계정 수준 분석을 포함합니다. 작업: 다이어그램, 교차 링크로 단순화합니다. |
| help/blueprints/customer-journey-analytics/cja-rtcdp.md | Real-time Customer Data Platform 블루프린트가 포함된 Customer Journey Analytics | 타깃팅 및 맞춤화를 위해 CJA에서 RTCDP으로 대상을 만들고 게시합니다. | 다이어그램 | 다이어그램 |  |  | CJA-RTCDP 대상 게시 통합 |  | 1 | 3 | 강력한 아키텍처 중심(시스템 간 통합, 배포 형태). 최소한의 이야기. 고유 컨텐츠: CJA 대상자 게시 지연 보호 기능. |
| help/blueprints/customer-journey-analytics/cja-ajo.md | Journey Optimizer 블루프린트가 포함된 Customer Journey Analytics | CJA에서 AJO 전달 및 상호 작용 데이터를 분석하고 CJA 대상을 AJO에 게시합니다. | 다이어그램 | 다이어그램 |  |  | CJA-AJO 통합 및 분석 |  | 1 | 3 | 강력한 아키텍처 중심. 최소한의 이야기. 고유 컨텐츠: 양방향 CJA-AJO 데이터 공유 패턴. |
| help/blueprints/customer-journey-analytics/analysis.md | 데이터 분석 및 인텔리전스 블루프린트 | Experience Platform 쿼리 서비스를 사용하여 데이터 레이크 데이터를 탐색적으로 분석할 수 있습니다. | 다이어그램 | 다이어그램 |  |  | Experience Platform Query Service 및 BI 도구 통합 |  | 1 | 3 | CJA 전용 이 아닌 쿼리 서비스를 다룹니다. CJA 폴더에 잘못 배치될 수 있습니다. experience-platform/으로 재배치되는 것이 좋습니다. 강력한 설계 대상(PostgreSQL, BI 도구). |
| help/blueprints/customer-journeys/overview.md | 고객 여정 블루프린트 | 최신 마케팅 플랫폼은 여정 전반에 걸쳐 이벤트 기반 캠페인 및 브랜드 주도 캠페인을 지원합니다. | 탐색 | 탐색 |  |  |  |  |  |  | 재정의 1: overview.md. 여정 하위 범주에 대한 TOC. Journey Optimizer 및 Campaign 위치 지정에 대해 설명합니다. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md | Journey Optimizer 블루프린트 | 채널 전반의 이벤트 기반 1:1 프로필 오케스트레이션 및 대상 기반 브랜드 커뮤니케이션. | 탐색 | 탐색 |  |  |  |  |  |  | 재정의 1: overview.md. 사용 사례 탭 및 통합 패턴이 있는 랜딩 페이지. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-journeys.md | Journey Optimizer - 트리거된 메시징 및 Adobe Experience Platform 블루프린트 | 실시간 이벤트 기반 워크플로우는 고객 행동을 기반으로 개인화된 다단계 경험을 제공합니다. | 패턴 | 복제 |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md | 4 | 2 | 주의해서 2를 재정의: 에이전트가 중복될 수 있지만 불확정으로 플래그가 지정되었습니다. 축소하기 전에 범위 정렬을 확인하십시오. 아키텍처 고려 사항은 고유할 수 있으며(프로필 신선도, 세그먼트 자격 타이밍) 다이어그램에 보존할 가치가 있을 수 있습니다. |
| help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-campaigns.md | Journey Optimizer - Campaign 오케스트레이션 | 아웃바운드 채널 간 예약된 대상 기반 다단계 통신(이메일, SMS, 푸시, DM). | 패턴 | 복제 |  |  |  | help/blueprints/use-case-patterns/campaign-management-orchestration/batch-outbound-message-activation.md | 3 | 2 | 재정의 2: 동일한 패턴. 여러 아키텍처 다이어그램. 다이어그램으로 유지 고유 컨텐츠: 관계형 데이터베이스/대상 포털/스키니 프로필 아키텍처 세부 정보. |
| help/blueprints/customer-journeys/journey-optimizer/3rd-party-messaging.md | Journey Optimizer - 서드파티 메시지 블루프린트 | Journey Optimizer과 서드파티 메시징 시스템의 통합 기능을 보여 줍니다. | 혼합 | 분할 | campaign-management-오케스트레이션 | Journey Optimizer과 서드파티 메시징 통합 | 타사 메시징 아키텍처 |  | 2 | 2 | 동점→ 나뉜다 다이어그램(시스템 간 토폴로지) + 패턴 콘텐츠(구현 단계, 통합 제한: 전달자 인증, 정적 IP 없음, 속도 제한). 둘 다 보존할 가치가 있어. |
| help/blueprints/customer-journeys/decision-management/decision-management-overview.md | 의사 결정 관리 블루프린트 | 중앙 집중식 오퍼 라이브러리 및 의사 결정 엔진을 통해 고객 여정 전반에 개인화된 오퍼를 제공합니다. | 탐색 | 탐색 |  |  |  |  |  |  | 재정의 1: overview.md. 의사 결정 관리 구성 요소 및 Edge와 허브 배포 접근 방식에 대해 설명합니다. |
| help/blueprints/customer-journeys/decision-management/decision-management-edge.md | Edge의 의사 결정 관리 블루프린트 | Edge Network에서 1초 미만의 지연 시간을 두고 실시간 웹 및 모바일 경험에서 개인화된 오퍼를 제공합니다. | 혼합 | 복제 |  |  |  | help/blueprints/use-case-patterns/personalization/offer-decisioning.md | 2 | 3 | 재정의 2: offer-decisioning에 매핑합니다. Edge 배포 변형 - 허브 블루프린트와 함께 단일 배포 옵션 다이어그램으로 통합하는 것이 좋습니다. |
| help/blueprints/customer-journeys/decision-management/decision-management-hub.md | 허브의 의사 결정 관리 블루프린트 | 키오스크, 에이전트 지원 경험 및 아웃바운드 게재를 포함한 채널 간에 개인화된 오퍼를 제공합니다. | 혼합 | 복제 |  |  |  | help/blueprints/use-case-patterns/personalization/offer-decisioning.md | 2 | 3 | 재정의 2: offer-decisioning에 매핑합니다. 허브 배포 변형 — Edge Blueprint를 단일 배포 옵션 다이어그램에 통합하는 것이 좋습니다. |
| help/blueprints/customer-journeys/campaign-v8/campaign-v8-overview.md | Campaign v8 블루프린트, Campaign 및 플랫폼 | ETL, 세그먼테이션 및 트랜잭션 메시지 기능을 갖춘 차세대 일괄 캠페인 관리 플랫폼입니다. | 패턴 | 패턴 | campaign-management-오케스트레이션 | Campaign v8 일괄 오케스트레이션 및 트랜잭션 메시지 | Campaign v8 아키텍처 배포 모델 |  | 4 | 3 | 고유한 기술 접근 방식(AJO이 아닌 Campaign v8 기본 제공). 여러 아키텍처 다이어그램, 비즈니스 프레임, KPI는 가드레일에 포함됨(20M msg/hr 배치, 1M/hr 실시간). 기존 패턴 카탈로그에 해당하는 항목이 없습니다. 참고: 점수도 분할로 간주됩니다. 패턴을 제안하지만 작성자는 다이어그램을 유지할 수 있습니다. |
| help/blueprints/customer-journeys/campaign-v8/rtcdp-and-campaign-v8.md | Real-Time CDP와 Adobe Campaign v8 통합 패턴 | 개인화된 대화를 위해 RTCDP 대상 및 Campaign v8과의 프로필 통합을 소개합니다. | 다이어그램 | 다이어그램 |  |  | RTCDP - Campaign v8 대상자 및 프로필 교환 |  | 1 | 2 | 독립형 사용 사례가 아닌 통합 커넥터 블루프린트입니다. 다이어그램 + 간단한 사전 요구 사항/보호. 설계 중심. |
| help/blueprints/customer-journeys/campaign-v8/ajo-and-campaign-v8.md | Journey Optimizer와 Adobe Campaign v8 블루프린트 | 1:1 경험을 위한 Campaign v8 트랜잭션 메시징과 함께 AJO 오케스트레이션을 보여 줍니다. | 다이어그램 | 다이어그램 |  |  | Journey Optimizer - Campaign v8 트랜잭션 메시지 통합 |  | 1 | 2 | 통합 커넥터. 다이어그램 + 구현 단계 + 기술 제한(4,000msg/5분 스로틀, 이벤트 시작 전용). AJO 및 Campaign v8 패턴에 대한 상호 링크. |
| help/blueprints/customer-journeys/campaign-v7/campaign-v7-overview.md | Campaign v7 블루프린트 | 더 이상 사용되지 않는 기능: 배치 기반 메시징, 온보딩, 리마케팅, DM, 간단한 트랜잭션 메시지. | 탐색 | 탐색 |  |  |  |  |  |  | 더 이상 사용되지 않는 제품(v8에 대한 프론트메터 링크). 최소 콘텐츠(아키텍처 다이어그램만 해당). 마이그레이션하지 마십시오. |
| help/blueprints/customer-journeys/campaign-v7/rtcdp-and-campaign-v7.md | Real-Time CDP과 Campaign v7 및 Campaign Standard 통합 패턴 | 개인화된 대화를 위해 RTCDP 및 Campaign v7/Standard와 실시간 고객 프로필을 통합하는 방법을 소개합니다. | 다이어그램 | 다이어그램 |  |  | RTCDP - Campaign v7/Standard 대상자 및 프로필 교환 |  | 1 | 2 | 사용하지 않음. 통합 커넥터. 다이어그램 + 포괄적인 구현 단계. 새로운 패턴으로 마이그레이션하지 말고 그대로 두십시오. |
| help/blueprints/customer-journeys/campaign-v7/ajo-and-campaign-v7.md | Journey Optimizer와 Adobe Campaign v7 블루프린트 | 1:1 경험을 위한 Campaign v7 트랜잭션 메시지와 함께 AJO 오케스트레이션을 보여 줍니다. | 다이어그램 | 다이어그램 |  |  | Journey Optimizer - Campaign v7 트랜잭션 메시지 통합 |  | 1 | 2 | 사용하지 않음. 통합 커넥터. 다이어그램 + 구현 단계 + 제한. 이주하지 말고 그대로 두어라. |
