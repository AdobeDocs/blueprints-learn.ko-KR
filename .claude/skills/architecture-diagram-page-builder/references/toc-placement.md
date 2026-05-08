---
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---
# TOC.md 배치 참조

스킬이 새 아키텍처 다이어그램 페이지를 생성할 때 사이트 탐색에서 페이지를 검색할 수 있도록 `/help/blueprints/TOC.md`에 항목을 추가해야 합니다. 이 문서는 해당 항목의 위치와 방법을 정확하게 정의합니다.

## 상위 섹션

모든 아키텍처 다이어그램 페이지는 TOC.md의 최상위 `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` 섹션 아래에 있습니다. 해당 섹션 내에서 여러 하위 섹션은 주제별로 페이지를 그룹화합니다.

## 하위 섹션 매핑

새 페이지의 주제 폴더와 일치하는 하위 섹션을 선택합니다.

| 주제 폴더 | 목차 하위 섹션 제목 |
| --- | --- |
| `experience-platform/` | `+ Architecture overviews{#architecture-overview}` |
| `experience-platform/deployment/` | `+ Deployment{#deployment}`(`Architecture overviews` 내에 중첩된 하위 섹션) |
| `audience-activation/` | `+ Audience & Profile Activation{#audience-activation}` |
| `b2b/` | `+ B2B activation & marketing{#b2b-activation}` |
| `customer-journey-analytics/` | `+ Customer Journey Analytics{#customer-journey-analytics}` |
| `customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

사용자가 이 표에 없는 주제 폴더를 제안하는 경우 새 최상위 하위 섹션으로 취급하고 일시 중지 — 작성 여부를 확인하도록 사용자에게 요청합니다. 새로운 하위 섹션을 묵묵히 발명하지 마십시오.

## 시작 형식

```
    + [{Page title}](/help/blueprints/{topic-folder}/{filename}.md)
```

규칙:

- **들여쓰기:** 정확히 4개의 공백, `+ `. TOC 파서는 이에 따라 달라집니다. 탭 또는 다른 간격으로 인해 탐색이 중단됩니다.
- **링크 텍스트:** 페이지 제목이 `title` 프런트 텍스트와 정확히 일치합니다. 동일한 하위 섹션의 기존 형제 항목이 로컬 규칙과 일치하는 경우에만 `[!DNL ...]`을(를) 사용합니다.
- `/help/blueprints/`(으)로 시작하는 **링크 대상:** 절대 경로입니다. 항상 `.md` 확장을 포함하십시오.
- **위치:**&#x200B;은(는) 사용자가 다른 위치를 지정하지 않는 한 일치하는 하위 섹션의 마지막 항목으로 추가됩니다. 모든 동위 항목의 기존 순서를 유지합니다.

## 중첩된 하위 섹션

`+ Architecture overviews{#architecture-overview}`에 SDK 페이지에 대한 중첩된 `+ Deployment{#deployment}` 블록이 포함되어 있습니다. 새 페이지가 `experience-platform/deployment/` 아래에 있는 경우 항목을 `Deployment` 안에 들여쓰기로 **6**&#x200B;의 공백을 넣으십시오.

```
      + [{Page title}](/help/blueprints/experience-platform/deployment/{filename}.md)
```

기타 하위 섹션(`Audience & Profile Activation`, `B2B activation & marketing` 등) 중첩된 그룹화도 포함할 수 있습니다. 항목을 배치하기 전에 섹션을 검사합니다. 중첩된 그룹화가 있고 새 페이지가 그 안에 속해 있는 경우에는 두 개의 추가 공백을 들여쓰거나, 그렇지 않으면 하위 섹션의 최상위 수준에 항목을 배치하십시오.

## 작업한 예

### 예제 1 — 최상위 AEP 페이지

- 항목 폴더: `experience-platform/`
- 파일 이름: `mix-modeler-integration.md`
- 페이지 제목: `Adobe Mix Modeler integration with Experience Platform`

시작:

```
    + [Adobe Mix Modeler integration with Experience Platform](/help/blueprints/experience-platform/mix-modeler-integration.md)
```

`+ Architecture overviews{#architecture-overview}` 아래에 배치되었습니다.

### 예제 2 - AJO 여정 아키텍처

- 항목 폴더: `customer-journeys/`
- 파일 이름: `cross-channel-journey-architecture.md`
- 페이지 제목: `Cross-channel journey architecture`

시작:

```
    + [Cross-channel journey architecture](/help/blueprints/customer-journeys/cross-channel-journey-architecture.md)
```

`+ Customer journeys{#customer-journeys}` 아래에 배치되었습니다.

### 예제 3 — 배포 SDK 페이지

- 항목 폴더: `experience-platform/deployment/`
- 파일 이름: `mobile-sdk-architecture.md`
- 페이지 제목: `Mobile SDK deployment architecture`

시작(6자리 들여쓰기 참고):

```
      + [Mobile SDK deployment architecture](/help/blueprints/experience-platform/deployment/mobile-sdk-architecture.md)
```

`+ Architecture overviews{#architecture-overview}` 내부의 `+ Deployment{#deployment}` 아래에 배치되었습니다.

## 확인

TOC.md를 편집한 후 영향을 받는 하위 섹션을 다시 읽고 다음을 확인합니다.

1. 새 항목에서는 들여쓰기의 정확히 4개 공백(`Deployment` 아래에 중첩된 경우 6개)을 사용합니다.
2. 링크 대상이 `.md` 확장명을 포함하여 디스크의 파일 경로와 일치합니다.
3. 항목은 하위 섹션 간에 유동하지 않고 올바른 하위 섹션 내에 그룹화됩니다.
4. 기존 항목의 순서가 변경되거나 수정되지 않았습니다.
