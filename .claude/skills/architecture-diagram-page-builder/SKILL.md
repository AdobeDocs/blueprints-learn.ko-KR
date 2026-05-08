---
name: architecture-diagram-page-builder
description: Adobe Experience Platform 블루프린트 저장소에 대한 새 아키텍처 다이어그램 페이지 만들기 안내서입니다. 새로운 최상위 아키텍처 다이어그램, 통합 아키텍처 페이지 또는 애플리케이션 아키텍처 개요를 추가할 때 이 기술을 사용하십시오. 아키텍처 페이지는 심층적인 사용 사례(사용 사례 패턴 빌더에 속함)가 아닌 최상위 수준의 AEP 및 애플리케이션 아키텍처와 주요 통합 지점을 다룹니다. 페이지 정보 수집, Markdown 파일 생성, 올바른 항목 폴더에 배치, TOC.md 업데이트와 같은 전체 워크플로를 처리합니다.
source-git-commit: 83e85d946e455cde46001af0a2112637b7fe24cc
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 2%

---


# 아키텍처 다이어그램 페이지 빌더

이 스킬은 Adobe Experience Platform 블루프린트 저장소에 대한 새 아키텍처 다이어그램 페이지를 만드는 방법을 안내합니다. 아키텍처 다이어그램 페이지는 AEP과 Adobe 애플리케이션이 어떻게 서로 맞물리고, 이들 간에 기본 데이터가 흐르며, 작성자가 솔루션을 디자인할 때 알아야 하는 통합 지점에 대한 최상위 시각적 참조를 제공합니다.

## 범위

아키텍처 다이어그램 페이지는 다음을 포함하는 **포커스가 있는 참조 스타일 페이지**(일반적으로 40~100줄 Markdown)입니다.

- 각 다이어그램의 목적에 대한 간략한 설명이 포함된 하나 이상의 아키텍처 다이어그램
- 아키텍처가 지원하는 사용 사례 패턴에 대한 링크(아키텍처 페이지가 해당 콘텐츠를 복제하지 않음)
- 기본 데이터 흐름 및 통합 지점에 대한 간략한 목록 그림
- 애플리케이션 도메인에서 자세히 읽기 위한 Experience League 링크

자세한 사용 사례 콘텐츠 위치가 **아닙니다**. KPI, 비즈니스 목표, 전술적 사용 사례 예, 기능 체인 및 성향 설명은 `use-case-pattern-builder` 스킬을 통해 생성된 사용 사례 패턴 페이지에 대신 속합니다. 전체 보호 기능은 `references/scope-guardrails.md`을(를) 참조하십시오.

## 시작하기 전에 읽어야 함

템플릿 및 규칙에 대한 다음 참조 파일을 참조하십시오.

- `references/diagram-template.md` — 자리 표시자 값이 있는 전체 Markdown 템플릿
- `references/toc-placement.md` — TOC.md의 하위 섹션 매핑 테이블 및 항목 형식
- `references/scope-guardrails.md` — 아키텍처 페이지와 사용 사례 패턴 페이지의 항목에 대한 규칙

## 1단계: 정보 수집

파일을 생성하기 전에 사용자를 인터뷰하여 필요한 모든 정보를 수집합니다. 모든 필수 항목이 제공되거나 명시적으로 지연될 때까지 콘텐츠 생성을 진행하지 마십시오.

### 필수 정보

1. **페이지 제목** - 사람이 읽을 수 있는 제목(예: `Adobe Journey Optimizer architecture diagrams`).

2. **주제 폴더** — 페이지가 있는 위치입니다. 다이어그램의 주 도메인을 기반으로 정확히 하나를 선택하십시오.
   - `experience-platform/` — 최상위 AEP, 다중 앱 또는 플랫폼 수준 다이어그램
   - `customer-journeys/` — AJO, 캠페인, 여정 오케스트레이션
   - `customer-journey-analytics/` — CJA 아키텍처
   - `audience-activation/` — RTCDP, 대상 및 프로필 활성화
   - `b2b/` — B2B별 아키텍처

3. **파일 이름** — 페이지 제목에서 파생된 Kebab-case(예: `Journey Optimizer architecture` -> `journey-optimizer-architecture.md`). 사용자와 확인합니다.

4. **페이지 목적** — 다이어그램이 전체적으로 보여 주는 내용을 설명하는 1~2개의 문장입니다. `description` 프론트마클 필드 및 여는 단락에 사용됩니다.

5. **Adobe 솔루션** — 페이지 중앙에 있는 쉼표로 구분된 Adobe 제품 목록입니다. `solution` 프론트마터 필드에 사용됩니다. 예: `Experience Platform, Journey Optimizer, Customer Journey Analytics`.

6. **다이어그램** — 하나 이상의 다이어그램. 각 다이어그램에 대해 다음을 수집합니다.
   - **이미지 파일 이름**(예: `aep_data_flow.svg`). SVG 기본 설정, PNG 허용.
   - **섹션 제목** — 다이어그램의 H2 머리글이 됩니다(예: `Data flow diagram`, `Detailed architecture diagram`).
   - **목적 설명** — 다이어그램에 표시되는 내용을 설명하는 1~2개의 문장입니다.
   - **대체 텍스트** — 간단한 설명.

7. **지원되는 사용 사례 패턴** — 이 아키텍처가 지원하는 2~5개의 기존 패턴입니다.

   **먼저 후보자를 추천합니다.** 사용자에게 패턴을 제공하도록 요청하기 전에 `/help/blueprints/use-case-patterns/`을(를) 스캔하고 위에서 수집한 페이지 제목, 페이지 목적 및 Adobe 솔루션을 기반으로 3~6개의 가능한 일치 항목을 제안하십시오. 각 제안에 대해 다음 내용이 표시됩니다.
   - 패턴 이름(연결된 경로 포함)
   - 이 아키텍처에 맞는 이유에 대한 한 문장의 근거

   제안 사항을 번호 매기기 관심 목록으로 표시하고 (a) 임의 항목을 수락하고, (b) 임의 항목을 거부하고, (c) 누락된 패턴을 추가하도록 사용자에게 요청합니다. 실제 파일을 가리키는 제안만 생성합니다. 제안하기 전에 확인하기 위해 glob/read를 사용합니다. 패턴 이름을 환각하지 마십시오.

   허용되는 각 패턴에 대해 카테고리와 파일 이름을 캡처합니다. 생성하기 전에 `/help/blueprints/use-case-patterns/{category}/{pattern-file}.md`에 각 파일이 있는지 확인하십시오.

8. **기본 데이터 흐름/통합 지점** — 다이어그램(예: `Real-time event ingestion from Web SDK to Edge Network`, `Profile synchronization between Experience Platform Hub and Edge`)에 표시되는 주요 흐름 및 통합 경계를 설명하는 글머리 기호 3~7개.

9. **Experience League 링크** — 자세한 내용은 관련 Experience League 설명서에 대한 3~6개의 링크를 참조하십시오. 각각 `https://experienceleague.adobe.com/`(으)로 시작해야 합니다.

   **먼저 후보자를 추천합니다.** Adobe 솔루션 및 페이지 용도를 기반으로 4~8개의 그럴듯한 Experience League 문서(예: 각 명명된 솔루션에 대한 표준 랜딩 또는 개요 페이지, 주요 통합 안내서, 배포 참조)를 제안합니다. 각 제안에 대해 다음 내용이 표시됩니다.
   - 문서 제목
   - URL
   - 페이지에 맞는 이유에 대한 한 줄짜리 설명

   URL을 실제로 가져오지 않은 경우 제안을 **확인되지 않음**(으)로 표시합니다. 생성된 파일에 삽입되기 전에 사용자가 각 URL을 확인하거나 대체해야 합니다. (a) 수락하고, (b) 모든 URL을 이미 가지고 있는 확인된 URL로 교체하고, (c) 해당 URL을 추가하도록 사용자에게 요청합니다. 본 적이 없는 URL은 발명하지 마십시오. 확실하지 않은 경우 문서 제목을 제안하고 사용자가 URL을 제공하도록 하십시오.

### 선택 사항

- **관련 콘텐츠 호출** — 페이지 위쪽에 `>[!MORELIKETHIS]` 블록으로 렌더링된 단일 링크입니다. Experience League에 형제 통합 또는 구성 안내서가 있는 경우 유용합니다.

사용자가 모든 필수 항목을 제공하지 않는 경우 계속 진행하기 전에 누락된 항목을 요청하십시오. 다이어그램, 패턴 또는 링크를 조작하지 마십시오.

## 2단계: 범위 확인

생성하기 전에 사용자의 다이어그램 설명, 데이터 흐름 글머리 기호 및 초안 산문을 다시 읽으십시오. `references/scope-guardrails.md`에서 가드레일을 적용합니다.

계획된 콘텐츠에 다음 중 하나가 나타나면 사용자에게 경고하고 해당 섹션을 사용 사례 패턴 페이지로 리디렉션하도록 오퍼합니다(또는 아키텍처 페이지에서 트리밍합니다).

- KPI 또는 측정 공식
- 비즈니스 목표 또는 비즈니스 영향 설명
- 전술적 사용 사례 예(특정 개인화 시나리오, 캠페인 예 등)
- 함수 체인(`A > B > C > D` 스타일)
- 사용자 중심의 storytelling

계획된 컨텐츠가 아키텍처 페이지 범위(최상위 아키텍처, 시스템 데이터 흐름, 통합 지점, 배포 토폴로지, 에지 및 허브) 내에 있는 경우 사용자에게 확인하고 3단계로 진행합니다.

## 3단계: 컨텐츠 생성

다음 위치에 페이지 생성:

```
/help/blueprints/{topic-folder}/{kebab-filename}.md
```

`references/diagram-template.md`을(를) 원본 템플릿으로 사용합니다. 수집된 정보로 모든 자리 표시자 값을 채웁니다. 생성된 파일에는 다음이 포함되어야 합니다.

1. **YAML 앞면 문제** — `title`, `description`, `solution`만
   - **`exl-id`**&#x200B;을(를) 포함하지 않음 — 게시 파이프라인이 자동으로 할당합니다.
   - **포함하지 않음** `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` 또는 `thumbnail` - 자동으로 채워집니다.

2. **H1 제목** — 페이지 제목입니다.

3. **단락 열기** — 페이지 목적 입력에서 파생된 1~2개의 문장입니다.

4. **선택적 `>[!MORELIKETHIS]` 블록** — 사용자가 관련 콘텐츠 링크를 제공한 경우에만 해당됩니다.

5. **다이어그램당 하나의 H2 섹션** — 사용자가 제공한 순서대로. 각 섹션에는 다음이 포함됩니다.
   - 섹션 제목(H2 제목)
   - 도표의 목적을 설명하는 1-2개의 문장
   - 표준 규칙을 사용하여 포함된 이미지:

     ```html
     <img src="assets/{filename}" alt="{Alt Text}" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />
     ```

6. **`## Use case patterns supported`** — 글머리 기호 목록입니다. 각 글머리 기호:

   ```
   - [{Pattern name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) -- {1-line note on why this architecture enables the pattern}
   ```

7. **`## Primary data flows and integration points`** — 3~7개의 흐름/통합 항목의 글머리 기호 목록입니다.

8. **`## Further reading`** — 글머리 기호 Experience League 링크 목록:

   ```
   - [{Article title}]({Experience League URL})
   ```

기존 페이지의 규칙과 일치하는 본문 텍스트와 글머리 기호로 된 Adobe 제품 이름에 `[!DNL ...]` 구문을 사용합니다.

## 4단계: 상호 참조 업데이트

**`/help/blueprints/TOC.md`**&#x200B;을(를) 업데이트하여 탐색에 새 페이지를 추가합니다. 이는 업데이트할 유일한 상호 참조 페이지입니다.

전체 하위 섹션 매핑 테이블 및 규칙에 대해 `references/toc-placement.md`을(를) 읽어 보십시오. 요약:

| 주제 폴더 | 목차 하위 섹션 |
| --- | --- |
| `experience-platform/` | `+ Architecture overviews{#architecture-overview}` |
| `experience-platform/deployment/` | `+ Deployment{#deployment}`(아키텍처 개요의 하위 섹션) |
| `audience-activation/` | `+ Audience & Profile Activation{#audience-activation}` |
| `b2b/` | `+ B2B activation & marketing{#b2b-activation}` |
| `customer-journey-analytics/` | `+ Customer Journey Analytics{#customer-journey-analytics}` |
| `customer-journeys/` | `+ Customer journeys{#customer-journeys}` |

시작 형식(4칸 들여쓰기 + `+`):

```
    + [{Page title}](/help/blueprints/{topic-folder}/{filename}.md)
```

사용자가 다른 위치를 지정하지 않는 한 새 항목을 일치하는 하위 섹션의 마지막 항목으로 추가합니다. 정확한 4공간 들여쓰기를 유지합니다. TOC 구문 분석은 여기에 따라 달라집니다.

## 5단계: 유효성 검사

모든 파일을 만들고 업데이트한 후 다음을 확인하고 오류가 발생하면 사용자에게 보고합니다.

1. **이미지 자산 존재** — 각 다이어그램에 대해 `/help/blueprints/{topic-folder}/assets/{filename}`이(가) 있는지 확인하십시오. 누락된 경우 **경고**. 차단하지 마십시오(사용자가 다이어그램 디자인과 함께 작성할 수 있음). 사용자가 추가할 내용을 알 수 있도록 누락된 파일의 명확한 목록을 표시합니다.

2. **사용 사례 패턴 링크** — 파일의 모든 패턴 링크는 `/help/blueprints/use-case-patterns/` 아래의 기존 Markdown 파일을 가리킵니다. `Read` 또는 glob을 사용하여 각 대상이 있는지 확인하십시오.

3. **Experience League 링크** — `## Further reading` 섹션의 모든 URL이 `https://experienceleague.adobe.com/`(으)로 시작하는지 확인합니다.

4. **목차 항목 배치** — 새 항목은 올바른 하위 섹션 내에 있으며 4개의 공백 들여쓰기를 사용하며 경로는 생성된 파일 위치와 정확히 일치합니다.

5. **파일 이름 지정** — 페이지 파일 이름은 kebab-case이며 TOC.md에서 참조된 경로와 일치합니다.

6. **Frontmatter 완성도** — 페이지에 `title`, `description` 및 `solution`이(가) 포함됩니다. **not**&#x200B;에 `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` 또는 `thumbnail`이(가) 포함되어야 합니다.

작업 완료를 고려하기 전에 유효성 검사 문제를 해결하십시오.

## 메모

- 기존 페이지의 규칙에 따라 항상 본문 텍스트와 글머리 기호로 묶은 Adobe 제품 이름에 `[!DNL ...]` 구문을 사용하십시오.
- 아키텍처 다이어그램은 일반적으로 SVG(선명하고 크기 조절에 선호됨)이지만 래스터 소스 아트워크에는 PNG를 사용할 수 있습니다.
- `<img>` 포함 인라인 스타일 문자열(`border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;`) 및 `class="modal-image"`이 필요합니다. 이 문자열을 사용하면 Experience League 모달 확대/축소 상호 작용을 사용할 수 있습니다.
- 사용자가 아직 존재하지 않는 완전히 새로운 주제 폴더의 페이지를 만드는 경우 TOC.md에 `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` 아래에 새로운 최상위 하위 섹션이 필요하다는 경고를 표시하십시오. 사용자의 명시적 승인을 통해 이를 별도의 단계로 처리합니다.
- 아키텍처 다이어그램이 *단일 사용 사례 전체*&#x200B;을(를) 광범위하게 문서화하는 경우(KPI, 비즈니스 목표, 기능 체인 포함) 사용자를 `use-case-pattern-builder`(아키텍처 페이지가 아님)으로 리디렉션합니다.
