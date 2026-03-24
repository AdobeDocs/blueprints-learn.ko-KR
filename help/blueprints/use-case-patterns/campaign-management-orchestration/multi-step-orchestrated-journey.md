---
title: 여러 단계로 조정된 여정
description: 대기, 조건 및 시간 경과에 따른 여러 메시지 작업을 사용하는 분기, 다중 터치 여정을 통해 프로필을 안내하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 5667b188-1b20-4a85-aebb-74efd5f771a1
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8211'
ht-degree: 1%

---

# 여러 단계로 조정된 여정

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) 및 [!DNL Real-Time Customer Data Platform]&#x200B;(RT-CDP)을 사용하여 여러 단계로 오케스트레이션된 여정을 빌드하기 위한 포괄적인 구현 블루프린트를 제공합니다. 시간이 지남에 따라 여러 메시지를 전달하는 분기, 멀티 터치 고객 여정을 조정해야 하는 솔루션 설계자, 마케팅 엔지니어 및 구현 엔지니어를 위해 설계되었습니다.

실행 가능한 모든 구현 옵션, 모든 구성 지점의 결정 고려 사항 및 [!DNL Adobe Experience League] 설명서에 대한 링크를 제공합니다. 이 안내서를 사용하여 여러 단계로 구성된 여정 구현을 계획, 구성 및 검증할 수 있습니다.

## 사용 사례 개요

여러 단계로 구성된 통합 여정은 단일 메시지로 원하는 고객 성과를 달성하기에 충분하지 않은 비즈니스 시나리오를 처리합니다. 여정은 일회성 전송 대신 프로필 속성, 동작 신호 또는 이벤트 데이터를 기반으로 경로를 조정하는 분기 논리를 사용하여 며칠 또는 몇 주 동안 간격을 두고 이메일, SMS 메시지, 푸시 알림 또는 인앱 메시지 등 일련의 터치포인트를 통해 각 프로필을 안내합니다.

이러한 여정은 AJO에서 가장 복잡한 캠페인 패턴입니다. 대상 기반 또는 이벤트 기반 항목을 작업 노드(메시지), 조건 노드(분기 논리), 대기 노드(시간 지연) 및 종료 기준(전환 이벤트 또는 시간 초과)의 캔버스와 결합합니다. 각 프로필은 각 단계에서 컨텍스트에 맞는 콘텐츠를 제공받으며 자체 속도로 독립적으로 여정을 통해 진행됩니다.

이 패턴은 단일 전송 캠페인에 대한 일괄 아웃바운드 메시지 활성화와 단일 이벤트 응답에 대한 이벤트 트리거 메시징과 같은 더 간단한 패턴을 대체합니다. 사용 사례에서 시간에 따른 여러 상호 작용을 통해 프로필을 양성해야 하는 경우 이 패턴을 사용합니다.

>[!NOTE]
>여정에서 개별 의사 결정 지점에서 최적의 오퍼, 콘텐츠 또는 채널을 동적으로 선택해야 하는 경우 [의사 결정을 사용한 크로스 채널 여정](cross-channel-journey-with-decisioning.md)을 참조하세요. 이 패턴은 AJO Decisioning 통합으로 이 패턴을 확장합니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 고객 유지 능력 향상

가치 중심의 경험과 지속적인 관계 관리를 통해 기존 고객의 참여와 갱신을 유지합니다.

**KPI:** 유지, 고객 생애 가치, 참여

[고객 유지 관리 향상에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### 고객 온보딩 개선

능률적이고 개인화된 환영 경험과 활성화 여정을 통해 신규 고객의 가치 실현 시간을 단축합니다.

**KPI:** 참여, 유지, 전환율

[고객 온보딩 향상에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/improve-customer-onboarding.md)

### 휴면 상태 고객 재참여

행동 신호를 기반으로 타겟팅된 재활성화 캠페인을 통해 비활성 상태이거나 종료된 고객을 다시 확보할 수 있습니다.

**KPI:** 참여, 유지, 전환율

[고객 유지 관리 향상에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/improve-customer-retention.md)

### 포기한 장바구니 및 여정 복구

구매, 애플리케이션 또는 등록 중에 중단한 사용자를 적시에 개인화된 후속 조치와 함께 다시 참여시킵니다.

**KPI:** 전환율, 증분 매출, 참여

[포기한 장바구니 및 여정 복구에 대해 자세히 알아보기](/help/blueprints/business-objectives/customer-experience/recover-abandoned-carts-journeys.md)

## 예시 전술 사용 사례

다음 시나리오는 여러 단계로 조정된 여정 패턴의 일반적인 애플리케이션을 보여 줍니다.

- **고객 온보딩 시리즈** — 환영 전자 메일, 기능 교육, 등록 후 처음 14일 동안의 활성화 메시지 표시
- **재참여 드립 캠페인** - 미리 알림 이메일, 인센티브 제공, 3주 이상 경과된 고객에 대한 최종 공지
- **충성도 마일스톤 여정** — 계층 업그레이드 알림, 전용 제공, 멤버십 갱신일이 다가오면 갱신 미리 알림
- **되찾기 시퀀스** — &quot;보고싶다&quot;는 이메일을 보낸 다음 이메일을 통해 할인 오퍼를 받은 다음, 소멸된 구매자를 위한 최종 SMS 미리 알림을 보냅니다.
- **제품 채택 여정** — 평가판 시작, 사용 팁, 평가판 기간 진행 시 업그레이드 안내
- **구독 갱신 시퀀스** — 30일 알림, 7일 미리 알림, 예정된 구독 갱신에 대한 만료일 메시지
- **구매 후 양육** - 구매 후 30일 동안 감사 이메일, 사용 방법 안내서, 교차 판매 권장 사항, 검토 요청

## 주요 성과 지표

다음 KPI를 사용하여 여러 단계로 조정된 여정 구현의 효과를 측정합니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 여정 완료율 | 조기 종료 없이 전체 여정을 완료하는 프로필의 비율 | 여정 보고서: 종료됨(완료됨) / 입력됨 |
| 단계 전환율 | 한 단계에서 다음 단계로 진행되는 프로필의 백분율 | 여정 보고서의 노드당 지표 |
| 채널 참여 비율 | 각 터치포인트에서의 오픈율, 클릭스루 비율 및 응답 비율 | 메시지당 게재 및 참여 지표 |
| 종료 기준 전환율 | 여정 시간 초과 전에 종료 이벤트(예: 구매, 등록)를 트리거하는 프로필의 비율 | 종료 기준 히트 수/총 입력 |
| 전환 시간 | 여정 시작부터 종료 기준 이벤트까지의 평균 기간 | 여정 분석: 항목 타임스탬프에서 전환 이벤트 타임스탬프로의 전환 |
| 여정 드롭오프율 | 각 단계에서 관여를 중단하는 프로필의 비율(폴아웃 분석) | 여정 단계 간 CJA 폴아웃 시각화 |
| 유지/재참여 비율 | 활성 상태로 돌아가는 타겟팅된 프로필의 비율 | CJA의 여정 후 행동 분석 |

## 사용 사례 패턴

**여러 단계로 조정된 여정**

대기, 조건 및 시간 경과에 따른 여러 메시지 작업을 사용하는 분기, 다중 터치 여정을 통해 프로필을 안내합니다.

**함수 체인:** 대상 평가 > 여정 실행(다중 노드) > 조건 분기 > 메시지 배달(xN) > 종료 기준 > 보고

## 애플리케이션

다음 응용 프로그램을 사용하여 이 사용 사례 패턴을 구현합니다.

- **[!DNL Adobe Journey Optimizer](AJO)** — 여정 오케스트레이션 엔진, 메시지 작성, 채널 구성, 콘텐츠 실험, 빈도 및 충돌 관리, 보고
- **[!DNL Adobe Real-Time Customer Data Platform](RT-CDP)** — 여정 항목 대상에 대한 대상 평가 및 정의, 개인화를 위한 프로필 데이터 및 조건 분기
- **[!DNL Adobe Experience Platform](AEP)** — 프로필 저장소, ID 서비스, 이벤트 데이터 수집 및 기본 데이터 인프라

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 것 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | 여정 만들기 및 게시 권한이 있는 AJO 샌드박스 . 여정에 사용되는 모든 채널의 채널 표면을 구성해야 합니다. 사용자는 여정 및 여정 권한이 있는 적절한 역할(마케터, 캠페인 관리자)이 있어야 합니다. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 여러 메시지에서 조건 분기 및 개인화에 사용되는 특성이 있는 XDM 프로필 스키마(예: 충성도 계층, 제품 관심 분야, 참여 점수). 종료 기준 및 조건 평가를 유도하는 전환 이벤트에 대한 경험 이벤트 스키마(예: 구매 이벤트, 양식 제출). | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [스키마 구성 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| 데이터 소스 및 수집 | 가정 위치 | 종료 기준이나 조건이 실시간 이벤트에 의존하는 경우(예: 여정을 종료하는 구매 이벤트) 이벤트 스트리밍이 활성화되어야 합니다. 분기하는 데 사용되는 프로필 속성에 대한 일괄 처리 수집 동작 이벤트 수집을 위한 웹 SDK 또는 서버측 API. | [스트리밍 수집 개요](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/streaming/overview), [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| ID 및 프로필 구성 | 가정 위치 | 여정에 사용된 모든 채널(이메일, SMS, 푸시)에서 프로필을 확인할 수 있어야 합니다. 여정이 웹 및 모바일 터치포인트에 적용되는 경우 교차 장치 ID를 구성해야 합니다. 샌드박스에 대해 병합 정책을 구성해야 합니다. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| 대상 정의 및 세분화 | 필수 | 대상 읽기 여정에 대해 시작 대상을 정의해야 합니다. 분기를 위해 조건 노드에서 세그먼트를 사용할 수도 있습니다. 평가 방법(일괄 처리 또는 스트리밍)은 여정 입력 요구 사항과 일치해야 합니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 함수 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 참여 점수, 마지막 활동 이후의 일 수 또는 라이프타임 구매 값과 같은 계산된 속성은 조건 분기 논리를 개선하여 보다 지능적인 여정 경로 결정을 가능하게 합니다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | 스토리지를 관리하고 데이터 보존 규정을 준수하기 위해 여정 이벤트 데이터 보존 정책을 구성해야 합니다. 동의 적용은 옵트인 프로필만 각 채널 터치포인트에서 메시지를 수신하도록 합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [데이터 세트 만료](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/ui/dataset-expiration) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 거버넌스 레이블은 여러 메시지 터치포인트에서 호환되는 개인화를 보장합니다. 특히 여정이 채널 간 개인화에 PII 또는 중요한 데이터를 사용할 때 중요합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview) |
| 모니터링 및 가시성 | 포함됨 | 여정 실행 모니터링 처리 실패, 프로필 항목 병목 현상 및 게재 문제에 대한 경고를 모니터링합니다. 지연 또는 오류가 고객 경험에 영향을 미치는 프로덕션 여정에 필수적입니다. | [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview), [가시성 통찰력 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home) |
| 보고 및 분석 | 포함됨 | 전체 여정에서 CJA funnel 및 폴아웃 분석은 AJO 기본 보고서보다 더 심층적인 insight을 제공합니다. 단계별 전환 분석, 집단 비교 및 여정 최적화를 가능하게 합니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer]&#x200B;(AJO)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 채널 구성 | 1단계: 채널 설정 | 여정의 각 메시징 터치포인트에 대한 채널 표면(이메일, SMS, 푸시)을 구성합니다 |
| 메시지 작성 | 2단계: 메시지 콘텐츠 만들기 | 개인화, 다이내믹 콘텐츠 및 각 여정 작업 노드에 대한 템플릿을 사용하여 메시지 콘텐츠 작성 |
| Journey Orchestration | 3단계: 여정 디자인 및 활성화 | 시작, 작업, 조건, 대기 및 종료 노드가 포함된 여러 단계 여정 캔버스 디자인; 테스트 및 게시 |
| 빈도 및 비즈니스 규칙 | 4단계: 관리 및 최적화 | 여정 접점 및 기타 동시 캠페인에서 오버메시징을 방지하도록 빈도 상한을 구성합니다 |
| 충돌 및 우선 순위 관리 | 4단계: 관리 및 최적화 | 다른 활성 통신과 경쟁하는 여정에 대해 우선 순위 점수를 할당하고 충돌 감지를 구성합니다 |
| 콘텐츠 실험 | 4단계: 관리 및 최적화 | 여정 작업 노드 내의 메시지 콘텐츠에 대한 A/B 테스트를 실행하여 성능 최적화 |
| 보고 및 성능 분석 | 5단계: 보고 및 모니터링 | 여정 실행, 단계별 게재 지표 및 참여 성능 모니터링 |

### [!DNL Real-Time CDP]&#x200B;(RT-CDP)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 1단계: 채널 설정(사전 요구 사항) | 대상 읽기 여정에 대한 시작 대상을 정의하고 평가합니다. 분기를 위한 조건 대상을 정의합니다. |
| 동의 및 거버넌스 적용 | 4단계: 관리 및 최적화 | 여정 메시지 작업 전반에 동의 환경 설정 및 데이터 사용 정책 적용 |

## 필요 조건

구현을 시작하기 전에 다음 전제 조건을 완료하십시오.

- [ ] AJO 샌드박스가 여정 만들기 및 게시 권한으로 프로비저닝되었습니다.
- [ ] 하나 이상의 채널 표면(전자 메일, SMS 또는 푸시)이 구성되어 활성 상태입니다.
- [ ] 프로필 스키마에 조건 분기 및 개인화에 필요한 특성이 포함되어 있습니다.
- [ 종료 기준에 사용되는 전환 이벤트에 대해 ] 경험 이벤트 스키마가 구성되어 있습니다.
- [ 종료 기준 또는 이벤트 트리거 항목에 사용된 실시간 이벤트에 대해 ] 이벤트 스트리밍이 활성화됩니다
- [ ] ID 네임스페이스 및 병합 정책이 채널 간 프로필 확인을 위해 구성되었습니다.
- [ 각 메시지 터치포인트에 대해 ]개의 콘텐츠 자산(이미지, 복사본, CTA)이 준비되었습니다.
- [ ] 시작 대상을 정의하고 평가합니다(대상 읽기 여정).
- [ ] 이벤트 스키마 트리거가 구성되었습니다(이벤트 트리거 여정).
- [ ]개의 테스트 프로필을 여정 테스트 모드 유효성 검사에 사용할 수 있습니다.
- [ ] 비표시 목록이 검토되었으며 사용된 모든 채널에 대해 최신 상태입니다.

## 구현 옵션

다음 옵션을 검토하여 여러 단계로 오케스트레이션된 여정에 가장 적합한 접근 방식을 결정하십시오.

### 옵션 A: 대상자 읽기 오케스트레이션된 여정

**우수 사례:** 알려진 대상이 여정에 들어가고 예약된 접점(온보딩 시리즈, 갱신 시퀀스, 재참여 드릴, 충성도 마일스톤 여정)을 통해 진행되는 시간 기반 육성 시퀀스.

**작동 방식:**

대상은 여정 시작 시 일회성 읽기로 읽거나 반복 일정으로 읽습니다. 모든 자격 있는 프로필은 동시에 여정에 진입한 다음 대기 기간 및 조건 평가에 의해 제어되어 각자의 속도로 캔버스를 진행합니다. 여정을 통한 각 프로필의 경로는 독립적입니다. 어떤 프로필은 &quot;참여&quot; 분기를 취하지만, 다른 프로필은 비헤이비어 또는 속성에 따라 &quot;미참여&quot; 분기를 취합니다.

대상자는 대상자 읽기 활동이 실행될 때 평가됩니다. 반복 여정의 경우 대상은 각 반복에 대해 다시 평가되며, 여정에 이미 있는 프로필이 여정을 계속하는 동안 새로운 자격 프로필이 대상자로 진입합니다. 이 접근 방식은 예측 가능한 시작 타이밍을 제공하며 예약된 라이프사이클 프로그램에 적합합니다.

**주요 고려 사항:**

- 여정 활성화 전에 대상을 정의하고 평가해야 합니다.
- 반복 읽기를 사용하면 각 주기에 새 한정자를 입력할 수 있습니다.
- 여정의 프로필은 다시 읽지 않습니다. 새 한정자만 후속 읽기에 입력합니다
- 대기 단계에는 대상 읽기 여정에 대해 최소 1시간의 기간이 있습니다.

**장점:**

- 비즈니스 일정에 맞춰 예측 가능한 시작 시간
- 대규모 대상 볼륨 지원(초당 최대 20,000개의 프로필 기본 스로틀)
- 알려진 대상 모집단으로 간단한 테스트 및 모니터링
- 반복 입력(일별, 주별, 월별)에 대해 예약할 수 있습니다.

**제한 사항:**

- 실시간 입력이 아닌 배치 기반 — 프로필이 자격이 되었을 때가 아니라 예약된 읽기 시간에 입력합니다.
- 즉각적인 응답이 필요한 동작 시작 시퀀스에 적합하지 않음
- 읽기 사이의 대상 변경 내용은 이미 여정에 있는 프로필에 반영되지 않습니다

**Experience League:**

- [대상자 활동 읽기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [여정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)

### 옵션 B: 이벤트가 트리거된 오케스트레이션된 여정

**가장 좋은 방법:** 실시간 이벤트가 여정을 시작하는 동작 시작 시퀀스(장바구니 포기 에스컬레이션, 구매 후 육성, 마일스톤 트리거 충성도 여정, 체험판 활성화 시퀀스).

**작동 방식:**

단일 이벤트(예: 구매, 장바구니 포기, 양식 제출 또는 앱 설치)는 실시간으로 개별 프로필에 대한 여정 항목을 트리거합니다. 이벤트가 수신되면 프로필이 여정에 들어간 다음 조건을 가진 터치포인트 시퀀스, 대기 및 분기를 통해 진행합니다. 이 접근 방식은 여정 트리거 메시지의 신속성과 전체 이벤트의 여러 단계 오케스트레이션을 결합합니다.

트리거 이벤트는 스키마 및 조건이 정의된 여정 이벤트로 구성해야 합니다. 여정은 이벤트를 계속 수신하고 이벤트가 도착하면 한 번에 하나씩 프로필을 입력합니다. 후속 여정 노드는 이어질 분기를 결정하기 위해 프로필의 응답을 평가할 수 있습니다.

**주요 고려 사항:**

- 실시간 이벤트 스트리밍이 활성화되어야 합니다.
- false 트리거를 방지하도록 이벤트 스키마 및 조건을 정확하게 구성해야 합니다.
- 재입력 규칙이 중요함 — 이벤트가 다시 실행될 경우 프로필이 재입력할 수 있는지 여부를 결정합니다.
- 샌드박스당 초당 최대 5,000개의 이벤트 지원

**장점:**

- 상황에 맞는 고객 행동을 기반으로 실시간 입력
- 각 프로필은 이벤트가 발생할 때 스케줄이 아니라 독립적으로 들어갑니다
- 행동 응답 시퀀스(장바구니 포기, 구매 후)에 대한 자연어 적합도
- 입력 후 개인화된 분기를 위해 프로필 데이터와 결합할 수 있음

**제한 사항:**

- 스트리밍 이벤트 인프라를 구축해야 합니다.
- 이벤트 스키마 구성 및 테스트의 복잡성 증가
- 각 이벤트는 일괄 대상자 활성화에 적합하지 않은 하나의 프로필에 들어갑니다.
- 디버깅하려면 개별 프로필 여정을 추적해야 합니다.

**Experience League:**

- [일반 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [대상자 선별 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)

### 옵션 C: 멀티채널 오케스트레이션된 여정

**가장 좋은 방법:** 각 접점에서 서로 다른 채널을 사용하는 크로스 채널 시퀀스(이메일 및 SMS, 푸시 에스컬레이션 또는 이메일 및 인앱 보완 메시지). 대상 읽기 또는 이벤트 트리거 항목을 사용할 수 있습니다.

**작동 방식:**

이 옵션은 동일한 여정 내에 여러 메시징 채널을 통합하여 옵션 A 또는 옵션 B를 확장합니다. 여정의 각 작업 노드는 서로 다른 채널(이메일, SMS, 푸시, 인앱 또는 웹)을 타깃팅할 수 있으므로 각각에 대해 별도의 채널 표면이 필요합니다. 여정 디자이너는 각 단계에서 적절한 채널을 선택하여 에스컬레이션 패턴(예: 이메일 먼저, 참여가 없는 경우 SMS 다음) 또는 보완 패턴(예: 인앱 강화 이메일)을 활성화합니다.

크로스 채널 여정은 사용된 각 채널에 대한 채널 표면이 필요하며 채널별 개인화, 문자 제한 및 옵트인 요구 사항을 고려해야 합니다. 조건 노드는 이전 메시지와의 참여를 확인할 수 있습니다(예: &quot;열린 이메일&quot;). 을 분기 조건으로 사용하여) 다음 채널을 결정합니다.

**주요 고려 사항:**

- 여정에 사용된 각 채널에 대해 활성 채널 표면 필요
- 각 채널에는 서로 다른 개인화 기능 및 콘텐츠 제한 사항이 있습니다
- 채널별로 동의를 확인해야 합니다. 이메일에 대해 프로필이 옵트인될 수 있지만 SMS는 아닐 수 있습니다.
- 채널 간 오버메시징을 방지하도록 채널별 주파수 상한을 구성해야 합니다.

**장점:**

- 선호하는 채널에서 프로필을 참여시켜 도달 범위 극대화
- 응답하지 않는 프로필에 대한 에스컬레이션 전략 활성화
- 채널 전반의 보완 메시징을 지원하여 기능 강화
- 가장 정교한 고객 경험

**제한 사항:**

- 최고의 구현 복잡성 — 각 채널에 대한 구성 필요
- 각 터치포인트에서 각 채널에 대해 콘텐츠를 작성해야 합니다
- 채널 전반에서 동의 및 빈도 관리가 더욱 복잡해짐
- 테스트를 수행하려면 모든 채널 표면에 대한 유효성 검사가 필요합니다

**Experience League:**

- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 옵션 비교

다음 표에서는 주요 기준에서 세 가지 구현 옵션을 비교합니다.

| 기준 | 옵션 A: 대상자 읽기 | 옵션 B: 이벤트가 트리거됨 | 옵션 C: 다중 채널 |
| --- | --- | --- | --- |
| 다음에 최적 | 예약된 라이프사이클 프로그램, 육성 시리즈 | 행동 응답 시퀀스, 장바구니 포기 | 크로스 채널 에스컬레이션, 보완 메시징 |
| 시작 시간 | 예약됨(일괄 처리) | 실시간(이벤트 기반) | 예약됨 또는 실시간 |
| 복잡성 | 중간 | Medium 하이 | 높음 |
| 시작 볼륨 | 초당 최대 20,000개의 프로필 | 초당 최대 5,000개의 이벤트 | 기본 시작 메서드와 동일 |
| 채널 범위 | 단일 또는 다중 채널 | 단일 또는 다중 채널 | 여러 채널 필요 |
| 필요 | 정의된 대상자, 평가 일정 | 스트리밍 이벤트 인프라 | 각 채널에 대한 채널 표면 |
| 실시간 응답 | No — 일괄 처리 항목 | 예 — 이벤트 발생 즉시 | 시작 방법에 따라 다름 |

### 적절한 옵션 선택

다음 의사 결정 플로우를 사용하여 올바른 구현 접근 방식을 선택합니다.

1. **고객 동작 또는 이벤트에 의해 여정이 시작되었습니까?** 그렇다면 **옵션 B**(이벤트 트리거됨)을(를) 선택하십시오. 예약된 대상자 읽기에 의해 여정이 시작된 경우 **옵션 A**(대상자 읽기)을 선택합니다.

2. **여정이 여러 개의 메시징 채널(예: 전자 메일 및 SMS)을 사용합니까?** 해당하는 경우 선택한 시작 방법(A 또는 B) 위에 **옵션 C**(다중 채널)을 적용합니다. 여정이 전체에서 단일 채널을 사용하는 경우 옵션 A 또는 B만으로 충분합니다.

3. **참여를 기준으로 다른 채널로 에스컬레이션해야 합니까?** 해당하는 경우 이전 메시지와의 연결을 확인하고 대체 채널로 분기하는 조건 노드가 있는 **옵션 C**&#x200B;을(를) 선택하십시오.

4. **대상자를 미리 알고 일정에 따라 처리합니까?** 필요한 경우 **옵션 A**&#x200B;을(를) 선택하십시오. 작업을 수행하는 동안 프로필이 여정을 입력해야 하는 경우 **옵션 B**&#x200B;을 선택하세요.

## 구현 단계

다음 단계는 여러 단계로 구성된 오케스트레이션된 여정의 전체적인 구현을 안내합니다.

### 1단계: 채널 설정 및 대상자 준비

**응용 프로그램 함수:** AJO: 채널 구성, RT-CDP: 대상 평가

여정을 디자인하기 전에 모든 채널 표면이 활성 상태여야 하며, 엔트리 대상(옵션 A의 경우)을 정의하고 평가해야 합니다. 이 단계에서는 인프라가 메시지 전송 준비가 되었는지 확인합니다.

#### 각 터치포인트에 대한 채널 유형 결정

여정은 각 터치포인트에서 어떤 메시징 채널을 사용합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이메일만 | 여정은 이메일을 통해서만 통신합니다(온보딩, 교육) | 가장 간단한 설정, 이메일 하위 도메인 및 IP 풀 필요, 받은 편지함 배치 조건 |
| SMS만 | 시간 구분 경고, 약속 미리 알림 | SMS 공급자 자격 증명(Sinch, Twilio, Infobip) 필요, 메시지당 비용 상승, 보다 엄격한 옵트아웃 규칙 |
| 푸시만 | 모바일 사용자를 위한 인앱 참여 시퀀스 | APNs/FCM 자격 증명이 필요합니다. 사용자에게 앱이 설치되어 있어야 합니다. |
| 다중 채널 | 채널 간 에스컬레이션 또는 보완 메시징 | 채널당 채널 표면 필요, 가장 복잡하지만 가장 높은 도달 범위 |

#### 대상 평가 방법 결정(옵션 A)

프로필이 얼마나 빨리 참가 대상자에 적합해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 배치 평가 | 대상은 일정에 따라 읽히며(매일, 매주), 실시간 입력이 필요하지 않습니다. | 간단한 설정, 여정 읽기 전에 대상 평가, 복잡한 세그먼트 규칙 지원 |
| 스트리밍 평가 | 프로필은 속성이 변경될 때 거의 실시간으로 적합해야 합니다. | 세그먼트 규칙 표현식은 스트리밍 적격이어야 합니다. 거의 실시간으로 적격해야 합니다. |

#### 하위 도메인 위임 방법(이메일 채널) 결정

이메일 전송 하위 도메인을 Adobe에 위임하는 방법은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 전체 위임 | Adobe에서 DNS 레코드 관리, 가장 간단한 설정 | 가장 빠른 구성: Adobe이 SPF, DKIM, DMARC 처리 |
| CNAME 위임 | 조직에서 DNS 제어 유지 | DNS 관리자 개입 필요, CNAME 레코드를 구성해야 함 |

#### UI 탐색

- 채널 표면: 관리 > 채널 > 채널 표면 > 표면 만들기
- 하위 도메인: 관리 > 채널 > 하위 도메인
- SMS 구성: 관리 > 채널 > SMS 구성
- 푸시 구성: 관리 > 채널 > 푸시 알림 설정
- 대상: 고객 > 대상 > 대상 만들기 > 규칙 빌드

#### 주요 구성 세부 정보

- 이메일에 대한 IP 풀 정리 상태 확인 — 새로운 IP 풀은 2-4주에 걸쳐 점진적인 정리 계획이 필요합니다.
- SMS의 경우 공급자 자격 증명을 구성하고 발신자 번호 등록을 확인합니다
- 푸시의 경우 APNs 인증서 및 FCM 서버 키 업로드
- 대상 모집단을 다루는 세그먼트 규칙과 함께 세그먼트 빌더를 사용하여 시작 대상자 정의
- 대상 정의에 제외 규칙 포함(최근에 전환됨, 전체적으로 구독 취소됨 제외)

#### 옵션 분기 위치

**옵션 A(대상자 읽기)의 경우:**
시작 대상자를 정의하고 평가합니다. 대상자에 0이 아닌 모집단이 있는지 확인합니다. 여정이 일회성 대상자 읽기 또는 반복 읽기 일정을 사용할지 여부를 결정합니다.

**옵션 B(이벤트 트리거됨)의 경우:**
트리거 이벤트 스키마가 구성되어 있고 이벤트가 플랫폼으로 스트리밍되는지 확인하십시오. 사전 정의된 대상이 필요하지 않습니다. 프로필은 이벤트 수신 시 개별적으로 입력합니다.

**옵션 C(다중 채널)의 경우:**
여정(이메일, SMS, 푸시, 인앱)에 사용되는 각 채널에 대한 채널 표면을 구성합니다. 대상 모집단에 대한 채널별 동의 상태를 확인합니다.

#### Experience League 설명서

- [채널 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)


### 2단계: 메시지 콘텐츠 만들기

**응용 프로그램 함수:** AJO: 메시지 작성

여정의 각 터치포인트에 대한 메시지 콘텐츠를 작성합니다. 각 메시지는 서로 다른 콘텐츠, 개인화 깊이 및 채널을 가질 수 있다. 이 단계에서는 여정 작업 노드가 참조할 모든 제공 가능한 콘텐츠를 작성합니다.

#### 콘텐츠 접근 방식 결정

각 메시지를 템플릿에서 시작하거나, 처음부터 디자인하거나, HTML을 가져와야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기존 콘텐츠 템플릿 | 레이아웃이 설정된 브랜드 일치 메시지 | 가장 빠름, 브랜드 규정 준수 보장, 템플릿이 존재하고 채널 유형과 일치해야 함 |
| 처음부터 디자인 | 각 터치포인트에 대한 고유하고 사용자 정의 레이아웃 | 가장 유연하고 긴 빌드 시간; 이메일 Designer 드래그 앤 드롭 사용 |
| HTML 가져오기 | 외부 디자인 도구에서 사전 빌드된 HTML | 깨끗한 HTML 필요, 응답성을 위해 조정이 필요할 수 있음 |

#### 개인화 깊이 결정

각 메시지에 포함되는 개인화는 얼마입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기본 토큰 삽입 | 이름, 도시, 단순 프로필 속성 | 복잡성 감소, XDM 경로에서 Handlebars 구문 사용 |
| 조건부 콘텐츠 블록 | 세그먼트 또는 속성에 따라 다른 콘텐츠 표시 | Medium 복잡성, 다이내믹 콘텐츠 규칙 필요 |
| 여정 컨텍스트 기반 개인화 | 콘텐츠는 여정 경로, 이전 상호 작용에 따라 다릅니다 | 복잡성 증가, 여정 컨텍스트 변수 및 이벤트 데이터 활용 |

#### 조각 전략 결정

공유 콘텐츠 블록(머리글, 바닥글, 법적 텍스트)을 재사용 가능한 조각으로 생성해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 재사용 가능한 조각 | 여러 메시지가 공통 요소를 공유하므로 브랜드 일관성이 필요합니다. | 변경 사항은 조각을 사용하여 모든 메시지에 전파됩니다. 메시지당 최대 30개의 조각 |
| 인라인 콘텐츠 | 고유한 레이아웃이 있는 일회성 메시지 | 단일 사용 콘텐츠에 더 빨리 제공, 메시지 간 일관성에 이점 없음 |

#### UI 탐색

- 컨텐츠 관리 > 컨텐츠 템플릿 > 찾아보기
- 이메일 Designer(캠페인 또는 여정 작업 내)
- 콘텐츠 관리 > 조각 > 조각 만들기

#### 주요 구성 세부 정보

- 여정의 각 메시지 작업에 대한 컨텐츠 작성 — 4단계 여정은 4개의 개별 메시지 디자인이 필요할 수 있습니다
- XDM 프로필 경로를 참조하는 개인화 표현식 사용(예: `{{profile.person.name.firstName}}`)
- 세그먼트별 변형에 대한 동적 콘텐츠 블록 구성
- 테스트 프로필로 각 메시지를 미리 보고 개인화 렌더링 확인
- 콘텐츠 검토를 위해 내부 이해 당사자에게 증명 보내기
- SMS의 경우 문자 제한(표준 GSM 인코딩의 경우 160자)을 준수합니다
- 푸시의 경우 제목, 본문, 이미지 및 딥링크/URL 작업 구성

#### Experience League 설명서

- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [이메일 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [SMS 메시지 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [푸시 알림 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)


### 3단계: 여정 디자인 및 활성화

**응용 프로그램 함수:** AJO: Journey Orchestration

시작 노드, 작업 노드(메시지), 조건 노드(분기), 대기 노드(시간 지연) 및 종료 기준을 포함하는 여러 단계 여정 캔버스를 디자인합니다. 그런 다음 테스트 프로필로 테스트하고 게시합니다.

#### 항목 유형 결정

프로필은 어떻게 여정을 입력합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 대상자 읽기 | 예약된 육성 시퀀스, 일괄 처리된 알려진 대상 | 읽기 시 대상 평가, 일회성 또는 반복 읽기 지원, 초당 최대 20,000개의 프로필 수 |
| 단일 이벤트 | 실시간 행동 트리거(구매, 장바구니 포기) | 실시간 입력, 이벤트 스트리밍 필요, 최대 5,000개 이벤트/초 |
| 대상 자격 조건 | 프로필이 거의 실시간으로 대상자에 들어오거나 나갈 때 시작 | 스트리밍 평가, 세그먼트 멤버십 변경에 의해 트리거됨 |
| 비즈니스 이벤트 | 조직 전체의 이벤트는 대상에 대한 여정을 트리거합니다. | 제품 출시, 날씨 이벤트, 시스템 경고에 유용함 |

#### 재등록 정책 결정

완료 또는 종료 후 프로필이 여정에 다시 들어갈 수 있습니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 재등록 허용(쿨다운 포함) | 프로필은 여정을 반복해야 할 수 있습니다(반복 구매, 시즌 재참여) | 최소 쿨다운 5분. 쿨다운 창 내에서 중복 항목을 방지합니다. |
| 다시 등록 안 함 | 일회성 여정(온보딩, 단일 라이프사이클 이벤트) | 프로필이 여정을 완료하거나 종료하므로 다시 입력할 수 없습니다. |

#### 접점 간 대기 기간 결정

여정은 각 메시지 사이에 얼마나 기다려야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 고정 기간(예: 3일) | 프로필 동작에 관계없이 일관된 게재 간격 | 간단하고 예측 가능한 시간, 대상 읽기 여정에 최소 1시간 |
| 특정 날짜/시간 | 메시지가 정확한 시간에 도착해야 합니다(예: 갱신 날짜). | 프로필 속성 또는 표현식을 사용하여 정확한 날짜/시간 확인 |
| 사용자 정의 표현식 | 프로필 데이터 또는 여정 컨텍스트를 기반으로 동적 대기 | 가장 유연함, 표현식 작성 필요 |

#### 분기 조건 결정

프로필에 적용할 경로를 결정하는 조건은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 프로필 속성 확인 | 충성도 계층, 제품 관심 분야, 지역을 기반으로 한 분기 | 평가 시 사용 가능한 프로필 데이터 사용 |
| 세그먼트 멤버십 확인 | 프로필이 특정 대상에 속하는지 여부를 기반으로 한 분기 | 대상자를 정의하고 평가해야 함 |
| 이벤트 데이터 검사 | 프로필에서 작업을 수행했는지 여부(열린 이메일, 클릭한 링크)를 기반으로 한 분기 | 여정 범위 이벤트 데이터를 평가합니다. 참여 기반 분기에 유용합니다. |
| 비율 분할 | 경로 간에 프로필을 임의로 배포(A/B 테스트 또는 제어된 롤아웃) | 프로필 데이터 사용 안 함, 무작위 할당 |

#### 종료 기준 결정

프로필이 여정을 조기에 종료하는 이벤트 또는 조건은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 전환 이벤트 | 프로필이 원하는 작업(구매, 등록, 양식 제출)을 완료합니다 | 이벤트 스트리밍 필요, 가장 일반적인 종료 기준 |
| 대상자 멤버십 종료 | 프로필이 시작 대상자를 떠나거나 제외 대상자에 참여합니다. | 스트리밍 대상에 대해 거의 실시간으로 평가됩니다. |
| 시간 제한 | 최대 여정 기간 도달(최대 91일) | 기본 안전망, 여정 속성에서 구성 가능 |
| 종료 기준 없음 | 프로필이 전체 여정 경로를 자동으로 완료합니다 | 가장 간단함. 수동으로 제거하지 않는 한 모든 프로필이 전체 여정 통과 |

#### 여정 시간 초과 결정

프로필이 여정에 남아 있을 수 있는 최대 기간은 얼마입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 91일(최대) | 장기 실행 여정(분기별 갱신, 확장 온보딩) | 최대 허용. 시간 초과 시 여정에 남아 있는 프로필은 자동으로 종료됩니다 |
| 사용자 정의 짧은 기간 | 여정은 정의된 기간(7일, 14일, 30일) 내에 완료되어야 합니다. | 사용 사례의 자연 라이프사이클을 기반으로 설정 |

#### UI 탐색

- 만들기 여정: 여정 > 여정 만들기
- 여정 속성: 여정 캔버스 > 속성 패널
- 시작 노드: 여정 캔버스 > &quot;대상자 읽기&quot; 또는 이벤트 활동 드래그
- 작업 노드: 여정 캔버스 > 채널 드래그 작업(이메일, SMS, 푸시)
- 조건 노드: 여정 캔버스 > &quot;조건&quot; 활동 끌기
- 대기 노드: 여정 캔버스 > &quot;대기&quot; 활동 드래그
- 종료 기준: 여정 속성 > 종료 기준 > 구성
- 테스트 모드: 여정 캔버스 > 테스트 모드 전환
- 게시: 여정 캔버스 > 게시

#### 주요 구성 세부 정보

- 명확한 설명 규칙을 사용하여 여정 이름을 지정합니다(예: &quot;Onboarding_Series_Email_v1&quot;).
- 일관된 대기 단계 처리를 위한 여정 시간대 설정
- 각 작업 노드를 적절한 채널 표면과 작성된 메시지 콘텐츠에 대한 링크로 구성합니다
- 모든 분기는 종료 활동으로 종료해야 합니다.
- 사용 사례에 적합한 재입력 규칙 구성
- 테스트 프로필과 함께 테스트 모드를 사용하여 게시하기 전에 전체 여정 경로를 시뮬레이션하십시오
- 테스트 프로필이 예상 경로를 통과하고 올바른 메시지를 수신하는지 확인합니다.

#### 옵션 분기 위치

**옵션 A(대상자 읽기)의 경우:**

- &quot;대상자 읽기&quot; 활동을 시작 노드로 드래그합니다.
- 1단계에서 정의된 대상 선택
- 필요한 경우 반복 읽기 일정(일별, 주별) 구성
- 다운스트림 시스템 로드가 문제인 경우 읽기 속도 스로틀을 구성합니다

**옵션 B(이벤트 트리거됨)의 경우:**

- 트리거 이벤트를 시작 노드로 드래그합니다.
- 이벤트 스키마 및 항목 조건 구성
- 재입력 규칙을 신중하게 설정하여 반복되는 이벤트에서 중복 항목을 방지합니다.

**옵션 C(다중 채널)의 경우:**

- 옵션 A 또는 B의 입력 방법 사용
- 각 작업 노드에서 해당 터치포인트에 대한 적절한 채널 표면을 선택합니다
- 채널 사이에 조건 노드를 추가하여 참여를 확인합니다(예: &quot;프로필에서 이메일을 열었습니까?&quot;). 대체 채널로 이동

#### Experience League 설명서

- [여정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [대상자 활동 읽기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [일반 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [대상자 선별 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [여정에 메시지 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [조건 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)
- [종료 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [여정 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)


### 4단계: 관리 및 최적화 구성

**응용 프로그램 기능:** AJO: 빈도 및 비즈니스 규칙, AJO: 충돌 및 우선 순위 관리, AJO: 콘텐츠 실험, RT-CDP: 동의 및 거버넌스 적용

과도한 메시징을 방지하기 위해 빈도 상한을 적용하고, 다른 활성 통신과의 충돌 해결에 우선 순위 점수를 할당하고, 선택적으로 여정 메시지 내에 A/B 테스트를 구성하고, 동의 적용을 확인합니다.

#### 빈도 상한 구성 결정

여정 메시지가 전역 빈도 상한을 준수해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 빈도 규칙 적용 | 여정은 다른 캠페인 및 여정과 함께 작동하므로 프로필을 과도하게 보내서는 안 됩니다 | 프로필이 다른 통신에서 이미 최대 한도를 초과한 경우 메시지가 표시되지 않을 수 있습니다 |
| 캡핑 제외 | 여정 메시지는 매우 중요하며 항상 전달되어야 합니다(트랜잭션, 규정). | 제한적으로 사용. 과다 사용할 경우 메시지 피로에 기여할 수 있음 |

#### 우선 순위 점수 할당 결정

다른 활성 캠페인 및 여정과 관련하여 이 여정의 등급은 어떻게 매겨야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 높은 우선 순위(70-100) | 여정 메시지는 중요한 라이프사이클 커뮤니케이션(온보딩, 갱신) | 다른 통신과 충돌이 발생할 때 우선 순위가 높은 것이 좋습니다. |
| Medium 우선 순위(30-69) | 여정 메시지는 중요하지만 시급하지 않습니다(육성, 교육) | 우선 순위가 높은 통신에 의해 억제될 수 있음 |
| 낮은 우선 순위(0-29) | 여정 메시지는 보충 또는 홍보용 메시지입니다 | 우선 순위가 높은 메시지와 경쟁할 때 억제됩니다. |

#### 콘텐츠 실험 결정

여정 메시지에 A/B 또는 다변량 테스트가 포함되어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 예 — A/B 테스트 | 특정 터치 포인트에서 제목 줄, CTA 또는 컨텐츠 레이아웃 최적화 | 통계적 유의성을 위해 변형당 충분한 양 필요, 2~10회 처리 지원 |
| 실험 없음 | 콘텐츠가 완료되었거나 볼륨이 너무 낮아 의미 있는 테스트를 수행할 수 없습니다. | 간단한 설정, 변형 추적 불필요 |

#### UI 탐색

- 빈도 규칙: 관리 > 비즈니스 규칙 > 규칙 만들기
- 우선 순위 점수: 여정 속성 > 우선 순위 점수
- 충돌 탐지: 관리 > 비즈니스 규칙 > 충돌 및 우선 순위
- 콘텐츠 실험: 여정 캔버스 > 메시지 작업 선택 > 콘텐츠 실험 전환
- 동의 정책: 개인 정보 > 정책 > 동의 정책

#### 주요 구성 세부 정보

- 채널별 빈도 상한 설정(예: 최대 3개의 이메일/주, 최대 1개의 SMS/일, 최대 2개의 푸시/일)
- 다른 활성 통신에 비해 비즈니스 중요도를 반영하는 여정(0-100)에 우선 순위 점수를 지정합니다
- 충돌 감지 패널을 검토하여 겹치는 캠페인이나 여정을 식별합니다
- 콘텐츠 실험을 실행하는 경우, 처리 변형을 정의하고, 트래픽 할당을 설정하고, 성공 지표(열기, 클릭 또는 전환)를 선택하고, 신뢰 임계값(일반적으로 95%)을 설정합니다.
- 여정에 사용된 각 채널에 대해 동의 집행이 활성화되어 있는지 확인합니다

#### Experience League 설명서

- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [비즈니스 규칙 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [여정 한도 및 중재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)


### 5단계: 보고 및 모니터링 구성

**응용 프로그램 함수:** AJO: 보고 및 성능 분석, 모니터링 및 가시성, 보고 및 분석

활성화 중 및 활성화 후 여정 실행을 모니터링하고, 단계별로 게재 및 참여 지표를 검토하고, 여정 처리 오류에 대한 경고를 구성하고, 필요한 경우 딥funnel 및 폴아웃 시각화를 위한 CJA 작업 영역 분석을 빌드합니다.

#### 보고 방법 결정

이 여정에 필요한 보고 도구는 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| AJO 기본 보고서만 | 기본 제공 및 참여 모니터링으로 충분함 | 라이브 보고서(실행 중) 및 모든 시간 보고서(실행 후). 라이브에 대해 60초마다 새로 고칩니다. |
| AJO + CJA 분석 | 딥funnel 분석, 단계 전환율, 폴아웃 시각화 또는 여정 간 비교가 필요합니다 | CJA 데이터 세트에 연결된 AJO 연결 및 데이터 보기 필요, 가장 포괄적 |
| CJA 전용 | 조직은 CJA을 기본 분석 플랫폼으로 사용합니다 | CJA 구성이 필요합니다. AJO 기본 보고서는 여전히 백업으로 사용할 수 있습니다. |

#### 경고 구성 결정

경고를 트리거해야 하는 여정 실패는 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 여정 처리 경고 | 프로덕션 여정에 항상 권장 | 프로필 항목 실패, 작업 노드 오류 및 여정 정지에 대한 경고 |
| 게재 실패 경고 | 고가치 커뮤니케이션 여정에 중대 | 임계값을 초과하는 바운스 비율, 게재 실패에 대한 경고 |

#### UI 탐색

- 라이브 보고서 여정: 여정 > 여정 선택 > 라이브 보고서
- 모든 시간 보고서 여정: 여정 > 여정 선택 > 모든 시간 보고서
- 경고: 경고 > 경고 규칙 > 가입
- CJA 작업 공간: 프로젝트 > 새 프로젝트 만들기

#### 주요 구성 세부 정보

- 여정 실행 중에 라이브 보고서에 액세스하여 프로필 항목, 종료 및 단계별 게재 지표를 실시간으로 모니터링합니다
- 여정 완료 후(또는 충분한 데이터가 누적된 후) 전체 시간 보고서를 검토하여 포괄적인 분석을 수행합니다
- 여정 처리 실패 및 게재 문제에 대한 플랫폼 경고 구성
- CJA 분석의 경우 CJA 연결에 AJO 경험 이벤트 데이터 세트(메시지 피드백, 이메일 추적, 여정 단계 이벤트)가 포함되어 있는지 확인합니다
- 다음을 사용하여 CJA Workspace 구축:
   - 각 여정 단계에서 프로필 수를 보여주는 funnel 시각화
   - 폴아웃 시각화를 통해 드롭오프 지점 식별
   - 단계 전환율 계산
   - 전환 시간 분석
   - 채널 수준 참여 분류 (다중 채널 여정의 경우)

#### Experience League 설명서

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## 구현 시 고려 사항

구현 전과 중에 다음 보호 기능, 위험, 모범 사례 및 장단점을 검토하십시오.

### 보호 기능 및 제한 사항

- 샌드박스당 최대 **500개의 라이브 여정** — [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 최대 **여정 기간은 91일**(전역 시간 제한)입니다. 시간 제한 시 여정에 있는 프로필은 자동으로 종료됩니다
- 여정 캔버스당 최대 **50개 활동**
- 초당 최대 **20,000개의 프로필 읽기**(기본 스로틀)
- 단일 이벤트 여정은 샌드박스당 최대 **초당 5,000개의 이벤트**&#x200B;를 지원합니다.
- 대기 단계에는 대상 읽기 여정에 대해 **최소 기간 1시간**&#x200B;이 있습니다.
- 여정 **다시 시작 쿨다운 최소값은 5분**&#x200B;입니다.
- 샌드박스당 최대 **채널 유형당 10개 채널 표면**
- 최적의 전달성을 위해 권장되는 최대 이메일 크기: **100KB**
- 메시지당 최대 **30개의 콘텐츠 조각**
- 실험당 최대 **10개의 콘텐츠 실험 처리**(변형)
- 샌드박스당 최대 **최대 구성**&#x200B;개
- 샌드박스당 최대 **4,000개의 세그먼트 정의**

### 일반적인 함정

- **테스트하지 않고 게시:** 게시하기 전에 항상 테스트 프로필과 함께 테스트 모드를 사용하여 전체 여정 경로의 유효성을 검사하십시오. 프로필이 예상 분기를 통과하고 대기 단계가 올바로 진행되며 메시지가 제대로 렌더링되는지 확인하십시오.
- **여정에 종료 활동이 없습니다.** 모든 분기 분기는 종료 활동으로 종료해야 합니다. 종료 노드가 없는 분기가 남아 있으면 여정을 게시할 수 없습니다.
- **매우 광범위한 시작 조건:** 느슨하게 정의된 시작 대상 또는 이벤트 조건이 의도하지 않은 프로필로 여정을 채울 수 있습니다. 특정 속성 확인 및 제외 규칙으로 항목 기준을 세분화합니다.
- **다시 시작 규칙을 무시합니다.** 이벤트가 트리거된 여정의 경우 프로필에서 트리거된 이벤트를 여러 번 실행할 수 있습니다. 적절한 재입력 구성(재입력 거부 또는 쿨다운 기간)이 없으면 프로필이 여정에 누적되어 메시지가 중복될 수 있습니다.
- **대기 단계 시간대 혼동:** 대기 기간이 UTC로 처리됩니다. 예상 로컬 시간에 대기 단계가 진행되도록 여정 속성에서 여정 시간대를 명시적으로 설정합니다.
- **실시간 여정 편집:** 실시간 여정은 직접 편집할 수 없습니다. 변경하려면 여정을 복제하고 복사본을 수정하고 원본을 중지하고 새 버전을 게시합니다. 시작하기 전에 여정 버전 관리를 계획하십시오.
- **종료 기준이 정의되지 않음:** 종료 기준이 없으면 중간 여정을 전환하는 프로필은 관련 없거나 모순될 수 있는 후속 메시지를 계속 수신하게 됩니다. 전환 이벤트에 대한 종료 기준을 항상 구성합니다.
- **채널 동의 정렬 오류:** 프로필이 전자 메일에 대해 옵트인될 수 있지만 SMS는 아닐 수 있습니다. 다중 채널 여정은 채널별 동의를 준수해야 합니다. 동의 필드가 각 채널 표면에 채워지고 적용되는지 확인합니다.

### 우수 사례

- **단순 시작, 반복:** 복잡한 분기를 추가하기 전에 선형 2-3단계 여정으로 시작합니다. 조건 및 채널에서 계층화하기 전에 핵심 흐름이 작동하는지 확인하십시오.
- **설명 이름 지정 규칙을 사용합니다.** 이름 여정 노드, 조건 및 대기 단계(예: &quot;Wait 1&quot; 대신 &quot;Wait_3_Days_After_Welcome&quot;). 이렇게 하면 테스트 모드 디버깅 및 보고서 해석이 훨씬 쉬워집니다.
- **미리 종료 기준을 구성합니다.** 여정 경로를 디자인하기 전에 전환 이벤트를 종료 기준으로 정의합니다. 이렇게 하면 전환한 프로필이 진행 중인 단계에 관계없이 여정에서 제거됩니다.
- **의미 있는 대기 시간 설정:** 고객 행동 데이터를 기본 대기 시간(일반 상호 작용, 예상 응답 창 및 채널 관련 케이던스(예: 이메일 간 2~3일, SMS 간 1주))으로 설정합니다.
- **조건 노드를 사용하여 참여 확인:** 메시지 작업 후 조건을 추가하여 프로필이 참여(열림, 클릭)되었는지 확인합니다. 연결된 프로필을 한 경로로 라우팅하고 연결되지 않은 프로필을 에스컬레이션 또는 대체 채널 경로로 라우팅합니다.
- **분기를 위해 계산된 특성 활용:** 참여 점수, 구매 빈도 또는 마지막 활동 이후의 일 수와 같은 계산된 특성을 사용하여 임의로 분기하지 않고 데이터 기반의 분기 결정을 내릴 수 있습니다.
- **반복적으로 모니터링 및 최적화:** 처음 실행하는 동안 매주 여정 보고서를 검토합니다. 드롭오프 지점을 식별하고, 대기 시간을 조정하고, 조건을 세분화하고, 단계별 성능 데이터를 기반으로 메시지 콘텐츠를 최적화합니다.
- **여정 버전:** 변경할 때 여정을 복제하여 새 버전을 만드십시오. 감사 및 최적화 추적을 위해 버전 변경 사항 로그를 유지 관리합니다.

### 절충안 결정

다음과 같은 상충관계는 특정 비즈니스 요구 사항의 맥락에서 평가되어야 합니다.

#### 대상 읽기 항목과 이벤트 트리거 항목 비교

대상자 읽기 항목은 보다 쉽게 관리하고 테스트할 수 있는 예측 가능한 일괄 처리 기반 처리를 제공합니다. 이벤트 트리거 항목은 상황에 따라 더 연관성이 있지만 스트리밍 인프라 및 보다 세심한 재진입 관리가 필요한 실시간 응답성을 제공합니다.

- **대상자 읽기 우대:** 예측 가능성, 대용량 처리, 예약된 라이프사이클 프로그램, 간단한 테스트
- **이벤트 트리거된 선호도:** 실시간 관련성, 행동 컨텍스트, 개별 프로필 간격, 고객 행동에 대한 즉각적인 응답
- **권장 사항:** 시간이 비즈니스 중심인 계획된 라이프사이클 프로그램(온보딩, 갱신)에는 대상 읽기를 사용하십시오. 타이밍이 고객 중심인 행동 응답 시퀀스(장바구니 포기, 구매 후)에 대해 이벤트가 트리거된 사용자 지정 규칙을 사용합니다.

#### 단일 채널과 다중 채널 여정 비교

단일 채널 여정은 구현, 테스트 및 관리가 더 간단합니다. 멀티채널 여정은 광범위한 도달 및 에스컬레이션 기능을 제공하지만 콘텐츠 작성, 동의 관리 및 빈도 거버넌스의 복잡성을 증가시킵니다.

- **단일 채널 우대:** 더 빠른 구현, 더 간단한 동의 관리, 더 낮은 콘텐츠 제작 노력, 더 쉬운 디버깅
- **다중 채널 지원:** 높은 참여 가능성, 반응하지 않는 프로필에 대한 채널 에스컬레이션, 보다 포괄적인 고객 경험
- **권장 사항:** 단일 채널 여정으로 시작하여 다중 채널로 확장하기 전에 흐름 및 비즈니스 영향을 확인하십시오. 참여 데이터가 기본 채널이 대상자에게 효과적으로 도달하지 않는 채널을 점진적으로 추가합니다.

#### 여정 복잡성과 관리 용이성 비교

많은 조건과 경로가 있는 고도로 분기된 여정은 더 많은 시나리오를 처리할 수 있지만 테스트, 디버그 및 최적화가 더 어려워집니다. 더 적은 수의 분기로 더 간단한 여정을 관리하면 더 쉽지만 덜 개인화된 경험을 제공할 수 있습니다.

- **복잡한 여정 선호:** 세분화된 개인화, 세그먼트별 경로, 포괄적인 시나리오 적용 범위
- **여정이 더 간단합니다.** 배포 시간 단축, 테스트 용이성, 보고 명확성, 유지 관리 부담 감소
- **권장 사항:** 여정을 3~5개의 주 분기 및 15~25개의 활동으로 제한합니다. 논리의 복잡성이 더 필요한 경우 단일 모노리식 여정이 아닌 여정 간 조정을 통해 여러 여정으로 분할하는 것이 좋습니다.

#### 빈도 상한 엄격성 대 여정 완료

엄격한 빈도 상한은 초과 메시징으로부터 보호하지만 여정 메시지를 표시하지 않아 프로필이 단계를 건너뛰고 여정 완료율을 낮출 수 있습니다. Lenient Caps는 여정 메시지가 전달되지만 채널 피로가 발생할 수 있습니다.

- **Strict caps favor:** 고객 환경 보호, 구독 취소 비율 감소, 브랜드 신뢰
- **Lenient caps favor:** 여정 완료율, 전체 메시지 시퀀스 게재, 마케팅 프로그램 효율성
- **권장 사항:** 최대 한도에 도달하면 중요 여정 메시지(온보딩, 갱신)에 우선 순위 점수를 더 높게 할당하여 프로모션 캠페인보다 우선합니다. 진정한 필수 커뮤니케이션에만 &quot;최대 가용량 면제&quot;를 예약합니다.

## 관련 설명서

다음 리소스는 이 구현에 사용되는 기능에 대한 추가 세부 정보를 제공합니다.

### 여정

- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [여정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-gs)
- [여정 속성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/journey-properties)
- [여정 게시](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/publishing-the-journey)
- [여정 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/testing-the-journey)

### 여정 활동

- [대상자 활동 읽기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [일반 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/general-events)
- [대상자 선별 이벤트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/audience-qualification-events)
- [조건 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity)
- [대기 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/wait-activity)
- [여정에 메시지 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/journeys-message)
- [종료 활동](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/end-activity)
- [사용자 정의 액션 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions)

### 시작 및 종료 관리

- [여정 항목 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/entry-management)
- [종료 기준](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/create-journey/exit-criteria)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [채널 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)

### 메시지 작성 및 개인화

- [이메일 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [이메일 Designer 콘텐츠 구성 요소 사용](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)
- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)

### 콘텐츠 실험

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [통계적 계산](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### 빈도, 충돌 및 우선 순위

- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [비즈니스 규칙 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [충돌 및 우선 순위 관리 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [여정 한도 및 중재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/api/edge-segmentation)

### 보고 및 분석

- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)
- [Analysis Workspace 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/home)
- [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)

### 동의 및 거버넌스

- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)
- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [제외 목록 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### 데이터 기반

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [프로필 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/home)
- [계산된 속성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview)
