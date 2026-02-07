---
name: blueprint-document-reference
description: Adobe Digital Experience Blueprint 문서 생성 및 편집에 대한 참조입니다. 새 블루프린트를 만들거나 블루프린트 페이지를 추가하거나 사용자가 블루프린트 구조, 섹션, 템플릿에 대해 묻거나 Adobe Experience League를 참조할 때 사용합니다.
source-git-commit: dfa21942ecf2a1db06df6f6cc945f5572811ca93
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---


# 블루프린트 문서 참조

이 저장소에서 블루프린트 문서를 만들거나 편집할 때 이 기술을 사용하십시오. 블루프린트는 기존 비즈니스 문제를 해결하고 아키텍처 다이어그램, 기술 고려 사항 및 Adobe Experience League 설명서에 대한 링크를 포함하는 반복 가능한 구현입니다.

## 적용 시기

- 새 블루프린트 문서 또는 블루프린트 개요 페이지 만들기
- 기존 블루프린트에서 섹션 추가 또는 재구성
- Adobe Experience League 설명서에 연결하거나 인용하기
- 블루프린트 규칙에 새 콘텐츠 정렬(프론트메터, 제목, 다이어그램)

## 빠른 참조

1. **문서 목적**: 블루프린트는 Adobe Experience Platform과 응용 프로그램의 통합 방법을 보여 주는 시스템 및 데이터 흐름 아키텍처를 제공합니다. 시각적이고 기술적인 것이지 마케팅이 아니다.
2. **섹션**: 템플릿의 표준 섹션을 사용하십시오. 해당하는 경우에만 생략하십시오([reference.md](reference.md) 참조).
3. **Experience League**: 제품 문서, API, 보호 및 자습서를 위해 Experience League에 연결하는 것이 좋습니다. 전체 URL을 사용하십시오. URL 패턴 및 서식은 [reference.md](reference.md)을(를) 참조하십시오.
4. **저장소 구조**: 블루프린트가 `help/blueprints/` 아래에 있습니다. 블루프린트 페이지를 추가하거나 이동할 때 `help/blueprints/TOC.md`을(를) 업데이트합니다.

## 문서 템플릿

모든 블루프린트 페이지는 이 구조를 따라야 합니다. 적용되는 섹션만 포함합니다.

```markdown
---
title: [Short descriptive title]
description: "[One sentence: what this blueprint shows and why it matters.]"
solution: [Product name, e.g. Real-Time Customer Data Platform, Journey Optimizer]
exl-id: [UUID - leave blank if new, this will be auto-generated as part of the Experience League publishing flow]
---
# [H1 - same as title or expanded]

[1–3 paragraphs: what the blueprint covers, key capabilities, and who it’s for.]

## Applications

* [Product 1]
* [Product 2]

## Use cases

* [Use case 1]
* [Use case 2]

## Prerequisites

[Bullets or short paragraphs: required products, config, or setup.]

## Architecture Diagram

<img src="[path to SVG/image]" alt="[Descriptive alt]" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## Guardrails

[Link to Experience League guardrails and any blueprint-specific limits.]

## Implementation patterns

[Optional: named patterns with bullets.]

## Implementation steps

1. [Step with link to Experience League where relevant]
2. ...

## Implementation considerations

[Optional: identity, performance, security, etc.]

## Related documentation

[Grouped links to Experience League: product docs, APIs, tutorials.]
```

개요 또는 허브 페이지의 경우 소개, 사용 사례(또는 탭), 아키텍처 이미지, 시나리오/패턴 테이블, 사전 요구 사항, 보호 기능, 관련 문서 등의 더 짧은 구조를 사용합니다. 예제는 `help/blueprints/`의 기존 개요를 참조하십시오.

## 프론트메터

| 필드 | 필수 | 참고 사항 |
|-------|----------|--------|
| `title` | 예 | 짧음. Adobe 스타일에 대한 제품 이름에 `[!DNL Product Name]`을(를) 사용합니다. |
| `description` | 예 | 한 문장, 검색 및 카드에 사용 |
| `solution` | 예 | 기본 제품(예: Real-Time Customer Data Platform, Journey Optimizer) |
| `exl-id` | 예 | UUID; 새 페이지를 보려면 비워 둡니다. |
| `doc-type` | 개요 | 기본 블루프린트 개요 페이지에 `overview-page` 사용 |
| `kt` | 선택 사항 | 기술 자료 문서 ID(연결된 경우) |

## Adobe Experience League 참조

- **연결할 시기**: 제품 설명서, API 참조, 보호 기능, 자습서 및 구성 단계를 위한 Experience League에 연결합니다. 긴 절차를 복제하지 마십시오. 요약 및 링크하십시오.
- **URL 형식**: 전체 URL을 사용합니다. `https://experienceleague.adobe.com/docs/...` 또는 `https://experienceleague.adobe.com/en/docs/...`을(를) 선호합니다. 개발자 문서의 경우 `https://developer.adobe.com/...`도 유효합니다.
- **링크 텍스트**: 설명 텍스트를 사용하십시오(예: &quot;여기를 클릭&quot;하지 않고 &quot;[스키마 만들기] (url)&quot;). 링크 텍스트의 제품 이름은 필요한 경우 `[!DNL Product Name]`을(를) 사용하십시오.
- **관련 설명서 섹션**: 범주(예: 대상 구성, SDK 설명서, 프로필 및 세그멘테이션, 튜토리얼)별로 링크를 그룹화하는 &quot;관련 설명서&quot; 섹션으로 블루프린트를 종료합니다.

자세한 URL 패턴, 링크 그룹화 및 예제는 [reference.md](reference.md)을(를) 참조하십시오.

## 제출 전 체크리스트

- [ ] Frontmatter에 `title`, `description`, `solution`, `exl-id`이(가) 있습니다.
- [ ]개의 H1이 제목과 일치하거나 적절히 확장합니다.
- [ ] 아키텍처 다이어그램이 있고 대체 텍스트가 설명적입니다.
- [ ] 구현 단계는 프로시저가 있는 Experience League에 연결됩니다.
- [ ] 보호 섹션 링크를 통해 공식 Experience League 보호 문서 연결
- [ ] 관련 설명서 섹션에는 관련 Experience League 링크가 포함되어 있습니다.
- [ ]개의 새 페이지 또는 이동된 페이지가 `help/blueprints/TOC.md`에 반영됩니다.

## 추가 리소스

- 전체 템플릿 및 섹션 메모: [reference.md](reference.md)
- 기존 블루프린트: `help/blueprints/`(예: `audience-activation/real-time-lookup.md`, `customer-journeys/journey-optimizer/journey-optimizer-overview.md`)
- 목차 및 탐색: `help/blueprints/TOC.md`
