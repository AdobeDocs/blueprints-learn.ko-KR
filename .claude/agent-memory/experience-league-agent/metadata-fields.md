---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---
# Adobe Experience League — 승인된 메타데이터 필드 참조

*출처: Adobe ExSourced 작성 안내서(크롤링 2006년 2월 26일) + 블루프린트-학습.en*

&#x200B;---

## 메타데이터 계층

이 순서로 메타데이터 캐스케이드(문서가 TOC를 재정의함, TOC가 저장소를 재정의함):
1. 제1조 문제(최우선)
2. 사용 안내서의 TOC.md
3. 저장소 루트의 metadata.md(가장 낮은 우선 순위)

&#x200B;---

## 문서 수준 필드

### 필수

| 필드 | 설명 | 형식/제한 |
|-------|-------------|----------------------|
| `title` | SEO 페이지 제목입니다. 검색 결과에 나타납니다. | 최대 60자, 제목 대/소문자, 제품 이름에 `[!DNL Product]`을(를) 사용, 의도하지 않은 경우 H1을 정확히 복제하지 않음 |
| `description` | 검색 엔진 및 ExL 권장 사항에 대한 Meta 설명. | 150-160자. 이상적으로 &quot;방법 알아보기...&quot;를 시작합니다. 또는 &quot;자세히 알아보기...&quot;, 누락/null인 경우 유효성 검사가 실패합니다. |
| `exl-id` | 시스템에서 할당한 고유 식별자. 콘텐츠 추적에 사용됩니다. | UUID 형식(예: `70573eb9-cd69-4fe6-b2ae-dae81665a308`); **파일을 복사할 때 삭제** — 자동 할당됩니다. 파일 간에 복제되지 않습니다. |

### 적극 권장

| 필드 | 설명 | 유효한 값 |
|-------|-------------|--------------|
| `solution` | 이 문서에는 Adobe 제품이 포함됩니다. ExL 검색/필터링 및 콘텐츠 권장 사항에 사용됩니다. | 쉼표로 구분, 대/소문자를 구분, 승인된 열거와 일치해야 함(아래 유효한 솔루션 값 참조) |

### 선택 사항 — 공통

| 필드 | 설명 | 유효한 값/참고 사항 |
|-------|-------------|----------------------|
| `kt` | 기존 지식-문서 JIRA 번호. 분석 추적에 사용됩니다. | 정수(예: `7207`), 공백 허용 가능, `null` 허용 가능 |
| `thumbnail` | 권장 사항/분석에 대한 썸네일 이미지 참조. | 파일 이름 문자열 또는 `null` 또는 비어 있음 |
| `version` | 제품 버전 필터. 주로 AEM 및 Campaign 블루프린트에 사용됩니다. | E.g. `Campaign v8`, `Campaign v8 Client Console`; version.yml과 일치해야 함 |
| `doc-type` | 저장소/분석에 사용되는 콘텐츠 분류. | `blueprint`, `overview-page`, `Video`, `Tutorial`, `Troubleshooting`(소문자 기본 설정) |
| `feature` | ExL 페이지에서 &quot;주제&quot;로 표시된 주제 태그. | 기사당 1-2, 제목 케이스, feature.yml과 일치해야 함, 쉼표로 구분 |
| `feature-set` | 기능 검증을 위한 상위 응용 프로그램입니다. | feature.yml 값과 일치해야 함 |
| `role` | 타겟 대상자 역할. ExL에서 &quot;Created for&quot;으로 표시됨. | `Admin`, `Architect`, `Data Architect`, `Data Engineer`, `Developer`, `Leader`, `User` |
| `level` | 사용자 경험 수준. ExL에서 &quot;Created for&quot;으로 표시됨. | `Beginner`, `Intermediate`, `Experienced`(제목 대/소문자) |
| `topic` | 검색/필터링에 대한 제품 간 주제. | 제목 대/소문자, topic.yml과 일치해야 함, 쉼표로 구분 |
| `type` | 가이드 분류. | `Documentation`(기본값), `Tutorial`, `Troubleshooting` |
| `last-substantial-update` | &quot;새로운 기능&quot; 위젯에서 컨텐츠를 표시합니다. | 형식: `YYYY-MM-DD` |
| `hide` | 모든 검색 및 권장 사항에서 페이지를 제외합니다. 또한 색인을 아니요로 설정합니다. | `yes` 또는 `no` |
| `hidefromtoc` | 목차 탐색에서 제거되지만 직접 링크를 통해 페이지에 계속 액세스할 수 있습니다. | `yes` 또는 `no` |
| `index` | 외부 검색/사이트 맵에 페이지를 표시할지 여부를 제어합니다. | `yes`/`no` 또는 `y`/`n`; 기본값: `no`(인덱싱됨) |
| `recommendations` | &quot;이 기능에 대한 추가 도움말&quot; 위젯 동작을 제어합니다. | `noDisplay`(위젯 표시 방지), `noCatalog`(권장 사항 풀에서 제외) |
| `internal` | 페이지를 Adobe 내부 전용으로 표시합니다. 내부 링크 플래그 지정을 방지합니다. | `yes` |
| `short-description` | ExL 랜딩 페이지에 대한 압축된 설명입니다. 생략하면 `description`을(를) 사용합니다. | 한 문장, 최대 20단어 |
| `activity` | 페이지 사용 분류. | `understand`, `implement`, `troubleshoot`(소문자) |
| `sub-product` | 제품 하위 구성 요소. 유효한 열거형에 대해 솔루션 팀과 협력합니다. | 소문자(예: `search`, `assets`, `sites`) |
| `team` | 분석에 대한 팀 할당. | E.g. `TM` |
| `landing-page-name` | 이동 경로의 랜딩 페이지에 대한 링크입니다. | E.g. `experience-manager` |
| `landing-page-breadcrumb-title` | 랜딩 페이지 링크에 대한 탐색 표시 텍스트입니다. | E.g. `AEM` |
| `auto-video-transcripts` | 기본적으로 비디오 트랜스크립트를 활성화합니다. | `true` |
| `badgeType` | 콘텐츠 상태에 대한 배지. | 다양합니다. 예: `informative`, `positive` |
| `badgePremium` | Premium 배지 표시기. | Adobe 배지 사양별 |
| `badgeLabel` | 배지 레이블 텍스트입니다. | 짧은 문자열 |
| `source-git-url` | Source 저장소 URL. | 전체 GitHub URL |
| `cloud` | 문서 수준에서 클라우드 범주 재정의. | 제목 대/소문자, cloud.yml과 일치해야 함 |

&#x200B;---

## TOC.md 필드

| 필드 | 설명 | 메모 |
|-------|-------------|-------|
| `user-guide-title` | ExL 탐색 표시 및 랜딩 페이지에 표시되는 안내서 이름. | 목차 파일에 필요 |
| `breadcrumb-title` | User-guide-title이 너무 긴 경우 탐색 표시의 가이드 이름이 짧아집니다. | 선택 사항 |
| `user-guide-description` | ExL 랜딩 페이지에 대한 안내서 요약. | 한 문장, 최대 20단어 권장 |
| `product` | 안내서에 대한 Analytics 추적. 단일 값만 | product.yml과 일치해야 합니다(유효한 제품 값 참조). |
| `mini-toc-levels` | 오른쪽 탐색 mini-TOC에 표시되는 제목 수준 수입니다. | 정수 1-6, 기본값 2 |
| `role` | 안내서의 기본 대상 역할입니다. | 아티클 `role`과(와) 동일한 값, 쉼표로 구분 |
| `index` | 안내서가 인덱싱되는지 여부입니다. | `yes`/`no` |

&#x200B;---

## 저장소 수준 metadata.md 필드

| 필드 | 메모 |
|-------|-------|
| `cloud` | 리포지토리의 모든 문서에 대한 기본 클라우드 범주 |
| `solution` | 모든 문서에 대한 기본 솔루션 |
| `product` | 분석 추적을 위한 기본 제품 |
| `type` | 기본 안내서 유형 |
| `doc-type` | 기본 문서 유형 |
| `mini-toc-levels` | 기본 mini-TOC 수준 |
| `git-repo` | GitHub 저장소 URL; &quot;이 페이지 편집&quot; 및 &quot;문제 로그&quot; 단추를 활성화합니다. |
| `index` | 기본 색인 설정 |

&#x200B;---

## 유효한 솔루션 값(대/소문자 구분)

이 리포지토리에 사용되는 일반적인 값:
- `Experience Platform`
- `Real-Time Customer Data Platform`
- `Journey Optimizer`
- `Journey Optimizer B2B Edition`
- `Customer Journey Analytics`
- `Campaign`
- `Campaign v8`
- `Campaign Classic v7`
- `Campaign Standard`
- `Audience Manager`
- `Target`
- `Analytics`
- `Data Collection`
- `Commerce`
- `Marketo Engage`
- `Experience Cloud`
- `Journey Orchestration`

여러 값: 쉼표로 구분, 예: `Real-Time Customer Data Platform, Campaign`

&#x200B;---

## 유효한 제품 값(`product` 필드 — 분석 추적)

전체 목록이 필요하면 시스템 프롬프트 를 참조하십시오. 키 값:
- `adobe experience platform` / `experience platform` / `aem`
- `adobe analytics` / `analytics` / `aa`
- `adobe journey optimizer` / `journey optimizer` / `jo`
- `adobe customer journey analytics` / `customer journey analytics` / `cja`
- `adobe real time customer data platform` / `real time cdp` / `rtcdp`
- `adobe marketo` / `marketo` / `amk`
- `adobe campaign` / `campaign` / `ac`
- `adobe target` / `target` / `at`

&#x200B;---

## 유효한 역할 값

- `Admin`
- `Architect`
- `Data Architect`
- `Data Engineer`
- `Developer`
- `Leader`
- `User`

&#x200B;---

## 주요 유효성 검사 규칙

1. 복사한 파일에 동일한 UUID가 있는 `exl-id`을(를) 그대로 유지하지 마십시오. 이 파일을 삭제하고 시스템에서 새 파일을 할당하도록 하십시오.
2. 빈/null `thumbnail` 및 `kt`은(는) 사용할 수 있습니다. 레거시 필드입니다.
3. `solution` 값은 승인된 열거형과 정확히 일치해야 합니다. 대소문자를 구분합니다.
4. 누락되거나 null인 경우 `description` 유효성 검사가 실패합니다. 항상 의미 있는 값을 입력하십시오.
5. `title` 값에 콜론, 대괄호 또는 선행 특수 문자가 포함된 경우 따옴표로 묶습니다.
6. 여러 `solution` 값은 단일 문자열 값 내에서 쉼표로 구분됩니다.
7. `product`은(는) 단일 값만 사용합니다(분석 추적의 경우). 쉼표로 구분된 값을 사용하지 마십시오.
8. 새 열거형 값을 요청하려면 &quot;콘텐츠 태그 지정&quot; 구성 요소로 UGP JIRA 티켓을 제출합니다.
