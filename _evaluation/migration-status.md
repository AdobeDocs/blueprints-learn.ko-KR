---
source-git-commit: 2ed15399073fce5ebd1c2ba07b1cf70ec706452c
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 2%
---
# 사용 사례 패턴을 보여주는 마이그레이션 상태 &quot; 블루프린트

이 문서는 블루프린트 재구성 작업의 상태를 캡처하므로 세션 간에 깔끔하게 재개할 수 있습니다.

**마지막 업데이트:** 2026-09-24

## 지금 현재 위치

B2B 섹션이 더 이상 일시 중지되지 않습니다. 게시된 아키텍처 범위는 이제 대상/프로필 및 계정 활성화 페이지로 제한되며, 중단된 페이지는 카테고리 개요로 리디렉션됩니다.

**현재 상태:** B2B 아키텍처 정리가 완료되었습니다. 대상/프로필 및 계정 활성화 페이지는 아키텍처 다이어그램 카테고리에 있으며, 다른 B2B 아키텍처 페이지는 폐기되고 카테고리 개요로 리디렉션됩니다.

## 작업 접근 방식

> 아래의 작업 접근 방식은 기록적입니다. 그 후 B2B 섹션은 위에 기록된 대로 배치되었습니다.

이 세션에서 동의한 현재 작업 패턴은 다음과 같습니다.

1. **블루프린트를 그대로 유지**&quot; 사용 중단 없음. 각 블루프린트는 아키텍처 중심의 페이지로 유지됩니다.
2. **H1 직후 관련/중복 사용 사례 패턴을 가진 모든 블루프린트에 상호 연결 TIP**&#x200B;을(를) 추가합니다.

   ```
   >[!TIP]
   >This blueprint is also available as a [use case pattern](<absolute path>) under <Category>.
   ```

3. **다이어그램 마이그레이션**&quot; 블루프린트에 관련 패턴에 없는 아키텍처 다이어그램이 있는 경우 절대 경로를 통해 동일한 SVG을 참조하는 패턴에 `## Architecture` 섹션을 추가하십시오. 자산은 원래 위치에 유지됩니다(파일 복사본 없음).
4. 패턴을 다루는 블루프린트에서 **구현 단계 트리밍**. 제거할 섹션에는 일반적으로 `## Implementation steps`, `## Implementation patterns`, `## Implementation considerations`, 경우에 따라 `## Prerequisites`이(가) 포함됩니다. 블루프린트별 판단 을 사용합니다.
5. **한 명씩 걸으며**&quot; 블루프린트에 따라 변경 내용을 제안하고 사용자 승인을 받은 다음 적용합니다.

### 유니버설 규칙

- 상호 연결 TIP 문구가 일치합니다. `>This blueprint is also available as a [use case pattern](...) under <Category>.`
- 새 파일(마이그레이션 중에 만든 사용 사례 패턴) **다음을 포함하지 않음`exl-id`**&quot; Adobe 게시가 지정합니다.
- 새로 작성된 파일의 이미지 참조는 상대 경로가 아닌 절대 경로(`/help/blueprints/...`)를 사용합니다.
- 기존 페이지의 기존 `exl-id` 값이 유지됩니다.
- `redirects.csv`의 리디렉션이 `/en/docs/...` 경로를 사용하는 `source,dest` 형식을 따릅니다(`.html` 없음).

## A단계 &quot;E(초기 구조 작업)&quot; 완료

| 단계 | 결과 |
| --- | --- |
| A | `B2B Activation & Marketing` 사용 사례 패턴 범주를 만들었습니다. 기존 패턴 3개를 재배치했습니다(`b2b-audience-activation`† `b2b/account-audience-activation`, `buying-group-based-marketing`† `b2b/buying-group-marketing`, `b2b-analytics`† `b2b/account-analytics`). 3개의 리디렉션이 추가되었습니다. |
| B | 4개의 B2B 블루프린트를 `use-case-patterns/b2b/`(`marketo-data-journeys`, `paid-media-orchestration`, `campaign-intake-and-creation`, `campaign-review-and-approval`)에 복사했습니다. |
| C | B2B 이외의 블루프린트 4개(`real-time-profile-lookup`, `data-science-profile-enrichment`, `edge-profile-access`, `campaign-v8-orchestration`)를 복사했습니다. |
| D | 2개의 분할 블루프린트(`audience-sharing-with-target`, `third-party-messaging`)를 복사했습니다. |
| E | 9개의 중복 분류된 블루프린트에 교차 링크 팁이 추가되었습니다. |

6개 카테고리의 A€E: **26개 패턴** 다음의 사용 사례 패턴 합계.

## 섹션별 연습(진행 중)

이 연습에서는 사용자 검토 아래 각 블루프린트에 대해 개별적으로 교차 링크/다이어그램 마이그레이션/impl-trim 접근 방식을 적용합니다.

### oe... Audience &amp; Profile Activation > 8/8 complete

| # | 블루프린트 | 수행한 동작 |
| --- | --- | --- |
| 1 | `audience-manager.md` | 상호 연결 팁 + 다이어그램이 패턴(`anonymous-visitor-web-personalization`)으로 마이그레이션됨 + RTCDP 구현 단계 제거됨 |
| 2 | `enterprise-destinations.md` | 상호 연결 팁 + 다이어그램을 패턴(`audience-activation-to-destinations`)으로 마이그레이션했습니다. |
| 3 | `advertising-activation.md` | Impl 단계가 제거됨 (99 †&#39; 35 라인) |
| 4 | `customer-activity.md` | Impl 단계가 제거됨 (51 †&#39; 40 라인) |
| 5 | `data-science.md` | Impl 고려 사항이 제거됨 (46 †&#39; 40 줄) |
| 6 | `real-time-lookup.md` | Prereqs + impl 패턴/단계/고려 사항 제거(156†&#39; 73줄) |
| 7 | `segment-match.md` | **변경 내용 없음**(사용자가 현재 상태로 남도록 선택됨) |
| 8 | `rtcdp-target.md` | Impl 패턴 + 고려 사항 제거(99†&#39; 74 라인) |

### &quot;B2B 활성화 및 마케팅&quot; 1/10 진행 중

| # | 블루프린트 | 상태 |
| --- | --- | --- |
| 1 | `b2b/overview.md` | 완료됨 - B2B 범주 개요 업데이트됨 |
| 2 | `b2b/b2bactivation.md` | 중단됨 - 아키텍처 다이어그램 대상자/프로필 페이지로 대체됨 |
| 3 | `b2b/b2b-account-activation.md` | 유지 - 아키텍처-다이어그램 B2B 카테고리로 마이그레이션됨 |
| 4 | `b2b/b2b-buying-group-journeys.md` | 중단됨 |
| 5 | `b2b/b2b-journeys-with-marketo.md` | 중단됨 |
| 6 | `b2b/ajo-b2b-paid-media-controller.md` | 중단됨 |
| 7 | `b2b/marketo-engage-and-workfront-integration-blueprint/overview.md` | 중단됨 |
| 8 | `b2b/marketo-engage-and-workfront-integration-blueprint/intake-and-create.md` | 중단됨 |
| 9 | `b2b/marketo-engage-and-workfront-integration-blueprint/review-and-approve-blueprint.md` | 중단됨 |
| 10 | `b2b/marketo-engage-and-workfront-integration-blueprint/customer-success-stories.md` | 중단됨 |

### 아시 Customer Journey Analytics &lt; € &quot; 0/5 아직 시작되지 않음

파일: `overview.md`, `b2b-cja.md`(E단계 복제, 교차 링크 추가), `cja-rtcdp.md`(Group 2&quot;에서 `customer-analytics-insight-generation`에 대한 교차 링크 권장), `cja-ajo.md`(Group 2&quot;와 동일), `analysis.md`(Group 3, experience-platform/로 재배치 가능).

### 고객 여정 &quot; 폐기 정리 완료, 보존된 페이지 마이그레이션 보류 중

파일: `overview.md`, `journey-optimizer/`(4개 파일: 개요, 여정 [단계 E], 캠페인 [단계 E], 타사 메시징 [단계 D]), `campaign-v8/`(3개 파일: 개요 [단계 C], rtcdp-and-v8, ajo-and-v8). `decision-management/` 및 `campaign-v7/`이(가) 완전히 중단되었습니다. 이전 항목은 감사에 남아 있으며 URL은 승인된 개요 페이지로 리디렉션됩니다.

### 아시 Experience Platform &lt; € &quot; 0/6 아직 시작되지 않음

파일: `experience-cloud.md`, `platform-applications.md`, `platform-data-flow.md`, `guardrails.md`, `deployment/websdk.md`, `deployment/appsdk.md`. 감사에서 모두 0개의 패턴 신호를 사용하여 다이어그램 전용으로 점수가 매겨졌습니다. **모든 &quot;변경 내용 없음&quot;**&quot; 사용 사례 패턴이 겹치지 않는 기본 아키텍처일 수 있습니다.

의사 결정 관리 및 Campaign v7 종료 의사 결정이 완료되었습니다. 관련 미해결 질문
은(는) 기록 전용이며 나머지 마이그레이션 작업을 차단해서는 안 됩니다.

## 참조 파일

| 파일 | 목적 |
| --- | --- |
| [blueprint-audit.md](blueprint-audit.md) | 권장 사항이 있는 블루프린트당 감사 테이블(43행) |
| [rubric.md](rubric.md) | 블루프린트를 분류하는 데 사용되는 채점 규칙 |
| [migration-redirects.csv](migration-redirects.csv) | 마이그레이션에서 스테이징된 리디렉션 |
| [redirects.csv](../redirects.csv) | 정식 리디렉션 파일(단계 A에 추가된 3개 행) |

## 미해결 질문(감사 결과)

&#x200B;2. **`journey-optimizer-journeys.md`**(이)가 `event-triggered-messaging`의 불확실한 복제본으로 플래그가 지정되었습니다. 트리밍하기 전에 범위를 확인하십시오.
&#x200B;3. **`customer-journey-analytics/analysis.md`**(으)로 표시되는 콘텐츠는 CJA이 아닌 Experience Platform 쿼리 서비스에 대한 것입니다. `experience-platform/`(으)로 재배치하는 것이 좋습니다.
&#x200B;4. **`customer-success-stories.md`**(으)로 링크 전용 페이지입니다. 탐색 분류를 확인하십시오.
&#x200B;5. 완료된 B2B 아키텍처 처리로 대체된 기록 TOC 앵커 질문입니다.

## 다시 시작하는 방법

이 리포지토리에서 새 클라우드 코드 세션을 열고 다음과 같이 말합니다.

> 블루프린트 마이그레이션을 다시 시작하겠습니다. `_evaluation/migration-status.md`을(를) 읽어 중지된 위치를 확인하세요.

B2B 아키텍처 정리가 완료되었습니다. 유효성 검사 후 다음으로 계획된 아키텍처 범주를 계속 진행합니다.
