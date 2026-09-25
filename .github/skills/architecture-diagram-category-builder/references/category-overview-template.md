---
source-git-commit: e0ecfa4d74b8fcc0bbaf35d44c33c725a1b1a539
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%
---
# 카테고리 개요.md 템플릿

`help/blueprints/architecture-diagrams/`의 모든 범주 폴더에는 다른 5개처럼 보이는 `overview.md`이(가) 필요합니다. 이 정확한 구조를 사용합니다.

## 프론트메터

```yaml
---
title: {Category Label}
description: {One-sentence summary of what this category covers.}
solution: {Primary Adobe solution(s), comma-separated}
doc-type: overview-page
---
```

새 페이지에 `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` 또는 `thumbnail`을(를) 포함하지 마십시오. 게시 파이프라인이 자동으로 채웁니다.

## 본문

```markdown
# {Category Label}

{1-3 paragraph intro describing what this category of diagrams covers and why it matters.}

| Diagram | Description |
| --- | --- |
| [{Page title}]({filename}.md) | {One-sentence description of the page} |
| [{Page title}]({filename}.md) | {One-sentence description of the page} |
```

규칙:

- TOC.md에 나타나는 순서대로 카테고리의 모든 페이지를 나열합니다.
- 개요가 형제 페이지와 함께 사용되므로 링크 대상은 상대 파일 이름(`/help/blueprints/...` 접두사가 없음)입니다.
- 설명은 한 문장이며 레이블처럼 읽으면 후행 기간이 필요하지 않습니다.
- 범주에 자연스러운 하위 그룹화가 있는 경우(예: 고객 여정 아래의 &quot;사용되지 않는 다이어그램&quot;) 동일한 형식으로 `## {Sub-group name}` 제목 뒤에 고유한 2열 테이블을 추가하십시오. 다이어그램 썸네일이나 추가 열을 표에 혼합하지 마십시오.
- 이 표에 `<img>` 다이어그램 썸네일을 포함하지 마십시오. `Diagram`(링크) 및 `Description`(텍스트) 두 열로 유지합니다. 썸네일은 카테고리 개요가 아니라 개별 콘텐츠 페이지에 속합니다.
- 표 셀 내부에 중첩된 `<ul><li>` HTML을 사용하지 마십시오. 일반 텍스트만.

## 예(고객 인사이트)

```markdown
---
title: Customer Insights
description: Unify and analyze data and customer behaviors from across the customer journey
solution: Customer Journey Analytics
doc-type: overview-page
---
# Customer Insights

Customer Journey Analytics shows how brands can unify customer data and behavior from various interaction channels and sources to create a journey-based view of all customer interactions.

| Diagram | Description |
| --- | --- |
| [Adobe Customer Journey Analytics](cja.md) | Core Customer Journey Analytics architecture, including B2B and audience-sharing derivations |
| [Adobe Customer Journey Analytics & Adobe Journey Optimizer integration](cja-ajo-integration.md) | Campaign and journey insights integration between Customer Journey Analytics and Journey Optimizer |
```
