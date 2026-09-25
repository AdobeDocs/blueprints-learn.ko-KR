---
name: architecture-diagram-category-builder
description: Adobe Experience Platform 블루프린트 저장소의 아키텍처 다이어그램 및 블루프린트 아래에 있는 새로운 최상위 수준 카테고리(하위 섹션) 생성을 안내합니다. 제안된 아키텍처 다이어그램이 기존 카테고리(아키텍처 개요, 대상 및 프로필 활성화, B2B 활성화 및 마케팅, 고객 인사이트, 고객 여정)에 맞지 않고 새 카테고리가 필요한 경우 이 기술을 사용합니다. 전체 워크플로를 처리합니다. 새 카테고리가 실제로 보장되는지 확인하고 폴더/앵커 명명 규칙을 적용하고, 폴더 구조와 overview.md 랜딩 페이지를 만들고, TOC.md 하위 섹션을 추가하고, 아키텍처-다이어그램 랜딩 페이지 카드 그리드를 업데이트합니다. *기존* 범주에 페이지를 추가하려면 대신 architecture-diagram-page-builder를 사용하십시오.
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%
---

# 아키텍처 다이어그램 범주 빌더

이 스킬은 `/help/blueprints/TOC.md`의 `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` 아래에 새로운 최상위 범주를 만드는 데 도움이 됩니다. 범주는 `customer-insights/` 또는 `b2b-activation-marketing/`과(와) 같은 폴더입니다. 고유한 `overview.md` 랜딩 페이지 및 고유한 목차 하위 섹션이 있는 관련 아키텍처 다이어그램 페이지 그룹입니다.

**드문 작업입니다.** 오늘은 다섯 가지 카테고리가 있습니다. 여섯 번째 추가는 아키텍처 콘텐츠의 새 도메인이 기존 카테고리에 맞지 않을 때만 수행되어야 하며, 기존 카테고리 아래에 페이지를 구성하지 않기 위한 바로 가기로는 불가능합니다.

## 시작하기 전에 읽어야 함

- `./references/naming-conventions.md` — 폴더/앵커/레이블 이름 지정 규칙과 그 이유가 중요합니다. 이 내용을 충분히 읽어보십시오. 범주를 지정해야 하는 방식에 대한 유일한 출처입니다.
- `./references/category-overview-template.md` — 새 범주의 `overview.md`에 필요한 정확한 구조.
- 아직 `../architecture-diagram-page-builder/SKILL.md`을(를) 선택하지 않은 경우 쉼표()도 추가합니다. 범주가 존재하면 해당 스킬을 사용하여 범주의 개별 페이지가 추가됩니다(이 스킬은 아님).

## 1단계: 새 카테고리가 실제로 필요한지 확인

다른 작업을 수행하기 전에 5개의 기존 범주와 해당 범위를 사용자에게 나열합니다.

| 카테고리 | 폴더 | 범위 |
| --- | --- | --- |
| 아키텍처 개요 | `architecture-overviews/` | 최상위 Experience Cloud/Experience Platform 아키텍처, 보호 기능, 배포 SDK |
| 대상자 및 프로필 활성화 | `audience-profile-activation/` | Real-Time CDP, Audience Manager을 통한 대상/프로필 구축 및 활성화 |
| B2B 활성화 및 마케팅 | `b2b-activation-marketing/` | 계정 기반 활성화, 구매 그룹 여정, Marketo/Workfront |
| 고객 인사이트 | `customer-insights/` | Customer Journey Analytics 및 통합 |
| 고객 여정 | `customer-journeys/` | Journey Optimizer, 의사 결정 관리, Campaign v7/v8 |

사용자에게 제안된 콘텐츠가 이들 중 어느 것에도 맞지 않은지 확인하십시오. 일치하는 항목(예: 새 B2B 다이어그램, 새 개인화 다이어그램)은 새로 만드는 대신 해당 기존 범주에 대한 `architecture-diagram-page-builder`(으)로 리디렉션합니다. 사용자가 진정으로 새로운 카테고리가 보증된다고 확인한 경우에만 단계 2로 진행하십시오.

## 2단계: 범주 정보 수집

질문 양식을 사용하여 한 번에 수집합니다.

1. **범주 레이블** — 사람이 읽을 수 있는 전체 목차 레이블(예: 약어가 아닌 &quot;Commerce 아키텍처&quot;). 2-3개의 추천 구문 + &quot;기타&quot;를 제시합니다.
2. **한 문장 설명** — 이 범주가 다루는 내용, 즉 `overview.md` FRONTMATTER 및 LANDPAGE 카드에 대한 설명.
3. **기본 Adobe 솔루션** — `solution` 필드.
4. **초기 페이지** — 사용자가 이미 이 범주에 1개 이상의 페이지를 배치할 준비가 되어 있습니까? 아니면 나중에 수행할 페이지에 대해 범주를 스캐폴딩하고 있습니까?

`./references/naming-conventions.md`의 슬러그 규칙(소문자, 드롭 `&`, 하이픈 넣기, 약어 없음)을 사용하여 범주 레이블에서 폴더 이름과 앵커를 파생합니다. 파생된 폴더/앵커를 사용자에게 표시하고 계속하기 전에 확인합니다. 이 세부 정보는 나중에 수정하기에 많은 비용이 듭니다.

## 3단계: 폴더 구조 만들기

```
help/blueprints/architecture-diagrams/{new-folder}/
help/blueprints/architecture-diagrams/{new-folder}/assets/
help/blueprints/architecture-diagrams/{new-folder}/overview.md
```

`./references/category-overview-template.md`을(를) 사용하여 `overview.md` 생성. 초기 페이지가 준비된 경우 이제 표에 나열합니다. `architecture-diagram-page-builder`을 사용하여 해당 페이지 파일을 직접 생성하십시오. 이 스킬은 개별 다이어그램 페이지가 아닌 범주 스캐폴드와 개요 페이지만 만듭니다. 페이지가 아직 없는 경우 첫 번째 페이지가 추가될 때까지 테이블이 비어 있거나 생략될 수 있습니다. 자리 표시자 행을 인벤터리하는 대신 사용자에게 이 점을 참고하십시오.

`assets/` 폴더는 만들 때 비어 있을 수 있습니다. 이 폴더는 카테고리에 추가된 첫 번째 다이어그램 페이지에 이미지를 넣을 공간이 있도록 존재합니다.

## 4단계: TOC.md 하위 섹션 추가

새 범주를 `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` 아래에 최상위 수준 항목으로 삽입합니다. 마지막 기존 범주 다음에 배치됩니다. 사용자가 다르게 지정하지 않는 한:

```
  + {Category Label}{#{folder-slug}}
    + [Overview](/help/blueprints/architecture-diagrams/{new-folder}/overview.md)
    + [{Page title}](/help/blueprints/architecture-diagrams/{new-folder}/{filename}.md)
```

규칙:

- 다른 다섯 개 항목과 일치하는 항목 머리글에 대한 2자리 들여쓰기입니다.
- 앵커 `{#{folder-slug}}`은(는) 폴더 이름과 정확히 같아야 합니다(naming-conventions.md 참조).
- `+ [Overview]`은(는) 항상 콘텐츠 페이지 앞에 있는 첫 번째 항목인 4칸 들여쓰기입니다.
- 다른 모든 TOC.md 항목의 기존 순서와 내용을 유지합니다. 즉, 관련 없는 섹션만 삽입하고, 다시 정렬하거나 다시 작성하지 않습니다.

## 5단계: 아키텍처 다이어그램 및 블루프린트 랜딩 페이지 업데이트

다른 5개의 카드에서 사용하는 것과 동일한 `<table style="table-layout:fixed; width:100%;">` 그리드에 새 카드를 `help/blueprints/architecture-diagrams/overview.md`에 추가합니다. 새 카드:

- `{new-folder}/overview.md`(으)로 연결된 링크입니다.
- `{new-folder}/assets/`의 대표 다이어그램 썸네일(또는 아직 다이어그램이 없는 경우 중립 자리 표시자 참고)을 사용합니다. 이미지 경로를 인벤터리하는 대신 사용자에게 플래그를 지정합니다.
- 기존 카드와 정확히 동일한 인라인 스타일 블록을 사용합니다(이미지의 경우 `width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;`, 텍스트 div의 경우 `min-height:100px;`).

**격자 레이아웃을 다시 계산합니다.** 기존 5개의 카드가 3열 그리드(2개의 행, 하나의 후행 빈 셀)를 채웁니다. 여섯 번째 카드를 추가하면 빈 셀이 정확히 채워집니다. 레이아웃을 변경할 필요가 없습니다. 7번째, 8번째 등 카테고리인 경우 새 카드로 새 `<tr>`을(를) 추가하고 해당 행의 나머지 빈 셀에 빈 `<td style="width:33%; ...;"></td>` 요소를 패딩하여 행이 레깅되지 않도록 합니다.

## 6단계: 유효성 검사

확인 후 사용자에게 보고합니다.

1. **명명 일관성** — 폴더 이름, TOC 앵커 및 범주 레이블 슬러그가 동일합니다(명명 규칙.md당).
2. **overview.md 구조** — `category-overview-template.md`과(와) 일치(소개 + 2열 `Diagram | Description` 테이블, 테이블에 포함된 이미지 또는 중첩된 목록 없음).
3. **TOC.md 배치** — 새 하위 섹션은 아키텍처 다이어그램 및 블루프린트 아래에 있으며, `+ [Overview]`은(는) 첫 번째, 들여쓰기가 올바르며, 다른 항목은 변경되지 않았습니다.
4. **랜딩 페이지 카드** — 올바른 눈금 위치에 추가되고, 표준 카드 스타일을 사용하며, 새 `overview.md`에 연결됩니다.
5. **리디렉션** — 이 범주가 이전에 다른 곳에 있던 콘텐츠를 통합하거나 이름을 변경하는 경우(새 범주는 드물지만 확인), 이전 아키텍처 다이어그램 이름 바꾸기에 사용되는 기존 `source,dest` 형식에 따라 `redirects.csv`에 항목을 추가합니다.

작업 완료를 고려하기 전에 유효성 검사 문제를 해결하십시오.

## 메모

- 사용자가 나중에 카테고리(레이블, 폴더 또는 앵커)의 이름을 바꾸는 경우 새 카테고리가 아닌 이름 바꾸기 작업입니다. 새 이름에 대한 naming-conventions.md 규칙을 따르고 모든 내부 링크(TOC.md, 두 개요 페이지, 동일 수준의 상대 링크, 스킬 문서)를 업데이트한 다음 리디렉션 항목을 추가합니다. 이전에 이 리포지토리에서 처리했던 것과 동일한 방법으로 카테고리 이름을 바꿉니다. 폴더 `git mv`, 리포지토리 전체 검색 및 바꾸기, 관련 없는 외부 URL(예: `experienceleague.adobe.com/docs/experience-platform/...` 제품 문서 링크)과 충돌할 수 있는 블라인드 전역 문자열 바꾸기 등을 수행합니다.
- 이 스킬과 `architecture-diagram-page-builder`을(를) 동기화 상태로 유지: `architecture-diagram-page-builder`의 `references/toc-placement.md`에 있는 하위 섹션 매핑 테이블에 새 범주가 아직 나열되지 않은 경우 여기에 추가하십시오.
