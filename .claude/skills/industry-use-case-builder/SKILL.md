---
name: industry-use-case-builder
description: Adobe Experience Platform 블루프린트 저장소의 새로운 산업 사용 사례 만들기 안내서입니다. 이 기술은 업계 카테고리(소매, 자동차, 헬스케어, 금융 서비스, 보험, 미디어 및 엔터테인먼트, 통신, 여행 및 접대, B2B)에 새 사용 사례를 추가하거나, 사용자가 업계 페이지에 비즈니스 시나리오를 추가하려는 경우 또는 사용 사례 카탈로그를 업데이트할 때 사용합니다. 전체 워크플로를 처리합니다. 사용 사례 세부 정보 수집, 성숙도 수준 평가, 콘텐츠 생성, 업계 개요 페이지 및 사용 사례 카탈로그 업데이트, 아이콘 생성을 위한 사용 사례 아이콘 생성기 기술 호출.
source-git-commit: ed8928687806b619e95d8d320478d27c13722a80
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 1%

---


# 업계 사용 사례 빌더

이 스킬은 Adobe Experience Platform 블루프린트 저장소의 새로운 업계 사용 사례를 만드는 데 도움이 됩니다. 각 단계를 순차적으로 수행합니다. 시작하기 전에 참조 파일을 읽습니다.

- `references/use-case-template.md` — 사용 사례 섹션의 정확한 템플릿
- `references/catalog-row-template.md` — 카탈로그 테이블 행의 정확한 형식
- `references/maturity-criteria.md` — 완성도 평가를 위한 세부 지침

## 1단계: 정보 수집

콘텐츠를 생성하기 전에 사용자를 인터뷰하여 필요한 모든 세부 정보를 수집합니다.

### 필수 필드

1. **수직 시장** — 다음 중 하나여야 합니다.
   - 자동차
   - b2b
   - 금융 서비스
   - 헬스케어
   - 보험
   - 미디어 엔터테인먼트
   - 소매
   - 전기 통신
   - 여행 접대

2. **사용 사례 이름** — 명확하고 설명적인 제목(예: &quot;포기한 장바구니 전자 메일 복구&quot;, &quot;의약품 준수 캠페인&quot;).

3. **설명** — 비즈니스 시나리오와 중요한 이유를 설명하는 1~2개의 문장입니다.

4. **비즈니스 영향** — 특정 지표(예: &quot;클릭스루 비율 20~30% 증가&quot;, &quot;리필 비율 15~25% 향상&quot;)로 정량화된 결과.

5. **사용 사례 패턴** — 다음 기존 패턴 중 정확히 하나에 매핑해야 합니다.
   - 대상으로 Audience Activation
   - 세그먼트가 일치하는 Audience Collaboration
   - 이벤트 전달
   - B2B Audience Activation
   - 익명 방문자 웹 Personalization
   - 알려진 방문자 웹/앱 Personalization
   - Offer Decisioning
   - 행동 추천
   - 일괄 아웃바운드 메시지 활성화
   - 이벤트 트리거된 메시징
   - 여러 단계로 조정된 여정
   - Decisioning을 사용한 크로스 채널 여정
   - 구매 그룹 기반 마케팅 및 여정 관리
   - Customer Analytics &amp; Insight 세대
   - B2B 분석
   - Brand Concierge 대화 경험

6. **기술 고려 사항** — 데이터 요구 사항, 통합, 규정/규정 준수 요구 사항, 성능 고려 사항 및 아키텍처 정보를 다루는 4~8개 항목입니다.

계속하기 전에 누락된 필드를 요청하십시오. 세부 사항을 가정하거나 조작하지 마십시오.

## 2단계: 성숙도 평가

전체 루브릭을 보려면 `references/maturity-criteria.md`을(를) 읽으십시오. 다음 세 가지 완성도 레벨 중 하나를 지정합니다.

- **기본** `[!BADGE Foundational]{type=Neutral}` — 단일 단계 또는 이벤트 트리거 패턴(이벤트 트리거 메시징, 일괄 아웃바운드), 간단한 데이터 요구 사항, 최소 AI/ML, 표준 통합.
- **새로 만들기** `[!BADGE Emerging]{type=Informative}` — 여러 단계 여정, 행동 데이터, 권장 사항 모델, 알려진 방문자 개인화, 중간 수준의 통합 복잡성.
- **고급** `[!BADGE Advanced]{type=Caution}` — 크로스 채널 의사 결정, AI 기반 예측, 오퍼 의사 결정, 복잡한 오케스트레이션, 여러 시스템 통합.

### 평가 워크플로우

1. 사용 사례가 매핑되는 사용 사례 패턴을 식별합니다.
2. 빠른 일치를 위해 완성도 기준의 &quot;일반적인 패턴&quot; 목록을 확인하십시오.
3. 패턴이 성숙도를 명확하게 나타내지 않는 경우 데이터 복잡성, AI/ML 요구 사항 및 통합 범위를 평가합니다.
4. &quot;패턴 매핑({pattern}) 및 {key factors}을(를) 기반으로 {reasoning}(으)로 인해 {level}(으)로 분류하겠습니다.&quot;
5. 콘텐츠 생성으로 진행하기 전에 사용자가 확인하거나 재정의할 때까지 기다립니다.

## 3단계: 컨텐츠 생성

두 개의 파일에서 콘텐츠를 생성하거나 업데이트합니다.

### A. 업계 개요 파일

**파일 경로:** `/help/blueprints/industry-use-cases/{industry}/{industry}-overview.md`

현재 구조 및 콘텐츠를 이해하려면 먼저 기존 파일을 읽으십시오. `references/use-case-template.md`의 정확한 템플릿 다음에 새 섹션을 추가하십시오.

```markdown
## {Use Case Title}

{1-2 sentence description of the business scenario and why it matters}

### Business impact

{Quantified business outcomes, e.g., "Retailers typically see a 20-30% increase in click-through rates..."}

### How to implement

Use the [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) pattern. {1-2 sentence explanation of why this pattern applies}

### Technical considerations

- {4-8 bullet points covering data integration, regulatory, performance, or architectural considerations}
```

일관된 서식을 유지하면서 새 섹션을 기존 사용 사례 섹션 뒤에 배치합니다.

### B. 사용 사례 카탈로그

**파일 경로:** `/help/blueprints/industry-use-cases/use-case-catalog.md`

먼저 기존 카탈로그 파일을 읽습니다. 올바른 업계 탭에 새 행을 추가합니다. 카탈로그에서는 `>[!TAB {Industry}]`개의 표식이 있는 탭 구조를 사용합니다. 각 탭에는 다음 열이 포함된 테이블이 있습니다.

| 열 | 콘텐츠 |
| --- | --- |
| 아이콘 | `<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">`(아직 아이콘이 없으면 비워 둠) |
| 사용 사례 | `[{Use Case Title}]({industry}/{industry}-overview.md#{anchor})` 여기서 anchor는 kebab의 머리글입니다. |
| 설명 | 한 문장 요약 |
| 완성도 | 할당된 수준에 대한 배지 구문 |
| 패턴 | `[{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md)` |

**배치 규칙:** 각 산업 탭 내에서 행은 기본, 새로 만들기, 고급 순서로 완성도별로 그룹화됩니다. 올바른 완성도 그룹의 끝에 새 행을 배치합니다.

패턴 파일 경로:
- `audience-building-activation/audience-activation-to-destinations.md`
- `audience-building-activation/audience-collaboration-segment-match.md`
- `audience-building-activation/event-forwarding.md`
- `audience-building-activation/b2b-audience-activation.md`
- `personalization/anonymous-visitor-web-personalization.md`
- `personalization/known-visitor-web-app-personalization.md`
- `personalization/offer-decisioning.md`
- `personalization/behavioral-recommendation.md`
- `campaign-management-orchestration/batch-outbound-message-activation.md`
- `campaign-management-orchestration/event-triggered-messaging.md`
- `campaign-management-orchestration/multi-step-orchestrated-journey.md`
- `campaign-management-orchestration/cross-channel-journey-with-decisioning.md`
- `campaign-management-orchestration/buying-group-based-marketing.md`
- `analysis/customer-analytics-insight-generation.md`
- `analysis/b2b-analytics.md`
- `conversational-experience/brand-concierge-conversational-experience.md`

## 4단계: 아이콘 생성

콘텐츠가 만들어지면 `use-case-icon-generator` 스킬을 호출하여 새 사용 사례에 대한 아이콘 사양을 생성합니다. 다음과 같은 방법으로 스킬을 제공합니다.
- 사용 사례 이름
- 업계 카테고리
- 사용 사례에 대한 간략한 설명

사용자가 아이콘 파일을 생성했으면 아이콘 참조를 포함하도록 카탈로그 행을 업데이트합니다.

```
<img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40">
```

## 5단계: 유효성 검사

완료하기 전에 다음을 모두 확인하십시오.

1. **템플릿 준수** - 업계 개요 섹션은 템플릿을 정확하게 따릅니다(제목#, 설명, 비즈니스 영향 ###, 구현 방법, 기술 고려 사항 ###).
2. **카탈로그 배치** — 카탈로그 행이 올바른 산업 탭과 올바른 완성도 그룹(기본, 새로 만들기, 고급)에 있습니다.
3. **패턴 링크 유효성** — 개요 및 카탈로그의 패턴 링크가 위 목록의 유효한 패턴 파일 경로를 사용합니다.
4. **앵커 일관성** — 카탈로그 링크(예: `#abandoned-cart-email-recovery`)의 앵커는 kebab-case로 변환된 개요 파일의 `##` 머리글과 일치합니다.
5. **아이콘 경로 규칙** — 아이콘 경로가 `assets/use-case-icons/{industry}/icon-{kebab-name}.png`을(를) 따릅니다.

유효성 검사 중에 발견된 문제를 보고하고 완료하기 전에 수정하십시오.
