---
source-git-commit: 7511cc0e5c099d5d3ee1275a374cd9ffdc972335
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---
# 블루프린트 평가 지침

이 규칙은 &quot;아키텍처 다이어그램 및 블루프린트&quot; 섹션의 모든 문서에 적용됩니다.
[TOC.md](../help/blueprints/TOC.md)(76-133행) 중 하나를 선택하여 각 블루프린트가
**사용 사례 패턴**, **아키텍처 다이어그램**, 둘 다(**분할**) 또는 다음으로 플래그가 지정됨
기존 패턴의 **복제**.

이 규칙을 적용한 출력은 [blueprint-audit.md](blueprint-audit.md)입니다.

## 정의

- **사용 사례 패턴** — 특정 비즈니스 또는 기술 목표를 설명하는 문서 및
해당 목표를 달성하기 위한 가능한 구현 접근 방식 및 고려 사항의 개요를 제공합니다.
정식 셰이프: `.claude/skills/use-case-pattern-builder/references/pattern-template.md`.
- **아키텍처 다이어그램** — 시스템의 기능을 나타내는 비주얼 다이어그램입니다.
통합 및 데이터 흐름. 최소한의 이야기, 도표는 인공물이다.
정식 예: [platform-data-flow.md](../help/blueprints/experience-platform/platform-data-flow.md).

## 채점

각 블루프린트는 처음부터 끝까지 읽으며 8개의 이진 신호에 대해 채점됩니다. 각 신호가 기여함
+1 - 패턴 점수 또는 다이어그램 점수

### 패턴 신호(각각 = +1 패턴)

1. **비즈니스 목표 프레임** — 프레임 수익, 보존, 획득, 리드 생성, 비용
절감, 고객 경험 또는 유사한 비즈니스 성과
2. **KPI 또는 성공 지표** — 지표, 전환율, 일치율, ROI 또는
비슷한 결과 측정.
3. **여러 구현 옵션 또는 완성도 계층** — 옵션 A/옵션 B, 기본 및
독자가 선택하는 고급 또는 비교 가능한 대안.
4. **사전 요구 사항 또는 준비 체크리스트** - 구현하기 전에 준비해야 할 사항을 나열합니다.
5. **Narrative 구현 단계 > ~30줄** — 실질적인 구현 방법 지침이지, 아님
간단한 개요입니다.

### 다이어그램 신호(각각 = +1 다이어그램)

6. 시스템 토폴로지를 표시하는 **아키텍처/데이터 흐름 이미지 있음** — `.svg`, `.png` 또는 `.jpg`,
데이터 흐름 또는 통합 화살표.
7. **시스템 간 통합 토폴로지, 배포 셰이프 또는 보호 기능** — 방법을 설명합니다.
구성 요소는 연결되는데, 여기서 데이터가 전달됩니다. 배포 모델(edge와 hub) 또는 용량 제한이 있습니다.
8. **대상자는 솔루션 설계자입니다** - 프레이밍에서 배포, SDK, Edge, Hub 또는 이와 유사한 기능을 사용합니다.
마케터 중심의 프레임화(캠페인, 여정,
audiences).

## 권장 사항 논리

우선 재정의 규칙을 적용합니다. 재정의가 실행되지 않는 경우 점수에서 권장 사항을 파생합니다.

### 규칙 재정의(가장 높은 우선 순위)

1. **파일 이름이`overview.md`**→(는) 권장 사항 = `Navigation`입니다. 마이그레이션에서 제외됨,
페이지는 하위 파일이 확정된 후 수정되는 목차 스타일 랜딩 페이지입니다.
2. **동등한 패턴이`help/blueprints/use-case-patterns/`**에 이미 →
권장 사항 = `Duplicate`. 마이그레이션 작업은 블루프린트를 순수한 로 단순화하는 것입니다.
아키텍처 다이어그램을 만들고 기존 패턴에 &quot;사용 사례 패턴 보기&quot; 크로스링크를 추가합니다.
`duplicate_of` 열에 기존 패턴 경로를 기록하십시오.
3. **파일이 `experience-platform/`에 있으며 비즈니스 목표 신호(#1)가 없습니다.** 기본적→
   다른 점수에 관계없이 `Diagram`입니다. 이 폴더는 아키텍처 개요 계층입니다.

### 점수 기반 권장 사항(재정의 실행이 없는 경우)

| 패턴 점수 | 다이어그램 점수 | 추천 | 추론 |
| --- | --- | --- | --- |
| ≥ 3 | ≤ 1 | `Pattern` | 강한 패턴 신호, 약한 다이어그램 신호→ 패턴으로 이동합니다. |
| ≤ 1 | ≥ 2 | `Diagram` | 약한 패턴 신호, 우세한 시각적/토폴로지 포커스가 다이어그램으로 →. |
| ≥ 3 | ≥ 2 | `Split` | 풍부한 패턴 컨텐츠와 의미 있는 다이어그램→ 모두 패턴을 추출하고, 원본을 다이어그램으로 줄이며, 교차 링크합니다. |
| 2 | 2 | `Split` | 중간 정도의 강도로 →. |
| 2 | ≤ 1 | `Pattern` | 패턴 기울이기, 유의한 다이어그램 값 없음. |
| ≤ 1 | ≤ 1 | `Diagram` | 전체적으로 얇음 — 기존의 최소 아키텍처 페이지일 수 있습니다. |

## 지침 적용 방법

범위의 각 블루프린트 Markdown 파일에 대해:

1. 전체 파일을 처음부터 끝까지 읽습니다.
2. 8개의 신호 각각 존재/부재를 표시하십시오.
3. 우선 적용 규칙을 순서대로 적용합니다. 하나라도 문제가 발생하면 그렇게 하는 것이 좋습니다.
4. 그렇지 않으면 패턴 점수 및 다이어그램 점수를 계산하고 권장 사항을 조회합니다.
5. `Pattern` 및 `Split` 권장 사항에 대해 다음을 제안합니다.
   - `proposed_pattern_category` — 다음 중 하나:
     `audience-building-activation`, `personalization`, `campaign-management-orchestration`,
     `analysis`, `conversational-experience` 또는 `(new) <name>` 레이블이 지정된 새 범주.
   - `proposed_pattern_title` — 기존 패턴을 따르는 짧은 작업 지향 제목
이름 지정 스타일입니다.
6. `Diagram` 및 `Split` 권장 사항에 대해 다음을 제안합니다.
   - `proposed_diagram_title` — 일반적으로 비즈니스 프레이밍의 기존 제목을 트리밍합니다.
7. 블루프린트의 범위를 기존 패턴 카탈로그와 비교하여 발견된 모든 중복 항목을 캡처합니다.
`duplicate_of`에 있습니다.
8. 진행 중인 질문, 보존할 가치가 있는 고유한 기술 콘텐츠 또는 마이그레이션 위험을 `notes`에 기록하십시오.

## 기존 사용 사례 패턴 카탈로그(중복 감지용)

| 카테고리 | 패턴 |
| --- | --- |
| 대상자 구축 활성화 | audience-activation-to-destinations, audience-collaboration-segment-match, b2b-audience-activation, 이벤트 전달 |
| 개인화 | anonymous-visitor-web-personalization, known-visitor-web-app-personalization, offer-decisioning, behavior-recommendation |
| campaign-management-오케스트레이션 | 일괄 아웃바운드 메시지 활성화, 이벤트 트리거 메시징, 다단계 오케스트레이션된 여정, 크로스 채널 여정 - 의사 결정, 구매 그룹 기반 마케팅 |
| 분석 | customer-analytics-insight-generation, b2b-analytics |
| 대화경험 | 브랜드 컨시어지 대화 경험 |
