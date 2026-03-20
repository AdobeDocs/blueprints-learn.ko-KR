---
name: use-case-pattern-builder
description: Adobe Experience Platform 블루프린트 저장소에 대한 새로운 사용 사례 패턴 콘텐츠의 생성 안내서입니다. 새 사용 사례 패턴을 추가하거나 구현 지침 콘텐츠를 만들거나 사용자가 블루프린트 사이트에 패턴 추가를 언급할 때 이 기술을 사용합니다. 전체 워크플로를 처리합니다. 패턴 정보를 수집하고 올바른 템플릿 구조로 Markdown 파일을 생성하며 모든 상호 참조 페이지(TOC.md, overview.md)를 업데이트합니다.
source-git-commit: ed8928687806b619e95d8d320478d27c13722a80
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---


# 사용 사례 패턴 빌더

이 스킬은 Adobe Experience Platform 블루프린트 저장소의 새 사용 사례 패턴을 만드는 데 도움이 됩니다. 이 워크플로우는 사용자로부터 패턴 정보를 수집하고, 올바른 템플릿 구조로 Markdown 콘텐츠 파일을 생성하고, 새 패턴을 검색할 수 있도록 모든 상호 참조 페이지를 업데이트하는 전체 워크플로우를 처리합니다.

시작하기 전에 전체 템플릿 구조와 업데이트할 페이지의 체크리스트에 대한 다음 참조 파일을 읽으십시오.

- `references/pattern-template.md` — 자리 표시자 값이 있는 전체 Markdown 템플릿
- `references/pages-to-update.md` — 패턴을 추가할 때 업데이트해야 하는 페이지의 체크리스트

## 1단계: 정보 수집

파일을 생성하기 전에 사용자를 인터뷰하여 필요한 모든 정보를 수집합니다. 다음을 요청하고 모든 항목이 제공되거나 명시적으로 연기될 때까지 콘텐츠 생성을 진행하지 마십시오.

### 필수 정보

1. **패턴 이름** — 사람이 읽을 수 있는 제목(예: &quot;이벤트 트리거 메시지&quot;).

2. **범주** — 다음 중 정확히 하나:
   - `audience-building-activation`
   - `personalization`
   - `campaign-management-orchestration`
   - `analysis`
   - `conversational-experience`

3. **기본 기능 설명** — 이 패턴의 역할을 설명하는 한 문장입니다(개요 테이블 및 프론트마클 설명에 사용됨).

4. **핵심 Adobe 솔루션** — 이 패턴의 중심인 Adobe 제품입니다. Journey Optimizer, Real-Time Customer Data Platform, Experience Platform, Customer Journey Analytics, Brand Concierge, Journey Optimizer B2B edition, Real-Time CDP B2B edition 또는 기타 중에서 적절히 선택하십시오.

5. **함수 체인 단계** — `>`로 구분된 패턴의 실행 흐름을 설명하는 3~6개의 순차적 단계입니다. 예: &quot;이벤트 수집 > 여정 항목 > 조건 평가 > 메시지 게재 > 보고&quot;.

6. **지원되는 비즈니스 목표** — `/help/blueprints/business-objectives/`에 있는 기존 집합에서 하나 이상의 비즈니스 목표. 각 속성에는 목표 이름, 범주 하위 폴더 및 파일 이름이 포함되어야 합니다. 콘텐츠를 생성하기 전에 참조된 파일이 있는지 확인하십시오.

7. **전술적 사용 사례 예** — 이 패턴을 다양한 비즈니스 컨텍스트에 적용하는 방법을 설명하는 글머리 기호 시나리오가 6~10개 있습니다. 각 시나리오에는 굵은 시나리오 이름 뒤에 설명이 있어야 합니다.

8. **KPI** — KPI(이름), 설명(측정 항목), 측정(공식 또는 접근 방식)의 세 가지 열이 있는 테이블입니다.

9. **구현 옵션** — 2~4개의 구현 옵션. 각 옵션에 대해 다음을 수집합니다.
   - 옵션 이름
   - (이 옵션을 사용해야 하는 경우)에 가장 적합합니다.
   - 작동 방식(2~4개 단락)
   - 주요 고려 사항(글머리 기호 목록)
   - 장점(글머리 기호 목록)
   - 제한 사항(글머리 기호 목록)
   - Experience League 링크(관련 설명서의 URL)

### 선택 사항이지만 권장됨

- 사용 사례 개요 단락(3~5개 단락). 제공되지 않을 경우 다른 정보에서 초안 작성
- 각 Adobe 앱의 역할에 대한 설명이 포함된 애플리케이션 목록
- 기본 함수 테이블(함수, 상태, 제자리에 있어야 하는 항목, Experience League 참조)
- 지원 함수 테이블(함수, 상태, 중요한 이유, Experience League 참조)
- 응용 프로그램 함수 테이블(응용 프로그램당 하나, 함수, 구현 단계, 설명 포함)
- 사전 요구 사항 체크리스트

사용자가 선택적 항목을 제공하지 않는 경우 패턴 카테고리, 솔루션 및 함수 체인을 기반으로 적절한 기본값을 생성합니다.

## 2단계: 컨텐츠 생성

다음 경로에서 패턴 Markdown 파일을 생성합니다.

```
/help/blueprints/use-case-patterns/{category}/{kebab-case-pattern-name}.md
```

파일 이름은 패턴 이름에서 파생된 kebab-case를 사용해야 합니다. 예를 들어 &quot;이벤트가 트리거된 메시징&quot;은 `event-triggered-messaging.md`이 됩니다.

`references/pattern-template.md`의 템플릿을 사용하고 수집된 정보로 모든 자리 표시자 값을 채우십시오. 생성된 파일은 템플릿의 모든 섹션을 포함해야 합니다.

1. **YAML 프론트메터** — 제목, 설명, 솔루션(쉼표로 구분), exl-id(`xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`와(과) 같은 UUID 자리 표시자 생성 — 게시 팀이 실제 자리 표시자를 할당함).

2. **섹션 열기** — `# {Pattern name}` 제목 뒤에 소개 단락이 있고 &quot;이 안내서를 사용하여 이해하십시오...&quot; 문장.

3. **사용 사례 개요** — 패턴 범위, 적용 시, 수행할 작업과 수행할 수 없는 작업, 일반적인 이해 당사자를 설명하는 3~5개 단락입니다.

4. **주요 비즈니스 목표** - 각 목표는 간단한 설명과 KPI 요약 행이 있는 연결된 머리글입니다.

5. **전략 사용 사례 예** — 글머리 기호 6-10개 시나리오 목록입니다.

6. **주요 성능 지표** - KPI, 설명, 측정 열이 있는 테이블.

7. **사용 사례 패턴** — 설명 단락 및 함수 체인입니다.

8. **응용 프로그램** — 서식 및 설명이 `[!DNL ...]`인 Adobe 응용 프로그램 목록입니다.

9. **기본 함수** — 열이 있는 테이블: 기본 함수, 상태, 배치되어야 하는 항목, Experience League 참조. 상태 값: 필수, 적절히 가정, 해당 사항 없음.

10. **지원 함수** — 열이 있는 표: 지원 함수, 상태, 중요한 이유, Experience League 참조. 상태 값: 권장, 포함, 해당되지 않음.

11. **응용 프로그램 함수** — 열이 있는 응용 프로그램당 하나의 테이블(함수, 구현 단계, 설명).

12. **필수 구성 요소** — `- [ ]` 구문을 사용하는 체크리스트입니다.

13. **구현 옵션** — 2~4개의 세부 옵션(각각 최상의 방법, 작동 방식, 주요 고려 사항, 장점, 제한 사항 및 Experience League 링크가 있음).

14. **옵션 비교** — 끝에 있는 요약 비교 표입니다.

## 3단계: 상호 참조 업데이트

패턴 파일을 생성한 후 다음 파일을 업데이트합니다. 자세한 검사 목록은 `references/pages-to-update.md`을(를) 참조하십시오.

### TOC.md

**파일:** `/help/blueprints/TOC.md`

올바른 범주 섹션 아래에 새 항목을 추가합니다. 범주는 다음 목차 섹션에 매핑됩니다.

| 카테고리 슬러그 | 목차 섹션 제목 |
| --- | --- |
| `audience-building-activation` | `+ Audience Building & Activation{#audience-building-activation}` |
| `personalization` | `+ Personalization{#personalization-patterns}` |
| `campaign-management-orchestration` | `+ Campaign Management & Orchestration{#campaign-orchestration-patterns}` |
| `analysis` | `+ Analysis{#analysis-patterns}` |
| `conversational-experience` | `+ Conversational Experience{#conversational-experience-patterns}` |

항목 형식은 다음과 같습니다.

```
    + [{{Pattern Title}}](/help/blueprints/use-case-patterns/{{category}}/{{filename}}.md)
```

일치하는 섹션의 마지막 기존 항목 뒤에 새 항목을 추가합니다. 정확한 들여쓰기(`+` 앞에 4개의 공백)를 유지합니다.

### 개요 페이지

**파일:** `/help/blueprints/use-case-patterns/overview.md`

새 행을 올바른 범주 테이블에 추가합니다. 형식은 다음과 같습니다.

```
| [{{Pattern Title}}]({{category}}/{{filename}}.md) | {{Primary capability description}} | [!DNL {{Solution1}}], [!DNL {{Solution2}}] |
```

일치하는 범주 테이블에서 마지막 기존 행 뒤에 새 행을 추가합니다.

## 4단계: 유효성 검사

모든 파일을 만들고 업데이트한 후 다음을 확인하십시오.

1. **비즈니스 목표 링크** — 패턴 파일의 모든 비즈니스 목표 링크는 `/help/blueprints/business-objectives/`에 있는 기존 파일을 가리킵니다. glob 또는 read 를 사용하여 각 대상 파일이 있는지 확인합니다.

2. **목차 항목 배치** — 새 목차 항목이 올바른 범주 섹션 내에 있으며 올바른 들여쓰기 및 경로 형식을 사용합니다.

3. **개요 테이블 행** — 새 개요 행은 올바른 범주 테이블에 있으며 기존 행과 동일한 열 형식을 따릅니다.

4. **파일 이름 지정** — 패턴 파일 이름은 kebab-case를 사용하며 TOC.md 및 overview.md 모두에서 참조된 경로와 일치합니다.

5. **프론트메일 완성도** — 패턴 파일에는 YAML 프론트메일의 제목, 설명, 솔루션 및 exl-id가 포함됩니다.

6. **Experience League 링크** — 모든 Experience League URL이 올바른지 확인합니다(`https://experienceleague.adobe.com/ko`(으)로 시작).

사용자에게 유효성 검사 실패를 보고하고 이를 수정한 후에 작업 완료를 고려하십시오.

## 메모

- 기존 패턴 파일의 규칙에 따라 표 및 본문에서 Adobe 제품 이름에 항상 `[!DNL ...]` 구문을 사용하십시오.
- Frontmatter의 `exl-id`은(는) 자리 표시자 UUID여야 합니다. 게시 파이프라인은 실제 값을 할당합니다.
- 여러 패턴을 한 번에 만들려는 경우 각 패턴에 대해 단계 2-4를 반복하되 단계 1의 모든 정보를 수집합니다.
- 위의 목록에 없는 새 카테고리가 필요한 경우 TOC.md 및 overview.md에 새 섹션이 생성되어야 한다고 사용자에게 경고하고 이를 별도의 단계로 처리합니다.
