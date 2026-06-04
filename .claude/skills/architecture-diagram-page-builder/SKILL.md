---
name: architecture-diagram-page-builder
description: Adobe Experience Platform 블루프린트 저장소에 대한 새 아키텍처 다이어그램 페이지 만들기 안내서입니다. 새로운 최상위 아키텍처 다이어그램, 통합 아키텍처 페이지 또는 애플리케이션 아키텍처 개요를 추가할 때 이 기술을 사용하십시오. 아키텍처 페이지는 심층적인 사용 사례(사용 사례 패턴 빌더에 속함)가 아닌 최상위 수준의 AEP 및 애플리케이션 아키텍처와 주요 통합 지점을 다룹니다. 페이지 정보 수집, Markdown 파일 생성, 올바른 항목 폴더에 배치, TOC.md 업데이트와 같은 전체 워크플로를 처리합니다.
source-git-commit: 4d236750286c28a8b8eb53a5bdec0645cc0e3e91
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 1%

---


# 아키텍처 다이어그램 페이지 빌더

이 스킬은 Adobe Experience Platform 블루프린트 저장소에 대한 새 아키텍처 다이어그램 페이지를 만드는 방법을 안내합니다. 아키텍처 다이어그램 페이지는 AEP과 Adobe 애플리케이션이 어떻게 서로 맞물리고, 이들 간에 기본 데이터가 흐르며, 작성자가 솔루션을 디자인할 때 알아야 하는 통합 지점에 대한 최상위 시각적 참조를 제공합니다.

## 범위

아키텍처 다이어그램 페이지는 다음을 포함하는 **포커스가 있는 참조 스타일 페이지**(일반적으로 40~100줄 Markdown)입니다.

- 각 다이어그램의 목적에 대한 간략한 설명이 포함된 하나 이상의 아키텍처 다이어그램
- 아키텍처가 지원하는 사용 사례 패턴에 대한 링크(아키텍처 페이지가 해당 콘텐츠를 복제하지 않음)
- 기본 데이터 흐름 및 통합 지점에 대한 간략한 목록 그림
- 애플리케이션 도메인에서 자세히 읽기 위한 Experience League 링크

자세한 사용 사례 콘텐츠 위치가 **아닙니다**. `use-case-pattern-builder` 스킬을 통해 생성된 사용 사례 패턴 페이지에는 KPI, 비즈니스 목표, 전술적 사용 사례 예, 기능 및 성향 설명이 대신 포함됩니다. 전체 보호 기능은 `references/scope-guardrails.md`을(를) 참조하십시오.

## 시작하기 전에 읽어야 함

템플릿 및 규칙에 대한 다음 참조 파일을 참조하십시오.

- `references/diagram-template.md` — 자리 표시자 값이 있는 전체 Markdown 템플릿
- `references/toc-placement.md` — TOC.md의 하위 섹션 매핑 테이블 및 항목 형식
- `references/scope-guardrails.md` — 아키텍처 페이지와 사용 사례 패턴 페이지의 항목에 대한 규칙

## 1단계: 정보 수집

**선형 인터뷰가 아닌 양식을 사용하십시오.** 한 번에 한 질문씩 하지 않고 논리 일괄 처리로 `AskUserQuestion` 양식을 제시하여 필요한 모든 정보를 수집합니다. 이렇게 하면 사용자에게 경험이 빠르고 스캔할 수 있습니다.

### AskUserQuestion 제약 조건

- `AskUserQuestion` 호출당 최대 **4개 질문**.
- 질문당 최대 **4개 옵션**.
- 질문에 4개 이상의 그럴듯한 옵션이 있는 경우 두 번의 호출로 분할합니다(예: 처음 4개 옵션을 물은 다음 5번째에 예/아니오로 따라가십시오).
- 여러 개의 답변이 적용되는 질문(솔루션, 패턴, 데이터 흐름)에는 `multiSelect: true`을(를) 사용하십시오.

### 1라운드 — 핵심 페이지 정보(1개의 AskUserQuestion 호출, 최대 4개의 질문)

단일 양식으로 다음 사항을 모두 요청합니다.

1. **페이지 제목** — 사용자가 이미 알려준 내용에서 파생된 2~3개의 제안된 변형과 &quot;기타&quot; 이스케이프 해치가 있습니다.
2. **주제 폴더** — 5개의 유효한 폴더를 옵션으로 제공합니다. 사용자의 입력에 따라 추천 폴더를 선택하십시오.
3. **Adobe 솔루션** — 다중 선택. 페이지 주제에 따라 가장 적합한 후보를 제안합니다.
4. **다이어그램 수** — 페이지에 포함되는 다이어그램 수(1 / 2 / 3 / 4+)입니다.

### 2라운드 — 다이어그램 세부 정보(AskUserQuestion 호출 1회, 최대 4개 질문)

각 다이어그램의 이미지 파일 이름과 페이지 용도를 한 가지 형식으로 묻습니다.

- 각 다이어그램(단일 양식 라운드에서 최대 2개)에 대해 2~3개의 제안된 파일 이름(페이지 제목에서 파생됨)과 &quot;기타&quot; 옵션이 있는 질문으로 **이미지 파일 이름**&#x200B;을 요청합니다.
- 2-3개의 추천 문구와 &quot;기타&quot;가 포함된 질문으로 **페이지 목적**(1-2 문장 설명)을 요청합니다.
- **`>[!MORELIKETHIS]`callout**&#x200B;이 필요한지 여부를 묻습니다(예/아니요). [예]인 경우 URL을 수집하고 후속 메시지에서 텍스트를 연결합니다.

> **섹션 제목 및 대체 텍스트:** 이미지 파일 이름이 설명적인 경우(예: `fac-architecture.svg`, `fac-dataflow.svg`) H2 섹션 제목과 대체 텍스트를 유추하십시오. 사용자에게 물어볼 필요가 없습니다. 파일 이름 스템, 제목 대 및 인간화된 이름을 섹션 제목(예: `Architecture diagram`, `Data flow diagram`)으로 사용합니다. 파일 이름이 모호한지 여부만 묻습니다.

### 3라운드 — 사용 사례 패턴(스캔 후 AskUserQuestion)

이 양식을 제시하기 전에 **glob`/help/blueprints/use-case-patterns/`**&#x200B;을(를) 만들고 페이지 제목, 목적 및 솔루션을 기준으로 3~5개의 일치하는 패턴을 식별하십시오. 제안하기 전에 각 파일이 있는지 확인하십시오.

상위 4명의 후보를 `multiSelect` 질문으로 제시합니다. 강력한 다섯 번째 후보가 존재할 경우, 그 후보에 대해 별도의 예/아니오 질문을 따르십시오. 사용자가 놓친 패턴의 이름도 지정할 수 있도록 하십시오.

파일이 존재하는 것으로 확인된 패턴만 포함합니다. 패턴 이름을 환각하지 마십시오.

### 4라운드 — 데이터 흐름 및 Experience League 링크(AskUserQuestion 호출 1개)

**데이터 흐름:** 미리 작성된 3-5개의 데이터 흐름 글머리 기호를 `multiSelect` 질문으로 제안합니다(페이지 항목에서 파생). 사용자가 적용할 을(를) 선택합니다. 각 옵션을 하나의 간결한 문장으로 유지하십시오. 목록에 없는 사용자 정의 흐름이 필요한 경우 후속 조치에서 제공할 수 있습니다.

**Experience League 링크:** 양식 뒤에 문서 제목, URL 및 한 줄 이유가 있는 4~6개의 추천 링크로 구성된 Markdown 표를 제시합니다. 모든 URL을 **확인되지 않음**(으)로 표시합니다. (a) 수락하거나, (b) 확인된 URL로 대체하거나, (c) 직접 추가하도록 사용자에게 요청합니다. 목록이 길면 최대 4개의 옵션과 함께 후속 `AskUserQuestion`을(를) 사용하십시오. 그렇지 않으면 일반 텍스트로 확인을 수락하십시오.

가져오지 않은 URL은 발명하지 마십시오. 확실하지 않은 경우 문서 제목을 제안하고 사용자가 URL을 제공하도록 합니다.

### 모든 라운드가 완료된 경우

파일을 생성하기 전에 사용자와 전체 정보 세트를 확인합니다. 필수 항목이 여전히 누락되었거나 값 없이 &quot;기타&quot;로 표시된 경우 계속하기 전에 요청하십시오. 다이어그램, 패턴 또는 링크를 조작하지 마십시오.

## 2단계: 범위 확인

생성하기 전에 사용자의 다이어그램 설명, 데이터 흐름 글머리 기호 및 초안 산문을 다시 읽으십시오. `references/scope-guardrails.md`에서 가드레일을 적용합니다.

계획된 콘텐츠에 다음 중 하나가 나타나면 사용자에게 경고하고 해당 섹션을 사용 사례 패턴 페이지로 리디렉션하도록 오퍼합니다(또는 아키텍처 페이지에서 트리밍합니다).

- KPI 또는 측정 공식
- 비즈니스 목표 또는 비즈니스 영향 설명
- 전술적 사용 사례 예(특정 개인화 시나리오, 캠페인 예 등)
- 기능(`A > B > C > D` 스타일)
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

**배치하기 전에 중첩된 하위 그룹을 검사합니다.** 일부 하위 섹션(특히 `Audience & Profile Activation`)에는 중첩된 그룹화(예: `Real-Time Customer Data Platform (RTCDP) {#known-customer-audience-activation}`)가 포함되어 있습니다. 편집하기 전에 TOC.md의 영향을 받는 하위 섹션을 읽으십시오. 새 최상위 아키텍처 페이지는 하위 섹션의 4공간 들여쓰기 수준(**없음**, 6공간 들여쓰기를 사용하는 중첩된 하위 그룹 내에 있음)에 속합니다. 마지막으로 중첩된 하위 그룹 항목 뒤에 다음 최상위 하위 섹션 머리글 앞에 새 항목을 배치합니다.

## 5단계: 유효성 검사

모든 파일을 만들고 업데이트한 후 다음을 확인하고 오류가 발생하면 사용자에게 보고합니다.

1. **이미지 자산 존재** — 각 다이어그램에 대해 `/help/blueprints/{topic-folder}/assets/{filename}`이(가) 있는지 확인하십시오. 누락된 경우 **경고**. 차단하지 마십시오(사용자가 다이어그램 디자인과 함께 작성할 수 있음). 사용자가 추가할 내용을 알 수 있도록 누락된 파일의 명확한 목록을 표시합니다.

2. **사용 사례 패턴 링크** — 파일의 모든 패턴 링크는 `/help/blueprints/use-case-patterns/` 아래의 기존 Markdown 파일을 가리킵니다. `Read` 또는 glob을 사용하여 각 대상이 있는지 확인하십시오.

3. **Experience League 링크** — `## Further reading` 섹션의 모든 URL이 `https://experienceleague.adobe.com/ko`(으)로 시작하는지 확인합니다.

4. **목차 항목 배치** — 새 항목은 올바른 하위 섹션 내에 있으며 4개의 공백 들여쓰기를 사용하며 경로는 생성된 파일 위치와 정확히 일치합니다.

5. **파일 이름 지정** — 페이지 파일 이름은 kebab-case이며 TOC.md에서 참조된 경로와 일치합니다.

6. **Frontmatter 완성도** — 페이지에 `title`, `description` 및 `solution`이(가) 포함됩니다. **not**&#x200B;에 `exl-id`, `product_v2`, `feature_v2`, `role_v2`, `topic_v2`, `TQID`, `kt` 또는 `thumbnail`이(가) 포함되어야 합니다.

작업 완료를 고려하기 전에 유효성 검사 문제를 해결하십시오.

## 메모

- 기존 페이지의 규칙에 따라 항상 본문 텍스트와 글머리 기호로 묶은 Adobe 제품 이름에 `[!DNL ...]` 구문을 사용하십시오.
- 아키텍처 다이어그램은 일반적으로 SVG(선명하고 크기 조절에 선호됨)이지만 래스터 소스 아트워크에는 PNG를 사용할 수 있습니다.
- `<img>` 포함 인라인 스타일 문자열(`border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;`) 및 `class="modal-image"`이 필요합니다. 이 문자열을 사용하면 Experience League 모달 확대/축소 상호 작용을 사용할 수 있습니다.
- 사용자가 아직 존재하지 않는 완전히 새로운 주제 폴더의 페이지를 만드는 경우 TOC.md에 `+ Architecture Diagrams and Blueprints{#architecture-diagrams}` 아래에 새로운 최상위 하위 섹션이 필요하다는 경고를 표시하십시오. 사용자의 명시적 승인을 통해 이를 별도의 단계로 처리합니다.
- 아키텍처 다이어그램이 *단일 사용 사례 전체*&#x200B;을(를) 광범위하게 문서화하는 경우(KPI, 비즈니스 목표, 기능 포함) 사용자를 `use-case-pattern-builder`(아키텍처 페이지가 아님)으로 리디렉션하십시오.
