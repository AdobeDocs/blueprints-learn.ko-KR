---
source-git-commit: c766cd3153efce4635089d008daf3eb426eb7a24
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
# 이름 지정 규칙: 아키텍처 다이어그램 및 블루프린트

이 문서는 `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` 아래의 범주 이름을 지정하는 방법에 대한 올바른 원본입니다. `architecture-diagram-category-builder` 스킬(새 범주)과 `architecture-diagram-page-builder` 스킬(기존 범주 내의 새 페이지)은 모두 이 규칙을 따라야 합니다.

## 규칙

**폴더 이름 = TOC 앵커 슬러그 = kebab-전체 TOC 레이블의 대/소문자입니다.** 세 가지 모두 약어나 잘림 없이 정확하게 일치해야 합니다.

| 목차 레이블 | 앵커 | 폴더 |
| --- | --- | --- |
| 아키텍처 개요 | `#architecture-overviews` | `architecture-overviews/` |
| 대상자 및 프로필 활성화 | `#audience-profile-activation` | `audience-profile-activation/` |
| B2B 활성화 및 마케팅 | `#b2b-activation-marketing` | `b2b-activation-marketing/` |
| 고객 인사이트 | `#customer-insights` | `customer-insights/` |
| 고객 여정 | `#customer-journeys` | `customer-journeys/` |

이는 5개 범주(2026-09-16년 현재)의 현재 수정된 상태입니다. 이 리포지토리의 기록 앞부분에서 일부 생략되었습니다(`architecture-overview`, `audience-activation`, `b2b-activation`). 이러한 불일치가 수정되었습니다. 새 카테고리 또는 기존 카테고리에 대해 축약된 폴더/앵커 이름을 다시 도입하지 마십시오.

## 이것이 중요한 이유

- **예측 가능성** 기여자(사람 또는 에이전트)는 TOC.md를 열지 않고도 TOC 레이블의 폴더 경로를 추측할 수 있고 그 반대의 경우도 가능합니다.
- **안전한 자동화.** 레이블(또는 경로의 레이블)에서 경로를 생성하는 기술과 스크립트는 매핑이 정확하고 기계적(kebab-case, 약어 없음)일 때만 안정적으로 작동합니다.
- **위생 리디렉션.** 이름을 바꿀 때마다 `redirects.csv`에 새 항목이 필요합니다. 처음부터 이름을 안정적이고 완전히 기술적으로 유지하면 반복되는 이름 바꾸기 이탈을 방지할 수 있습니다.

## 레이블에서 슬러그를 파생하는 방법

1. 레이블을 소문자로 표시합니다.
2. `&`을(를) 완전히 삭제하고 하이픈으로 주변 단어를 연결하십시오(예: `Audience & Profile Activation` -> `audience-profile-activation`).
3. 공백을 하이픈으로 바꿉니다.
4. 하이픈 이외의 구두점 제거.
5. 레이블에서 단어를 줄이거나, 자르거나, 삭제하지 마십시오(&quot;B2B 활성화 및 마케팅&quot;에 `b2b-activation` 없음, `b2b-activation-marketing` 사용).

## 필요한 범주별 자산

`help/blueprints/architecture-diagrams/` 바로 아래에 있는 모든 범주 폴더에는 다음이 포함되어야 합니다.

1. **`overview.md`** — 범주의 랜딩 페이지입니다. 필요한 구조는 `./category-overview-template.md`을(를) 참조하십시오. 모든 범주 개요 페이지는 동일한 모양으로 표시되어야 합니다. 도입 단락을 클릭한 다음 범주의 모든 페이지를 나열하는 단일 `| Diagram | Description |` 테이블(목차 순서로 표시). 중첩된 `<ul><li>` 셀, 포함된 다이어그램 이미지 또는 세 번째 열을 사용하지 마십시오. 기존 5개의 범주와 정확하게 일치합니다.
2. **`assets/`** — 만들 때 비어 있더라도 다이어그램 이미지의 폴더입니다(첫 번째 다이어그램이 추가되면 생성).

## TOC.md 요구 사항

- 범주의 `+ [Overview](/help/blueprints/architecture-diagrams/{folder}/overview.md)` 항목은 항상 콘텐츠 페이지 앞의 범주 머리글 아래에 있는 **first** 항목입니다.
- 범주 제목과 해당 앵커는 `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` 바로 아래에 있으며, 다른 5개 범주와 동일한 2개 공간 들여쓰기 수준입니다.
- 콘텐츠 페이지는 4개의 공백으로 들여씁니다(`+` 앞에는 4개의 공백이 붙음). 중첩된 하위 그룹화(예: 대상 및 프로필 활성화 아래의 RTCDP 그룹화)는 6개의 공백으로 들여씁니다.

## 랜딩 페이지 요구 사항

`help/blueprints/architecture-diagrams/overview.md`(최상위 아키텍처 다이어그램 및 블루프린트 랜딩 페이지)에는 TOC 순서로 카테고리당 카드가 정확히 하나만 있어야 합니다. 각 카드:

- 범주의 `overview.md` 링크(콘텐츠 페이지 아님).
- 표준 카드 CSS(`background-color:#ffffff; border:1px solid #d3d3d3;` + 파일에 이미 있는 공유 크기 조정/패딩 규칙)로 스타일이 지정된 해당 범주의 `assets/` 폴더에서 대표 다이어그램 이미지를 썸네일로 사용합니다.
- 카테고리 이름(굵게/강함) 및 카테고리 개요의 소개와 일치하는 한 문장 설명을 포함합니다.

범주의 수가 3의 배수인 경우 테이블이 클린 전체 행(셀당 3열, `table-layout:fixed`, `width:33%`)으로 렌더링됩니다. 3의 배수가 아닌 경우 마지막 행의 누락된 슬롯당 빈 `<td>`을(를) 하나 추가합니다(테이블을 불규칙하게/스타일이 지정되지 않도록 하지 마십시오).
