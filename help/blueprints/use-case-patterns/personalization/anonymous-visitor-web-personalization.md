---
title: 익명 방문자 웹 Personalization
description: 세션 내 행동 신호를 기반으로 미확인된 방문자에게 개인화된 웹 콘텐츠를 전달하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 126dd712603494513b71a8a6e1c4b99bdb7ff212
workflow-type: tm+mt
source-wordcount: '8076'
ht-degree: 1%

---


# 익명 방문자 웹 개인화

이 참조 플랜은 세션 내 동작 신호를 기반으로 개인화된 웹 콘텐츠를 익명(미확인) 방문자에게 제공하기 위한 구현 지침을 제공합니다. [!DNL Web SDK] 구성 및 에지 대상 정의부터 콘텐츠 전달 및 성능 보고를 통한 전체 구현 라이프사이클을 포함하며 [!DNL Adobe Journey Optimizer]&#x200B;(AJO), [!DNL Adobe Real-Time Customer Data Platform]&#x200B;(RT-CDP) 및 [!DNL Adobe Experience Platform]&#x200B;(AEP)과(와) 함께 작업하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

이 플랜을 사용하여 아키텍처를 이해하고, 구현 옵션을 평가하고, 정보에 입각한 구성 결정을 내리고, 각 구현 단계에 대한 관련 Experience League 설명서를 찾을 수 있습니다.

패턴은 제한된 데이터로 작동합니다. 즉, 동일한 장치나 쿠키를 사용한 이전 방문에서 누적된 익명 에지 프로필과 현재 세션에서 관찰할 수 있는 항목만 해당됩니다. 이렇게 하면 방문자가 계정이 없거나 인증되지 않은 funnel의 최상위 개인화에 적합합니다.

## 사용 사례 개요

익명 방문자 웹 Personalization은 아직 식별되지 않음(로그인하지 않음, 알려진 ID가 없음, 통합 고객 프로필로 해결할 수 없음)인 웹 사이트 방문자에게 관련성 있고 개인화된 콘텐츠를 제공해야 하는 비즈니스 요구를 해결합니다. 이러한 제한에도 불구하고 페이지 보기, 사이트에서 보낸 시간, 스크롤 깊이, 참조 소스, 지리적 위치, 장치 유형 및 UTM 캠페인 매개변수와 같은 세션 내 동작 신호를 사용하여 의미 있는 개인화를 달성할 수 있습니다.

이 패턴은 AJO의 웹 채널 표면과 코드 기반 경험을 사용하여 페이지 콘텐츠를 실시간으로 수정합니다. 방문자가 사이트를 탐색할 때 1초 미만의 지연 시간으로 결정을 내려야 하므로 Edge 세그먼테이션은 기본 평가 방법입니다. [!DNL Web SDK]은(는) 동작 신호를 수집하여 [!DNL AEP Edge Network]&#x200B;(으)로 보냅니다. 여기서 에지 평가 대상 규칙은 전달할 콘텐츠 변형을 결정합니다.

전체 통합 프로필 및 세그먼트 멤버십을 활용하는 알려진 방문자 웹/앱 개인화와 달리, 이 패턴은 현재 세션에서 관찰할 수 있는 데이터와 방문자의 ECID([!DNL Experience Cloud ID])와 연결된 모든 익명 에지 프로필로 제한됩니다. 이러한 구분은 구현 계획에 중요합니다. 개인화에 사용할 수 있는 동작 신호는 [!DNL Web SDK]이(가) 캡처하는 내용과 쿠키 기반 ECID를 통해 세션 간 Edge 프로필 저장소에서 지속되는 것으로 제한됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

**[웹 사이트 참여 늘리기](../../business-objectives/acquisition-growth/increase-website-engagement.md)**

익명 방문자 신호에 맞춘 적절한 경험을 통해 사이트에서 보낸 시간, 세션당 페이지 수 및 웹 콘텐츠와의 상호 작용을 개선합니다.

| KPI |
| --- |
| Time On (웹) 페이지 |
| 참여 |
| 전환율 |

**[개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**

아직 자신을 식별하지 않은 방문자에게도 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 콘텐츠, 오퍼 및 메시지를 맞춤화할 수 있습니다.

| KPI |
| --- |
| 참여 |
| 전환율 |
| 고객 만족도(CSAT) |

**[전환율 증가](../../business-objectives/revenue-monetization/increase-conversion-rates.md)**

행동 컨텍스트에 따라 가장 관련성이 높은 콘텐츠를 제시하여 구매, 등록 또는 양식 제출과 같은 원하는 작업을 완료하는 방문자 및 잠재 고객의 비율을 향상시킵니다.

| KPI |
| --- |
| 전환율 |
| 잠재 고객 전환 |
| 잠재 고객당 비용 |

## 예시 전술 사용 사례

다음 예제는 이 패턴을 적용할 수 있는 특정 시나리오를 보여 줍니다.

- **조회 소스에 기반한 랜딩 페이지 헤드라인 A/B 테스트** - Google, 소셜 미디어 또는 직접 트래픽에서 도착하는 방문자에 대해 다양한 헤드라인을 테스트하여 획득 채널별 참여를 최적화합니다.
- **찾아보기 동작에 따른 카테고리 친화성 권장 사항** - 검색 및 전환을 늘리기 위해 현재 세션에서 표시된 페이지에 따라 제품 또는 콘텐츠 권장 사항을 표시합니다.
- **떠나려는 방문자를 위한 종료 의도 오퍼** - 동작 신호가 방문자가 사이트를 포기하려는 것으로 표시되면 프로모션 오퍼나 리드 캡처 양식을 제공합니다.
- **지리적 타겟팅 프로모션 배너** - 방문자의 지리적 위치를 기반으로 위치별 프로모션, 스토어 로케이터 콘텐츠 또는 지역 오퍼를 표시합니다
- **장치별 콘텐츠 레이아웃 최적화** - 방문자가 데스크톱, 태블릿 또는 모바일에 있는지 여부에 따라 콘텐츠 레이아웃, 이미지 크기 및 CTA 배치를 조정합니다
- **신규 방문자와 재방문자 환영 메시지 비교** - 세션 간 ECID 지속성을 사용하여 최초 방문자와 재방문자 경험을 구별합니다.
- **현재 세션에서 본 페이지를 기반으로 한 콘텐츠 권장 사항** - 방문자가 이미 본 페이지를 기반으로 관련 문서, 제품 또는 리소스를 동적으로 표시합니다
- **UTM 캠페인 매개 변수를 기반으로 한 동적 영웅 배너** — 추천 캠페인의 메시지 또는 크리에이티브와 일치하도록 영웅 배너를 개인화합니다

## 주요 성과 지표

다음 KPI를 사용하여 이 사용 사례 패턴의 효과를 측정합니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| Personalization 노출률 | 개인화된 콘텐츠가 게재된 적격한 페이지 조회수의 비율 | AJO 캠페인 보고서: 노출 횟수 / 총 페이지 보기 수 |
| 클릭스루 비율(CTR) | 클릭으로 이어지는 개인화된 콘텐츠 노출 비율입니다. | AJO 캠페인 보고서: 클릭수 / 노출수 |
| 참여 상승도 | 페이지, 세션당 페이지 수 또는 스크롤 깊이가 개인화된 컨텐츠와 기본 컨텐츠의 시간 증가 | CJA 작업 공간 비교: 개인화된 집단 대 제어 |
| 전환율 | 원하는 작업을 완료한 개인화된 콘텐츠에 노출된 방문자의 비율 | CJA funnel 분석: 노출 > 상호 작용 > 전환 |
| 바운스 비율 감소 | 개인화된 콘텐츠를 수신한 방문자의 단일 페이지 세션 수 감소 | CJA 세션 분석: 개인화된 횟수와 기본값에 대한 바운스 비율 델타 |
| 실험 성공률 | 통계적으로 유의한 승자를 생성하는 A/B 테스트의 백분율 | AJO 실험 보고서: 신뢰 임계값에 도달하는 실험 |

## 사용 사례 패턴

다음은 이 사용 사례의 핵심 패턴 및 함수 체인에 대해 설명합니다.

**익명 방문자 웹 Personalization**

AJO 웹 채널을 통해 미확인된 방문자에 대한 세션 내 행동 신호를 기반으로 개인화된 콘텐츠를 제공합니다.

**함수 체인:** 웹 표면 구성 > 행동 규칙 평가 > 콘텐츠 게재 > 노출 추적 > 보고

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Adobe Journey Optimizer](AJO)** — 웹 채널 표면 구성, 콘텐츠 작성(웹 및 코드 기반 경험), 캠페인 실행, 콘텐츠 실험(A/B 테스트), 의사 결정(동적 콘텐츠 선택) 및 보고
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** - 세션 내 동작 신호를 기반으로 실시간 대상 평가를 위한 Edge 세그멘테이션, 익명 Edge 프로필 관리
- **[!DNL Adobe Experience Platform](AEP)** — 동작 신호 수집의 경우 [!DNL Web SDK], 실시간 데이터 라우팅 및 개인화 전달의 경우 [!DNL Edge Network], 데이터스트림 구성

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | 웹 채널 권한이 구성된 AJO 샌드박스 입니다. [!DNL Web SDK] 구현 팀에 부여된 구현 권한 및 데이터스트림 액세스 웹 채널 구성, 대상자 관리 및 캠페인 실행을 허용하는 역할이 규정된 사용자. | [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 웹 행동 신호(페이지 보기, 클릭 수, 스크롤 깊이, 참조 데이터, UTM 매개 변수)를 캡처하는 경험 이벤트 스키마. 실시간 평가를 지원하려면 스키마에 표준 웹 인터랙션 필드 그룹이 포함되어야 하며 에지 프로필에 대해 활성화되어야 합니다. 해당 데이터 세트를 만들고 프로필이 활성화되어야 합니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home) |
| 데이터 소스 및 수집 | 필수 | [!DNL AEP Edge Network]&#x200B;(으)로 데이터를 라우팅하도록 구성된 데이터 스트림을 사용하여 모든 대상 웹 속성에 [!DNL Web SDK]을(를) 구현해야 합니다. 데이터 스트림에는 [!DNL Adobe Experience Platform] 및 [!DNL Adobe Journey Optimizer] 서비스가 활성화되어 있어야 합니다. 이는 중요한 종속성입니다. [!DNL Web SDK]이(가) 없으면 동작 신호 수집이나 경험 전달을 수행할 수 없습니다. | [Web SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) |
| ID 및 프로필 구성 | 필수 | 익명 방문자에 대한 기본 ID 네임스페이스로 구성된 ECID([!DNL Experience Cloud ID]). 가장자리에서 익명 프로필 데이터를 확인하려면 `isActiveOnEdge: true`(으)로 Edge 병합 정책을 구성해야 합니다. 샌드박스당 하나의 병합 정책만 에지에서 활성화할 수 있습니다. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) |
| 대상 정의 및 세분화 | 필수 | 세션 내 행동 신호를 기반으로 정의된 Edge 평가 대상 세그먼트. Edge 세그먼테이션은 1초 미만의 평가 지연에 필수입니다. 세그먼트 규칙은 에지 적격 세그먼트 규칙 표현식(단순 속성 확인 및 세그먼트 멤버십 — 시계열 쿼리나 복잡한 집계 없음)만 사용해야 합니다. | [Edge 세그멘테이션](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 해당 사항 없음 | 집계할 최소 내역 프로필 데이터가 있으므로 익명 방문자의 값이 제한됩니다. Edge 프로필이 여러 세션에서 이전 익명 방문의 의미 있는 행동 데이터를 수집하는 경우 적용할 수 있습니다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | 스토리지를 관리하고 개인정보 보호 요구 사항을 준수하려면 익명 에지 프로필에 대해 익명 프로필 만료를 구성해야 합니다. ECID 전용 프로필은 14일에서 365일 사이에 만료되도록 설정할 수 있습니다. 쿠키 동의 정책은 행동 데이터 수집에 적용되어야 합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 행동 데이터의 거버넌스 레이블은 특히 지역 타겟팅(S2 중요 지역 레이블) 및 디바이스 기반 개인화에 대한 규정 준수를 보장합니다. 레이블은 제한된 행동 데이터가 승인되지 않은 개인화 컨텍스트에서 사용되지 않도록 합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home) |
| 모니터링 및 가시성 | 추천 | [!DNL Edge Network] 및 [!DNL Web SDK] 데이터 흐름 모니터링은 개인화 게재 문제를 탐지하는 데 도움이 됩니다. 데이터 스트림 오류, 수집 오류 및 에지 전달 예외 항목에 대한 경고를 구성합니다. 개인화 실패로 인해 방문자 경험이 저하되는 프로덕션 배포에 매우 중요합니다. | [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | Personalization 성능 보고는 기능 체인의 일부입니다(5단계). CJA의 익명 방문자 개인화 효과 분석을 통해 AJO 기본 보고서에서 제공하는 것 이상으로 심도 있는 funnel 분석, 집단 비교 및 전환 영향 측정을 수행할 수 있습니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer]&#x200B;(AJO)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 채널 구성 | 1단계: 웹 표면 구성 | 대상 웹 속성에서 개인화된 콘텐츠가 전달될 위치를 정의하는 웹 채널 표면 구성 |
| 메시지 작성 | 3단계: 콘텐츠 작성 및 변형 작성 | 웹 디자이너, 코드 기반 경험 편집기 또는 콘텐츠 템플릿을 사용하여 웹 표면에 대한 개인화된 콘텐츠 변형을 작성할 수 있습니다 |
| 캠페인 실행 | 4단계: 캠페인 및 게재 구성 | 대상자, 콘텐츠 및 게재 구성을 바인딩하는 웹 캠페인 만들기 및 활성화 |
| 결정 | 3단계: 콘텐츠 작성 및 변형 작성(옵션 C) | 행동 신호를 기반으로 다이내믹 콘텐츠 선택을 위한 의사 결정 정책, 자격 규칙 및 등급 전략을 구성합니다. |
| 콘텐츠 실험 | 3단계: 콘텐츠 작성 및 변형 작성(옵션 B) | 트래픽 할당, 성공 지표 및 신뢰도 임계값을 사용하여 A/B 및 다변량 콘텐츠 실험 구성 |
| 보고 및 성능 분석 | 5단계: 보고 및 성능 분석 | 개인화 게재 지표, 변형 효과, 실험 결과 및 전환 영향 모니터링 |

### [!DNL Real-Time CDP]&#x200B;(RT-CDP)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 2단계: 행동 대상 정의 | 실시간 개인화 타깃팅을 위해 세션 내 행동 신호를 사용하여 에지 기반 대상 세그먼트를 정의하고 평가합니다 |

## 필요 조건

구현을 시작하기 전에 다음을 완료하십시오.

- [ ] [!DNL Web SDK]이(가) 페이지 보기, 클릭 수 및 관련 동작 상호 작용을 캡처하는 `sendEvent` 호출을 사용하여 모든 대상 웹 속성에 구현되었습니다.
- [ [!DNL Adobe Experience Platform] 및 [!DNL Adobe Journey Optimizer] 서비스를 사용하도록 설정한 데이터 수집 UI에서 ] 데이터 스트림이 구성되었습니다.
- [ ] 경험 이벤트 스키마가 웹 인터랙션 필드 그룹(페이지 보기 수, 참조 데이터, UTM 매개 변수, 장치 컨텍스트)과 함께 존재하며 프로필에 대해 활성화됨
- [ ] ECID ID 네임스페이스가 구성되어 있으며 웹 동작 이벤트 스키마에서 기본 ID로 지정되었습니다.
- [ ] Edge 병합 정책이 대상 샌드박스에서 `isActiveOnEdge: true`(으)로 구성되었습니다.
- [ ] AJO 웹 채널이 프로비저닝되어 target 샌드박스에서 액세스할 수 있습니다.
- [ 각 개인화 사용 사례에 대해 ]개의 콘텐츠 변형(복사, 이미지, CTA)을 디자인하고 승인합니다.
- [ ] 성공 지표가 정의되었습니다(측정을 위한 전환 또는 참여 이벤트를 구성하는 항목).
- [ 동작 데이터를 수집하기 전에 개인 정보 보호 규정을 준수하도록 웹 사이트에서 ] 쿠키 동의 메커니즘이 구현되었습니다

## 구현 옵션

이 섹션에서는 세 가지 구현 접근 방식에 대해 설명합니다. 개인화 요구 사항에 가장 적합한 옵션을 선택합니다.

### 옵션 A: 규칙 기반 웹 개인화

**추천 항목:** 지리적 타겟팅 배너, 참조 소스별 헤드라인, 장치별 레이아웃, 새 방문자와 재방문자 메시지 비교 등 간단하고 결정론적인 개인화 간단한 조건부 논리(조건 X인 경우 컨텐츠 Y 표시)로 컨텐츠 변형을 결정할 수 있는 경우 이 옵션을 선택합니다.

**작동 방식:**

규칙 기반 개인화는 에지 평가 대상 세그먼트를 사용하여 방문자에게 표시되는 콘텐츠 변형을 결정합니다. 각 대상 세그먼트는 캠페인에 정의된 조건부 규칙을 통해 특정 콘텐츠 변형에 매핑됩니다. 방문자가 페이지를 로드할 때 [!DNL Web SDK]은(는) [!DNL Edge Network]에 동작 신호를 보내 정의된 대상 규칙에 대해 방문자의 Edge 프로필을 밀리초 단위로 평가합니다. 일치하는 콘텐츠 변형이 [!DNL Edge Network] 응답에서 반환되고 페이지에서 렌더링됩니다.

이 접근 방식을 사용하려면 RT-CDP에서 고유한 대상 세그먼트(예: &quot;Google 검색의 방문자&quot;, &quot;캘리포니아에 있는 방문자&quot;, &quot;모바일 장치 방문자&quot;)를 정의하고 AJO에서 해당 콘텐츠 변형을 생성해야 합니다. 캠페인은 조건부 콘텐츠 규칙 또는 세그먼트당 별도의 캠페인을 사용하여 각 대상을 콘텐츠 변형에 바인딩합니다. AI 등급이나 트래픽 분할은 포함되지 않습니다. 대상과 콘텐츠 간의 관계는 결정적입니다.

**주요 고려 사항:**

- 에지 적격 세그먼트 규칙 표현식으로 표현할 수 있는 잘 정의된 대상 기준이 필요합니다.
- 컨텐츠 변형은 각 대상 세그먼트에 대해 미리 작성해야 합니다
- 새 개인화 규칙을 추가하려면 새 대상 세그먼트 및 콘텐츠 변형을 만들어야 합니다
- 콘텐츠 변형 효과에 대한 통계적 측정을 제공하지 않음

**장점:**

- 구현 및 이해 - 대상과 콘텐츠 간의 명확한 인과관계
- 실험 오버헤드나 트래픽 분할이 필요하지 않음
- 결정론적 동작으로 인해 테스트 및 QA가 간단합니다.
- 에지 평가가 순전히 규칙 기반이므로 지연 시간 감소
- 각 세그먼트에 대해 성과가 가장 좋은 콘텐츠를 비즈니스가 이미 알고 있을 때 잘 작동합니다

**제한 사항:**

- 개인화가 결과를 향상하는지 기본 콘텐츠를 향상하는지 여부를 측정하는 내장 메커니즘이 없습니다.
- 각 세그먼트를 표시할 콘텐츠에 대한 수동 의사 결정 필요
- 시간이 지남에 따라 조정하거나 최적화하지 않음 — 수동으로 변경할 때까지 정적 규칙
- 많은 세그먼트 및 변형으로 크기를 조정하면 구성 복잡성이 증가합니다

**Experience League:**

- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)

### 옵션 B: 실험 기반 웹 개인화

**A/B 및 다변량 테스트 — 통계적 중요도 측정이 포함된 헤드라인 변형, CTA 단추 색상, 레이아웃 대체 요소, 프로모션 오퍼 테스트**&#x200B;영구 개인화 규칙에 커밋하기 전에 성과가 가장 좋은 콘텐츠 변형을 확인해야 하는 경우 이 옵션을 선택합니다.

**작동 방식:**

실험 기반 개인화는 AJO 콘텐츠 실험을 사용하여 콘텐츠 처리 그룹에 방문자를 임의로 할당하고 정의된 성공 지표에 대해 가장 성과가 좋은 변형을 측정합니다. 트래픽은 변형 간에 분할되고(예: A/B의 경우 50/50, A/B/C의 경우 33/33/34) 통계적 중요도에 도달할 때까지 성능이 추적됩니다.

이 실험은 AJO 웹 캠페인에 임베드되어 있습니다. 방문자가 페이지를 로드할 때 [!DNL Edge Network]은(는) 구성된 트래픽 할당을 기반으로 처리 그룹에 이 페이지를 할당합니다. 방문자는 실험 기간 동안 일관되게 동일한 처리를 봅니다(구성에 따라 세션 수준 또는 방문자 수준의 지속성). 성공 지표(클릭 수, 전환 수, 참여 이벤트)는 [!DNL Web SDK]을(를) 통해 추적되고 AJO 실험 보고서에 보고됩니다.

이 옵션은 타깃팅에 대해 사전 정의된 대상 세그먼트가 필요하지 않으며, 모든 방문자(또는 타깃팅된 하위 집합)는 실험에 참여합니다. 목표는 미리 결정된 콘텐츠로 알려진 세그먼트를 타겟팅하지 않고 성과가 가장 좋은 콘텐츠를 찾는 것입니다.

**주요 고려 사항:**

- 적절한 기간 내에 통계적 중요도에 도달하려면 충분한 트래픽 볼륨이 필요합니다.
- 실험에서는 항시 유효한 신뢰 구간을 갖는 베이지안 통계적 모형을 사용한다
- 증분 리프트를 측정하려면 홀드아웃 그룹(개인화된 콘텐츠를 받지 않음)을 권장합니다
- 캠페인당 한 번에 하나의 실험만 활성화할 수 있습니다
- 실험을 수정하려면 캠페인을 중지하고 다시 시작해야 합니다

**장점:**

- 콘텐츠 변형 효과에 대한 통계적으로 엄격한 측정 제공
- 개인화 의사 결정 — 데이터 기반 컨텐츠 선택에서 추측 제거
- 진정한 증분 리프트 측정을 위한 홀드아웃 그룹 지원
- 신뢰 구간 및 승자 선언을 통한 내장 실험 보고
- 결과는 우승 변형을 식별하여 향후 규칙 기반 개인화(옵션 A)에 알릴 수 있습니다

**제한 사항:**

- 의미 있는 트래픽 볼륨이 필요합니다. 트래픽이 적은 페이지는 중요도에 도달하려면 몇 주가 걸릴 수 있습니다.
- 트래픽 분할은 일부 방문자가 테스트 기간 동안 차선적인 콘텐츠를 본다는 것을 의미합니다
- 실험 중 세그먼트별로 개인화할 수 없음(모든 방문자 또는 하위 집합이 동일하게 참여)
- 실험당 최대 10개의 처리 변형
- 지속적인 최적화 없음 — 시작과 끝을 통해 실험이 분리됨

**Experience League:**

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

### 옵션 C: 의사 결정 기반 웹 개인화

**가장 적합한 대상:** 의사 결정 정책이 세션 신호를 평가하고 적격 항목 카탈로그에서 최적의 콘텐츠를 선택하는 동적 콘텐츠 선택(범주 선호도 권장 사항, 종료 목적 오퍼, 행동 권장 사항). 콘텐츠 선택 로직이 단순 규칙에 비해 너무 복잡하거나, AI 등급 최적화를 원하거나, 적격한 콘텐츠 항목 집합이 크고 동적인 경우 이 옵션을 선택합니다.

**작동 방식:**

Decisioning 기반 개인화는 AJO Decisioning을 사용하여 동작 신호를 평가하고 관리되는 콘텐츠 항목(오퍼) 카탈로그에서 각 방문자에 대한 최상의 콘텐츠 변형을 선택합니다. 각 컨텐츠 항목에는 자격 규칙(자격 부여), 표시(각 배치에서 컨텐츠가 보이는 모양) 및 선택적 제한 조건(표시 빈도)이 있습니다. 의사 결정 정책은 배치(콘텐츠가 페이지에 표시되는 위치)를 콘텐츠 항목 컬렉션에 연결하고 등급 전략을 적용하여 최상의 옵션을 선택합니다.

방문자가 페이지를 로드할 때 [!DNL Web SDK]이(가) 결정 범위를 포함하는 [!DNL Edge Network] 요청을 보냅니다. Decisioning 엔진은 콘텐츠 항목 자격 규칙에 대해 방문자의 에지 프로필을 평가하고 등급 전략(우선 순위 기반, 공식 기반 또는 AI 등급)을 적용한 다음 우승 콘텐츠 항목을 반환합니다. 이 작업은 1초 미만의 지연 시간이 있는 에지에서 발생합니다.

순위 전략에 따라 적합한 콘텐츠 항목의 순서가 결정됩니다. 우선 순위 기반 등급은 수동으로 할당된 우선 순위 값을 사용합니다. 공식 기반 등급은 사용자 정의 표현식(예: 페이지 조회수의 최근성 가중치 부여)을 사용합니다. AI 등급 순위는 시간이 지남에 따라 선택한 성공 지표에 대해 최적화하는 기계 학습 모델을 사용하지만, 교육을 위해서는 최소 1,000개의 전환 이벤트가 필요합니다.

**주요 고려 사항:**

- 배치, 자격 규칙, 콘텐츠 항목, 대체 항목, 컬렉션, 의사 결정 정책 등 의사 결정 구성 요소를 설정해야 합니다.
- AI 등급 전략은 모델을 교육하기 위해 충분한 전환 볼륨(1,000개 이상의 이벤트)이 필요합니다
- Edge 의사 결정은 edge 프로필 스토어에서 사용할 수 있는 프로필 속성으로 제한됩니다
- 컨텐츠 항목은 Decisioning 라이브러리에서 관리 및 유지 관리되어야 합니다
- 개인화된 항목이 충족되지 않는 경우에 대해 대체 콘텐츠를 정의해야 합니다.

**장점:**

- 개별 대상자-콘텐츠 매핑 없이 대규모 콘텐츠 카탈로그로 확장
- AI 등급 전략은 관찰된 성과를 기반으로 콘텐츠 선택을 지속적으로 최적화합니다
- 자격 규칙 및 최대 가용량 제한은 콘텐츠 전달을 미세하게 제어할 수 있도록 합니다
- 대상 세그먼트로 표현하기 어려운 복잡한 비즈니스 논리 지원
- 여러 채널에서 재사용 가능 — 동일한 의사 결정 정책으로 웹, 이메일 및 모바일 개인화를 지원할 수 있습니다.

**제한 사항:**

- 구현 복잡성 증가 — 전체 의사 결정 구성 요소 스택 설정 필요
- AI 등급을 획득하려면 효과적인 교육을 위해 상당한 전환 양과 시간이 필요합니다
- Edge 프로필 데이터 제한 사항은 익명 방문자의 자격 규칙 복잡성을 제한합니다
- 컨텐츠 품목 관리 간접비 — 각 품목에는 표시, 자격 규칙 및 유지보수가 필요합니다.
- 디버깅 의사 결정 논리는 규칙 기반 접근 방식보다 더 복잡합니다

**Experience League:**

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)

### 옵션 비교

다음 표에서는 주요 기준에서 세 가지 구현 옵션을 비교합니다.

| 기준 | 옵션 A: 규칙 기반 | 옵션 B: 실험 | 옵션 C: Decisioning |
| --- | --- | --- | --- |
| 다음에 최적 | 알려진 세그먼트-콘텐츠 매핑 | 가장 적합한 콘텐츠 검색 | 큰 카탈로그에서 동적 콘텐츠 선택 |
| 복잡성 | 낮음 | 중간 | 높음 |
| 지연 | Sub-second(edge) | Sub-second(edge) | Sub-second(edge) |
| Personalization precision | 세그먼트 수준(대상 규칙) | 방문자 수준(무작위 할당) | 방문자 수준(자격 + 순위) |
| 콘텐츠 최적화 | 수동(측정 없음) | 통계 테스트 (A/B) | 연속(AI 등급) 또는 수동(우선 순위) |
| 대상 세그먼트 필요 | 예(에지 평가) | 아니요(트래픽 분할) | 선택 사항(적격성 규칙의 경우) |
| 측정 기능 | 내장된 기능 없음(CJA 필요) | 기본 제공 실험 보고서 | 기본 제공 의사 결정 보고서 |
| 콘텐츠 카탈로그 크기 | 작음(1:1 세그먼트-콘텐츠) | 작게(2-10개 변형) | 큼(무제한 적격 항목) |
| 필요 | Edge 대상, 콘텐츠 변형 | 실험이 활성화된 캠페인 | 의사 결정 구성 요소 (배치, 오퍼, 정책) |

### 적절한 옵션 선택

다음 의사 결정 논리를 사용하여 적절한 구현 옵션을 선택합니다.

1. **각 방문자 세그먼트에 표시할 콘텐츠를 이미 알고 있습니까?**
   - 예: **옵션 A(규칙 기반)**&#x200B;로 시작합니다. 세그먼트별로 콘텐츠 전략을 수립하여 결정론적 전달이 필요합니다.
   - 아니요: 질문 2로 진행합니다.

2. **최상의 성능을 찾기 위해 적은 수의 콘텐츠 변형을 테스트해야 합니까?**
   - 예: **옵션 B(실험)**&#x200B;을(를) 선택합니다. 콘텐츠 전략을 커밋하기 전에 통계적 유효성 검사가 필요합니다.
   - 아니요: 질문 3으로 진행합니다.

3. **자격 요건 및 순위 요구 사항이 복잡한 대량의 콘텐츠 항목 카탈로그를 가지고 있습니까?**
   - 예: **옵션 C(Decisioning)**&#x200B;을 선택합니다. 단순한 규칙을 넘어 확장되는 다이내믹 콘텐츠 선택이 필요합니다.
   - 아니요: 단순화를 위해 **옵션 A(규칙 기반)**&#x200B;로 시작한 다음 요구 사항이 증가함에 따라 옵션 B 또는 C로 발전합니다.

**옵션 결합:** 이러한 옵션은 함께 사용할 수 없습니다. 일반적인 진행은 옵션 B(실험)로 시작하여 우승 콘텐츠를 검색한 다음, 지속적인 전달을 위해 옵션 A(규칙 기반)를 사용하여 우승자를 배포하는 것입니다. 옵션 A가 간단한 결정론적 규칙을 처리하는 반면, 옵션 C(의사 결정)는 동적 카탈로그 기반 선택이 필요한 사용 사례의 경우 맨 위에 계층화될 수 있습니다.

## 구현 단계

다음 단계에서는 전체 구현 워크플로에 대해 설명합니다.

### 1단계: 웹 표면 구성

**응용 프로그램 함수:** AJO: 채널 구성

웹 사이트에서 개인화된 콘텐츠가 전달될 위치를 지정하는 웹 채널 표면을 정의합니다. 웹 표면은 특정 페이지 URL 또는 URL 패턴과 AJO이 콘텐츠를 삽입하거나 바꿀 수 있는 페이지에서의 위치(CSS 선택기 또는 코드 기반 경험 표면)를 식별합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 표면 유형** — 개인화된 콘텐츠를 어떻게 페이지에 전달해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 웹 채널(비주얼 편집기) | 개인화에는 드래그 앤 드롭 시각적 편집기를 사용하여 표시되는 페이지 요소(배너, 헤드라인, 이미지, CTA)를 수정하는 작업이 포함됩니다 | 웹 디자이너 브라우저 확장이 필요합니다. 마케팅 주도 콘텐츠 변경에 가장 적합합니다. 기존 페이지 요소를 시각적으로 수정하도록 제한됩니다. |
| 코드 기반 경험 | 개인화를 사용하려면 웹 사이트 애플리케이션 코드가 소비하고 렌더링하는 구조화된 데이터(JSON)를 삽입해야 합니다 | JSON 페이로드를 사용하려면 개발자 구현이 필요합니다. 복잡한 개인화를 위한 최대 유연성. SPA, 동적 구성 요소 및 프로그래밍 방식 렌더링에 가장 적합합니다. |
| 둘 다(하이브리드) | 동일한 사이트에서 서로 다른 개인화에는 서로 다른 게재 메커니즘이 필요합니다 | 프로그래밍 방식의 렌더링에서 간단한 시각적 변경 사항과 코드 기반 경험을 위해 웹 채널을 사용합니다. 구현 복잡성을 증가시키지만 적용 범위를 최대화합니다. |

>[!NOTE]
>**결정: 표면 범위** — 웹 표면 범위가 포함되는 URL 범위

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 정확한 URL 일치 | Personalization은 특정 페이지(예: 홈페이지, 랜딩 페이지)를 타깃팅합니다 | 가장 정확한 타겟팅. 각 페이지에 대해 별도의 서피스가 필요합니다. |
| 와일드카드가 있는 URL 패턴 | Personalization은 페이지 카테고리(예: 모든 제품 페이지, 모든 블로그 문서)에 적용됩니다 | 표면 관리 부담 감소. 일치하는 모든 페이지에서 작동하도록 콘텐츠 변형을 디자인해야 합니다. |
| 단일 페이지 애플리케이션(SPA) 표면 | 웹 사이트는 URL 변경 사항이 전체 페이지 다시 로드를 트리거하지 않는 SPA입니다 | 보기 변경 시 SPA 인식 [!DNL Web SDK] 구성과 `sendEvent` 호출이 필요합니다. 표면 정의는 URL이 아닌 SPA 보기 이름을 사용합니다. |

**UI 탐색:** [!DNL Journey Optimizer] > 관리 > 채널 > 웹 구성

**키 구성 세부 정보:**

- 표면에 대한 페이지 URL 또는 URL 패턴 정의
- 컨텐츠 배치에 사용할 CSS 선택기 또는 표면 URI 지정
- 코드 기반 경험의 경우 애플리케이션 코드가 참조할 표면 이름을 정의합니다
- 캠페인을 만들 AJO 샌드박스와 표면을 연결합니다

**Experience League 설명서:**

- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [웹 경험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [코드 기반 경험 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [코드 기반 경험 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

### 2단계: 행동 대상자 정의

**응용 프로그램 함수:** RT-CDP: 대상 평가

개인화 타깃팅을 유도하는 세션 내 행동 신호를 기반으로 에지 평가 대상 세그먼트를 정의합니다. 이러한 대상은 각 개인화된 경험에 적합한 방문자를 결정합니다. 이 패턴은 방문자가 사이트를 탐색할 때 1초 이내에 개인화를 결정해야 하므로 Edge 평가가 필수입니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 동작 신호 선택** — 개인화 타깃팅을 유도하는 세션 내 신호는 무엇입니까?

| 신호 | 사용 시기 | Edge 자격 요건 |
| --- | --- | --- |
| 참조 소스/UTM 매개 변수 | Campaign별 랜딩 페이지 개인화 | 적격 — 현재 이벤트에 대한 간단한 속성 확인 |
| 지리적 위치(국가, 지역, 도시) | 지역별 프로모션, 언어별 콘텐츠, 스토어 로케이터 | 적격 — 프로필 속성 확인 |
| 장치 유형(데스크탑, 모바일, 태블릿) | 장치에 최적화된 컨텐츠 레이아웃 및 CTA | 적격 — 프로필 속성 확인 |
| 세션에서 본 페이지 | 카테고리 친화성, 콘텐츠 권장 사항 | 제한 적용 가능 — 간단한 이벤트 수 확인만 |
| 새 방문자와 재방문자 비교 | 환영 메시지, 점진적 참여 | 적격 — ECID 지속성은 재방문자를 나타냅니다. |
| 사이트에서 보낸 시간/스크롤 깊이 | 종료 의도, 참여 기반 오퍼 | 사용자 정의 구현이 필요할 수 있음 — 기본적으로 Edge에 적합하지 않음 |

>[!NOTE]
>**결정: 대상 평가 메서드** - 이 패턴의 모든 대상은 에지 평가를 사용해야 합니다. 세그먼트를 정의하기 전에 자격 조건을 확인합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 에지 평가 | 이 패턴에 필요 | 세그먼트 규칙 표현식은 단순 속성 비교, 세그먼트 멤버십 확인, 시계열 쿼리 또는 집계 함수 없음 등 Edge에 적격해야 합니다. 1초 미만의 평가 대기 시간입니다. |
| 스트리밍 평가(대체) | 세그먼트 규칙 표현식이 Edge에 적합하지 않지만 거의 실시간으로 허용되는 경우 | 초~분 간 지연. 보다 복잡한 세그먼트 규칙 표현식을 지원합니다. 개인화 전달이 눈에 띄게 지연될 수 있습니다. |

**UI 탐색:** 고객 > 대상 > 대상 만들기 > 규칙 빌드

**키 구성 세부 정보:**

- 세그먼트 빌더를 사용하여 행동 속성을 사용하는 대상 규칙을 정의합니다.
- 세그먼트 규칙 표현식이 지원되는 함수(단순 속성 비교, 세그먼트 멤버십)만 사용하는지 확인하여 에지 자격 확인
- 병합 정책을 F4에 구성된 에지 활성 병합 정책으로 설정합니다.
- 세그먼트의 유효성을 검사하기 위한 대상 모집단 미리 보기가 예상 결과를 반환합니다.
- 세션 내 페이지 보기를 기반으로 하는 대상의 경우, 시계열 쿼리가 아닌 현재 세션의 이벤트 수준 속성을 사용하십시오

**옵션이 나뉘는 위치:**

**옵션 A(규칙 기반)의 경우:**
각 콘텐츠 변형에 대해 고유한 대상 세그먼트를 만듭니다. 각 세그먼트는 특정 행동 조건을 나타냅니다(예: &quot;레퍼러 = Google AND 지역 = US&quot; 맵이 콘텐츠 변형 A로 매핑됨). 대상자 수는 개인화 규칙 수와 같습니다.

**옵션 B(실험)의 경우:**
대상 정의는 선택 사항입니다. 실험이 모든 방문자를 타깃팅하는 경우 대상이 필요하지 않습니다. 트래픽 분할은 변형 할당을 처리합니다. 실험이 특정 하위 집합을 타깃팅하는 경우(예: 모바일 방문자만) 실험 적격성에 대한 단일 타깃팅 대상을 정의합니다.

**옵션 C(Decisioning)의 경우:**
콘텐츠 항목에서 자격 규칙으로 사용할 대상을 정의합니다. 이러한 대상은 결정 정책에서 어떤 콘텐츠 항목에 대한 자격이 있는지 방문자를 결정합니다. 의사 결정 엔진은 적격 항목 중에서 콘텐츠 선택을 처리합니다.

**Experience League 설명서:**

- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)

### 3단계: 콘텐츠 작성 및 변형 만들기

**응용 프로그램 함수:** AJO: 메시지 작성, AJO: 콘텐츠 실험(옵션 B), AJO: 의사 결정(옵션 C)

대상 멤버십(옵션 A), 실험 할당(옵션 B) 또는 의사 결정 논리(옵션 C)를 기반으로 방문자에게 전달되는 개인화된 콘텐츠 변형을 만듭니다. 이 단계에서는 AJO 웹 디자이너 또는 코드 기반 경험 편집기를 사용한 컨텐츠 작성과 컨텐츠 선택 방법을 제어하는 실험 또는 의사 결정 구성을 다룹니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 콘텐츠 작성 방법** — 웹 콘텐츠 변형을 작성하는 방법

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 웹 비주얼 편집기 | 마케팅 팀은 코드 없이 시각적으로 페이지 요소를 수정할 수 있습니다 | 브라우저 확장이 필요합니다. 텍스트, 이미지 및 CTA 수정 사항에 가장 적합합니다. 기존 페이지 요소를 수정하도록 제한됩니다. |
| 코드 기반 경험 편집기 | 컨텐츠에는 애플리케이션 코드가 렌더링하는 구조화된 데이터(JSON)가 필요합니다 | 최고의 유연성. 페이로드를 사용하려면 개발자 구현이 필요합니다. 동적 구성 요소 및 SPA에 가장 적합합니다. |
| HTML/CSS 코드 편집기 | 콘텐츠를 수정하려면 사용자 지정 HTML 또는 CSS가 필요합니다 | 직접 코드 제어. HTML/CSS 전문 지식이 필요합니다. 복잡한 레이아웃 변경에 가장 적합합니다. |

>[!NOTE]
>**결정: Personalization 토큰** — 콘텐츠에 프로필 또는 컨텍스트 특성을 사용하는 동적 개인화가 포함되어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 정적 콘텐츠 변형 | 각 변형은 동적 토큰이 없는 고정된 콘텐츠 조각입니다 | 가장 간단한 접근. 콘텐츠는 예측 가능하고 QA가 용이합니다. 속성 값이 누락될 위험이 없습니다. |
| 개인화 표현식이 포함된 다이내믹 콘텐츠 | 컨텐츠에는 프로필 또는 이벤트 속성(예: 도시 이름, 참조 소스)으로 확인되는 Handlebars 스타일의 토큰이 포함되어 있습니다 | 더 관련성 있는 콘텐츠. 익명 프로필에서 null일 수 있는 특성에 대한 대체 값이 필요합니다. 도우미가 있는 `{{profile.homeAddress.city}}` 구문을 사용하십시오. |
| 조건부 콘텐츠 블록 | 여러 콘텐츠 블록이 단일 변형 내의 특성 조건에 따라 렌더링됩니다. | 필요한 개별 변형의 수를 줄입니다. 콘텐츠 복잡성을 증가시킵니다. 공유 레이아웃 내의 작은 변형에 적합합니다. |

**UI 탐색:** [!DNL Journey Optimizer] > 캠페인 > 캠페인 선택 > 콘텐츠 편집

**키 구성 세부 정보:**

- 웹 디자이너(시각적 수정) 또는 코드 기반 경험 편집기(JSON 페이로드)를 사용하여 콘텐츠를 작성합니다
- 개인화 표현식 편집기를 사용하여 Edge 프로필 속성에서 동적 토큰을 삽입합니다
- 익명 프로필에서 비어 있을 수 있는 개인화 토큰에 대한 대체 콘텐츠 구성
- 테스트 프로필로 콘텐츠 미리보기를 통해 시나리오 간 렌더링 확인

**옵션이 나뉘는 위치:**

**옵션 A(규칙 기반)의 경우:**
2단계에서 정의된 각 대상 세그먼트에 대해 고유한 콘텐츠 변형을 작성합니다. 캠페인 구성에서 조건부 콘텐츠 규칙을 사용하여 각 변형을 타겟 대상에 바인딩합니다. 대상 규칙과 일치하지 않는 방문자에 대해 기본 콘텐츠 변형이 있는지 확인하십시오.

**옵션 B(실험)의 경우:**
작성자 처리 변형(A, B, C 등) 실험용. 캠페인에 대한 콘텐츠 실험을 활성화하고, 해당 콘텐츠로 처리 변형을 정의하고, 트래픽 할당 백분율을 설정하고, 성공 지표를 구성합니다.

- 개별 콘텐츠로 2~10개의 처리 변형 정의
- 트래픽 할당 설정(예: A/B의 경우 50/50, 또는 위험이 낮은 테스트의 경우 가중 분할)
- 선택적으로 홀드아웃 그룹(예: 10%가 기본 컨텐츠를 수신함)을 포함하여 증분 리프트를 측정합니다
- 성공 지표 를 선택합니다. 고유 열기, 고유 클릭 수, 전환 또는 사용자 지정 지표
- 신뢰 임계값을 설정합니다. 표준 테스트의 경우 95%, 중요 결정의 경우 99%, 방향 학습의 경우 90%.
- **UI 탐색:** 캠페인 > 콘텐츠 실험 > 처리 추가 > 트래픽 할당 > 성공 지표

**옵션 C(Decisioning)의 경우:**
Decisioning 구성 요소 스택을 설정하고 캠페인에 통합합니다.

1. **배치 만들기** — 페이지 콘텐츠 항목이 표시될 위치를 정의합니다(웹 HTML, 웹 JSON, 웹 이미지).
   - **UI 탐색:** [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리 > 배치
2. **자격 규칙 정의** - 각 콘텐츠 항목에 대해 자격이 있는 방문자를 결정하는 Edge 프로필 특성을 기반으로 규칙을 만듭니다.
   - **UI 탐색:** [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리 > 규칙
3. **콘텐츠 항목 만들기(오퍼)** - 각 배치, 자격 규칙, 우선 순위 및 선택적 한도에 대한 표시가 있는 개인화된 콘텐츠 항목을 작성합니다
   - **UI 탐색:** [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리 > 오퍼 > 오퍼 만들기
4. **대체 콘텐츠 만들기** — 개인화된 항목이 적격하지 않을 때 반환되는 대체 항목을 정의합니다.
   - **UI 탐색:** [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리 > 오퍼 > 대체 오퍼 만들기
5. **컬렉션으로 구성** - 컬렉션 한정자(태그)를 사용하여 콘텐츠 항목을 그룹화하고 컬렉션을 만듭니다.
   - **UI 탐색:** [!DNL Journey Optimizer] > 구성 요소 > 의사 결정 관리 > 컬렉션 한정자/컬렉션
6. **의사 결정 정책 만들기** — 배치에 컬렉션을 연결하고 순위 전략(우선 순위 기반, 수식 기반 또는 AI 등급)을 선택합니다.
   - **UI 탐색:** [!DNL Journey Optimizer] > 구성 요소 > 결정 관리 > 결정 > 결정 만들기

**Experience League 설명서:**

- [웹 경험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [코드 기반 경험 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 4단계: 캠페인 및 게재 구성

**응용 프로그램 함수:** AJO: 캠페인 실행

웹 표면(1단계), 대상 타기팅 또는 실험 구성(2~3단계) 및 콘텐츠 변형(3단계)을 제공 가능한 단위로 바인딩하는 AJO 웹 캠페인을 만들고 활성화합니다. 캠페인은 개인화된 콘텐츠가 방문자에게 제공되는 시기와 방법을 제어합니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 캠페인 유형** — 캠페인을 트리거하는 방법

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 예약된 캠페인(항상 켜짐) | Personalization은 자격을 갖춘 모든 방문자에 대해 계속 실행되어야 합니다 | 항상 개인화를 위해 종료 일자 없이 시작 일자를 설정합니다. 대상 평가는 에지에서 실시간으로 발생합니다. 웹 개인화에 가장 일반적입니다. |
| 예약된 캠페인(시간 제한) | Personalization은 특정 프로모션 기간 또는 시즌 이벤트와 연결되어 있습니다 | 명시적 시작 및 종료 날짜를 설정합니다. Campaign은 종료 날짜에 자동으로 비활성화됩니다. 홍보 캠페인에 적합합니다. |
| API 트리거된 캠페인 | Personalization 게재는 외부 시스템 이벤트에 의해 트리거되어야 합니다. | API 통합이 필요합니다. 익명 웹 개인화의 경우 흔하지 않습니다. 개인화가 활성화된 시기를 백엔드 시스템이 제어해야 하는 경우에 사용합니다. |

**UI 탐색:** [!DNL Journey Optimizer] > 캠페인 > 캠페인 만들기

**키 구성 세부 정보:**

- 1단계에서 구성된 웹 채널 및 웹 표면을 선택합니다.
- 타겟 대상 바인딩(옵션 A의 경우) 또는 실험 설정 구성(옵션 B의 경우) 또는 의사 결정 포함(옵션 C의 경우)
- 캠페인 일정(시작 날짜, 종료 날짜 또는 항상 켜짐) 설정
- 해당되는 경우 캠페인 수준 빈도 제한 구성
- 모든 구성 검토 및 캠페인 활성화

**옵션이 나뉘는 위치:**

**옵션 A(규칙 기반)의 경우:**
개인화 규칙당 하나의 캠페인을 만들고 각 캠페인은 해당 콘텐츠 변형을 통해 서로 다른 에지 대상을 타겟팅합니다. 또는 대상자 멤버십을 하나의 캠페인 내의 콘텐츠 변형에 매핑하는 조건부 콘텐츠 규칙이 있는 단일 캠페인을 사용할 수 있습니다.

**옵션 B(실험)의 경우:**
콘텐츠 실험이 활성화된 단일 캠페인을 만듭니다. 실험 구성(변형, 트래픽 할당, 성공 지표)은 3단계에서 정의되었습니다. 캠페인을 활성화하여 실험을 시작하십시오.

**옵션 C(Decisioning)의 경우:**
3단계에서 구성된 결정 정책을 임베드하는 캠페인을 만듭니다. 캠페인의 콘텐츠 작업은 의사 결정 범위를 참조하며, 이는 에지에서 의사 결정 엔진을 트리거합니다. 캠페인을 활성화하여 의사 결정 기반 콘텐츠 전달을 시작합니다.

**Experience League 설명서:**

- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### 5단계: 성과 보고 및 분석

**응용 프로그램 함수:** AJO: 보고 및 성능 분석

AJO 기본 제공 보고서를 사용하여 개인화 성능을 모니터링하고 선택적으로 CJA을 사용하여 분석을 확장하여 더 심층적인 크로스 채널 통찰력을 얻습니다. 이 단계에서는 라이브 및 내역 캠페인 보고서에 액세스하고, 실험 결과를 검토하고, 사용자 정의 분석 작업 공간을 구축하는 작업을 다룹니다.

이 단계의 **결정 지점:**

>[!NOTE]
>**결정: 보고 깊이** — 성능 분석은 얼마나 심층적으로 수행되어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| AJO 기본 보고서만 | 기본 게재 및 참여 지표로 충분함 | 노출 횟수, 클릭 수, CTR 및 전환 지표를 즉시 제공합니다. 캠페인 UI에서 즉시 사용할 수 있습니다. 제한된 맞춤화. |
| AJO 보고서 + CJA 분석 | 심층 funnel 분석, 집단 비교 또는 크로스 채널 영향 측정이 필요합니다 | CJA 데이터 세트에 연결된 AJO 연결 및 데이터 보기가 필요합니다. 자유 형식 분석, 사용자 지정 계산된 지표, 속성 모델링 및 대상 게시를 활성화합니다. |

**UI 탐색:** [!DNL Journey Optimizer] > 캠페인 > 캠페인 선택 > 보고서 보기

**키 구성 세부 정보:**

- 활성 캠페인 동안 라이브 보고서에 액세스하여 실시간 게재 모니터링(60초마다 새로 고침, 지난 24시간 표시)
- 포괄적인 분석을 위해 캠페인 완료 후 내역(항상) 보고서에 액세스(완전히 채워지는 데 최대 2시간 소요될 수 있음)
- 옵션 B(실험)의 경우: 실험 보고서를 검토하여 처리 성능 비교, 신뢰 구간 및 승자 선언을 수행합니다
- CJA 분석의 경우: CJA 연결에 AJO 경험 이벤트 데이터 세트가 포함되어 있고 데이터 보기가 웹 개인화 지표로 구성되어 있는지 확인합니다

**옵션이 나뉘는 위치:**

**옵션 A(규칙 기반)의 경우:**
각 대상 세그먼트에 대한 캠페인 보고서를 검토하여 개인화된 콘텐츠 변형에 대한 게재 및 참여 지표를 비교하십시오. CJA을 사용하여 개인화된 컨텐츠와 기본 컨텐츠의 전환 영향을 측정하는 비교 작업 영역을 구축할 수 있습니다.

**옵션 B(실험)의 경우:**
실험 보고서를 검토하여 통계적 신뢰, 치료 상승도 및 승자 식별을 확인하십시오. 우승자를 선언하기 전에 신뢰 임계값에 도달할 때까지 기다립니다. 우승 콘텐츠를 영구 변형으로 적용합니다(지속적인 전달을 위해 옵션 A로 전환).

- **UI 탐색:** 캠페인 > 콘텐츠 실험 > 보고서 보기
- **Experience League:** [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)

**옵션 C(Decisioning)의 경우:**
오퍼 노출률, 선택 빈도 및 콘텐츠 항목별 전환 속성을 포함한 의사 결정 성능 지표를 검토합니다. 등급 전략의 수행 방법과 대체 컨텐츠가 너무 자주 제공되는지 여부를 분석합니다(자격 규칙이 너무 제한적임을 나타냄).

**Experience League 설명서:**

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [콘텐츠 실험의 통계 계산](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

## 구현 시 고려 사항

이 섹션에서는 이 사용 사례 패턴에 대한 보호, 일반적인 위험, 우수 사례 및 보상 결정을 다룹니다.

### 보호 기능 및 제한 사항

구현 전 및 구현 중에 다음 보호 기능을 검토하십시오.

- Edge 세그먼트는 단순 특성 검사 및 세그먼트 멤버십으로 제한됩니다. 시계열 쿼리 또는 복잡한 집계 없음 — [Edge 세그먼테이션 자격](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- 샌드박스당 Edge에서 하나의 병합 정책만 활성화할 수 있습니다. [프로필 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 샌드박스당 최대 4,000개의 세그먼트 정의 — [세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 샌드박스당 최대 500개의 활성 라이브 캠페인 — [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 콘텐츠 실험당 최대 10개의 처리 변형 — [콘텐츠 실험 제한](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 샌드박스당 최대 10,000개의 승인된 개인화된 오퍼(옵션 C) — [의사 결정 관리 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 결정당 최대 30개 배치(옵션 C) — [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- AI 등급 모델은 교육을 위해 최소 1,000개의 전환 이벤트가 필요합니다(옵션 C)
- [!DNL Edge Network] 응답 시간 SLA: 에지 평가 세그먼트의 경우 200ms 미만
- 익명 프로필 만료: ECID 전용 프로필에 대해 14일에서 365일까지 구성 가능
- 라이브 보고서는 60초마다 새로 고침되며 지난 24시간 동안의 데이터를 표시합니다.
- 캠페인 완료 후 내역 보고서를 완전히 채우는 데 최대 2시간이 걸릴 수 있습니다

### 일반적인 함정

다음과 같은 일반적인 구현 실수를 방지하십시오.

- **[!DNL Web SDK]동작 신호를 AEP에 보내지 않습니다.** 데이터 스트림에 [!DNL Adobe Experience Platform] 서비스가 활성화되어 있고 이벤트 데이터 세트가 올바르게 매핑되었는지 확인하십시오. 이 옵션이 없으면 에지 프로필이 채워지지 않고 대상 평가가 자동으로 실패합니다. 방문자는 오류 표시가 없는 기본 콘텐츠를 수신합니다.
- **자격 조건을 0으로 되돌리는 Edge 대상:** Edge 세분화에는 엄격한 자격 요구 사항이 있습니다. 시계열 쿼리, 집계 함수 및 다중 엔티티 쿼리는 Edge에 적합하지 않습니다. 간단한 속성 비교 또는 세그먼트 멤버십 확인을 사용하여 세그먼트 규칙 표현식을 다시 작성합니다.
- **Edge에서 병합 정책이 활성화되지 않음:** 대상 세그먼트에서 사용하는 병합 정책에 `isActiveOnEdge: true`이(가) 없으면 Edge 프로필 조회가 실패하고 개인화가 전달되지 않습니다. 샌드박스당 하나의 병합 정책만 Edge에서 활성화할 수 있습니다. 충돌이 없는지 확인하십시오.
- **페이지 로드 시 Personalization 깜박임:** 페이지가 대상 콘텐츠 영역을 렌더링하기 전에 개인화 제안을 검색하는 [!DNL Web SDK] `sendEvent` 호출을 실행해야 합니다. 코드 조각 사전 숨김 또는 비동기 렌더링을 구현하여 개인화된 콘텐츠가 로드되기 전에 기본 콘텐츠가 깜박이지 않도록 합니다.
- **SPA 경로 변경 시 콘텐츠가 렌더링되지 않음:** 단일 페이지 응용 프로그램에는 경로가 변경될 때 업데이트된 보기 정보와 함께 명시적 `sendEvent` 호출이 필요합니다. 이 기능이 없으면 [!DNL Edge Network]은(는) 새 보기에 대한 개인화를 다시 평가하지 않습니다.
- **통계적 유의성에 도달하지 않는 실험:** 트래픽 볼륨이 부족하거나 처리 변형이 너무 많아 변형당 샘플 크기가 희석됩니다. 변형 수를 줄이거나 실험 기간을 늘리십시오. 실험을 조기에 중단하지 마십시오. 결과는 오해의 소지가 있을 수 있습니다.
- **대체 콘텐츠만 반환하는 결정:** 개인화된 콘텐츠 항목이 유효 날짜 범위 내에서 승인되었는지, 자격 규칙이 익명 방문자의 Edge 프로필 특성과 일치하는지 확인하십시오. 또한 최대 가용량 한도에 도달하지 않았는지 확인하십시오.

### 우수 사례

성공적인 구현을 위해 다음 권장 사항을 따르십시오.

- **단순하게 시작한 다음 반복하기:** 초기 개인화를 위해 옵션 A(규칙 기반)로 시작한 다음 옵션 B(실험)를 사용하여 가정을 확인하고 고급 사용 사례에 대해 옵션 C(의사 결정)를 사용합니다. 각 옵션은 기본 인프라를 기반으로 합니다.
- **깜박임 방지를 위해 미리 숨김을 사용합니다.** 개인화가 전달될 페이지에서 AEP 미리 숨김을 구현합니다. 이렇게 하면 개인화된 콘텐츠를 렌더링할 준비가 될 때까지 대상 콘텐츠 영역을 숨겨 시각적 깜박임이 방지됩니다.
- **대체 콘텐츠를 계획적으로 디자인합니다.** 기본(개인화되지 않은) 콘텐츠는 저절로 고품질 경험이어야 합니다. 개인화할 자격이 없는 방문자 또는 [!DNL Edge Network] 응답이 지연된 경우 성능이 저하된 경험을 받지 않아야 합니다.
- **대상자를 만들기 전에 Edge 적격성 확인:** 대상자 규칙 개발에 투자하기 전에 Experience League에서 적격성 기준을 검토하여 세그먼트 규칙 식이 Edge 적격인지 확인하십시오. 부적격 표현식은 이 패턴에 대해 허용되지 않는 지연 시간이 있는 일괄 처리 또는 스트리밍 평가로 자동 폴백됩니다.
- **에지 게재 성능 모니터링:** [!DNL Edge Network] 응답 시간 및 개인화 게재 실패에 대한 모니터링 경고를 설정합니다. Edge 전달 문제는 방문자에게 보이지 않으며(기본 컨텐츠가 표시됨) 사전 모니터링 없이 감지되지 않을 수 있습니다.
- **익명 프로필 만료 구성:** 세션 간 개인화(재방문자 인식)와 개인 정보 보호 준수 및 저장소 관리 간의 균형을 맞추기 위해 익명 에지 프로필에 적절한 만료 기간을 설정하십시오.
- **대표 프로필로 테스트:** 개인화된 콘텐츠를 미리 볼 때 실제 익명 방문자 시나리오(CRM 데이터 없음, 제한된 동작 기록, 다양한 지리적 위치 및 장치)를 나타내는 테스트 프로필을 사용하십시오.

### 절충안 결정

구현을 계획할 때 다음 절충안을 고려하십시오.

>[!NOTE]
>**절충: Personalization의 폭과 구현 복잡성 비교**
>
>보다 세분화된 개인화(많은 대상, 많은 콘텐츠 변형)는 더 연관성 있는 경험을 생성하지만 구성 복잡성 및 콘텐츠 프로덕션 오버헤드를 증가시킵니다.
>
>- **다양한 개인화 혜택:** 단순성, 출시 시간 단축, 콘텐츠 제작 비용 절감. 적은 수의 대상 및 변형은 의미 있는 개인화를 사용하는 방문자의 대다수를 포함합니다.
>- **세분화된 개인화 혜택:** 최대 관련성, 더 높은 참여 향상도, 더 나은 전환율. 많은 대상 및 변형은 맞춤화된 콘텐츠를 사용하여 특정 행동 신호를 처리합니다.
>- **권장 사항:** 가장 일반적인 방문자 세그먼트(예: 참조 소스, 장치 유형, 지리적 지역)를 타깃팅하는 3~5개의 영향력이 큰 개인화 규칙으로 시작합니다. 영향을 측정한 다음 관찰된 성능 및 비즈니스 가치를 기반으로 보다 세분화된 규칙으로 확장합니다.

>[!NOTE]
>**절충: 규칙 기반 결정론과 AI 기반 최적화 비교**
>
>규칙 기반 접근 방식(옵션 A)을 사용하면 각 방문자가 보는 콘텐츠를 비즈니스에 완벽하게 제어할 수 있습니다. AI 등급 접근 방식(옵션 C)은 시간에 따라 콘텐츠 선택을 최적화하지만 특정 콘텐츠를 선택한 이유에 대한 가시성을 줄입니다.
>
>- **규칙 기반 우대:** 예측 가능성, 감사 가능성, 비즈니스 제어. 마케팅 팀은 각 세그먼트가 수신하는 콘텐츠를 정확히 알고 있으며 이해 당사자에게 논리를 설명할 수 있습니다.
>- **AI 기반 지원:** 성능 최적화, 확장성, 지속적인 개선. AI 모델은 인간의 규칙 쓰기가 놓칠 수 있는 콘텐츠 방문자 선호도를 검색합니다.
>- **권장 사항:** 브랜드 일관성과 관련자 투명성이 중요한 높은 관심사 콘텐츠 의사 결정에 규칙 기반 을 사용합니다. 수동 규칙 관리가 까다롭고 지속적인 최적화를 통해 측정 가능한 상승도를 제공하는 대규모 콘텐츠 카탈로그에 AI 등급을 사용합니다.

>[!NOTE]
>**절충: 익명 프로필 지속성과 개인 정보 보호 규정 준수 비교**
>
>익명 프로필 만료가 길어지면 더 나은 세션 간 개인화가 가능합니다(재방문자를 인식하고 시간이 지남에 따라 행동 컨텍스트를 구축). 만료 기간이 짧을수록 개인 정보 보호 규정 준수가 향상되고 스토리지 비용이 절감됩니다.
>
>- **만료 기간이 길수록 좋습니다.** 익명의 프로필, 더 나은 방문자 인식, 개인화 결정을 위한 더 많은 데이터 등을 제공합니다. 만료를 90~365일로 설정합니다.
>- **만료 기간 단축:** 개인 정보 보호 규정 준수(GDPR, CCPA), 저장 비용 절감, 부실 프로필 데이터의 위험 최소화 만료를 14~30일로 설정하십시오.
>- **권장 사항:** 조직의 쿠키 동의 정책 및 개인 정보 요구 사항에 맞게 만료를 조정하십시오. 대부분의 구현에서 30~90일은 개인화 값과 개인 정보 보호 규정 준수 간에 적절한 균형을 제공합니다.

## 관련 설명서

다음 Experience League 리소스는 이 사용 사례 패턴에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

**웹 채널 및 코드 기반 경험**

- [웹 채널 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/get-started-web)
- [웹 경험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/web/create-web)
- [코드 기반 경험 채널](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/get-started-code-based)
- [코드 기반 경험 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based/code-based-configuration)

**대상 및 세분화**

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

**Personalization 및 컨텐츠**

- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)

**콘텐츠 실험**

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [통계적 계산](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

**의사 결정 관리**

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [의사 결정 규칙 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

**캠페인**

- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

**[!DNL Web SDK]및 데이터 수집**

- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [웹 SDK 설치](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview)
- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [태그 개요](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)

**ID 및 프로필**

- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [ID 네임스페이스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/features/namespaces)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)
- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)

**데이터 모델링**

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)

**보고 및 분석**

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

**데이터 거버넌스 및 개인 정보 보호**

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [고급 데이터 수명주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)

**보호 기능**

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/identity/guardrails)
