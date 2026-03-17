---
title: Decisioning을 사용한 크로스 채널 여정
description: 최적의 채널, 컨텐츠 또는 오퍼를 선택하기 위한 실시간 의사 결정을 통합하는 여러 단계 여정을 오케스트레이션하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
source-git-commit: 61c2666b4546222423e85e52270b436c59d846a3
workflow-type: tm+mt
source-wordcount: '8992'
ht-degree: 2%

---


# 의사 결정을 통한 크로스 채널 여정

이 안내서에서는 의사 결정을 통한 채널 간 여정에 대한 전체 구현 참조를 제공합니다. 하나 이상의 여정 노드에서 실시간 의사 결정을 통합하는 다단계, 다중 채널 여정을 오케스트레이션해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

이 안내서를 사용하여 구현 선택 사항의 전체 환경을 파악하고, 장단점을 평가하고, 자세한 구성 지침을 보려면 관련 Experience League 설명서로 이동하십시오.

의사 결정을 사용한 크로스 채널 여정은 [!DNL Adobe Experience Platform] 에코시스템에서 가장 정교한 캠페인 오케스트레이션 패턴입니다. 실시간 의사 결정을 통합하여 여러 단계로 오케스트레이션된 여정을 확장합니다. [!DNL AJO] 의사 결정을 사용하여 프로필의 현재 컨텍스트를 평가하고 여정 캔버스 내 하나 이상의 의사 결정 지점에서 최적의 채널, 콘텐츠 또는 오퍼를 동적으로 선택합니다.

## 사용 사례 개요

조직은 고정된 사전 결정된 시퀀스를 따르는 대신 각 개인의 실시간 컨텍스트에 동적으로 반응하는 개인화된 적응형 고객 여정을 제공해야 하는 경우가 점점 늘어나고 있습니다. 고객이 선호하는 채널, 참여 내역, 충성도 계층, 예측된 라이프타임 값 및 현재 제품 관심사는 모두 각 접점에서 다음 작업이 되어야 하는 요소에 영향을 줍니다.

의사 결정이 있는 크로스 채널 여정은 두 가지 강력한 [!DNL AJO] 기능인 여정 오케스트레이션(여러 단계 흐름, 타이밍, 조건 및 채널 전달을 관리)과 의사 결정(자격 규칙을 평가하고 등급 전략을 적용하고 각 의사 결정 지점에서 최적 오퍼 또는 콘텐츠 변형을 선택)을 결합하여 이 문제를 해결합니다.

이 패턴은 다음과 같은 경우에 적합합니다.

- 여정은 고정된 채널 또는 컨텐츠 시퀀스를 따르는 것이 아니라 각 프로필의 실시간 상태에 동적으로 적응해야 합니다
- 여러 오퍼, 콘텐츠 변형 또는 채널은 하나 이상의 여정 노드에서 후보이며 프로필 컨텍스트를 기반으로 최상의 옵션을 선택해야 합니다
- 여정 전반에서 오퍼 선택을 최적화하려면 AI 지원 또는 수식 기반 순위가 필요합니다
- 이 조직은 복잡한 분기 로직을 유지하는 대신 채널 선택 논리와 오퍼 관리를 중앙 집중식 의사 결정 프레임워크로 통합하고자 합니다

타겟 대상에는 라이프사이클 프로그램, 충성도 여정, 윈백 시퀀스 및 온보딩 플로우를 관리하는 마케터가 포함됩니다. 이 경우 규모에 맞게 개인화하려면 각 접점에서 자동화된 의사 결정이 필요합니다.

## 주요 비즈니스 목표

다음 비즈니스 목표는 이 사용 사례 패턴을 통해 해결됩니다.

**[개인화된 고객 경험 제공](../../business-objectives/customer-experience/deliver-personalized-customer-experiences.md)**
콘텐츠, 오퍼 및 메시지를 개별 환경 설정, 동작 및 라이프사이클 단계에 맞게 맞춤화할 수 있습니다.
**KPI:**&#x200B;개 참여, 전환율, 고객 만족도(CSAT)

**[고객 충성도 및 라이프타임 값 증가](../../business-objectives/revenue-monetization/increase-customer-loyalty-lifetime-value.md)**
고객 관계를 심화하고 충성도 프로그램, 보상 및 개인화된 참여를 통해 장기적인 가치를 극대화합니다.
**KPI:** 고객 생애 가치, 유지, 상향 판매/교차 판매 %

**[고객 유지 개선](../../business-objectives/customer-experience/improve-customer-retention.md)**
가치 중심의 경험과 지속적인 관계 관리를 통해 기존 고객의 참여와 갱신을 유지합니다.
**KPI:** 유지, 고객 생애 가치, 참여

**[교차 판매 및 상향 판매 매출 촉진](../../business-objectives/revenue-monetization/drive-cross-sell-upsell-revenue.md)**
행동 및 구매 내역을 기반으로 기존 고객에게 보완 및 프리미엄 제품 또는 서비스를 홍보합니다.
**KPI:** 상향 판매/교차 판매 %, 증분 수익, 고객 생애 가치

## 예시 전술 사용 사례

다음 시나리오는 의사 결정을 통해 크로스 채널 여정을 실제로 적용하는 방법을 보여줍니다.

- **적응형 되먹임 여정** — 의사 결정에서 각 프로필의 참여 기록을 기반으로 채널(이메일, 푸시 또는 SMS)을 선택하고 예측된 라이프타임 값을 기반으로 최고의 인센티브 오퍼를 동적으로 선택하는 다단계 여정
- **다음 단계 라이프사이클 여정** — 의사 결정은 고객 라이프사이클의 각 단계에서 전달할 내용을 결정하며 온보딩 콘텐츠, 교차 판매 오퍼, 충성도 보상 또는 유지 인센티브에서 선택합니다
- **다이내믹 콘텐츠 선택을 통해 개인화된 온보딩** — 각 터치포인트가 의사 결정을 사용하여 가장 관련성이 높은 제품 교육 콘텐츠, 팁 또는 활성화 오퍼를 선택하는 새로운 고객 온보딩 여정
- **개인화된 보상을 포함하는 크로스 채널 충성도 프로그램 여정** — 충성도 멤버는 의사 결정에서 계층, 구매 내역 및 카테고리 관심도에 따라 개인화된 보상 오퍼를 선택하는 여정을 통해 진행됩니다.
- **채널 및 인센티브 최적화를 통한 동적 재참여** - 응답 확률을 극대화하기 위해 도달 채널과 인센티브가 모두 동적으로 선택되는 휴면 상태 고객 재참여
- **AI 등급 콘텐츠 추천을 통한 고객 라이프사이클 육성** — 각 접점에서 AI 등급 결정이 가장 관련성이 높은 콘텐츠 또는 제품 추천을 선택하는 지속적인 육성 여정

## 주요 성과 지표

다음 KPI를 사용하여 이 사용 사례 패턴의 효과를 측정합니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 여정 완료율 | 전체 여정을 완료하는 프로필 비율 | 여정 보고서: 완료/입력됨 |
| 오퍼 수락율 | 참여(클릭, 상환)한 의사 결정 선택 오퍼의 비율 | Decisioning 보고서: 오퍼 클릭수 / 오퍼 노출 횟수 |
| 채널 참여 비율 | 여정에 사용된 각 채널 간 열람율 및 클릭률 | 여정 보고서의 채널당 게재 지표 |
| 전환율 | 타겟 전환 작업을 완료하는 여정 참가자의 백분율 | 여정 종료 이벤트 추적 또는 CJA funnel 분석 |
| 대체 오퍼 비율 | 개인화된 오퍼 대신 대체 오퍼를 반환하는 의사 결정 요청의 비율 | 의사 결정 보고서: 대체 선택 항목 / 총 선택 항목 |
| 고객 생애 가치 영향 | 여정 참여자와 컨트롤 그룹의 CLV 변경 | 홀드아웃 비교가 포함된 CJA 집단 분석 |
| 교차 판매/상향 판매 수익 | 의사 결정 선택 오퍼로 인한 증분 매출 | 오퍼 기반 전환에 대한 CJA 속성 분석 |
| 의사 결정 순위 효율성 | AI 등급 오퍼와 무작위/우선 순위 기반 선택 간의 성능 차이 | 순위 전략을 비교하는 A/B 실험 |

## 사용 사례 패턴

**의사 결정 포함 크로스 채널 여정**

하나 이상의 노드에서 실시간 의사 결정을 통합하는 다단계 멀티채널 여정을 오케스트레이션하여 최적의 채널, 컨텐츠 또는 오퍼를 선택합니다.

**함수 체인:** 대상 평가 > 여정 실행 > 의사 결정 노드 > 채널 선택 > 메시지 게재 > 보고

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Adobe Journey Optimizer] ([!DNL AJO])** — 여정 오케스트레이션(다단계 캔버스 디자인, 시작 조건, 대기, 조건, 종료 기준), 채널 간 메시지 작성, 채널 표면 구성, 충돌 및 우선 순위 관리
- **[!DNL Adobe Journey Optimizer]의사 결정** — 오퍼 및 콘텐츠 항목 관리, 자격 규칙, 순위 전략(우선 순위, 공식, AI), 의사 결정 정책, 배치, 대체 오퍼
- **[!DNL Adobe Real-Time Customer Data Platform] ([!DNL RT-CDP])** — 여정 입력 및 오퍼 자격 세그먼트에 대한 대상 평가, 계산된 특성 및 성향 점수를 통한 프로필 강화, 동의 및 거버넌스 적용
- **[!DNL Adobe Experience Platform] ([!DNL AEP])** — 실시간 고객 프로필 스토어, 크로스 채널 해결을 위한 ID 서비스, 데이터 모델링 및 수집 인프라

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | 여정, 캠페인 및 의사 결정 권한이 구성된 [!DNL AJO] 샌드박스. 가능한 모든 게재 채널의 채널 표면. 여정 디자이너, 의사 결정 관리자 및 콘텐츠 작성자를 위한 사용자 역할. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 프로필 스키마에는 의사 결정에 사용되는 속성(예: 충성도 계층, 구매 내역, 채널 환경 설정, 참여 점수)이 포함되어야 합니다. 오퍼 카탈로그 및 의사 결정 항목 스키마를 구성해야 합니다. ExperienceEvent 스키마는 자격 규칙 및 등급 수식에서 사용되는 행동 신호를 캡처해야 합니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/home), [스키마 구성 기본 사항](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/schema/composition) |
| 데이터 소스 및 수집 | 가정 위치 | 의사 결정에 사용되는 프로필 속성 및 동작 신호는 최신 상태여야 합니다. 여정이 이벤트가 트리거된 시작 또는 종료 기준을 사용하는 경우 실시간 이벤트 스트리밍이 필요합니다. 피드 의사 결정 컨텍스트가 있는 채널에 대해 웹 SDK, Mobile SDK 또는 서버측 컬렉션이 활성화되어 있어야 합니다. | [웹 SDK 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/home), [소스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/home) |
| ID 및 프로필 구성 | 필수 | 크로스 채널 ID 확인이 중요합니다. 여정은 이메일, 푸시, SMS 및 웹 전반의 프로필을 확인해야 합니다. 병합 정책은 의사 결정을 위해 통합 프로필을 생성해야 합니다. 모든 고객 식별자(CRM ID, 이메일, ECID, 전화)에 대한 ID 네임스페이스를 구성해야 합니다. | [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home), [병합 정책 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/merge-policies/overview) |
| 대상 정의 및 세분화 | 필수 | 여정에 대한 시작 대상자 정의. 여정 내에서 오퍼 자격 규칙 및 조건 분기에 사용되는 추가 세그먼트입니다. 평가 방법은 지연 요구 사항과 일치해야 합니다(실시간 입력의 경우 스트리밍, 예약의 경우 배치). | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home), [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 고객 AI 성향 점수, 참여 점수, 채널 환경 설정 점수 및 라이프타임 값 계산과 같은 계산된 속성은 의사 결정 품질을 크게 향상시킵니다. 이러한 보강된 프로필 속성을 통해 보다 정교한 자격 규칙 및 등급 공식을 사용할 수 있습니다. | [계산된 특성 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/overview), [Customer AI 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/intelligent-services/customer-ai/overview) |
| 데이터 수명 주기 관리 | 추천 | 오퍼 내역 및 의사 결정 이벤트 데이터는 시간이 지남에 따라 누적되며 보존 정책이 있어야 합니다. 여러 채널에 걸친 동의 적용은 매우 중요합니다. 채널에 대한 유효한 동의가 없는 프로필은 해당 채널의 전달 경로에서 제외되어야 합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-lifecycle/home), [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 의사 결정이 서로 다른 데이터 사용 제한 사항을 가진 다른 채널로 프로필을 라우팅할 수 있는 경우 여러 채널 및 오퍼 유형에서 거버넌스를 적용하는 것이 중요합니다. 모든 채널에서 준수 오퍼 게재를 보장합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home), [정책 적용](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/enforcement/overview) |
| 모니터링 및 가시성 | 포함됨 | 여정 및 의사 결정 모니터링은 프로덕션 운영에 필수적입니다. 여정 입력 오류, 의사 결정 폴백 스파이크 및 게재 오류에 대한 경고를 통해 신속한 문제 해결을 수행할 수 있습니다. | [경고 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/alerts/overview), [가시성 통찰력 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | 여정 및 의사 결정 보고서는 보고 단계에서 다룹니다. 의사 결정 효율성, 채널 혼합 최적화, 오퍼 성능 및 여정 ROI에 대한 CJA 분석은 등급 전략을 구체화하고 시간에 따라 여정을 최적화하는 데 필요한 통찰력을 제공합니다. | [CJA 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-overview/cja-overview), [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer] ([!DNL AJO])

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 채널 구성 | 2단계: 채널 구성 | 의사 결정에서 선택하거나 여정이 사용하는 모든 채널(이메일, SMS, 푸시, 인앱)에 대한 채널 표면 구성 |
| 메시지 작성 | 4단계: 메시지 작성 | 각 채널에 대한 메시지 콘텐츠를 작성하고 결정 출력(오퍼 배치, 다이내믹 콘텐츠 블록, 선택한 오퍼의 개인화 토큰)을 통합합니다. |
| 결정 | 3단계: 의사 결정 설정 | 여정의 각 결정 지점에 대해 오퍼 항목, 자격 규칙, 등급 전략, 의사 결정 정책 및 대체 오퍼를 구성합니다 |
| Journey Orchestration | 5단계: 여정 디자인 및 활성화 | 시작 조건, 의사 결정 노드, 채널 라우팅, 대기 단계, 메시지 작업 및 종료 기준을 사용하여 여러 단계 여정 캔버스 디자인 |
| 충돌 및 우선 순위 관리 | 5단계: 여정 디자인 및 활성화 | 여러 여정이 동일한 프로필을 동시에 타겟팅할 수 있는 경우 우선 순위 점수 및 충돌 탐지 구성 |
| 빈도 및 비즈니스 규칙 | 5단계: 여정 디자인 및 활성화 | 다중 채널 여정 내에서 과도한 메시지를 방지하기 위해 채널 간 메시지 빈도 제한 적용 |
| 보고 및 성능 분석 | 6단계: 보고 및 모니터링 | 여정 및 노드별 전달 지표, 의사 결정 성능 및 채널 참여 모니터링 |

### [!DNL Real-Time CDP] ([!DNL RT-CDP])

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 1단계: 대상 평가 | 참가 대상 또는 자격 있는 참가 이벤트를 정의하고 평가하며 의사 결정에 사용되는 자격 세그먼트를 만듭니다. |
| 프로필 보강 | 전제 조건 / 지원 | 의사 결정 품질을 개선하는 계산된 속성 및 성향 점수로 프로필을 보강합니다 |
| 동의 및 거버넌스 적용 | 2단계: 채널 구성 | 모든 채널에 동의 환경 설정 적용, 규정 준수 오퍼 게재 확인 |

## 필요 조건

구현을 시작하기 전에 다음을 완료하십시오.

- [ ] [!DNL AJO] 샌드박스가 여정 오케스트레이션 및 의사 결정 기능을 사용하도록 설정되어 있습니다.
- [ ] 모든 대상 채널(이메일, SMS, 푸시)에 활성 상태의 확인된 채널 표면이 있습니다.
- [ ] 프로필 스키마에는 의사 결정에 필요한 특성(충성도 계층, 구매 내역, 채널 환경 설정, 참여 점수)이 포함되어 있습니다.
- [ ] 크로스 채널 ID 확인이 구성되었습니다. 이메일, 푸시 토큰, 전화 번호 및 웹 식별자 간에 프로필을 확인할 수 있습니다.
- [ ] 시작 대상이 정의되어 있으며 0이 아닌 모집단으로 평가되고 있습니다.
- [ ] 오퍼 카탈로그 콘텐츠(크리에이티브 에셋, 카피, 법적 고지 사항)가 승인되어 구성할 준비가 되었습니다.
- [ ] 동의 데이터가 수집되고 있으며 모든 대상 채널에 대해 동의 집행이 활성 상태입니다.
- [ 각 채널에 대한 ]개의 콘텐츠 템플릿 및 조각이 디자인 및 승인되었습니다.
- [ 조직에 캠페인 간 빈도 정책이 있는 경우 ] 빈도 제한 규칙이 정의되고 배포됩니다.
- [ ] AI 등급 의사 결정을 사용하는 경우 모델 교육에 대해 최소 1,000개의 전환 이벤트가 존재합니다

## 구현 옵션

다음 옵션을 검토하고 요구 사항에 가장 적합한 방법을 선택하십시오.

### 옵션 A: offer decisioning 을 사용한 여정 (고정 채널, 다이내믹 콘텐츠)

**우수 사례:** 채널 시퀀스가 미리 결정되어 있지만 각 접점에서 제공되는 콘텐츠 또는 오퍼를 동적으로 선택해야 하는 여정 - 개인화된 보상을 통한 충성도 여정, 동적 인센티브를 통한 재참여, AI 등급 콘텐츠 추천을 통한 라이프사이클 육성.

#### 작동 방식

여정 캔버스는 고정된 채널 시퀀스 및 타이밍을 정의합니다(예: 0일: 이메일, 3일: 푸시, 7일: SMS). 각 메시지 작업 노드에서 결정 정책은 구성된 적격 항목 카탈로그에서 메시지에 포함할 최상의 오퍼 또는 콘텐츠를 선택합니다. 오퍼는 [!DNL AJO] 의사 결정 카탈로그에서 프로필이 적격한 오퍼를 필터링하는 자격 규칙과 가장 적합한 오퍼를 결정하는 순위 전략으로 관리됩니다.

이 접근 방법에서는 &quot;언제 어디서&quot;(여정 오케스트레이션)와 &quot;what&quot;(의사 결정)을 구분합니다. 여정 디자이너는 채널 흐름을 제어하는 반면, 의사 결정 관리자는 오퍼 카탈로그, 자격 규칙 및 순위 논리를 독립적으로 제어합니다. 이렇게 문제를 분리하면 구현을 보다 유지 관리할 수 있으며 여정 캔버스를 수정하지 않고도 오퍼 카탈로그를 발전시킬 수 있습니다.

오퍼 배치는 이메일 Designer 또는 기타 채널 편집기를 사용하여 메시지 콘텐츠에 직접 포함됩니다. 메시지가 게재 시간에 렌더링되면 의사 결정 엔진은 프로필의 자격 요건 및 순위를 평가하여 메시지의 각 배치에 대한 최적의 오퍼를 선택합니다.

#### 주요 고려 사항

- 채널 시퀀스가 정적입니다. 모든 프로필은 기본 설정에 관계없이 동일한 채널 경로를 따릅니다.
- 채널이 아닌 콘텐츠/오퍼만 선택하므로 의사 결정 복잡성이 낮습니다.
- 오퍼 카탈로그는 여정과 독립적으로 관리할 수 있습니다.
- 적합한 개인화된 오퍼가 없는 프로필을 처리할 수 있도록 각 배치에 대해 대체 오퍼를 구성해야 합니다.

#### 장점

- 더 간단한 여정 캔버스 — 채널 선택을 위한 분기 논리 없음
- 여정 설계와 오퍼 관리 간의 명확한 문제 분리
- 더욱 간편해진 테스트 및 검증 — 각 채널 경로가 결정적입니다.
- 구현 복잡성 감소 및 출시 기간 단축
- 오퍼 카탈로그 변경 사항은 여정 수정 없이 즉시 적용됩니다.

#### 제한 사항

- 개별 프로필 동작 또는 환경 설정에 따라 채널을 조정할 수 없음
- 한 채널을 다른 채널보다 선호하는 프로필은 미리 결정된 채널에서 메시지를 계속 수신합니다
- 채널 수준 참여율에 최적화되지 않음

#### Experience League 참조

- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)

### 옵션 B: 동적 채널 선택(고정 컨텐츠, 동적 채널)을 사용하는 여정

**가장 좋은 대상:** 각 접점의 콘텐츠는 비슷하지만 여정 컨텍스트를 기반으로 채널을 동적으로 선택해야 하는 채널입니다. 적응형 윈백(이메일 및 참여를 기반으로 한 푸시/SMS), 채널 최적화가 기본 목표인 다음 모범 작업 프로그램입니다.

#### 작동 방식

이 여정은 프로필 속성(예: 채널 환경 설정 점수, 마지막 참여 채널 또는 동의 상태) 또는 의사 결정 출력으로 알려 주는 조건 노드를 사용하여 프로필을 다른 채널 경로로 라우팅합니다. 각 경로는 자체 메시지 작업 노드를 통해 채널별 콘텐츠를 전달합니다. 의사 결정 로직은 프로필의 행동 이력을 기반으로 어느 채널이 참여를 유도할 가능성이 가장 높은지를 결정합니다.

채널 선택은 프로필 속성 평가가 있는 여정 조건 노드(예: `channelPreference = "push"`이(가) 푸시 경로로 라우팅되는 경우)를 사용하거나 각 &quot;오퍼&quot;가 채널을 나타내고 등급 전략에 따라 최상의 채널이 결정되는 채널별 항목을 사용한 의사 결정을 사용하여 구현할 수 있습니다.

이 접근 방식은 여러 채널에서 콘텐츠를 비교적 일관되게 유지하면서 전달 채널을 최적화합니다. 가능한 각 채널에 대해 메시지 콘텐츠를 작성해야 하며 모든 후보 채널에 대해 채널 표면을 구성해야 합니다.

#### 주요 고려 사항

- 각 후보 채널에 대한 메시지 콘텐츠 변형 필요
- 채널 표면은 가능한 모든 채널에 대해 활성화되어야 합니다
- 조건 논리 또는 의사 결정 구성은 동의를 고려해야 합니다. SMS 동의가 없는 프로필은 SMS 경로로 라우팅할 수 없습니다.
- 여정 캔버스는 각 채널의 분기 경로와 더 복잡합니다.

#### 장점

- 각 개별 프로필에 대한 채널 선택 최적화
- 선호하는 채널의 프로필에 도달하여 전반적인 참여도를 높입니다.
- 동의 인식 라우팅을 통해 자동으로 채널별 동의 준수
- 참여 기록 및 채널 환경 설정 점수를 라우팅 의사 결정에 통합할 수 있음

#### 제한 사항

- 여러 채널 분기가 있는 더 복잡한 여정 캔버스
- 콘텐츠는 각 채널에 대해 별도로 작성되어야 합니다(메시지 의도는 동일하지만)
- 테스트하기 어려움 — 가능한 모든 채널 경로의 유효성을 검사해야 함
- 각 채널 내의 콘텐츠 개인화는 정적입니다(offer decisioning 없음)

#### Experience League 참조

- [조건 활동](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [여정 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)

### 옵션 C: 전체 적응형 여정(동적 채널 + 동적 컨텐츠)

**최적의 용도:** 최대 개인화 — 각 노드에서 채널과 콘텐츠/오퍼가 모두 동적으로 선택됩니다. 성숙한 의사 결정 사례와 풍부한 프로필 데이터를 갖춘 고부가가치 고객 세그먼트, 정교한 충성도 프로그램 및 조직에 적합합니다.

#### 작동 방식

이 옵션은 옵션 A와 B를 결합합니다. 이 여정은 두 가지 수준에서 의사 결정을 사용합니다. 첫 번째는 각 터치포인트에 사용할 채널을 결정하는 것이고, 두 번째는 선택한 채널에서 전달할 콘텐츠 또는 오퍼를 결정하는 것입니다. 여정의 각 의사 결정 지점은 프로필의 현재 컨텍스트를 평가하여 채널과 콘텐츠를 모두 선택합니다.

구현하려면 채널 선택과 컨텐츠/오퍼 선택 모두에 대한 의사 결정 정책을 포함하는 포괄적인 의사 결정 설정이 필요합니다. 채널 선택은 각 항목이 동의 및 참여에 기반한 자격 규칙이 있는 채널을 나타내는 의사 결정 정책을 사용할 수 있으며, 콘텐츠 선택은 관련성에 따라 순위가 매겨진 오퍼 항목을 사용하는 별도의 의사 결정 정책을 사용합니다.

이는 가장 복잡한 변형이며 여정 오케스트레이션과 결정 간의 가장 깊은 통합이 필요합니다. 또한 가장 높은 수준의 개인화를 제공할 뿐만 아니라 가장 많은 구성, 테스트 및 지속적인 관리가 필요합니다.

#### 주요 고려 사항

- 의사 결정(채널 선택 및 콘텐츠 선택)의 두 계층 필요
- 여정 캔버스 복잡성은 각 노드에서 중첩된 분기 및 의사 결정을 통해 가장 높습니다
- 가능한 모든 채널-컨텐츠 조합에 대해 광범위한 테스트가 필요합니다.
- 효과적인 의사 결정을 위해 풍부한 프로필 데이터(참여 내역, 채널 환경 설정, 제품 친화성, 성향 점수)를 요구합니다
- AI 등급 의사 결정은 계산된 속성에서 상당한 이점을 얻습니다.

#### 장점

- 최대 개인화 — 모든 접점이 채널 및 콘텐츠에 최적화됩니다.
- 잘 구성된 구현을 위한 최고의 참여 및 전환 가능성
- 정적 여정 분기가 아닌 의사 결정에 모든 개인화 논리를 중앙 집중화합니다.
- AI 순위 모델 학습을 통해 지속적으로 향상시킬 수 있다

#### 제한 사항

- 최고의 구현 복잡성 및 시장 출시 기간
- 가장 광범위한 오퍼 카탈로그 및 채널 컨텐츠 준비 필요
- 게재 문제가 발생할 때 해결하기가 더 어려움
- 풍부한 프로필 속성을 갖춘 완성도 높은 데이터 인프라 필요
- AI 등급에는 모델 교육을 위한 충분한 전환 이벤트 볼륨이 필요합니다

#### Experience League 참조

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 옵션 비교

다음 표를 사용하여 세 가지 구현 옵션을 한 눈에 비교할 수 있습니다.

| 기준 | 옵션 A: Offer Decisioning | 옵션 B: 동적 채널 | 옵션 C: 전체 적응형 |
| --- | --- | --- | --- |
| 다음에 최적 | 고정 채널 시퀀스, 다이내믹 콘텐츠 | 채널 최적화, 일관된 콘텐츠 | 두 차원 모두에서 최대 개인화 |
| 복잡성 | 중간 | Medium 하이 | 높음 |
| 여정 캔버스 | 단순(작업 노드에서 의사 결정 시 선형) | 중재(채널 경로의 분기) | 복합(다중 수준 의사 결정을 사용한 중첩 분기) |
| 의사 결정 범위 | 컨텐츠/오퍼 선택 항목만 | 채널 선택만 | 채널 및 콘텐츠 선택 모두 |
| 콘텐츠 요구 사항 | 채널당 하나의 콘텐츠 세트(오퍼 배치 포함) | 각 후보 채널에 대한 컨텐츠 | 각 후보 채널에 대한 오퍼 배치가 있는 콘텐츠 |
| 프로필 데이터 요구 사항 | 중재(오퍼 자격 속성) | 중재(채널 환경 설정, 참여) | 높음(채널 및 오퍼 속성 모두) |
| 시장 출시 기간 | 빠름 | 중재 | 최장 |
| 지속적인 관리 | 오퍼 카탈로그 관리 | 채널 라우팅 논리 관리 | 오퍼 카탈로그 및 채널 라우팅 모두 |
| Personalization 깊이 | 컨텐츠는 다양하며, 채널은 고정됨 | 채널은 다르고, 콘텐츠는 비슷함 | 채널과 콘텐츠는 모두 다양합니다 |

### 적절한 옵션 선택

다음 지침을 사용하여 상황에 가장 적합한 옵션을 결정하십시오.

- **옵션 A로 시작** 채널 전략이 이미 정의되어 있고(예: &quot;항상 이메일을 먼저 보낸 후 푸시, SMS 순으로 전송&quot;) 기본 개인화가 각 접점에서 올바른 오퍼 또는 콘텐츠를 선택하는 경우. 이는 의사 결정을 처음 수행하는 조직에 가장 일반적인 시작점입니다.

- **채널 최적화가 기본 목표인 경우 옵션 B를 선택합니다**. 각 고객이 참여할 가능성이 가장 높은 채널을 통해 각 고객에게 연결하려고 하지만 메시지 내용은 채널 간에 비교적 일관적입니다. 이를 위해서는 프로필에 대한 채널 환경 설정 데이터가 필요합니다.

- **옵션 C**&#x200B;은(는) 성숙한 의사 결정 인프라, 풍부한 프로필 데이터(계산된 특성 및 성향 점수 포함), 잘 채워진 오퍼 카탈로그 및 복잡성을 관리할 조직 용량이 있는 경우에만 선택합니다. 많은 조직이 옵션 A 또는 B로 시작하여 의사 결정 성숙도가 증가함에 따라 옵션 C로 진화합니다.

- **확실하지 않은 경우** 옵션 A로 시작하십시오. 가장 낮은 복잡성으로 의미 있는 개인화를 제공하며, 나중에 옵션 C로 발전할 경우 옵션 A에 대해 빌드한 오퍼 카탈로그를 직접 재사용할 수 있습니다.

## 구현 단계

다음 단계는 이 사용 사례 패턴의 전체적인 구현을 살펴봅니다.

### 1단계: 대상 평가

**응용 프로그램 함수:** [!DNL RT-CDP]: 대상 평가

이 단계는 여정에 입력하는 프로필과 여정 내 오퍼 자격 규칙 또는 조건 분기에 사용되는 추가 세그먼트를 결정하는 시작 대상을 구성합니다. 대상 정의는 모든 다운스트림 여정 및 의사 결정 논리의 기초입니다.

#### 결정: 항목 유형

예약된 대상자 읽기 또는 실시간 이벤트 트리거를 통해 프로필이 여정에 들어가는 방법은 무엇입니까?

>[!NOTE]
>여정의 타이밍 및 트리거 요구 사항에 따라 하나의 항목 유형을 선택합니다.

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 대상자 읽기(일괄 입력) | 라이프사이클 프로그램, 충성도 여정, 예약된 재참여 캠페인 | 프로필은 예약된 시간에 일괄적으로 입력되며, 대상은 읽기 시간에 평가되며, 큰 대상 크기를 지원합니다. |
| 대상 자격(스트리밍) | 프로필이 세그먼트에 들어오거나 나갈 때 입력이 발생해야 하는 동작 트리거된 여정 | 거의 실시간으로 입력, 스트리밍 가능 세그먼트 정의 필요, 마일스톤 기반 여정에 적합 |
| 단일 이벤트(이벤트 트리거) | 특정 이벤트는 여정을 트리거해야 합니다(예: 구매, 장바구니 포기, 등록). | 이벤트에 대한 실시간 항목, 이벤트 스키마 구성 필요, 초당 5,000개의 이벤트로 제한 |

#### 의사 결정: 대상 평가 방법

대상자는 얼마나 빨리 프로필을 검증해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 일괄 처리 | 일별 또는 주기적 대상자 업데이트로 충분합니다. 예약된 캠페인 스타일 여정 | 작업당 최대 2,400개의 프로필 처리, 일정 기반, 대부분의 세그먼트 규칙 표현식 지원 |
| 스트리밍 | 이벤트 트리거 또는 자격 기반 항목에 대한 실시간 대상 멤버십이 필요합니다 | 거의 실시간으로, 제한된 세그먼트 규칙 함수 세트, 시간 기반 집계 없음 |
| Edge | 동일 세션 검증 필요 | 밀리초 지연, 단순 속성 확인만 가능, 에지 프로필 속성으로 제한 |

#### 주요 구성 세부 정보

**UI 탐색:** 고객 > 대상 > 대상 만들기 > 규칙 빌드

- 관련 프로필 속성 및 행동 이벤트를 타깃팅하는 세그먼트 규칙 표현식과 함께 세그먼트 빌더 를 사용하여 시작 대상을 정의합니다
- 오퍼 자격 규칙이 세그먼트 멤버십을 참조하는 경우 추가 자격 세그먼트를 만듭니다(예: &quot;고가치 고객&quot;, &quot;충성도 골드 계층&quot;)
- 여정 구성으로 진행하기 전에 대상 모집단이 0이 아닌지 확인하십시오.
- 의사 결정에 필요한 통합 프로필 보기를 생성하는 병합 정책을 선택합니다

#### Experience League 설명서

- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/edge-segmentation)
- [Profile Query Language 참조](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/pql/overview)

### 2단계: 채널 구성

**응용 프로그램 함수:** [!DNL AJO]: 채널 구성

이 단계는 여정이 메시지 전달에 사용할 수 있는 모든 채널에 대해 채널 표면을 구성합니다. 메시지를 작성하거나 여정을 게시하려면 모든 후보 채널에 활성 상태의 검증된 표면이 있어야 합니다. 이 패턴의 경우, 일반적으로 이메일, SMS 및 푸시에 대한 표면을 최소한으로 구성하게 되며, 의사 결정에서 이러한 채널을 선택할 수 있는 경우 인앱 또는 웹이 될 수 있습니다.

#### 의사 결정: 구성할 채널

고정 여정 단계(옵션 A/B) 또는 의사 결정 선택 가능한 채널(옵션 B/C)로서 여정의 후보가 되는 채널은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이메일만 | Offer Decisioning이 포함된 단일 채널 여정(옵션 A, 이메일만 해당) | 가장 간단한 구성, 하위 도메인 위임 및 IP 웜업 필요 |
| 이메일 + 푸시 | 2채널 여정, 참여 중심 여정에 공통 | 푸시를 사용하려면 APNs/FCM 자격 증명이 필요합니다. 모바일 앱에는 SDK이 통합되어야 합니다. |
| 이메일 + SMS + 푸시 | 전체 크로스 채널 여정, 옵션 B 및 C에 가장 일반적 | SMS에는 공급자 자격 증명(Sinch, Twilio, Infobip)이 필요하며, 각 채널에는 자체 표면이 필요합니다 |
| 이메일 + SMS + 푸시 + 인앱 | 세션 내 표면을 포함한 최대 채널 범위 | 인앱에는 모바일 SDK 및 앱 표면 구성이 필요합니다 |

#### 결정: 하위 도메인 위임 방법(이메일)

보내는 하위 도메인을 Adobe에 어떻게 위임해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 전체 위임 | 조직은 Adobe이 보내는 하위 도메인에 대한 모든 DNS 레코드를 관리하도록 합니다. | 가장 간단한 설정, Adobe은 SPF, DKIM, DMARC을 처리하며 DNS에 대한 제어 감소 |
| CNAME 위임 | 조직에서 DNS 레코드 제어를 유지 관리해야 함 | 더욱 복잡한 설정, 고객이 DNS 관리, 유연성 향상 |

#### 주요 구성 세부 정보

**UI 탐색:** 관리 > 채널 > 채널 표면 > 표면 만들기

- 이메일: 하위 도메인, IP 풀, 보낸 사람 이름, 회신 주소 및 구독 취소 처리 구성
- SMS의 경우: SMS 공급자 자격 증명 및 발신자 번호 구성
- 푸시: iOS 및 Android에 대한 APNs 및 FCM 자격 증명 구성
- 계속하기 전에 각 서피스가 활성 상태인지 확인하십시오.
- 이메일 전송 IP에 대해 IP 웜업이 완료되었는지 확인

#### Experience League 설명서

- [이메일 구성 시작](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [SMS 채널 구성](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 3단계: 의사 결정 설정

**응용 프로그램 함수:** [!DNL AJO]: 의사 결정

이 단계에서는 배치, 자격 규칙, 개인화된 오퍼, 대체 오퍼, 컬렉션 한정자, 컬렉션, 등급 전략 및 의사 결정 정책을 포함하여 전체 의사 결정 프레임워크를 구성합니다. 이 단계는 여정 결정 지점에서 호출될 결정 논리를 생성합니다.

#### 의사 결정: 의사 결정 범위

의사 결정을 위해 선택해야 할 사항 — 오퍼/콘텐츠 (옵션 A), 채널 (옵션 B) 또는 둘 다 (옵션 C)

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 오퍼/컨텐츠 선택 전용 | 채널 시퀀스가 고정됨, 개인화가 콘텐츠에 있음 | 의사 결정 정책은 배치당 콘텐츠 표현이 있는 오퍼 항목을 타겟팅합니다. |
| 채널 선택만 | 콘텐츠 일관성, 최적화는 게재 채널에 있음 | 의사 결정 항목은 채널을 나타내며, 자격 조건에는 동의 확인이 포함되며, 순위는 참여 데이터를 사용합니다. |
| 채널 및 컨텐츠 모두 | 채널 및 콘텐츠 전반의 완전한 적응형 개인화 | 두 단계의 의사 결정 정책이 필요합니다. 가장 복잡하지만 가장 높은 개인화 |

#### 의사 결정: 순위 전략

가장 적합한 오퍼를 선택하기 위해 적격 오퍼의 등급을 어떻게 지정해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 우선 순위 기반(수동) | 비즈니스 규칙이 오퍼 중요도를 결정하는 간단한 순위 | 각 오퍼에는 우선 순위 점수가 부여됩니다. 우선 순위가 가장 높은 오퍼가 승리합니다. 결정적이며 이해하기 쉽습니다. |
| 공식 기반(사용자 정의 표현식) | 순위는 프로필 속성(예: CLV, 계층, 친화성 점수)에 영향을 주어야 합니다. | 사용자 지정 순위 공식은 프로필 컨텍스트를 평가합니다. 우선순위보다 동적입니다. ML은 필요하지 않습니다. |
| AI 등급(자동 최적화) | 순위는 과거 전환 데이터를 기반으로 자동으로 최적화되어야 합니다. | AI 모델이 전환 이벤트에서 학습하고, 교육을 위해 최소 1,000개의 이벤트가 필요하며, 지속적으로 개선됩니다. |

#### 결정: 오퍼 한도

오퍼가 표시되는 횟수에 제한이 있어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 프로필별 상한 | 동일한 오퍼가 동일한 프로필에 반복적으로 표시되지 않도록 합니다. | 오퍼 피로도 방지, 높은 처리량에서 카운터 지연 가능 |
| 글로벌 상한 | 모든 프로필의 총 노출 횟수 제한(예: 제한된 인벤토리 프로모션) | 총 노출 제어. 공급 제한 오퍼에 유용함 |
| 상한 없음 | 모든 적격한 노출에 오퍼가 표시됩니다. | 가장 간단함, 항상 사용되는 콘텐츠 또는 무제한 오퍼에 적합 |

#### 주요 구성 세부 정보

**UI 탐색:** 구성 요소 > 의사 결정 관리 > 배치/오퍼/의사 결정

- 각 채널 및 콘텐츠 유형 조합에 대한 배치를 만듭니다(예: 이메일 HTML 배너, 푸시 JSON, SMS 텍스트).
- 프로필 속성 또는 대상자 멤버십을 참조하는 세그먼트 규칙 표현식을 사용하여 자격 규칙 정의
- 각 배치에 대한 표시가 있는 개인화된 오퍼를 만들고, 자격 규칙을 지정하고, 우선순위를 설정합니다
- 모든 배치를 포함하는 대체 오퍼를 만듭니다. 이 오퍼는 맞춤형 오퍼가 적격하지 않을 때 반환됩니다
- 컬렉션 한정자(태그)를 사용하여 오퍼를 컬렉션으로 구성
- 우선순위 기반, 공식 기반 또는 AI 등급 전략 구성
- 배치, 컬렉션, 등급 전략 및 대체 오퍼를 바인딩하는 의사 결정 정책 만들기
- 결정을 통해 선택하기 전에 모든 오퍼를 승인하십시오.

#### 옵션 분기 위치

**옵션 A(Offer Decisioning)의 경우:**
각 채널 내에서 콘텐츠 개인화에 중점을 둔 배치 및 오퍼를 만듭니다(예: 이메일 영웅 배너 오퍼, 이메일 바닥글 오퍼, 푸시 알림 본문 오퍼). 의사 결정 정책은 메시지의 각 배치에 가장 적합한 콘텐츠를 선택합니다.

**옵션 B(동적 채널 선택)의 경우:**
각 채널을 나타내는 의사 결정 항목을 만듭니다. 자격 규칙에는 동의 확인이 포함됩니다(예: 프로필에 SMS 항목에 대한 자격이 되려면 SMS 동의가 있어야 함). 순위는 채널 참여 점수 또는 수식 기반 표현식을 사용합니다.

옵션 C의 **전체 적응형):**
두 개의 의사 결정 레이어를 구성합니다. 즉, 채널 선택을 위한 하나의 의사 결정 정책 세트와 선택한 채널 내의 컨텐츠/오퍼 선택을 위한 별도의 정책 세트를 구성합니다. 두 레이어 모두 배치, 오퍼, 자격 규칙 및 순위 전략이 필요합니다.

#### Experience League 설명서

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [의사 결정 규칙 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)

### 4단계: 메시지 작성

**응용 프로그램 함수:** [!DNL AJO]: 메시지 작성

이 단계는 여정의 각 채널 및 터치포인트에 대한 메시지 콘텐츠를 구성하여 의사 결정 출력(선택한 오퍼 콘텐츠)을 메시지 템플릿에 통합합니다. 여정의 각 메시지 작업 노드에는 적절한 채널 표면이 있는 작성된 컨텐츠, 개인화 토큰 및 오퍼 배치 통합이 필요합니다.

#### 의사 결정: 콘텐츠 접근 방식

각 채널에 대해 메시지 콘텐츠를 만들려면 어떻게 해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 템플릿 기반 | 조직은 브랜드 템플릿을 수립했습니다. 일관성은 중요합니다 | 작성 시간 단축, 브랜드 일관성 보장, 디자인 유연성 제한 |
| 처음부터 디자인 | 이 여정에 대한 고유한 크리에이티브, 기존 템플릿 없음 | 전체 디자인 제어, 긴 작성 시간, 이메일 Designer 드래그 앤 드롭 사용 |
| HTML 가져오기 | Creative 팀은 외부에서 HTML을 생성합니다. [!DNL AJO]&#x200B;(으)로 가져오기 | 외부 디자인 워크플로를 보존합니다. 이메일 Designer과의 HTML 호환성 필요 |

#### 결정: Personalization 범위

의사 결정 출력 이상의 메시지에 포함되는 개인화 수준은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기본 개인화(이름, 인사말) | 오퍼 선택을 넘어 최소한의 개인화 필요 | 간단한 Handlebars 표현식, 낮은 복잡성 |
| 조건부 콘텐츠 블록 | 서로 다른 세그먼트 또는 속성에 대해 서로 다른 콘텐츠 섹션 | 다이내믹 콘텐츠 규칙을 사용합니다. 콘텐츠는 프로필 속성 또는 세그먼트 멤버십에 따라 다릅니다. |
| 의사 결정 통합을 통한 전체 개인화 | 프로필 기반 개인화와 결합된 메시지에 포함된 오퍼 배치 | Offer Decisioning 출력을 Handlebars 개인화 토큰과 결합합니다. 풍부한 경험 |

#### 주요 구성 세부 정보

**UI 탐색:** 캠페인 또는 여정 작업 선택 > 콘텐츠 편집 > 이메일 Designer/채널 편집기

- 여정에 사용된 각 채널의 메시지 콘텐츠 작성(이메일, SMS, 푸시, 인앱)
- 의사 결정 선택 오퍼가 표시되어야 하는 메시지 콘텐츠에 오퍼 의사 결정 배치 포함
- 프로필 특성에 대한 Handlebars 구문을 사용하여 개인화 표현식 추가(예: `{{profile.person.name.firstName}}`)
- 세그먼트별 메시지를 위한 조건부 콘텐츠 블록 구성
- 공유 요소(머리글, 바닥글, 법적 고지 사항)에 대한 재사용 가능한 콘텐츠 조각 만들기
- 샘플 프로필로 미리 보고 테스트하여 개인화 렌더링이 올바르게 렌더링되는지 확인
- 관련자 검토를 위한 증명 메시지 보내기

#### 옵션 분기 위치

**옵션 A(Offer Decisioning)의 경우:**
각 메시지에는 의사 결정 선택 콘텐츠가 표시되는 오퍼 배치가 포함됩니다. 메시지 레이아웃은 일관되지만 오퍼 영역에는 각 프로필에 가장 적합한 오퍼가 동적으로 표시됩니다.

**옵션 B(동적 채널 선택)의 경우:**
각 채널에는 별도로 작성된 고유한 메시지 콘텐츠가 있습니다. 콘텐츠는 채널 간에 유사하지만 채널 제한(이메일 HTML과 SMS 텍스트 및 푸시 알림 형식)에 맞게 조정됩니다.

옵션 C의 **전체 적응형):**
각 채널에는 포함된 오퍼 배치가 있는 자체 메시지 콘텐츠가 있습니다. 채널과 해당 채널 내의 오퍼 콘텐츠는 모두 동적으로 선택됩니다.

#### Experience League 설명서

- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [SMS 메시지 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/sms/create-sms)
- [푸시 알림 디자인](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/push/design-push)

### 5단계: 여정 디자인 및 활성화

**응용 프로그램 함수:** [!DNL AJO]: Journey Orchestration, [!DNL AJO]: 충돌 및 우선 순위 관리, [!DNL AJO]: 빈도 및 비즈니스 규칙

이 단계는 항목 구성, 구성된 의사 결정 정책에 연결된 의사 결정 노드, 채널 라우팅에 대한 조건 분할(옵션 B/C), 각 채널 경로에 대한 메시지 작업 노드, 접점 간 대기 노드, 종료 기준, 충돌/우선 순위 설정 및 빈도 제한 규칙을 포함하여 전체 여정 캔버스를 구성합니다. 이 단계는 이전에 구성된 모든 구성 요소를 오케스트레이션된 여정 흐름에 조립하여 활성화합니다.

#### 결정: 재등록 정책

완료하거나 종료한 후 프로필이 여정에 다시 들어갈 수 있습니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 재등록 허용(쿨다운 포함) | 프로필이 다시 자격을 얻을 수 있는 반복 여정(예: 분기별 충성도 갱신) | 즉시 다시 들어가지 않도록 쿨다운 기간(최소 5분)을 설정합니다. 프로필이 처음부터 다시 시작됩니다. |
| 다시 등록 안 함 | 각 프로필이 한 번만 트래버스되는 일회성 여정(예: 온보딩) | 완료 또는 종료 후 프로필로 다시 들어갈 수 없음, 간단한 동작 |

#### 결정: 종료 기준

완료하기 전에 어떤 조건에서 여정을 제거해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 대상자 멤버십 변경 | 프로필이 시작 대상자를 떠나거나 제외 대상자를 입력하면 종료되어야 합니다. | 세그먼트 변경 시 실시간 종료. &quot;전환됨&quot; 또는 &quot;옵트아웃됨&quot; 종료에 유용함 |
| 이벤트 발생 횟수 | 특정 이벤트(예: 구매, 구독 취소)가 종료를 트리거해야 합니다 | 이벤트에서 실시간 종료. 이벤트 스키마 구성 필요 |
| 시간 제한 | 여정의 최대 기간 경과 | 기본 최대값은 91일이며, 프로필이 무기한 남아 있지 않도록 합니다. |

#### 결정: 여정 시간 초과

프로필이 여정에 남아 있을 수 있는 최대 기간은 얼마입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 91일(최대) | 확장된 육성 시퀀스를 사용한 장기 라이프사이클 여정 | 최대 허용 기간. 91일 후 프로필 종료 |
| 사용자 정의 짧은 기간 | 시간 제한 캠페인 또는 시즌 여정 | 여정 비즈니스 논리를 기반으로 설정. 시간 제한이 짧을수록 부실 프로필이 줄어듭니다. |

#### 결정: 충돌 및 우선 순위 설정

이 여정에 다른 여정/캠페인과의 충돌 해결에 대한 우선 순위 점수가 있어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 높은 우선 순위(70-100) | 우선해야 하는 중요한 고객 여정(유지, 충성도) | 여러 통신이 경쟁할 때 우선 순위가 높음. 제한적으로 사용 |
| Medium 우선 순위(30-69) | 표준 라이프사이클 여정 | 균형 잡힌 우선 순위, 우선 순위가 높은 통신에 의해 억제될 수 있습니다. |
| 낮은 우선 순위(0-29) | 보충 또는 정보 여정 | 더 중요한 커뮤니케이션과 경쟁할 때 억제됩니다. |

#### 주요 구성 세부 정보

**UI 탐색:** 여정 > 여정 만들기

- 여정 만들기 및 속성 구성(이름, 설명, 시간대, 시간 초과)
- 항목 구성: 대상자 읽기(배치용) 또는 이벤트 트리거(실시간용)
- 3단계에서 구성된 결정 정책에 연결된 결정 노드 추가
- 의사 결정 출력 또는 프로필 속성에 따라 채널 라우팅을 위한 조건 분할 추가(옵션 B/C)
- 각 채널 경로에 대해 메시지 작업 노드를 추가하고 4단계에서 작성된 콘텐츠에 연결합니다.
- 터치포인트 사이에 대기 노드 추가(대상 읽기 여정의 경우 최소 1시간)
- 종료 기준 정의(대상 변경, 이벤트, 시간 초과)
- 충돌 해결에 우선 순위 점수 지정
- 여정 간 빈도 제한이 적용되는 경우 빈도 제한 구성
- 게시하기 전에 테스트 프로필을 사용하여 테스트 모드에서 여정 테스트
- 여정을 게시하여 라이브로 만들기

#### 옵션 분기 위치

**옵션 A(Offer Decisioning)의 경우:**
여정 캔버스는 각 메시지 작업 노드에 포함된 의사 결정 정책으로 선형입니다. 채널 선택을 위한 분기 없음. 오퍼 결정은 작업 노드 내에서 메시지 렌더링 시간에 수행됩니다.

**옵션 B(동적 채널 선택)의 경우:**
각 대기 단계 후에 채널 선택 기준(프로필 속성, 의사 결정 출력 또는 동의 상태)을 평가하는 조건 노드를 추가합니다. 각 조건 분기는 채널별 메시지 작업 노드로 연결됩니다. 조건과 일치하지 않는 프로필에 대한 기본/else 경로를 포함합니다.

옵션 C의 **전체 적응형):**
채널 선택 조건 노드를 의사 결정 정책이 포함된 메시지 작업 노드와 결합합니다. 각 접점에서: 먼저 조건 또는 결정이 채널을 결정한 다음 선택한 채널의 메시지 작업 내에서 결정 정책이 최적의 오퍼/콘텐츠를 선택합니다.

#### Experience League 설명서

- [여정 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [대상자 활동 읽기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [조건 활동](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [여정에 메시지 추가](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [여정 테스트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [우선 순위 점수](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [충돌 및 우선 순위 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### 6단계: 보고 및 모니터링

**응용 프로그램 함수:** [!DNL AJO]: 보고 및 성능 분석

이 단계에서는 라이브 보고서(실행 중) 및 내역 보고서(완료 후)를 통해 여정 및 의사 결정 성능 모니터링을 구성합니다. 오퍼 선택 분포, 대체 비율 및 순위 효율성을 포함한 의사 결정별 지표입니다. 원할 경우, 심층 크로스 채널 여정 및 의사 결정 ROI 분석을 위한 CJA 작업 영역 분석입니다.

#### 결정: 보고 깊이

필요한 보고 분석 수준은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| [!DNL AJO]개의 기본 보고서만 | 게재 및 참여 지표에 대한 운영 모니터링 | 기본 제공 라이브 및 기록 보고서, 추가 구성 없음, [!DNL AJO] 지표로 제한됨 |
| [!DNL AJO] + CJA 분석 | 심층 크로스 채널 분석, 의사 결정 효율성, 여정 ROI, 집단 분석 | CJA 연결 및 데이터 보기 필요, 속성, funnel 및 집단 분석 기능 제공 |

#### 주요 구성 세부 정보

**UI 탐색:** 여정 > 여정 선택 > 라이브 보고서 / 모든 시간 보고서

- 시작, 종료 및 노드당 지표에 대한 초기 실행 중 여정 라이브 보고서 모니터링
- 리뷰 의사 결정 성과: 오퍼 선택 배포, 대체 오퍼 비율, 순위 효율성
- 여정 완료 후 엔드 투 엔드 funnel 분석에 대한 내역 보고서 검토
- CJA 분석의 경우: CJA 연결에 [!DNL AJO]개의 데이터 세트(메시지 피드백 이벤트, 이메일 추적 이벤트)가 포함되어 있는지 확인합니다.
- 채널 믹스 분석, 오퍼 성능 비교 및 여정 전환 단계를 위한 패널이 있는 CJA 작업 공간 구축
- 여정 시작일 및 주요 구성 변경에 대한 주석 생성

#### Experience League 설명서

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/home)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## 구현 시 고려 사항

구현 전과 중에 다음 보호, 일반적인 위험, 모범 사례 및 상충 결정을 검토하십시오.

### 보호 기능 및 제한 사항

- 샌드박스당 최대 500개의 라이브 여정 — [Journey Optimizer 보호](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/get-started/guardrails)
- 최대 여정 기간은 91일입니다(전역 시간 초과).
- 여정 캔버스당 최대 50개 활동
- 읽기 대상 여정은 초당 최대 20,000개의 프로필을 처리할 수 있습니다.
- 단일 이벤트 여정은 샌드박스당 초당 최대 5,000개의 이벤트를 지원합니다
- 샌드박스당 최대 10,000개의 승인된 개인화된 오퍼
- 의사 결정당 최대 30개 배치
- 오퍼 게재 응답 시간 SLA: 단일 범위 요청의 경우 P95에서 500ms 미만
- AI 등급 모델은 교육을 위해 최소 1,000개의 전환 이벤트가 필요합니다
- 샌드박스당 채널 유형당 최대 10개 채널 표면
- 대기 단계에는 대상 읽기 여정에 대해 최소 1시간의 기간이 있습니다.
- 여정 재진입 쿨다운 최소값은 5분입니다.
- 샌드박스당 최대 4,000개의 세그먼트 정의 — [플랫폼 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)

### 일반적인 함정

**결정은 항상 대체 오퍼를 반환합니다.** 개인화된 오퍼가 유효 날짜 범위 내에서 승인되었는지(초안 상태가 아님), 자격 규칙이 대상 프로필의 특성과 일치하는지 확인하십시오. 오퍼 한도 제한에 도달하지 않았는지 확인하십시오. 개인화된 오퍼에 대한 자격이 명확하게 되는 프로필로 테스트합니다.

**여정이 게시하지만 프로필이 입력되지 않습니다.** 대상 읽기 여정의 경우 대상의 평가된 모집단이 0보다 큰지 확인하십시오. 이벤트가 트리거된 여정의 경우 이벤트 스키마, 트리거 조건 및 이벤트가 전송되고 있는지 확인합니다. 항목 대상 병합 정책이 여정의 예상 병합 정책과 일치하는지 확인하십시오.

**순위 수식이 올바르게 적용되지 않음:** 수식 구문이 유효하고 액세스 가능한 프로필 특성을 참조하는지 확인하십시오. 수식 오류는 경고 없이 자동으로 우선 순위 기반 순위로 돌아갑니다. 다른 속성 값을 갖는 프로필로 순위를 테스트하여 수식을 확인하면 예상 순서가 생성됩니다.

**채널 라우팅에서 동의를 무시함:** 채널 선택을 위한 조건 노드에는 동의 확인이 포함되어야 합니다. SMS 동의가 없는 프로필은 SMS 경로로 라우팅할 수 없습니다. 채널 선택을 위한 의사 결정(옵션 B/C)을 사용할 때 자격 규칙에 동의를 작성하십시오.

**높은 처리량에서 오퍼 제한 카운터 지연:** 높은 처리량의 시나리오에서 오퍼 제한 카운터의 지연 시간이 몇 초일 수 있습니다. 정확한 캡핑이 중요한 경우 버퍼와 함께 글로벌 캡을 사용하거나 빈도 규칙과 결합하십시오.

**여정 캔버스가 50개 활동 제한을 초과합니다.** 채널 여정과 의사 결정 노드가 많은 복합 옵션 C 채널이 50개 활동 제한에 도달할 수 있습니다. 조건 논리를 통합하거나, 터치포인트 수를 줄이거나, 여러 순차적 여정으로 분할하여 단순화합니다.

**Edge 의사 결정에서 빈 개인 맞춤화를 반환합니다.** 실시간 의사 결정에 Edge Decisioning을 사용하는 경우 데이터 스트림에 [!DNL Adobe Journey Optimizer] 서비스가 활성화되어 있고 의사 결정 범위의 형식이 올바른지 확인하십시오. Edge 의사 결정은 edge 프로필 스토어에서 사용할 수 있는 프로필 특성으로 제한됩니다.

### 우수 사례

**단순하게 시작하여 발전하기:** 옵션 A(고정 채널, 동적 오퍼)로 시작하여 의사 결정 프레임워크의 유효성을 검사한 다음 데이터 완성도와 조직 용량이 증가함에 따라 옵션 B 또는 C로 발전합니다.

**프로필 보강에 투자:** 참여 점수, 채널 환경 설정 지수 및 고객 AI 성향 점수와 같은 계산된 특성은 의사 결정 품질을 크게 향상시킵니다. 복잡한 등급 전략을 구성하기 전에 이러한 데이터 보강 속성을 빌드합니다.

**대체 오퍼를 항상 구성:** 모든 결정 정책에는 대체 오퍼가 있어야 합니다. 대체 오퍼는 개인화된 오퍼에 대한 자격이 없는 프로필을 제공하므로 진정으로 중요한 콘텐츠(빈 자리 표시자가 아님)로 디자인할 수 있습니다.

**다양한 프로필로 테스트:** 다양한 자격 경로, 채널 환경 설정 및 특성 조합을 나타내는 프로필에 테스트 모드를 사용합니다. 게시하기 전에 가능한 각 여정 경로 및 의사 결정 결과가 올바르게 작동하는지 확인하십시오.

**대체 비율을 상태 지표로 모니터링:** 대체 오퍼율이 높으면 자격 규칙이 너무 제한적이거나 오퍼 카탈로그에서 충분한 프로필 세그먼트를 다루지 않음을 나타냅니다. 잘 구성된 의사 결정에 대해 20% 미만의 폴백 비율을 타깃팅합니다.

**채널 간 일관성을 위해 콘텐츠 조각 사용:** 여정 내의 이메일, SMS 및 푸시 메시지 간에 브랜드 일관성을 유지하기 위해 공유 콘텐츠 조각(머리글, 바닥글, 법적 고지 사항, 구독 취소 블록)을 만듭니다.

**미리 종료 기준을 구성합니다.** 메시지를 계속 받는 대신 원하는 작업을 완료한 프로필이 여정에서 즉시 제거되도록 전환 이벤트(예: 구매, 등록)에 대한 종료 기준을 정의합니다.

**의미 있는 우선 순위 점수 할당:** 여러 여정 및 캠페인을 실행할 때 비즈니스 영향에 따라 우선 순위 점수를 할당합니다. 가치가 높은 보존 여정은 정보 통신보다 우선 순위가 높아야 합니다.

### 절충안 결정

구현 선택 사항을 알려면 다음 장단점을 검토하십시오.

#### 의사 결정 복잡성과 출시 시간 비교

보다 정교한 의사 결정(AI 등급이 있는 옵션 C)을 통해 더 높은 개인화를 제공할 수 있지만 구성, 데이터 준비 및 테스트 시간이 훨씬 더 필요합니다.

- **옵션 A/B는 다음과 같습니다.** 배포 속도 향상, 테스트 간소화, 관리 부담 감소
- **옵션 C는 다음과 같은 이점을 제공합니다.** 최대 개인화, 지속적인 AI 기반 최적화, 높은 참여 가능성
- **권장 사항:** 초기 실행을 위해 옵션 A 또는 B로 시작합니다. 성능 데이터를 수집하고 프로필 보강 속성을 동시에 빌드합니다. AI 등급 교육 및 잘 채워진 오퍼 카탈로그에 대한 전환 이벤트가 1,000개 이상 있는 경우 옵션 C로 진화하십시오.

#### 채널 선택을 위한 정적 분기 및 의사 결정 비교

채널 선택은 간단한 여정 조건 노드(프로필 속성을 직접 평가)를 통해 또는 의사 결정 프레임워크(여기서 채널은 자격 및 등급이 있는 의사 결정 항목으로 모델링됨)를 통해 구현할 수 있습니다.

- **정적 조건 노드를 선호하는 경우:** 단순성, 투명성, 간단한 문제 해결. 채널 선택 논리가 간단한 경우 가장 적합합니다(예: &quot;푸시 토큰이 존재하고 30일 이내에 마지막 푸시가 열려 있는 경우 푸시를 사용합니다. 그렇지 않은 경우 이메일을 사용합니다.&quot;).
- **의사 결정 기반 채널 선택 기능:** 중앙 집중식 관리, AI 최적화 가능성, 여정 캔버스를 수정하지 않고 순위 논리를 발전시키는 기능. 채널 선택이 복잡하고 시간이 지남에 따라 개선되어야 하는 경우에 가장 적합합니다.
- **권장 사항:** 채널 선택 기준이 간단하고 잘 정의된 경우 옵션 B에 정적 조건 노드를 사용하십시오. 시간이 지남에 따라 AI가 채널 선택을 최적화하도록 하거나 채널 선택 로직이 중앙 집중식 자격 조건 및 등급 관리의 혜택을 받을 수 있을 만큼 복잡한 경우 의사 결정 기반 채널 선택을 사용합니다.

#### 세부기간 및 카탈로그 관리 기능 제공

타겟팅된 오퍼가 많은 세분화된 큰 오퍼 카탈로그는 더 정밀한 개인화를 생성하지만 더 많은 관리 노력이 필요합니다. 더 넓은 자격을 갖춘 더 작은 카탈로그는 관리가 더 쉽지만 개인화가 덜 됩니다.

- **큰 카탈로그(많은 특정 오퍼) 선호 사항:** 높은 개인화 정밀도, 다양한 대상자를 위한 더 적절한 선택, 더 낮은 대체 비율
- **작은 카탈로그(더 적은 수의 광범위한 오퍼) 선호 사항:** 관리가 용이하고, 설정이 빨라지며, 테스트가 간단하고, 고아 오퍼의 위험이 낮습니다.
- **권장 사항:** 5~15개의 맞춤형 오퍼와 의사 결정당 대체 항목으로 시작합니다. 대체 오퍼를 가장 자주 수신하는 세그먼트를 확인할 때 오퍼를 더 추가합니다. 관리 가능한 성장을 위해 컬렉션 한정자를 사용하여 카테고리, 계층 또는 제품 라인별로 오퍼를 구성합니다.

#### 우선 순위 기반 및 AI 등급 의사 결정

우선 순위 기반 순위는 결정론적이고 투명합니다. AI 등급 의사 결정은 자동으로 최적화되지만 교육 데이터가 필요하며 투명성이 떨어집니다.

- **우선 순위 기반 순위 선호도:** 예측 가능성, 투명성, 즉각적인 배포, 교육 데이터 요구 사항 없음
- **AI 등급 의사 결정 우대:** 지속적인 최적화, 데이터 기반 선택, 명확하지 않은 오퍼 프로필 관심도를 발견할 수 있는 기능
- **권장 사항:** 초기 배포에 우선 순위 기반 또는 수식 기반 순위를 사용합니다. 최소 1,000개의 전환 이벤트를 누적하고 규칙 기반에서 모델 기반 최적화로 이동하고 싶은 경우 AI 등급 의사 결정으로 전환합니다.

## 관련 설명서

다음 리소스는 이 사용 사례 패턴에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

### 여정 편성

- [여정 시작](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [여정 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [대상자 활동 읽기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [일반 이벤트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [대상자 선별 이벤트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [조건 활동](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [여정에 메시지 추가](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [여정 테스트](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)

### 의사 결정 관리

- [의사 결정 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning)
- [배치 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-placements)
- [의사 결정 규칙 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-decision-rules)
- [개인화 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-personalized-offers)
- [대체 오퍼 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-fallback-offers)
- [컬렉션 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-collections)
- [컬렉션 수식어 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-tags)
- [결정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/create-components/creating-activities)
- [순위 전략](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/ranking/ranking-strategies)
- [메시지에 오퍼 게재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/decisioning/offer-decisioning/deliver-offers/deliver-offers-in-messages)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [이메일 표면 설정](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS 채널 구성](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 메시지 작성 및 개인화

- [이메일 만들기](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/channels/email/create-email)
- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 충돌, 우선순위 및 빈도 관리

- [충돌 및 우선 순위 관리 개요](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [우선 순위 점수](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [여정 한도 및 중재](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/methods/edge-segmentation)
- [대상자 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language 참조](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/pql/overview)

### 보고 및 분석

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [CJA 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-overview/cja-overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-workspace/home)

### 프로필 및 ID

- [실시간 고객 프로필 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/home)
- [ID 서비스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/home)
- [병합 정책 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/merge-policies/overview)
- [계산된 속성 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/computed-attributes/overview)
- [Customer AI 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/intelligent-services/customer-ai/overview)

### 데이터 거버넌스 및 동의

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/home)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [제외 목록 관리](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)
- [ID 서비스 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/identity/guardrails)
