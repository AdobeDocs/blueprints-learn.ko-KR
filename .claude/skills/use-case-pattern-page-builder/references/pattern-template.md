---
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 48%

---
# 사용 사례 패턴 템플릿

이 파일에는 사용 사례 패턴 페이지에 대한 전체 Markdown 템플릿이 들어 있습니다. 새 패턴을 생성할 때 모든 `{{placeholder}}` 값을 실제 콘텐츠로 바꾸십시오.

&#x200B;---

## 템플릿

````markdown
---
title: {{Pattern Title}}
description: {{One-sentence description of what this pattern teaches}}
solution: {{Comma-separated Adobe solutions}}
exl-id: {{generate-uuid-placeholder}}
---
# {{Pattern title}}

This guide provides an overview of {{pattern name}} using {{solutions with [!DNL ...] formatting}}. It is designed for solution architects, marketing technologists, and implementation engineers who need to {{primary capability description}}.

## Use case pattern

**{{Pattern Name}}**

{{One-two sentence description of what the pattern does and enables.}}

**Execution plan:** {{Step 1}} > {{Step 2}} > {{Step 3}} > {{Step 4}} > {{Step 5}}

## Use case overview

{{Paragraph 1: Define the pattern. What does it do? How does it differ from related patterns? Provide a clear, specific definition.}}

{{Paragraph 2: Describe the typical trigger or starting condition. When does this pattern apply? What event, schedule, or condition initiates it?}}

{{Paragraph 3: Describe what the pattern delivers. What is the end result for the customer or business? What channels or touchpoints does it affect?}}

{{Paragraph 4: Clarify scope boundaries. What does this pattern NOT cover? What adjacent patterns handle those needs? Reference other patterns by name if relevant.}}

{{Paragraph 5 (optional): Identify typical stakeholders and teams involved in implementation. Who owns what?}}

## Key business objectives

The following business objectives are supported by this use case pattern.

**[{{Objective Name}}](../../business-objectives/{{category}}/{{objective-file}}.md)**

{{Brief description of how this pattern supports the objective -- 1-2 sentences.}}

| KPIs |
| --- |
| {{KPI1}}, {{KPI2}}, {{KPI3}} |

{{Repeat the above block for each supported business objective.}}

## Example tactical use cases

The following scenarios illustrate how {{pattern name}} can be applied across different business contexts.

- **{{Scenario name}}** -- {{Description of the scenario and how it uses this pattern}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
- **{{Scenario name}}** -- {{Description}}
{{Include 6-10 scenarios total}}

## Key performance indicators

| KPI | Description | Measurement |
| --- | --- | --- |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |
| {{KPI Name}} | {{What it measures}} | {{Formula or measurement approach}} |

## Applications

The following Adobe applications are used in this use case pattern.

- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}
- **[!DNL {{Application Name}}] ({{Abbreviation}})** -- {{Description of the application's role in this pattern}}

## Related documentation

The following resources provide additional detail on the capabilities used in this pattern. Group the reference links to primary Experience League documents under descriptive subheadings.

### {{Topic group}}

- [{{Link text}}]({{URL}})
- [{{Link text}}]({{URL}})

### {{Topic group}}

- [{{Link text}}]({{URL}})
- [{{Link text}}]({{URL}})
````

&#x200B;---

## 이 템플릿 사용에 대한 참고 사항

- **YAML 프런트 넷:** `exl-id`은(는) 자리 표시자 UUID(예: `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`)여야 합니다. 게시 파이프라인은 실제 값을 할당합니다.
- **섹션 순서:** `Use case pattern` 섹션은 열기 시작 직후 `Use case overview` 앞에 옵니다. 그것은 독자들에게 선명하고, 한 줄로 된 정의와 높은 수준의 실행 계획을 앞세워 준다.
- **Adobe 제품 이름:** 본문 텍스트와 테이블(예: `[!DNL Journey Optimizer]`)에서 Adobe 제품 이름에 대해 항상 `[!DNL ...]` 구문을 사용하십시오. 제품 이름의 번역을 방지하는 Experience League 규칙입니다.
- **비즈니스 목표 링크:** 패턴 파일에서 비즈니스 목표 디렉터리로의 상대 경로를 사용합니다. `../../business-objectives/{{category}}/{{filename}}.md`.
- **Kebab-case 파일 이름:** 패턴 파일 이름은 패턴 제목에서 파생된 kebab-case여야 합니다. 예: &quot;이벤트가 트리거된 메시징&quot;은 `event-triggered-messaging.md`이(가) 됩니다.
- **실행 계획:** ` > `(공백, 보다 큼, 공백)을 단계 사이의 구분 기호로 사용합니다. 레이블을 정확히 `**Execution plan:**`(으)로 유지합니다.
- **관련 설명서:** 설명 `###` 하위 머리글(예: 응용 프로그램 또는 기능 영역별) 아래에 있는 그룹 참조 링크입니다. 패턴에 사용된 애플리케이션 및 기능에 대한 Experience League 참조입니다.
- **아키텍처(선택 사항):** 참조 아키텍처 다이어그램에서 패턴이 유용한 경우 `Applications`과(와) `Related documentation` 사이에 선택 사항인 `## Architecture` 섹션이 배치될 수 있습니다.
- **범위:** 이 템플릿에서는 자세한 구현 섹션(기본/지원/응용 프로그램 기능, 사전 요구 사항, 구현 옵션 및 단계별 구현 단계)을 의도적으로 제외합니다. 이러한 세부 정보는 `Related documentation`에서 연결된 Experience League 설명서에 있습니다.