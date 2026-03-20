---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---
# 사용 사례 패턴을 추가할 때 업데이트할 페이지

새로운 사용 사례 패턴을 만들 때 패턴을 검색할 수 있고 올바르게 연결할 수 있도록 다음 페이지를 업데이트해야 합니다.

## 필수 업데이트

### 1. TOC.md
- **파일:** `/help/blueprints/TOC.md`
- **작업:** 올바른 범주 섹션 아래에 새 항목 추가
- **형식:** `    + [{{Pattern Title}}](/help/blueprints/use-case-patterns/{{category}}/{{filename}}.md)`
- 범주별 **위치:**
   - 대상 구축 및 활성화: ~47행 이후(해당 섹션의 기존 항목 이후)
   - Personalization: 줄 ~52 이후
   - Campaign Management &amp; Orchestration: 58행 이후
   - 분석: 줄 ~61 이후
   - 대화형 경험: 줄 ~63

#### 범주-목차 매핑

| 카테고리 슬러그 | 목차 섹션 제목 | 앵커 |
| --- | --- | --- |
| `audience-building-activation` | `+ Audience Building & Activation` | `{#audience-building-activation}` |
| `personalization` | `+ Personalization` | `{#personalization-patterns}` |
| `campaign-management-orchestration` | `+ Campaign Management & Orchestration` | `{#campaign-orchestration-patterns}` |
| `analysis` | `+ Analysis` | `{#analysis-patterns}` |
| `conversational-experience` | `+ Conversational Experience` | `{#conversational-experience-patterns}` |

#### 들여쓰기 규칙

- 범주 머리글에는 공백 2개 + `+`(예: `  + Personalization{#personalization-patterns}`)가 사용됩니다.
- 패턴 항목은 4개의 공백 + `+`(예: `    + [Pattern Title](path)`)을 사용합니다.

### &#x200B;2. 사용 사례 패턴 개요
- **파일:** `/help/blueprints/use-case-patterns/overview.md`
- **작업:** 새 행을 올바른 범주 테이블에 추가합니다.
- **형식:** `| [{{Pattern Title}}]({{category}}/{{filename}}.md) | {{Primary capability description}} | [!DNL {{Solution1}}], [!DNL {{Solution2}}] |`
- 개요의 **범주:**
   - 대상 구축 및 활성화(18행)
   - Personalization (29행)
   - Campaign 관리 및 오케스트레이션(40행)
   - Analysis (52행)
   - 대화 경험(61행)

#### 행 형식 예

```
| [Event-Triggered Messaging](campaign-management-orchestration/event-triggered-messaging.md) | Listen for a real-time behavioral or system event, then deliver a contextual message to the triggering profile | [!DNL Journey Optimizer], [!DNL Real-Time CDP] |
```

## 유효성 검사 목록

- [ ] 패턴 Markdown 파일이 올바른 범주 디렉터리에 생성되었습니다.
- [ ] Frontmatter에 제목, 설명, 솔루션 및 exl-id가 포함됩니다.
- [ ] TOC.md 항목이 올바른 범주 아래에 추가됨
- [ ] Overview.md 테이블 행이 올바른 범주 아래에 추가되었습니다.
- [ ] 모든 비즈니스 목표 링크는 기존 파일을 가리킵니다
- [ ] 파일에서 kebab-대/소문자 명명 규칙을 사용합니다.
- [ ] 모든 Experience League 링크가 올바른 URL입니다.
- [ ] Adobe 제품 이름은 `[!DNL ...]` 구문을 사용합니다.
- [ ] 함수 체인이 ` > ` 구분 기호 형식을 사용함
- [ ] 패턴 파일에 필요한 모든 섹션이 포함되어 있습니다(pattern-template.md 참조).
