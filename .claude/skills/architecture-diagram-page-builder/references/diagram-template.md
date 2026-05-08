---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---
# 아키텍처 다이어그램 페이지 템플릿

아키텍처 다이어그램 페이지에 대한 전체 Markdown 템플릿입니다. 모든 `{placeholder}`을(를) 스킬 워크플로의 1단계 동안 수집된 값으로 바꿉니다. 적용되지 않는 선택적 섹션(예: `>[!MORELIKETHIS]` 블록)을 제거합니다. 생성된 파일에 빈 자리 표시자를 남기지 마십시오.

---

```markdown
---
title: {Page title}
description: {1-2 sentence page purpose, used for search snippets and previews}
solution: {Comma-separated Adobe solutions, e.g. Experience Platform, Journey Optimizer, Customer Journey Analytics}
---
# {Page title}

{Opening paragraph -- 1-2 sentences describing what the diagrams collectively illustrate. Frame the page as a top-level architecture reference, not a use case walkthrough.}

>[!MORELIKETHIS]
>
>[{Related-content link text}]({Related-content URL}).

## {Diagram 1 section title}

{1-2 sentence explanation of what the diagram shows and why it matters.}

<img src="assets/{filename-1}" alt="{Alt text for diagram 1}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## {Diagram 2 section title}

{1-2 sentence explanation.}

<img src="assets/{filename-2}" alt="{Alt text for diagram 2}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## Primary data flows and integration points

- {Flow or integration 1 -- e.g., "Real-time event ingestion from [!DNL Web SDK] to [!DNL Edge Network]"}
- {Flow or integration 2 -- e.g., "Profile sync between [!DNL Experience Platform] Hub and Edge"}
- {Flow or integration 3}
- {Flow or integration 4}
- {Flow or integration 5}

## Use case patterns supported

The architecture above supports the following use case patterns:

- [{Pattern 1 name}](/help/blueprints/use-case-patterns/{category}/{pattern-1-file}.md) -- {1-line note on why this architecture enables the pattern}
- [{Pattern 2 name}](/help/blueprints/use-case-patterns/{category}/{pattern-2-file}.md) -- {1-line note}
- [{Pattern 3 name}](/help/blueprints/use-case-patterns/{category}/{pattern-3-file}.md) -- {1-line note}

## Further reading

- [{Article 1 title}]({Experience League URL 1})
- [{Article 2 title}]({Experience League URL 2})
- [{Article 3 title}]({Experience League URL 3})
```

---

## Frontmatter 규칙

- **필수 필드:** `title`, `description`, `solution`.
- **금지된 필드**(게시 시 자동 할당): `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt`, `thumbnail`. 새로 작성된 파일에는 이러한 파일을 포함하지 마십시오.

## 본문 규칙

- **한 개의 H1** — 페이지 제목. `title` Frontmatter와 정확히 일치합니다.
- **다이어그램당 1개의 H2.** 도표 구역 안에서는 H3를 사용하지 말고, 1-2 문장 인트로와 이미지에 맞추어라.
- **`<img>`포함** — 인라인 스타일과 `class="modal-image"`이(가) 필요합니다. Experience League 모달-확대/축소 상호 작용을 촉진합니다.
- **이미지 경로** — 항상 `assets/{filename}`(페이지의 주제 폴더를 기준으로 함). 절대 경로를 사용하지 마십시오.
- **Adobe 제품 이름** — 본문 텍스트와 글머리 기호로 `[!DNL ...]`을(를) 래핑합니다. 예: `[!DNL Real-Time CDP]`, `[!DNL Journey Optimizer]`, `[!DNL Experience Platform]`
- **사용 사례 패턴 링크** — 항상 절대 `/help/blueprints/use-case-patterns/{category}/{file}.md` 양식을 사용하므로 링크가 이 콘텐츠를 포함할 수 있는 모든 페이지에서 확인됩니다.
- **Experience League 링크** — `https://experienceleague.adobe.com/`(으)로 시작하는 절대 URL입니다. 현지화된 변형보다 표준 문서 URL을 선호합니다.

## 섹션 순서 지정

독자가 예측 가능한 방식으로 스캔할 수 있도록 모든 아키텍처 페이지에서 순서를 일관되게 유지합니다.

1. 프론트메터
2. H1 + 단락 열기
3. (선택 사항) `>[!MORELIKETHIS]` 설명선
4. 다이어그램당 H2 1개(사용자 지정 순서로)
5. `## Use case patterns supported`
6. `## Primary data flows and integration points`
7. `## Further reading`

## 길이 예상

Markdown의 40-100줄이 대표적입니다. 페이지가 150줄을 초과하는 경우 콘텐츠가 사용 사례 패턴 영역으로 이동되었을 수 있습니다. `scope-guardrails.md`을(를) 다시 확인하고 분할을 고려하십시오.
