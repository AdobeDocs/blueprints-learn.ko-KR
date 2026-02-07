---
source-git-commit: dfa21942ecf2a1db06df6f6cc945f5572811ca93
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---
# 블루프린트 문서 참조 — 세부 안내서

## 문서 유형

| 유형 | 목적 | 위치 / 예 |
|------|---------|--------------------|
| **개요/허브** | 제품 또는 영역 소개, 시나리오 블루프린트 링크 | 예: `overview.md`, `journey-optimizer-overview.md` |
| **시나리오 블루프린트** | 단일 사용 사례: 아키텍처, 단계, 보호 기능 | 예: `real-time-lookup.md`, `journey-optimizer-journeys.md` |
| **목차** | 탐색, 컨텐츠 템플릿으로 사용하지 않음 | `help/blueprints/TOC.md` |

&#x200B;---

## 전체 섹션 참조

### 제목 및 설명(전문)

- **title**: 짧고 구체적입니다. 제품 이름에 `[!DNL Product Name]`을(를) 사용합니다(예: `[!DNL Journey Optimizer]`).
- **설명**: 한 문장. 블루프린트가 표시하는 내용과 그 결과(예: &quot;웹 및 모바일 개인화를 위한 가장자리에서 실시간 고객 프로필 액세스&quot;)를 설명합니다.

### 본문

| 섹션 | 포함 시기 | 콘텐츠 지침 |
|---------|-----------------|-------------------|
| **응용 프로그램** | 시나리오 블루프린트에 항상 사용 | 관련된 Adobe 제품/솔루션의 글머리 기호 목록(예: 실시간 고객 데이터 플랫폼, 데이터 수집). |
| **사용 사례** | 항상 | 이 블루프린트가 지원하는 비즈니스/기술 사용 사례의 글머리 기호 목록입니다. |
| **필수 구성 요소** | 설정이 필요한 경우 | 제품, 하위 도메인, SDK, 구성이 있어야 합니다. Experience League에 연결하여 설정 단계를 확인하십시오. |
| **아키텍처 다이어그램** | 항상 | 단일 기본 다이어그램(SVG 권장). 일관된 스타일 사용: `style="width:90%; border:1px solid #4a4a4a" class="modal-image"`. 의미 있는 `alt` 텍스트를 입력하십시오. |
| **보호 기능** | 제품에 보호 기능이 있을 때 항상 | 공식 Experience League 보호 페이지에 대한 링크입니다. 블루프린트별 제한(예: TTL, 비율 제한)을 글머리 기호로 추가합니다. |
| **구현 패턴** | 접근 방식이 여러 개인 경우 | 각 패턴의 이름을 지정합니다(예: &quot;패턴 1: 웹 SDK을 사용한 대상 멤버십 기반&quot;). 사용 시기와 절충안에 대해 글머리 기호를 사용하십시오. |
| **구현 단계** | 경로가 정의된 시나리오 블루프린트의 경우 | 번호 매기기 목록. 각 단계: 작업이 포함된 Experience League 링크 전체 절차는 복사하지 마십시오. |
| **구현 시 고려 사항** | 중요한 주의 사항이 있을 때 | 하위 섹션(예: ID 고려 사항, 속성 기반 개인화). 글머리 기호 또는 짧은 문단입니다. 링크를 통해 깊이 있게 연결할 수 있습니다. |
| **관련 설명서** | 항상 | Experience League(및 선택적으로 developer.adobe.com)에 연결된 그룹화된 링크입니다. 아래의 &quot;Experience League 링크 그룹&quot;을 참조하십시오. |

### 개요/허브 페이지

- 제품/영역 및 블루프린트가 다루는 내용에 대한 1~2개의 단락으로 시작합니다.
- **사용 사례**: 여러 범주에 대해 `>[!BEGINTABS]`/`>[!TAB ...]`/`>[!ENDTABS]`을(를) 사용할 수 있습니다.
- **아키텍처**: 기본 다이어그램 하나.
- **블루프린트 시나리오** 또는 **통합 패턴**: 시나리오 이름, 간단한 설명 및 시나리오 블루프린트에 연결된 테이블입니다.
- **필수 구성 요소**, **보호 기능**, **관련 설명서**: 위와 같습니다. 간결하게 유지하십시오.

&#x200B;---

## Adobe Experience League - 에이전트 지침

### Experience League 참조 시기

- **제품 설명서**: 제품 작동 방식, UI 흐름, 개념
- **API**: 끝점, 매개 변수, 예제(Experience Platform, Edge 등).
- **보호 기능**: 제품 또는 서비스에 대한 공식 보호 기능 페이지입니다.
- **튜토리얼**: 단계별 지침(예: 스키마 만들기, 대상 활성화).
- **구성**: 데이터스트림, 대상, 병합 정책, ID 등

Experience League의 긴 절차를 블루프린트에 붙여넣지 마십시오. 요약 및 링크.

### URL 패턴

| 컨텐츠 유형 | 기본 URL | 예제 경로 |
|--------------|----------|--------------|
| Experience Platform 문서 | `https://experienceleague.adobe.com/docs/experience-platform/` | `.../profile/home.html`, `.../destinations/catalog/...` |
| Experience League (en) | `https://experienceleague.adobe.com/en/docs/` | `/en/`을(를) 사용하는 위와 동일한 구조입니다. |
| Journey Optimizer    | `https://experienceleague.adobe.com/docs/journey-optimizer/` | `.../using/get-started/guardrails.html` |
| 웹 SDK | `https://experienceleague.adobe.com/docs/experience-platform/web-sdk/` | `.../home.html`, `.../commands/command-responses.html` |
| Edge Network 서버 API | `https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/` | `.../overview.html`, `.../guardrails.html` |
| Mobile SDK | `https://developer.adobe.com/client-sdks/` | `.../home/`, `.../edge/adobe-journey-optimizer-decisioning/` |
| 태그 | `https://experienceleague.adobe.com/docs/experience-platform/tags/` | `.../home.html` |
| Platform 튜토리얼 | `https://experienceleague.adobe.com/docs/platform-learn/tutorials/` | `.../profiles/create-merge-policies.html` |

현재 Experience League 사이트와 일치하는 표준 경로를 사용합니다(영어 경로를 알고 있는 경우 `/en/docs/` 선호).

### Markdown으로 링크 서식 지정

- **설명 링크 텍스트**: `[Create schemas](https://experienceleague.adobe.com/...)`이(가) &quot;여기를 클릭&quot;하지 않습니다.
- **텍스트 형식의 제품 이름**: Adobe 스타일에 따라 `[!DNL Product Name]`을(를) 사용합니다(예: `[!DNL Real-time Customer Profile]`).
- **외부 링크**: 템플릿 또는 파이프라인에 필요한 경우에만 `{target="_blank"}`을(를) 추가합니다(리포지토리의 기존 블루프린트를 확인).

### 관련 설명서 - 제안된 그룹

다음 그룹을 적용할 때 사용합니다.

1. **대상 구성**(활성화/에지 개인화 블루프린트의 경우)
2. **SDK 설명서**(Web SDK, Mobile SDK, Edge Network Server API, 태그)
3. **프로필 및 세분화**(실시간 고객 프로필, 병합 정책, 세분화)
4. **튜토리얼**(플랫폼 학습 또는 제품별 단계별 안내서)
5. **제품 설명서**(기본 제품 설명서 홈 또는 주요 하위 섹션)
6. **보호 기능**(보호 기능 섹션에 없는 경우)

예:

```markdown
## Related documentation

### Destination configurations
* [Custom Personalization Connection](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization)
* [Activate audiences to edge personalization destinations](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)

### SDK documentation
* [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Edge Network Server API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)

### Profile and segmentation
* [Real-time Customer Profile](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [Profile Guardrails](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)
```

&#x200B;---

## 보고서 및 목차

- **블루프린트 콘텐츠 경로**: `help/blueprints/`(영역별 하위 폴더 포함, 예: `audience-activation/`, `customer-journeys/journey-optimizer/`).
- **Assets**: 블루프린트(예: `assets/`, `images/`) 또는 공유 폴더(예: `experience-platform/assets/`)와 함께 찾습니다.
- **TOC**: 블루프린트 페이지를 추가, 이름 변경 또는 이동할 때 `help/blueprints/TOC.md`을(를) 편집합니다. `user-guide-title`, `breadcrumb-title`, `user-guide-description`, `product`, `mini-toc-levels`, `role` 및 `+` 계층 구조를 유지합니다.

&#x200B;---

## 이 저장소의 참조 예

- **시나리오 블루프린트(긴 양식)**: `help/blueprints/audience-activation/real-time-lookup.md`
- **탭 및 테이블이 있는 개요/허브**: `help/blueprints/customer-journeys/journey-optimizer/journey-optimizer-overview.md`
- **보호 기능 중심**: `help/blueprints/experience-platform/guardrails.md`
- **탐색**: `help/blueprints/TOC.md`, `help/blueprints/overview.md`

이러한 매개 변수는 섹션 순서, 프론트메터, 다이어그램 배치 및 Experience League 링크 사용에 대한 패턴으로 사용됩니다.
