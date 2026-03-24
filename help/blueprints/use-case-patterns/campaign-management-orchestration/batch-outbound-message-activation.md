---
title: 일괄 아웃바운드 메시지 활성화
description: 대상자를 평가하고 예약된 아웃바운드 메시지를 단일 배치 실행으로 전달하는 방법을 알아봅니다.
solution: Journey Optimizer, Real-Time Customer Data Platform
exl-id: 192853ce-02ab-46e6-9092-3db5354bc19c
source-git-commit: e8185f348f926acab2ca2e0c3cd55c08c663cf41
workflow-type: tm+mt
source-wordcount: '8246'
ht-degree: 1%

---

# 일괄 아웃바운드 메시지 활성화

이 안내서에서는 [!DNL Adobe Journey Optimizer]&#x200B;(AJO) 및 [!DNL Adobe Real-Time Customer Data Platform]&#x200B;(RT-CDP)을 사용하여 정의된 대상 세그먼트에 예약된 아웃바운드 메시지를 전달하기 위한 전체 구현 참조를 제공합니다. 실행 가능한 모든 구현 접근 방식, 각 선택을 유도하는 결정 고려 사항 및 [!DNL Adobe Experience League]에 대한 자세한 설명서를 찾을 위치를 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

일괄 아웃바운드 메시지 활성화는 일대다 아웃바운드 메시지의 기본 캠페인 패턴입니다. 대상 정의부터 메시지 전달 및 성능 분석에 이르기까지 전체 라이프사이클을 다룹니다. 이 안내서에서는 예약된 캠페인, 대상자에서 트리거된 여정 및 API에서 트리거된 캠페인의 세 가지 구현 옵션을 제공하고, 각 사용 사례에 적합한 접근 방식을 선택하기 위한 구조화된 결정 지침을 제공합니다.

구현 옵션, 거래 분석, UI 탐색 경로 및 [!DNL Experience League] 설명서 참조를 제공합니다.

## 사용 사례 개요

조직은 특정 시간에 또는 시스템 이벤트에 대한 응답으로 알려진 대상 세그먼트에 단일 메시지를 전달해야 하는 경우가 많습니다. 이 패턴은 [!DNL RT-CDP]의 대상 평가를 [!DNL Journey Optimizer]의 메시지 작성 및 캠페인 실행과 결합하여 해당 요구 사항을 해결합니다.

비즈니스 시나리오는 간단합니다. 메시지를 받을 사용자를 정의하고, 개인화로 메시지 콘텐츠를 만들고, 대상자와 메시지를 캠페인이나 여정에 바인딩하고, 일정에 따라, 대상자 자격을 통해 또는 시스템 트리거를 통해 전송을 실행합니다. 그 결과 게재, 참여 및 전환 지표에 대한 전체 보고가 포함된 메시지가 전달됩니다.

이 패턴은 한 번의 실행으로 알려진 대상자에게 단일 메시지를 전달하여 비즈니스 목표를 발전시킬 수 있을 때마다 적용됩니다. 실시간 행동 이벤트에 응답하는 이벤트 트리거 메시징과 시간이 지남에 따라 프로필을 여러 접점으로 안내하는 여러 단계 오케스트레이션된 여정과 다릅니다. 일괄 활성화 는 아웃바운드 메시지 사용 사례에 대한 가장 간단한 캠페인 패턴이며 가장 일반적인 시작점입니다.

## 주요 비즈니스 목표

이 섹션에서는 배치 아웃바운드 메시지 활성화가 지원하는 주요 비즈니스 목표를 식별합니다.

### 이메일 및 캠페인 참여 늘리기

**설명:** 최적화된 콘텐츠와 타깃팅을 통해 열람율, 클릭스루 비율 및 전체 캠페인 반응을 개선합니다.

**KPI:** 열람율, 참여, 전환율

### 매출 및 매출 증대

**설명:** 최적화된 디지털 채널, 캠페인 및 고객 여정을 통해 매출 성장을 촉진합니다.

**KPI:** 전환율, 증분 수익, 평균 주문 가격

**관련 비즈니스 목표:** [매출 및 판매 증가](/help/blueprints/business-objectives/revenue-monetization/increase-revenue-sales.md)

### 캠페인 실행 간소화

**설명:** 템플릿, 자동화 및 표준화된 프로세스를 통해 캠페인 빌드 시간을 줄이고 멀티채널 캠페인 게재를 간소화합니다.

**KPI:** 출시 속도, 효율성, 정시 완료율 %

## 예시 전술 사용 사례

다음 시나리오는 배치 아웃바운드 메시지 활성화의 일반적인 응용 프로그램을 보여 줍니다.

- **판매 발표 또는 프로모션 이메일 발송** — 예정된 날짜에 적격 고객의 세그먼트에 프로모션 오퍼를 브로드캐스트합니다.
- **제품 출시 푸시 알림** - 관심 있는 고객에게 푸시를 통해 새로운 제품 사용 가능 여부를 알립니다.
- **뉴스레터 또는 다이제스트 이메일** - 정기적인 콘텐츠 조회 수를 구독자 대상자에게 전달합니다.
- **이벤트 등록 초대** — 자격을 갖춘 잠재 고객을 웨비나, 회의 또는 직접 이벤트에 초대합니다.
- **구독 갱신 미리 알림 이메일** — 갱신 날짜가 다가오고 있는 고객에게 조치를 취하도록 미리 알림
- **충성도 프로그램 마일스톤 알림** - 충성도 계층 또는 포인트 임계값에 도달한 구성원을 축하합니다.
- **특정 call-to-action 이메일** — 구매 완료, 환경 설정 업데이트 또는 프로그램 등록과 같은 타깃팅된 작업을 실행합니다.
- **플래시 판매 또는 시간 제한 오퍼에 대한 SMS 캠페인** — SMS를 통해 옵트인 대상자에게 긴급 제한 프로모션을 보냅니다.

## 주요 성과 지표

다음 표는 캠페인 효과를 측정하는 데 사용되는 KPI를 정의합니다.

| KPI | 설명 | 측정 접근 방식 |
| --- | --- | --- |
| 게재율 | 수신자에게 정상적으로 전달된 메시지 비율 | 게재됨 / 전송됨 x 100 |
| 열람률 | 수신자가 연 게재된 메시지 비율 | 고유 열람수 / 게재됨 x 100 |
| 클릭스루 비율(CTR) | 링크를 클릭한 게재된 메시지 비율 | 고유 클릭 수 / 게재됨 x 100 |
| 클릭투오픈율(CTOR) | 링크를 클릭한 열린 메시지의 백분율 | 고유 클릭수 / 고유 열람수 x 100 |
| 전환율 | 원하는 작업을 완료한 수신자 비율 | 전환 / 게재됨 x 100 |
| 구독 취소 비율 | 메시지를 받은 후 구독을 취소한 수신자 비율 | 구독 취소 / 제공 x 100 |
| 바운스 비율 | 게재할 수 없는 메시지 비율 | 바운스 수 / 전송된 x 100 |
| 보낸 이메일당 매출 | 캠페인으로 인한 수익(보낸 메시지로 나누기) | 총 수익 / 전송됨 |

## 사용 사례 패턴

**일괄 아웃바운드 메시지 활성화**

대상을 평가한 다음, 단일 배치 실행에서 모든 자격 있는 프로필에 예약된 아웃바운드 메시지(이메일, SMS, 푸시)를 전달합니다.

**함수 체인:** 대상 평가 > 메시지 작성 > 캠페인 실행 > 보고

## 애플리케이션

다음 응용 프로그램을 사용하여 이 패턴을 구현합니다.

- **[!DNL Adobe Journey Optimizer] (AJO)** — 메시지 작성, 채널 구성, 캠페인 실행, 여정 오케스트레이션, 콘텐츠 실험, 빈도 규칙 및 보고
- **[!DNL Adobe Real-Time Customer Data Platform] (RT-CDP)** - 대상 평가, 동의 및 거버넌스 적용
- **[!DNL Adobe Experience Platform] (AEP)** — 프로필 저장소, ID 서비스, 스키마, 데이터 세트, 데이터 수집

## 기본 함수

이 사용 사례 패턴을 사용하려면 다음 기본 기능이 있어야 합니다. 각 함수에 대해 상태는 일반적으로 필요한지, 사전 구성되어 있다고 가정할지 또는 적용할 수 없는지 여부를 나타냅니다.

| 기본 함수 | 상태 | 제자리에 있어야 하는 사항 | Experience League 참조 |
| --- | --- | --- | --- |
| 관리 및 거버넌스 | 가정 위치 | AJO 샌드박스가 활성 채널 구성으로 프로비저닝되었습니다. 하위 도메인 위임, IP 풀 할당 및 IP 웜업 전송 완료. 캠페인/여정 생성 권한이 할당된 사용자 역할. | [샌드박스 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home), [액세스 제어 개요](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home) |
| 데이터 모델링 및 준비 | 필수 | 세분화 및 개인화에 사용되는 속성(예: 이름, 이메일, 환경 설정, 계층)이 있는 XDM 개별 프로필 스키마. 캠페인 이후 전환 추적을 위해 대상 전환 작업(예: `commerce.purchases`, `web.webInteraction`)을 캡처하는 XDM ExperienceEvent 스키마. 두 스키마 모두에 대해 프로필 지원 데이터 세트입니다. | [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home), [스키마 구성 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition) |
| 데이터 소스 및 수집 | 가정 위치 | 전환 이벤트를 캡처하려면 CTA 대상의 웹 SDK 또는 Analytics 태깅을 활성화해야 합니다. 프로필 속성에 대한 스트리밍 또는 일괄 처리 수집 파이프라인이 작동해야 합니다. | [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home), [소스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/sources/home) |
| ID 및 프로필 구성 | 가정 위치 | 이메일(및 모든 교차 장치 식별자)에 대한 ID 네임스페이스가 구성되어 있습니다. 전송 시 매핑, 수집 및 해결 가능한 개인화에 필요한 프로필 속성. 병합 정책이 구성되었습니다. | [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home), [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview) |
| 대상 정의 및 세분화 | 필수 | 세그먼트 빌더 또는 대상 구성을 사용하여 RT-CDP에 정의된 대상. 0이 아닌 모집단으로 게시하고 평가하는 대상자입니다. RT-CDP 대상 평가를 통한 구현 1단계에서 다룹니다. | [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home), [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) |

## 기능 지원

다음 기능은 이 사용 사례 패턴을 강화하지만 코어 실행에는 필요하지 않습니다.

| 지원 기능 | 상태 | 중요한 이유 | Experience League 참조 |
| --- | --- | --- | --- |
| 계산/파생 속성 생성 | 추천 | 마지막 구매 이후 일 수, 라이프타임 주문 수 또는 참여 점수와 같은 계산된 속성은 대상자 정밀도를 향상시키고 더 풍부한 메시지 개인화를 가능하게 합니다. | [계산된 특성 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/computed-attributes/overview) |
| 데이터 수명 주기 관리 | 추천 | 전환 추적을 유도하는 이벤트 데이터 세트에 대해 데이터 보존 정책(만료)이 적용되어야 합니다. 채널 수준 옵트인/옵트아웃 적용을 위해 동의 스키마 필드를 구성해야 합니다. | [고급 데이터 수명 주기 관리 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-lifecycle/home), [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents) |
| 데이터 사용 레이블 지정 및 적용 | 추천 | 개인화에 사용되는 PII 필드의 거버넌스 레이블은 활성화 중에 규정 준수를 보장합니다. 메시지 콘텐츠나 대상자 내보내기에서 중요한 프로필 데이터를 승인되지 않은 방식으로 사용하지 못하도록 합니다. | [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home), [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview) |
| 모니터링 및 가시성 | 포함됨 | 실시간 전송 모니터링은 보고 단계의 일부입니다. 수집 실패 또는 라이선스 사용에 대한 플랫폼 수준 경고 기능은 캠페인 수준 지표 이상의 운영 가시성을 제공합니다. | [Observability Insights 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/home), [경고 개요](https://experienceleague.adobe.com/en/docs/experience-platform/observability/alerts/overview) |
| 보고 및 분석 | 포함됨 | 캠페인 및 여정 보고서는 보고 단계에서 다룹니다. 보다 심층적인 크로스 채널 분석을 위해 CJA 통합은 AJO에 내장된 보고서 이상의 funnel 분석, 속성 모델링 및 집단 분석을 제공합니다. | [CJA 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview), [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo) |

## 애플리케이션 기능

이 계획은 응용 프로그램 함수 카탈로그에서 다음 함수를 실행합니다. 함수는 번호가 매겨진 단계가 아닌 구현 단계에 매핑됩니다.

### [!DNL Journey Optimizer]&#x200B;(AJO)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 채널 구성 | 2단계: 채널 구성 | 하위 도메인, IP 풀, 발신자 설정 및 제외 목록을 포함한 채널 표면(이메일, SMS 또는 푸시)을 구성하거나 확인합니다 |
| 메시지 작성 | 3단계: 메시지 작성 | 템플릿, 이메일 Designer, 개인화 표현식, 조건부 콘텐츠 블록 및 콘텐츠 조각을 사용하여 메시지 콘텐츠 만들기 |
| 캠페인 실행 | 4단계: 캠페인 또는 여정 만들기 | 대상자, 메시지 및 실행 일정을 바인딩하는 예약되거나 API 트리거된 캠페인을 만들고, 구성하고, 활성화합니다 |
| 콘텐츠 실험 | 4단계: 캠페인 또는 여정 만들기 | 필요한 경우 메시지 성능을 최적화하도록 A/B 또는 다변량 콘텐츠 실험 구성 |
| 빈도 및 비즈니스 규칙 | 4단계: 캠페인 또는 여정 만들기 | 필요한 경우 동시 캠페인 간 초과 메시징을 방지하기 위해 빈도 제한 규칙을 적용합니다 |
| 충돌 및 우선 순위 관리 | 4단계: 캠페인 또는 여정 만들기 | 여러 캠페인이 겹치는 대상을 타기팅할 때 우선 순위 점수를 할당하고 충돌 해결을 구성합니다 |
| 보고 및 성능 분석 | 5단계: 보고 및 성능 분석 | 실행 중 라이브 보고서를 통해 게재 지표를 모니터링하고 완료 후 내역 보고서를 통해 캠페인 성과를 분석합니다. |

### [!DNL Real-Time CDP]&#x200B;(RT-CDP)

| 함수 | 구현 단계 | 설명 |
| --- | --- | --- |
| 대상 평가 | 1단계: 대상 평가 | 세그먼트 빌더 또는 대상 컴포지션을 사용하여 대상 규칙을 정의하고 평가 방법(일괄 처리, 스트리밍 또는 에지)을 선택한 다음 대상 모집단을 확인합니다 |
| 동의 및 거버넌스 적용 | 1단계: 대상 평가 | 동의 환경 설정 및 데이터 사용 정책을 적용하여 동의한 프로필만 캠페인 메시지를 받도록 합니다. |

## 필요 조건

구현을 시작하기 전에 다음을 완료하십시오.

- [ ] AJO 샌드박스가 프로비저닝되고 활성 상태입니다.
- [ ] 전송 하위 도메인이 위임되고 확인되었습니다(SPF, DKIM, DMARC 구성됨).
- [ ] IP 풀이 할당되어 프로덕션 전송 볼륨을 위해 예열되었습니다.
- [ ] 활성 채널 표면(전자 메일, SMS 또는 푸시)이 하나 이상 있습니다
- [ ]개의 사용자 계정에 캠페인/여정 만들기 및 콘텐츠 작성 권한이 있습니다.
- [ ] XDM 프로필 스키마에 대상자 세분화 및 메시지 개인화에 필요한 특성이 포함되어 있습니다.
- [ ] XDM 이벤트 스키마가 캠페인 후 추적을 위해 전환 이벤트를 캡처합니다.
- [ ] 프로필 데이터가 ID 서비스를 통해 수집되고 통합됩니다.
- [ 전환 이벤트를 캡처하기 위해 CTA 대상 페이지에서 ] 웹 SDK 또는 Analytics 태그 지정을 활성화 중입니다.
- [ ] 동의 필드가 대상 메시징 채널의 프로필에 채워집니다.
- [ ]개의 콘텐츠 자산(이미지, 로고, 브랜드 지침)을 메시지 디자인에 사용할 수 있습니다.

## 구현 옵션

이 섹션에서는 비교 및 의사 결정 지침과 함께 배치 아웃바운드 메시지 활성화를 위한 세 가지 구현 옵션에 대해 설명합니다.

### 옵션 A: 예약된 캠페인(일회성 일괄 전송)

**가장 적합한 전송 대상:** 날짜 고정된 전송 — 판매 공지, 제품 출시, 이벤트 등록 기한, 갱신 알림, 뉴스레터 게시판 및 실행 날짜가 미리 알려진 모든 전송

**작동 방식:**

예약된 캠페인은 배치 아웃바운드 메시지의 가장 간단한 변형입니다. 마케터는 타겟 대상자를 정의하고, 메시지 콘텐츠를 작성하며, 전송 날짜 및 시간을 설정하고, 캠페인을 활성화합니다. 예약된 실행 시간에 AJO은 대상을 평가하여 현재 자격을 갖춘 모집단을 파악한 다음, 메시지를 단일 배치로 모든 자격을 갖춘 프로필에 전달합니다.

전체 구성은 AJO 캠페인 인터페이스 내에서 수행됩니다. 여정 캔버스, 분기 논리 및 대기 단계가 없습니다. 이렇게 하면 예약된 캠페인을 가장 빠르게 구성하고 쉽게 관리할 수 있습니다. 캠페인은 즉시 실행, 특정 미래 날짜/시간 또는 반복 일정(일별, 주별, 월별)에 대해 설정할 수 있습니다.

**주요 고려 사항:**

- 대상자는 실행 시 평가되므로 예약과 실행 사이에 적합한 프로필이 포함됩니다
- 분기, 대기 또는 조건 논리를 사용할 수 없음 - 메시지가 모든 자격 있는 프로필에 전달됩니다.
- 캠페인 구성 내에서 직접 콘텐츠 실험(A/B 테스트)을 지원합니다.
- 캠페인 속성에는 다른 캠페인과의 충돌 해결에 대한 우선 순위 점수가 포함됩니다

**장점:**

- 오버헤드가 가장 적은 간단한 구성
- 간단한 일괄 처리 전송을 위한 가장 빠른 시작 시간
- 반복 일정에 대한 기본 제공 지원
- 기본적으로 지원되는 콘텐츠 실험
- 실행 시 새로 고침 대상의 재평가

**제한 사항:**

- 게재 전 대기 단계, 조건 또는 분기 없음
- 예약과 실행 사이의 프로필 동작에 반응할 수 없음
- 단일 메시지 작업만 — 다중 터치 시퀀스 없음
- 활성화한 후에는 편집할 수 없습니다(복제 및 수정해야 함).

**Experience League:**

- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)

### 옵션 B: 대상자에서 트리거된 여정

**가장 적합한 전송 방법:** 동작 기반 전송 — 포기한 장바구니 알림, 체험판 만료 알림, 마일스톤 축하, 자격 기반 지원 및 트리거가 일정 날짜가 아닌 대상 자격 또는 비즈니스 이벤트인 모든 전송

**작동 방식:**

대상이 트리거된 여정은 프로필이 정의된 대상에 적합하거나 자격 부여 이벤트를 실행할 때 여정 캔버스를 사용하여 메시지를 전달합니다. 여정 항목은 고정된 일정이 아닌 대상자 멤버십 변경(대상자를 입력하는 프로필)에 의해 트리거됩니다. 여정 캔버스에서는 메시지 작업 전에 선택적 대기 단계, 조건 분기 및 제외 논리를 사용할 수 있으므로 예약된 캠페인보다 더 유연합니다.

여정은 대상 항목 읽기 이벤트를 사용하여 AJO 여정 인터페이스에 구성됩니다. 프로필이 대상자에 적합하면 여정을 입력하고 캔버스 노드를 진행합니다. 간단한 구현에는 단일 이메일 작업 노드만 포함될 수 있으므로, 기능적으로 예약된 캠페인과 유사하지만 대상자 자격 기반 입력 타이밍이 있습니다. 보다 복잡한 구현은 메시지 게재 전에 대기 노드(예: 자격 조건 후 24시간 대기), 조건 노드(예: 프로필이 이전 이메일을 열었는지 확인) 또는 제외 논리를 추가할 수 있습니다.

**주요 고려 사항:**

- 여정 항목은 달력 날짜가 아닌 대상 자격에 의해 트리거됩니다.
- 여정 캔버스는 사전 게재 논리를 위해 대기, 조건 및 분할 노드를 지원합니다
- 여정 재입력 규칙은 프로필이 여정을 여러 번 입력할 수 있는지 여부를 제어합니다
- 여정 중재 설정은 프로필이 이미 경쟁 여정에 있을 때의 동작을 결정합니다

**장점:**

- 고정된 일정이 아닌 대상 자격을 기준으로 유연한 시작 시간
- 대기 및 조건 노드는 사전 게재 논리(예: 지연, 확인, 억제)를 허용합니다.
- 재입력 제어는 동일한 프로필로 중복 전송을 방지합니다.
- 사용 사례가 발전하는 경우 여러 단계 여정으로 확장할 수 있습니다.
- 시작, 종료 및 노드 수준 지표를 사용하여 여정 수준 보고 지원

**제한 사항:**

- 예약된 캠페인보다 더 많은 구성 오버헤드
- 여정 캔버스는 단일 메시지 사용 사례의 경우도 복잡성을 가중시킵니다
- 여정은 게시되어야 하며 라이브 중에는 편집할 수 없습니다(새 버전을 만들어야 함).
- 시작 상한은 시간 창 내에 입력되는 프로필의 수를 제한할 수 있습니다

**Experience League:**

- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [대상자 여정 읽기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### 옵션 C: API 트리거된 캠페인

**가장 적합한 전송 대상:** 시스템 시작 전송 — 상향 판매 콘텐츠가 포함된 주문 확인, 지원 티켓 해결 후속 조치, 마케팅 콘텐츠가 포함된 트랜잭션 알림 및 특정 시점에 트리거가 외부 시스템에서 발생하는 모든 전송.

**작동 방식:**

API로 트리거된 캠페인은 트리거되는 시스템 이벤트가 발생하는 즉시 REST API 호출을 통해 활성화됩니다. 캠페인은 메시지 콘텐츠 및 채널 설정으로 AJO에 사전 구성되어 있지만, API 호출은 사전 정의된 대상을 바인딩하는 대신 수신자 프로필을 지정하고 동적 메시지 매개 변수를 채우는 컨텍스트 데이터를 전달할 수 있습니다.

이 변형은 전송 타이밍이 대상 평가 또는 일정 보다는 외부 시스템(예: 주문 관리 시스템, CRM 워크플로우 또는 지원 플랫폼)에 의해 결정될 때 이상적입니다. API 트리거 페이로드에서 전달된 컨텍스트 데이터(예: 주문 세부 사항, 티켓 번호 또는 제품 이름)는 프로필에 저장되지 않은 컨텍스트 속성을 사용하여 메시지 콘텐츠를 개인화할 수 있습니다.

**주요 고려 사항:**

- 사전 바인딩된 대상이 필요하지 않습니다. 수신자는 API 트리거 요청에 지정됩니다.
- 트리거 페이로드의 컨텍스트 데이터를 통해 프로필 속성 이상의 동적 개인화가 가능합니다
- 캠페인은 &quot;API 트리거됨&quot; 유형이어야 하며 트리거 요청을 받으려면 먼저 활성화해야 합니다
- 각 API 트리거 요청은 최대 20개의 프로필 수신자를 지원합니다
- 수신자가 API 호출에서 왔으므로 대상 평가(1단계)를 건너뛸 수 있습니다

**장점:**

- 이벤트 발생 시 외부 시스템에서 실시간 트리거
- 프로필에 저장되지 않은 데이터를 사용한 컨텍스트 기반 개인화(주문 세부 사항, 티켓 정보)
- 대상자 평가 오버헤드 없음 - 수신자가 직접 지정됨
- 트랜잭션 + 마케팅 하이브리드 메시지 지원

**제한 사항:**

- API 트리거를 전송하기 위해 외부 시스템 통합 필요
- API 트리거 요청당 최대 20명의 수신자
- 기본 제공 대상 평가 없음 - 호출 시스템이 수신자를 결정해야 합니다.
- API 통합 요구 사항으로 인한 기술 복잡성 증가
- API 트리거 캠페인에 대해서는 콘텐츠 실험이 지원되지 않습니다.

**Experience League:**

- [API 트리거된 캠페인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)
- [API를 사용하여 캠페인 트리거](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### 옵션 비교

다음 표에서는 주요 기준에서 세 가지 구현 옵션을 비교합니다.

| 기준 | 옵션 A: 예약된 캠페인 | 옵션 B: 대상자에서 트리거된 여정 | 옵션 C: API 트리거된 캠페인 |
| --- | --- | --- | --- |
| 다음에 최적 | 날짜가 고정된 전송 횟수(프로모션, 론치, 뉴스레터) | 비헤이비어 기반 전송(선별 이벤트, 이정표) | 시스템에서 시작한 전송(주문 확인, 트랜잭션) |
| 복잡성 | 낮음 | 중간 | Medium 하이 |
| 트리거 유형 | 일정 날짜/시간 또는 반복 일정 | 대상 자격 또는 비즈니스 이벤트 | 외부 시스템 API 호출 |
| 사전 게재 논리 | 없음 | 대기, 조건, 사용 가능한 노드 분할 | 없음(호출 시스템의 논리) |
| 대상 바인딩 | 사전 정의된 RT-CDP 대상 | 사전 정의된 RT-CDP 대상 | API 페이로드에 지정된 수신자 |
| 컨텍스트 데이터 | 프로필 속성만 | 프로필 속성만 | 프로필 속성 + API 페이로드 데이터 |
| 콘텐츠 실험 | 지원됨 | 지원됨(메시지 작업 시) | 지원되지 않음 |
| 빈도 상한 설정 | 지원됨 | 지원됨 | 지원됨 |
| 재입력 제어 | N/A(1회 실행) | 구성 가능한 재입력 규칙 | N/A(요청당) |
| 구성 인터페이스 | AJO 캠페인 | AJO 여정 | AJO 캠페인 + 외부 시스템 |
| 필요 | 대상자, 채널 표면, 메시지 | 대상, 채널 표면, 메시지, 여정 캔버스 | 채널 표면, 메시지, API 통합 |

### 적절한 옵션 선택

다음 의사 결정 플로우를 사용하여 적절한 구현 옵션을 선택합니다.

1. **외부 시스템 이벤트(예: 주문, 티켓 확인)에 의해 전송이 트리거되었습니까?** 그렇다면 **옵션 C: API 트리거 캠페인**&#x200B;을(를) 선택하십시오. 이 옵션은 상황별 페이로드 데이터와 함께 시스템에서 시작한 트리거를 지원하는 유일한 옵션입니다.

2. **특정 일정 날짜나 되풀이되는 일정에 따라 전송이 고정되었습니까?** 그렇다면 **옵션 A: 예약된 캠페인**&#x200B;을 선택하세요. 이는 날짜 기반 전송에 대해 구성하는 데 가장 간단하고 빠릅니다.

3. **전송이 대상 자격에 반응해야 합니까, 아니면 사전 전달 논리(대기, 조건, 제외)가 필요합니까?** 그렇다면 **옵션 B: 대상자에서 트리거된 여정**&#x200B;을 선택하십시오. 여정 캔버스에서는 동작 기반 입력 및 사전 게재 결정 논리를 유연하게 사용할 수 있습니다.

4. **특별한 시간 또는 논리 요구 사항 없이 알려진 대상자에게 간단한 브로드캐스트를 전송합니까?** 가장 낮은 구성 오버헤드로 **옵션 A: 예약된 캠페인**&#x200B;을 선택합니다.

## 구현 단계

이 섹션에서는 의사 결정 지점 및 옵션별 지침을 포함하여 각 구현 단계를 자세히 안내합니다.

### 1단계: 대상 평가

**응용 프로그램 함수:** RT-CDP: 대상 평가

이 단계에서는 캠페인 메시지를 받을 타겟 대상 세그먼트를 정의하고 평가합니다. 프로필 속성, 동작 신호 및 제외 규칙을 기반으로 전송 대상 프로필을 결정합니다.

>[!NOTE]
>옵션 C(API 트리거 캠페인)의 경우, 수신자가 API 트리거 페이로드에 완전히 지정된 경우 이 단계를 건너뛸 수 있습니다. 그러나 API로 트리거되는 캠페인이라도 메시지를 받지 않아야 하는 프로필을 필터링하는 제외 대상을 가질 수 있으므로 이점이 있습니다.

#### 의사 결정: 대상 기준

타겟 대상을 정의하는 조건은 무엇입니까? 프로필을 제외해야 하는 제외 규칙

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 프로필 속성 기반 대상 | 타겟 대상은 인구 통계학적, 환경 설정 또는 상태 속성으로 정의됩니다 | 구축 간소화, 모든 평가 방법 지원 |
| 행동 이벤트 기반 대상 | Target 대상은 기간 내에 수행한(또는 수행하지 않은) 작업에 의해 정의됩니다 | 이벤트 데이터 수집이 필요합니다. 시간 범위 규칙은 스트리밍 적격성을 제한할 수 있습니다. |
| 대상 구성(파생 대상) | Target 대상에는 여러 소스 대상자 간의 등급, 분할, 제외 또는 강화 작업이 필요합니다 | 보다 강력하지만 일괄 처리 전용 평가, 샌드박스당 10개의 컴포지션으로 제한 |

#### 의사 결정: 평가 방법

새 적격 또는 부적격 프로필을 반영하려면 대상자를 얼마나 빨리 업데이트해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 배치 평가 | 하루 동안의 대상자 신선도가 허용되는 예약된 캠페인(크고 복잡한 대상자) | 대부분의 세그먼트 유형의 기본값, 일별 일정 또는 온디맨드 프로세스, 모든 세그먼트 규칙 기능 지원 |
| 스트리밍 평가 | 프로필이 자격을 갖추기 위해 실시간에 가깝게 입력해야 하는 대상 트리거 여정 | 적합한 세그먼트 규칙 표현식에 대해 자동, 모든 세그먼트 유형이 스트리밍에 적합한 것은 아님, 실시간에 가까운 지연(초~분) |
| 에지 평가 | 이 패턴에 대해 전형적이지 않음(동일 페이지 개인화에 사용됨) | 제한된 세그먼트 규칙 지원, 밀리초 지연, 웹 개인화 패턴과 결합된 경우에만 해당됨 |

#### 결정: 병합 정책

대상자가 프로필 조각을 해결하는 데 사용해야 하는 병합 정책은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기본 병합 정책(타임스탬프 정렬) | 일괄 캠페인 사용 사례에 가장 일반적으로 사용 | 가장 최근 속성 값이 성공함, 아웃바운드 메시지의 표준 |
| 사용자 지정 병합 정책(데이터 세트 우선 순위) | 특정 데이터 소스가 키 속성에 우선 순위를 두어야 하는 시기 | CRM 데이터가 특정 필드에 대해 웹에서 수집한 데이터를 재정의해야 하는 경우에 유용합니다 |

#### UI 탐색

고객 > 대상 > 대상 만들기 > 규칙 빌드

#### 주요 구성 세부 정보

- 프로필 속성, 행동 이벤트 및 세그먼트 멤버십에 대한 세그먼트 규칙과 함께 세그먼트 빌더를 사용하여 대상자를 정의합니다
- 이미 전환했거나, 최근에 유사한 메시지를 받았거나, 옵트아웃한 프로필을 제외하도록 제외 규칙 적용
- 계속하기 전에 대상자에 0이 아닌 모집단이 있는지 확인하십시오
- 배치 캠페인의 경우 세그먼트 평가 일정이 활성 상태인지 확인하거나 주문형 평가를 트리거하십시오
- 동의 필드 확인(`consents.marketing.email.val`, `consents.marketing.sms.val` 등) 채워지고 강제 적용됩니다.

#### 옵션 분기 위치

**옵션 A(예약된 캠페인)의 경우:**

일괄 처리 평가가 일반적입니다. 대상자는 캠페인 실행 시 다시 평가되므로 가장 현재 자격이 있는 모집단을 타겟팅합니다. 대상자를 정의하고 모집단을 확인한 다음 캠페인 생성을 진행합니다.

옵션 B의 **대상(대상 트리거 여정):**

프로필이 자격이 될 때 여정을 입력하도록 스트리밍 평가가 선호됩니다. 세그먼트 규칙 표현식이 스트리밍에 적합한지 확인합니다(단순 이벤트 트리거, 속성 비교, 제한된 시간 범위). 대상을 구성하고 스트리밍 자격이 활성 상태인지 확인합니다.

**옵션 C(API 트리거된 캠페인)의 경우:**

대상 평가를 완전히 건너뛸 수 있습니다. 사용되는 경우 비표시 대상을 만들어 메시지를 받지 않아야 하는 프로필(예: 최근에 구독 취소함, 이미 전환됨)을 필터링합니다. 호출 시스템이 기본 수신자를 결정합니다.

#### Experience League 설명서

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [대상자 구성](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### 2단계: 채널 구성

**응용 프로그램 함수:** AJO: 채널 구성

이 단계에서는 메시지의 전송 인프라(하위 도메인, IP 풀, 보낸 사람 ID, 회신 주소 및 구독 취소 설정)를 정의하는 채널 표면(사전 설정)을 확인하거나 만듭니다. 메시지 콘텐츠를 작성하거나 캠페인을 활성화하려면 먼저 유효한 채널 표면이 있어야 합니다.

#### 의사 결정: Target 채널

캠페인 메시지를 전달할 메시지 채널은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 이메일 | 대부분의 캠페인 유형 — 뉴스레터, 프로모션, 알림, 갱신 | 위임된 하위 도메인, 웜된 IP 풀, 발신자 ID 및 구독 취소 구성이 필요합니다. |
| SMS | 시간에 민감한 메시지 또는 간단한 메시지 — 플래시 영업, 약속 알림 메시지, OTP 코드 | SMS 공급자 자격 증명(Sinch, Twilio 또는 Infobip) 필요, 메시지당 비용 증가, 보다 엄격한 동의 요구 사항 |
| 푸시 알림 | 모바일 참여 대상 — 앱 업데이트, 위치 기반 오퍼, 인앱 기능 공지 | APNs(iOS) 및/또는 FCM(Android) 자격 증명이 필요합니다. 사용자에게 푸시 권한이 부여된 앱이 설치되어 있어야 합니다. |

#### 의사 결정: 채널 표면 선택

적절한 채널 표면이 샌드박스에 이미 존재합니까, 아니면 새 채널 표면을 생성해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기존 표면 재사용 | 검증되고 활성 상태가 필요한 하위 도메인, 발신자 ID 및 채널 유형과 일치함 | 가장 빠른 경로, DNS 또는 웜업 구성이 필요 없음 |
| 새 표면 만들기 | 요구 사항과 일치하는 기존 표면이 없거나 새 하위 도메인/발신자 ID가 필요합니다. | 하위 도메인 위임, DNS 확인, IP 풀 할당 및 잠재적으로 IP 웜업 필요(새 IP의 경우 2~4주) |

#### 의사 결정: 구독 취소 처리

채널 표면에서 옵트아웃을 관리하려면 어떻게 해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 원클릭 목록 구독 취소 헤더 | 모든 마케팅 이메일에 대한 표준. 게재 가능성을 위해 주요 ISP(Gmail, Yahoo)에 필요 | ISP가 &quot;구독 취소&quot; 버튼으로 표시하는 mailto: 또는 URL 기반 구독 취소 헤더를 추가합니다. |
| 이메일 본문의 구독 취소 링크 | 목록 구독 취소 헤더를 지원하지 않는 이메일 클라이언트에 대한 대체 항목으로 필요합니다. | 목록 구독 취소 헤더와 함께 이메일 바닥글에 구독 취소 링크 포함 |
| 모두(권장) | 모든 마케팅 이메일에 대한 모범 사례 | 최대 규정 준수 범위 및 최상의 전달성 프로필 |

#### UI 탐색

관리 > 채널 > 채널 표면 > 표면 생성(또는 기존 선택)

#### 주요 구성 세부 정보

- 이메일: 보내는 하위 도메인, IP 풀, 보낸 사람 이름, 보낸 사람 이메일, 회신 주소 및 BCC 주소 바인딩(감사 사본이 필요한 경우)
- SMS의 경우: SMS 공급자 자격 증명과 짧은 코드 또는 긴 코드 설정을 구성합니다.
- 푸시: 앱의 인증서 또는 서버 키로 APNs 및/또는 FCM 자격 증명을 구성합니다.
- 계속하기 전에 채널 표면에 &quot;활성&quot; 상태가 표시되는지 확인하십시오.
- 보내는 하위 도메인에 대해 DNS 레코드(SPF, DKIM, DMARC)가 올바르게 구성되었는지 확인
- 부실 항목에 대한 제외 목록을 검토합니다. 활성화 전에 정리합니다.

#### Experience League 설명서

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [이메일 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [제외 목록 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### 3단계: 메시지 작성

**응용 프로그램 함수:** AJO: 메시지 작성

이 단계에서는 대상자에게 전달할 메시지 콘텐츠를 만듭니다. 여기에는 콘텐츠 템플릿 선택 또는 만들기, 메시지 레이아웃 디자인, 프로필 속성을 사용한 개인화 추가, 대상별 변형에 대한 조건부 콘텐츠 블록 구성, 재사용 가능한 콘텐츠 조각 만들기, 샘플 프로필로 메시지 미리 보기/테스트 등이 포함됩니다.

#### 의사 결정: 콘텐츠 접근 방식

메시지 콘텐츠는 어떻게 생성해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기존 템플릿에서 시작 | 브랜드 승인 템플릿이 존재하며 메시지 유형(프로모션, 트랜잭션, 뉴스레터)과 일치함 | 가장 빠른 작성 경로, 브랜드 일관성 보장, 샌드박스별 템플릿 |
| 처음부터 디자인 | 적합한 템플릿이 없거나 메시지에 고유한 레이아웃이 필요합니다. | 보다 유연하고 효율적인 작업 수행, 재사용을 위해 템플릿으로 저장 |
| HTML 가져오기 | 메시지 디자인이 외부적으로(예: 디자인 도구에서) 생성되었으며 HTML을 가져올 준비가 되었습니다. | 외부 디자인을 보존합니다. AJO 호환성 및 개인화 토큰을 조정해야 할 수 있습니다. |

#### 의사 결정: Personalization 깊이

메시지를 개인화해야 하는 프로필 속성과 조건부 콘텐츠 블록이 필요합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 기본 개인화(이름, 인사말) | 개인화된 인사말이 포함된 일반적인 콘텐츠로 충분한 간단한 캠페인 | 낮은 작업량, 렌더링 문제의 위험 최소화, 표준 프로필 속성 사용 |
| 속성 기반 개인화 | 메시지 콘텐츠는 프로필 속성(계층, 환경 설정, 위치)에 따라 다릅니다. | 확인된 XDM 경로가 필요합니다. 여러 프로필로 테스트하여 모든 변형이 올바르게 렌더링되는지 확인합니다. |
| 조건부 콘텐츠 블록 | 동일한 메시지 내에서 다른 대상 세그먼트에 다른 콘텐츠 섹션을 표시해야 합니다 | 보다 복잡한 작성, 각 조건에는 기본 폴백이 필요합니다. 모든 순열을 테스트하십시오. |
| 컨텍스트 기반 개인화(옵션 C만 해당) | API 트리거 캠페인은 트리거 페이로드에서 전달된 데이터를 렌더링해야 합니다(주문 세부 사항, 티켓 정보). | 컨텍스트 속성은 프로필에 저장되지 않습니다. 메시지에 자리 표시자를 정의하고 페이로드 필드에 매핑합니다. |

#### 의사 결정: 조각 전략

공유 콘텐츠 블록을 재사용 가능한 조각으로 생성해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 재사용 가능한 조각 | 머리글, 바닥글, 법적 고지 사항 또는 구독 취소 블록은 여러 캠페인에서 공유됩니다 | 조각에 대한 변경 사항이 이를 참조하는 모든 메시지(라이브 및 초안)에 전파됨, 메시지당 최대 30개 조각 |
| 인라인 콘텐츠 | 다른 캠페인에서 공유 요소가 없는 일회성 메시지 | 일회성 컨텐츠 사용이 간편하며 전파 위험이 없음 |

#### UI 탐색

캠페인 > 캠페인 선택 > 콘텐츠 편집 > 이메일 Designer(또는 SMS/푸시 편집기)

#### 주요 구성 세부 정보

- 드래그하여 놓는 콘텐츠 구성 요소(텍스트, 이미지, 단추, 구분선, 열)를 사용하여 메시지 레이아웃 디자인
- 제목 줄, 사전 머리글 텍스트 및 보낸 사람 표면 등 이메일 헤더 속성을 설정합니다.
- Handlebars 구문을 사용하여 개인화 식을 삽입합니다(예: `{{profile.person.name.firstName}}`).
- 서식(날짜, 숫자, 문자열 조작)을 위한 도우미 함수 구성
- 프로필 속성 또는 세그먼트 멤버십에 따라 다른 콘텐츠를 표시하려면 조건부 콘텐츠 규칙을 추가하십시오.
- 조건이 충족되지 않을 때 기본 대체 콘텐츠 구성
- SMS의 경우 문자 제한 고려 사항 내에서 메시지 본문을 구성합니다
- 푸시의 경우 제목, 본문, 이미지 및 작업 구성(딥링크 또는 URL)
- 개인화 렌더링을 확인하려면 샘플 프로필로 메시지를 미리 봅니다.
- 검토를 위해 내부 이해 당사자에게 증명 이메일 보내기
- 이메일 렌더링 기능을 사용하여 이메일 클라이언트 간 렌더링 테스트

#### Experience League 설명서

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
- [이메일 증명 보내기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [전자 메일 렌더링](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)
- [SMS 메시지 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/create-sms)
- [푸시 알림 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/design-push)

### 4단계: 캠페인 또는 여정 만들기

**응용 프로그램 함수:** AJO: Campaign 실행(옵션 A 및 C) 또는 AJO: Journey Orchestration(옵션 B)

이 단계에서는 대상자, 메시지 및 실행 메커니즘을 결과물 단위로 바인딩하는 캠페인이나 여정을 만듭니다. 이 세 가지 구현 옵션이 가장 크게 분기되는 부분입니다.

#### 의사 결정: 콘텐츠 실험

캠페인에 메시지 성능을 최적화하기 위한 A/B 테스트 또는 다변량 실험이 포함되어야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 실험 없음 | 콘텐츠 효과에 대한 높은 신뢰도로 단일 메시지 변형 | 가장 간단한 구성, 가장 빠른 활성화 |
| A/B 테스트(2개 변형) | 명확한 가설을 사용하여 제목란, CTA 또는 콘텐츠 레이아웃 테스트 | 트래픽을 50/50으로 분할하거나 가중치가 적용된 할당. 통계적 중요도에 충분한 대상 크기가 필요합니다. |
| 다변량 테스트(3+ 변형) | 여러 콘텐츠 요소를 동시에 테스트 | 대상이 더 많아야 하고, 신뢰 임계값에 도달하는 기간이 길어야 하며, 실험당 최대 10회 처리 |

#### 의사 결정: 빈도 제한

이 캠페인은 과도한 메시지를 방지하기 위해 전역 빈도 제한 규칙을 준수해야 합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 빈도 규칙 적용 | Campaign은 여러 개의 동시 전송을 사용하는 광범위한 메시징 프로그램의 일부입니다 | 고객 피로도를 방지합니다. 한도를 초과하는 프로필은 배송되지 않습니다. |
| 캡핑 제외 | 캠페인은 시간이 중요하거나 트랜잭션이며 최근 메시지 내역에 관계없이 모든 적격 프로필에 도달해야 합니다. | 를 제한적으로 사용하십시오. 빈도 규칙에서 캠페인을 제외하면 초과 메시지가 발생할 수 있습니다. |

#### 결정: 우선 순위 점수

다른 활성 캠페인과 관련하여 이 캠페인의 우선 순위 수준은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 높은 우선 순위(75-100) | 주요 캠페인 — 주요 제품 출시, 제한적 오퍼, 규정 준수 알림 | 충돌이 발생할 때 우선순위가 낮은 캠페인보다 우선합니다. |
| Medium 우선 순위(25-74) | 표준 마케팅 캠페인 — 뉴스레터, 참여 캠페인, 일반 프로모션 | 다른 캠페인과 균형 유지. 우선순위가 높은 캠페인이 충돌하는 경우 억제할 수 있음 |
| 낮은 우선 순위(0-24) | 전송 기능 향상 — 정보 업데이트, 2차 프로모션 | 우선순위가 높은 캠페인을 위해 억제됩니다. |

#### 옵션 분기 위치

**옵션 A(예약된 캠페인)의 경우:**

**UI 탐색:** 캠페인 > 캠페인 만들기 > 예약됨 > 마케팅

1. 새 예약된 마케팅 캠페인 만들기
2. 대상 선택기에서 대상 대상 선택
3. 채널 표면을 선택하고 작성된 메시지 콘텐츠를 연결합니다.
4. 실행 일정 구성: 즉시, 특정 날짜/시간 또는 반복
5. 선택적으로 콘텐츠 실험을 활성화하고 처리 변형을 정의합니다.
6. 필요한 경우 빈도 제한 및 우선 순위 점수 구성
7. 전체 캠페인 구성 검토
8. 캠페인 활성화

옵션 B의 **대상(대상 트리거 여정):**

**UI 탐색:** 여정 > 여정 만들기

1. 대상자 읽기 항목 이벤트로 새 여정 만들기
2. 타겟 대상을 시작 소스로 선택
3. 재입력 규칙 구성(재입력, 1회 입력 또는 대기 기간 후 재입력 허용)
4. 필요한 경우 대기 노드 추가(예: 검증 후 24시간 대기)
5. 선택적으로 조건 노드를 추가합니다(예: 프로필이 추가 기준을 충족하는지 확인).
6. 메시지 작업 노드를 추가하고 채널 표면 및 작성된 콘텐츠를 선택합니다.
7. 종료 기준 구성(예: 프로필 전환, 프로필 구독 취소)
8. 필요한 경우 메시지 작업에 대한 콘텐츠 실험 활성화
9. 여정 검토 및 게시

**옵션 C(API 트리거된 캠페인)의 경우:**

**UI 탐색:** 캠페인 > 캠페인 만들기 > API 트리거됨

1. 새 API 트리거 캠페인 만들기
2. 채널 표면을 선택하고 작성된 메시지 콘텐츠를 연결합니다.
3. API 트리거 페이로드에서 전달될 데이터에 대한 컨텍스트 기반 개인화 토큰 구성
4. 캠페인 검토 및 활성화
5. 외부 시스템의 API 트리거 통합에 사용할 캠페인 ID를 참고하십시오
6. 호출 시스템은 수신자 프로필 및 컨텍스트 데이터를 사용하여 캠페인 엔드포인트에 트리거 요청을 전송합니다

#### Experience League 설명서

- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [API 트리거된 캠페인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)
- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [대상자 여정 읽기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)
- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)

### 5단계: 보고 및 성능 분석

**응용 프로그램 함수:** AJO: 보고 및 성능 분석

이 단계는 라이브 보고서를 통해 실행 중에 게재 지표를 모니터링하고 내역 보고서를 통해 완료 후 캠페인 성과를 분석합니다. 필요한 경우 더 자세한 크로스 채널 분석을 위해 CJA 통합을 구성합니다.

#### 결정: 보고 방법

이 캠페인에 필요한 보고 수준은 무엇입니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| AJO 기본 보고서만 | 표준 게재 및 참여 지표는 충분함(전송, 게재, 열기, 클릭, 바운스) | 추가 구성 없음, 보고서가 캠페인/여정 UI에 내장되어 있음 |
| AJO 기본 보고서 + CJA 분석 | 게재 지표 이상의 크로스 채널 영향 분석, 속성 모델링 또는 funnel 분석이 필요합니다 | AJO 데이터 세트에 연결된 CJA 연결 및 데이터 보기가 필요합니다. 더 심층적인 분석 기능을 제공합니다. |
| CJA 프로그래밍 보고 | 이해 당사자를 위해 자동화된 대시보드 또는 예약된 보고서 전달이 필요합니다. | CJA Reporting API 통합이 필요합니다. 경영진 대시보드 및 반복 성능 요약에 유용합니다. |

#### 결정: 전환 추적

게재 및 참여 지표를 넘어 캠페인 성공을 어떻게 측정합니까?

| 옵션 | 선택 시기 | 고려 사항 |
| --- | --- | --- |
| 전환 추적 없음 | 캠페인 목표는 특정 다운스트림 작업 없이 인식 또는 참여(열기, 클릭)입니다 | 가장 간단함, 추가 이벤트 추적 불필요 |
| 웹 전환 추적 | Campaign CTA은 전환 이벤트(구매, 등록, 양식 제출)가 추적되는 웹 페이지에 연결됩니다 | 대상 페이지에서 웹 SDK 또는 Analytics 태그 지정이 필요합니다. 이벤트는 AEP 데이터 세트에서 캡처해야 합니다. |
| 사용자 지정 전환 이벤트 | 캠페인 성공은 웹에서 캡처되지 않은 비즈니스별 이벤트(예: 매장 구매, 콜센터 상호 작용)로 측정됩니다 | 사용자 지정 이벤트를 AEP에 수집하고 보고 데이터 세트에 포함해야 합니다. |

#### UI 탐색

- 라이브 보고서: 캠페인 > 캠페인 선택 > 라이브 보고서(또는 여정 > 여정 선택 > 라이브 보고서)
- 내역 보고서: 캠페인 > 캠페인 선택 > 모든 시간 보고서(또는 여정 > 여정 선택 > 모든 시간 보고서)

#### 주요 구성 세부 정보

- 캠페인 실행 중 라이브 보고서에 액세스하여 실시간 게재 및 참여 모니터링
- 주요 지표 검토: 보냄, 배달됨, 바운스, 열림, 클릭 수, 구독 취소(이메일), 보냄, 배달됨, 클릭 수, 오류(SMS), 보냄, 배달됨, 열림, 작업(푸시)
- 캠페인 완료 후 포괄적인 분석을 위해 내역(항상) 보고서에 액세스
- 게재 분석 funnel: 타겟팅됨 > 전송됨 > 게재됨 > 열기 > 클릭 수
- 게재 문제를 식별하기 위한 오류 및 제외 이유 검토
- 콘텐츠 실험이 활성화된 경우 실험 결과를 검토하고 통계적 신뢰도를 기다린 후 우승자를 선언하십시오
- CJA 통합의 경우 AJO 데이터 보기에 관련 AJO 데이터 세트(메시지 피드백 이벤트 데이터 세트, 이메일 추적 경험 이벤트 데이터 세트)가 포함되어 있는지 확인합니다

#### Experience League 설명서

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

## 구현 시 고려 사항

이 섹션에서는 보호, 일반적인 위험, 모범 사례 및 상충 결정 사항을 다룹니다.

### 보호 기능 및 제한 사항

- 샌드박스당 최대 500개의 활성 라이브 캠페인 — [Journey Optimizer 보호](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- 샌드박스당 최대 4,000개의 세그먼트 정의 — [실시간 고객 프로필 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- 샌드박스당 채널 유형당 최대 10개 채널 표면
- API 트리거 캠페인은 트리거 요청당 최대 20명의 프로필 수신자 지원
- 캠페인은 한 번 활성화하면 편집할 수 없음 — 대신 복제 및 수정
- 라이브 보고서는 60초마다 새로 고침되며 지난 24시간 동안의 데이터를 표시합니다.
- 캠페인 완료 후 내역 보고서를 완전히 채우는 데 최대 2시간이 걸릴 수 있습니다
- 콘텐츠 실험당 최대 10개의 처리(변형)
- 샌드박스당 최대 10개의 최대 구성 제한
- 메시지당 최대 30개의 콘텐츠 조각
- 최적의 전달성을 위해서는 최대 이메일 크기 100KB가 권장됩니다.
- IP 웜업 플랜은 새로운 IP에 대해 2~4주 동안 볼륨을 점진적으로 늘려야 함
- 제외 목록 항목은 구성 가능한 기간 동안 유지됩니다(소프트 바운스의 경우 기본 14일).

### 일반적인 함정

- **IP 워밍업이 완료되기 전에 보내기:** 높은 볼륨을 즉시 보내는 새 IP 주소는 ISP에 의해 플래그가 지정되므로 전달성이 떨어지고 블랙리스트가 발생할 수 있습니다. 프로덕션이 새 IP를 전송하기 전에 항상 IP 준비 계획을 완료합니다.

- **여러 프로필에서 개인화를 테스트하지 않음:** 일부 프로필에서 참조된 XDM 경로가 없거나 null인 경우 다른 테스트 프로필에 대해 작동하는 Personalization 토큰이 실패할 수 있습니다. 항상 다른 데이터 완전성 수준을 나타내는 여러 테스트 프로필로 미리 봅니다.

- **제외 목록 검토를 건너뜁니다.** 부실 제외 목록 항목은 유효한 주소에 대한 전달을 차단할 수 있지만, 누락된 항목은 바운스를 생성하는 잘못된 주소에 전달할 수 있습니다. 주요 캠페인 전에 제외 목록을 검토하고 정리합니다.

- **홍보 캠페인에 대한 빈도 제한 무시:** 다른 캠페인도 활성화된 상태에서 빈도 제한 없이 홍보 캠페인을 보내면 프로필에서 단기간에 여러 메시지를 받아 구독 취소와 스팸 고객 불만을 초래할 수 있습니다.

- **대상 모집단을 확인하지 않고 캠페인 예약:** 대상 대상을 확인하기 전에 캠페인을 활성화하면 0이 아닌 평가된 모집단이 배달되어 메시지가 0이 됩니다. 활성화하기 전에 항상 대상 크기를 확인하십시오.

- **대상이 트리거된 여정에 대해 일괄 평가 사용:** 여정이 일괄 평가와 함께 대상 읽기 항목을 사용하는 경우 프로필이 실시간에 가깝게 입력되지 않습니다. 실시간에 가까운 여정 입력이 필요한 경우 대상의 스트리밍 평가를 사용하십시오.

- **동의 적용을 구성하지 않음:** 유효한 마케팅 동의 없이 프로필에 메시지를 보내는 것은 규정을 위반하고 전달성의 평판을 손상시킵니다. 동의 필드가 채워지고 채널 표면 수준에서 적용되는지 확인합니다.

### 우수 사례

- 간단한 브로드캐스트 사용 사례에 대해 옵션 A(예약된 여정)로 시작하고 사전 게재 논리 또는 동작 기반 타이밍이 필요할 때만 옵션 B(대상에 의해 트리거된 캠페인)로 졸업합니다
- 최대 규정 준수를 위해 이메일 본문에 항상 원클릭 목록 구독 취소 헤더와 구독 취소 링크를 모두 포함합니다
- 캠페인 전반에서 일관성을 보장하기 위해 머리글, 바닥글 및 법적 고지 사항에 대해 재사용 가능한 콘텐츠 조각 만들기
- 캠페인을 활성화하기 전에 빈도 제한 규칙을 설정하여 동시 전송 간 초과 메시징을 방지합니다.
- 다변량 실험으로 진행하기 전에 A/B 테스트부터 시작하여 제목란 및 CTA를 최적화하려면 콘텐츠 실험을 사용하십시오
- 모든 활성 캠페인에 우선 순위 점수를 할당하여 일관된 충돌 해결을 보장합니다
- 캠페인 실행 시간 전에 완료하도록 배치 대상 평가를 예약하여 대상 데이터를 새로 고칩니다.
- 활성화 전에 증명 이메일을 보내고 이메일 렌더링 기능을 사용하여 이메일 클라이언트에 메시지가 올바르게 표시되는지 확인합니다.
- 캠페인 활성화 직후 라이브 보고서를 모니터링하여 게재 문제를 조기에 포착합니다.
- 향후 참조 및 지속적인 최적화를 위해 캠페인 구성 및 실험 결과 보관

### 절충안 결정

구현 선택 시 다음 절충점을 평가해야 합니다.

#### 단순성과 유연성 비교

예약된 캠페인(옵션 A)은 가장 간단한 구성을 제공하지만 사전 게재 논리를 제공하지 않습니다. 대상자가 트리거한 여정(옵션 B)는 사전 게재 논리를 제공하지만 구성 복잡성을 추가합니다.

- **옵션 A 우대:** 출시 속도, 운영 간소화, 마케터 셀프서비스
- **옵션 B는 다음과 같은 이점을 제공합니다.** 동작 타깃팅, 조건부 제외, 여러 단계 여정에 대한 확장성
- **권장 사항:** 간단한 전송을 위해 옵션 A로 시작합니다. 사용 사례에서 실제로 배달 전에 대기, 조건 또는 분기 논리가 필요한 경우에만 옵션 B로 이동합니다. 오케스트레이션 기능을 사용하지 않는 간단한 일괄 처리 전송에는 여정 캔버스를 사용하지 마십시오.

#### 대상의 신선도와 평가 비용 비교

스트리밍 평가는 실시간에 가까운 대상 업데이트를 제공하지만 세그먼트 규칙 제한이 있습니다. 배치 평가는 모든 세그먼트 규칙 함수를 지원하지만 일별 일정으로 평가합니다.

- **스트리밍 우대:** 적시성, 동작 중심의 정확성, 대상자에 의해 트리거된 여정 항목
- **일괄 처리 선호:** 복잡한 대상 논리, 많은 모집단, 낮은 평가 오버헤드
- **권장 사항:** 일별 새로 고침이 충분한 예약된 캠페인(옵션 A)에 일괄 처리 평가를 사용합니다. 프로필이 자격을 충족하면 입력해야 하는 대상으로 트리거된 여정(옵션 B)에 대해 스트리밍 평가를 사용합니다. 대상 세그먼트 규칙 표현식이 스트리밍에 적합하지 않으면 규칙을 재구조화하거나 배치 수준 지연을 적용합니다.

#### Personalization 깊이와 작성 복잡성 비교

심층적인 개인화(조건부 콘텐츠 블록, 동적 섹션)는 참여를 향상시키지만 작성 및 테스트 노력을 증가시킵니다.

- **심층적인 개인화 혜택:** 참여율 향상, 더 적절한 고객 경험, 더 나은 전환
- **간단한 개인화 혜택:** 실행 시간이 빨라지고 테스트 부담이 줄며 렌더링 오류 위험이 줄어듭니다
- **권장 사항:** 측정된 성능 향상에 따라 조건부 콘텐츠 블록의 기본 개인화(이름, 관련 제품 범주) 및 레이어로 시작합니다. 활성화하기 전에 항상 여러 테스트 프로필에서 모든 콘텐츠 변형을 테스트하십시오.

#### 빈도 제어와 메시지 도달

엄격한 빈도 제한은 초과 메시징을 방지하지만, 최근에 다른 메시지를 받은 프로필에 대한 캠페인 전달을 억제할 수 있습니다.

- **엄격한 제한 적용:** 고객 경험 품질, 낮은 구독 취소율, 브랜드 신뢰도
- **최대 제한 우대:** 최대 메시지 도달, 총 노출 수 증가, 캠페인 적용 범위
- **권장 사항:** 마케팅 캠페인에 대해 항상 빈도 제한을 사용하도록 설정하십시오. 채널별 상한(예: 일주일에 3~5개의 이메일, 일주일에 1~2개의 SMS)을 설정합니다. 시간이 중요한 메시지 또는 트랜잭션 메시지만 최대 가용량 규칙으로 제외합니다.

## 관련 설명서

이 단원에서는 항목별로 구성된 [!DNL Experience League] 설명서에 대한 포괄적인 링크를 제공합니다.

### 캠페인

- [캠페인 시작하기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/get-started-with-campaigns)
- [캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [API 트리거된 캠페인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/api-triggered-campaigns/api-triggered-campaigns)

### 여정

- [여정 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
- [대상자 여정 읽기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience)

### 채널 구성

- [이메일 구성 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/get-started-email-config)
- [하위 도메인 위임](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/delegate-subdomain)
- [IP 풀 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-pools)
- [IP 준비 계획](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/ip-warmup/ip-warmup-gs)
- [이메일 표면 설정](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/configure-email/email-settings)
- [SMS 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/sms/configure-sms/sms-configuration)
- [푸시 알림 채널 구성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/push/configure-push/push-configuration)
- [제외 목록 관리](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/monitor-reputation/manage-suppression-list)

### 메시지 작성 및 개인화

- [이메일 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/create-email)
- [이메일 콘텐츠 디자인](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/design-emails)
- [이메일 Designer 콘텐츠 구성 요소 사용](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/content-components)
- [이메일 콘텐츠 가져오기 또는 코드 작성](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/email/design-email/code-content)
- [개인화 추가](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalize)
- [Personalization 구문](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/personalization-syntax)
- [도우미 함수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/functions/functions)
- [다이내믹 콘텐츠](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/personalization/dynamic-content)

### 콘텐츠 관리

- [콘텐츠 템플릿 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-templates/content-templates)
- [컨텐츠 조각을 사용한 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/fragments/content-fragments)
- [콘텐츠 미리보기 및 테스트](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/preview-test)
- [이메일 증명 보내기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/proofs)
- [전자 메일 렌더링](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/preview-test/email-rendering)

### 콘텐츠 실험

- [콘텐츠 실험 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/content-experiment)
- [콘텐츠 실험 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/create-content-experiment)
- [콘텐츠 실험 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-report)
- [통계적 계산](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/content-management/content-experiment/experiment-calculations)

### 빈도 및 충돌 관리

- [빈도 규칙](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/frequency-rules)
- [비즈니스 규칙 개요](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/business-rules/business-rules)
- [충돌 및 우선 순위 관리 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/gs-conflict-prioritization)
- [우선 순위 점수](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/priority-scores)
- [잠재적인 충돌 파악](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/conflicts)
- [여정 한도 및 중재](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/conflict-prioritization/journey-capping)

### 대상자 및 세그멘테이션

- [세그먼테이션 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home)
- [세그먼트 빌더 UI 안내서](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder)
- [스트리밍 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/streaming-segmentation)
- [에지 세분화](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/methods/edge-segmentation)
- [대상자 구성](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/audience-composition)
- [Profile Query Language 참조](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/pql/overview)

### 보고

- [캠페인 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-live-report)
- [캠페인 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/campaign-global-report-cja)
- [여정 라이브 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-live-report)
- [여정 글로벌 보고서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/journey-global-report-cja)
- [Customer Journey Analytics 작업](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reports/report-cja-manage)
- [AJO + CJA 통합 안내서](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/reporting/channel-report/cja-ajo)

### 데이터 거버넌스 및 동의

- [데이터 거버넌스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home)
- [데이터 사용 레이블 개요](https://experienceleague.adobe.com/ko/docs/experience-platform/data-governance/labels/overview)
- [동의 및 환경 설정 필드 그룹](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/field-groups/profile/consents)
- [Journey Optimizer의 동의](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent-restricted)

### 데이터 모델링 및 ID

- [XDM 시스템 개요](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home)
- [스키마 컴포지션 기본 사항](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition)
- [ID 서비스 개요](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home)
- [병합 정책 개요](https://experienceleague.adobe.com/en/docs/experience-platform/profile/merge-policies/overview)

### 가드레일

- [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails)
- [실시간 고객 프로필 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [수집 보호](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/guardrails)

### 튜토리얼 및 시작하기

- [Journey Optimizer 시작](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/get-started)
- [첫 캠페인 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/create-campaign)
- [첫 여정 만들기](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)
