---
source-git-commit: a632042b3a7434dd88f52804e15e30fa06057e3b
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---
# Experience League 에이전트 메모리

## 이 저장소의 키 참조 파일- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/metadata.md` — 저장소 수준 메타데이터 기본값- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/help/blueprints/TOC.md` — 안내서 수준 메타데이터- `/Users/nick/Library/CloudStorage/OneDrive-Adobe/Documents/GitHub/blueprints-learn.en/.cursor/skills/blueprint-document-reference/reference.md` — 블루프린트 작성 패턴

## 메타데이터 규칙(전체 참조는 metadata-fields.md 참조)- 필요한 문서 프론트 문제: `title`, `description`, `exl-id`- Article Front Matter 적극 권장: `solution`- `exl-id`은(는) 유효한 UUID여야 합니다. 파일을 복사할 때 삭제/비워 둡니다(시스템에서 자동 할당).- `description`에서 &quot;방법 알아보기...&quot;를 시작해야 합니다. 또는 &quot;자세히 알아보기...&quot; Adobe 지침에 따라- SEO의 경우 최대 `title`자 ~60자; 제목의 제품 이름에는 `[!DNL ProductName]`을(를) 사용하십시오.- `solution` 값은 대/소문자를 구분하며 승인된 열거형과 일치해야 합니다(metadata-fields.md 참조).- `thumbnail: null` 또는 `thumbnail:`(빈)이(가) 모두 사용되었습니다. 비워 둘 수 있습니다.- `kt:`은(는) 레거시 필드(참조 문서 JIRA 번호)입니다. 이 저장소에는 계속 표시되며 공백은 허용됩니다.- TOC 파일 사용: `user-guide-title`, `breadcrumb-title`, `user-guide-description`, `product`, `mini-toc-levels`, `role`- 저장소 수준 `metadata.md`에서 사용하는 항목: `cloud`, `solution`, `product`, `type`, `doc-type`, `mini-toc-levels`, `git-repo`, `index`

## 이 저장소의 일반적인 패턴(blueprints-learn.en)- 대부분의 블루프린트 파일: `title`, `description`, `solution`, `exl-id`- 일부 이전 파일에는 `kt`, `thumbnail`도 포함되어 있습니다.- 일부 파일에서 `version` 사용(Campaign v8 블루프린트)- 개요 페이지에서 `doc-type: overview-page` 사용- `solution`에 종종 쉼표로 구분된 값이 여러 개 있습니다(예: `Real-Time Customer Data Platform, Campaign`).- `exl-id`이(가) 있는 경우 `solution`이(가) 없는 파일은 유효성 검사를 통과합니다.

## 이 리포지토리에 사용된 Adobe Markdown 확장- `>[!NOTE]`, `>[!TIP]`, `>[!IMPORTANT]`, `>[!WARNING]`, `>[!CAUTION]`- 탭 컨텐츠의 경우 `>[!BEGINTABS]` / `>[!TAB Name]` / `>[!ENDTABS]`- `[!DNL ProductName]` — 제품 이름에 대한 태그를 현지화하지 않음- `[!UICONTROL Label]` — UI 컨트롤 참조- `&lbrace;zoomable="yes"&rbrace;` — 이미지 확대/축소 속성- `&lbrace;width="1000"&rbrace;` — 이미지 너비 특성- `&lbrace;target="_blank"&rbrace;` — 외부 링크 대상

## 자세한 참조- 전체 메타데이터 필드 참조: `metadata-fields.md`- 저작 크롤링https://experienceleague.adobe.com/en/docs/authoring-guide-exl/using/home (Feb 26)
