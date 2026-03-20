---
source-git-commit: ef1c207922c1079117d8bd255dbfa32a1527b014
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---
# 사용 사례 카탈로그 행 템플릿

## 행 형식

사용 사례 카탈로그 테이블의 각 행은 다음과 같은 정확한 형식을 따릅니다.

```
| <img src="assets/use-case-icons/{industry}/icon-{kebab-name}.png" alt="{Alt Text}" width="40"> | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

### 아이콘이 없는 행(아이콘을 아직 사용할 수 없을 때 사용)

```
| | [{Use Case Title}]({industry}/{industry}-overview.md#{heading-anchor}) | {One-sentence description} | [!BADGE {Maturity}]{type={Type}} | [{Pattern Name}](/help/blueprints/use-case-patterns/{category}/{pattern-file}.md) |
```

## 필드 참조

| 필드 | 형식 | 예 |
| --- | --- | --- |
| 산업 | kebab-대/소문자 디렉터리 이름 | 소매, 금융 서비스, 여행 접대 |
| kebab-name | kebab-대/소문자 아이콘 사용 사례 이름 | 포기한 장바구니, 리드 육성 |
| 대체 텍스트 | 제목 대/소문자, 짧음 | 포기한 장바구니, 리드 육성 |
| 머리글 앵커 | kebab-개요의 ## 제목의 대소문자 | 장바구니-이메일 복구 중단 |
| 완성도 + 유형 | 배지 구문 | `[!BADGE Foundational]{type=Neutral}`, `[!BADGE Emerging]{type=Informative}`, `[!BADGE Advanced]{type=Caution}` |

## 카탈로그의 업계 탭 마커

카탈로그 파일은 다음 탭 구조를 사용합니다.

- `>[!TAB Retail]`
- `>[!TAB Automotive]`
- `>[!TAB Financial Services]`
- `>[!TAB Healthcare]`
- `>[!TAB Insurance]`
- `>[!TAB Media & Entertainment]`
- `>[!TAB Telecommunications]`
- `>[!TAB Travel & Hospitality]`
- `>[!TAB B2B]`

## 탭 내에서 순서 지정

행은 완성도 수준별로 정렬됩니다.

1. **기본**&#x200B;행 먼저(형식=Neutral)
2. **시작**&#x200B;개 행 초(유형=정보)
3. 마지막 **고급** 행(유형=주의)

동일한 완성도 수준 내에서 해당 그룹의 끝에 새 행을 추가합니다.
