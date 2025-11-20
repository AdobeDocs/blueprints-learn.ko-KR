---
title: '[!DNL Journey Optimizer] - 여정 블루프린트'
description: Adobe Experience Platform을 스트리밍 데이터, 고객 프로필 및 세분화의 중앙 허브로 사용하여 트리거된 메시지 및 경험을 실행합니다.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: e96b48e55c0fe2f48dc83f48ad41f5b686ec8dc1
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 15%

---

# [!DNL Journey Optimizer] 블루프린트

Adobe [!DNL Journey Optimizer]은(는) Adobe Experience Platform에 구축된 클라우드 기반 애플리케이션으로, 여러 채널에서 고객 여정을 실시간으로 예약 및 오케스트레이션할 수 있습니다. 이벤트 기반 트리거, 대상자 세분화 및 의사 결정 서비스를 지원하여 이메일, SMS, 푸시, 웹 및 인앱 메시지를 통해 개인화된 경험을 제공합니다. 인바운드 및 아웃바운드 시스템과 통합되므로 고객 라이프사이클 전반에 걸쳐 단일화된 고객 상태 관리 및 상황별 참여가 가능합니다.

이 블루프린트는 응용 프로그램의 기술 기능에 대해 간략하게 설명하고 [!DNL Journey Optimizer]을(를) 구성하는 다양한 아키텍처 구성 요소에 대해 자세히 살펴봅니다.

<br>

## 사용 사례

>[!BEGINTABS]
>[!TAB 여정(이벤트 기반, 실시간)]

- **포기 복구:** 사용자가 전자 메일, 푸시 또는 인앱을 통해 장바구니, 양식 또는 세션을 중단하는 경우 개인화된 메시지를 트리거합니다.
- **신규 사용자 등록:** 신규 사용자가 신규 계정 환경 설정, 관련 프로모션 또는 혜택을 등록한 후 즉시 신규 사용자를 참여시키십시오
- **트랜잭션 메시지:** 이벤트 트리거를 사용하여 실시간 확인, 경고 또는 업데이트(예: 주문 배송, 암호 재설정)를 보냅니다.
- **Contextal 타깃팅:** 사용자의 신호 및 위치를 기반으로 즉시 사용자와 통신하여 환경을 안내하고 안내하는 데 도움을 줍니다.
- **상황에 맞는 상향 판매/교차 판매:** 실시간 프로필 특성 및 최근 상호 작용을 기반으로 개인화된 오퍼를 제공합니다.

>[!TAB Campaign 오케스트레이션(예약됨, 브랜드 시작)]

- **프로모션 캠페인**: 제품 출시, 시즌 제안 또는 판매 이벤트에 대한 다단계, 멀티채널 캠페인을 시작합니다.
- **라이프사이클 마케팅**: 생일 메시지, 갱신 미리 알림 또는 충성도 이정표와 같은 반복 캠페인을 자동화합니다.
- **대상 기반 Funnel 푸시**: 비즈니스 논리 또는 CRM 특성을 기반으로 대상을 구조화된 캠페인으로 세그먼트화하고 푸시합니다.
- **뉴스레터 및 콘텐츠 배포**: 전자 메일 및 모바일에서 타겟팅된 대상자에게 개인화된 콘텐츠를 예약하고 제공합니다.
- **다시 참여 캠페인**: 비활성 사용자를 식별하고 비활성 임계값을 기반으로 참여 흐름에 다시 도입합니다.

>[!ENDTABS]

<br>

## 아키텍처

<img src="images/ajo-architecture.svg" alt="참조 아키텍처 Adobe Journey Optimizer 블루프린트" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 블루프린트 시나리오

| 시나리오 | 설명 |
| :-- | :-- |
| [여정](journey-optimizer-journeys.md) | Adobe Journey Optimizer의 AJO 여정은 실시간 이벤트 또는 대상 세그먼트에 의해 트리거된 자동화된 개인화된 고객 경험으로, 마케터가 이메일, SMS 및 푸시 알림과 같은 채널 간에 관련 메시지를 전달할 수 있습니다. |
| [Campaign 오케스트레이션](journey-optimizer-campaigns.md) | AJO Campaign Orchestration을 사용하면 마케터가 실시간 데이터 및 대상 인사이트를 사용하여 개인화된 크로스 채널 캠페인을 디자인하고 실행할 수 있습니다. 동적 타깃팅, 메시지 게재 및 여정 논리를 지원하여 이메일, SMS, 푸시 및 사용자 지정 채널 전반에서 고객 참여를 최적화할 수 있습니다. | |

<br>

## 통합 패턴

| 통합 | 설명 | 기술 고려 사항 |
| :-- | :-- | :-- |
| [서드파티 메시지](3rd-party-messaging.md) | Adobe [!DNL Journey Optimizer]을(를) 서드파티 메시징 플랫폼과 통합하여 개인화된 고객 커뮤니케이션을 통합 및 제공하는 방법을 보여 줍니다. | <ul><li>타사 시스템은 **전달자 토큰 인증**&#x200B;을 지원해야 합니다.</li><li>다중 테넌트 아키텍처로 인해 **고정 IP가 지원되지 않습니다**.</li><li>타사 시스템의 **API 속도 제한**&#x200B;에 유의하십시오. 고객은 **Adobe Journey Optimizer**&#x200B;에서 시작된 트래픽을 처리하기 위해 추가 용량을 구입해야 할 수 있습니다.</li><li>**의사 결정 관리**&#x200B;는 메시지 페이로드 또는 게재 논리에서 지원되지 않습니다.</li></ul> |
| [[!DNL Journey Optimizer] Adobe Campaign v8 사용](../campaign-v8/ajo-and-campaign-v8.md) | Adobe [!DNL Journey Optimizer]을(를) Adobe Campaign v8의 트랜잭션 메시지 기능과 통합하여 최종 메시지 배달을 실행하는 방법을 보여 줍니다. | <ul><li>메시지 제한이 없습니다. 5분당 4,000개 메시지 제한.</li><li>이벤트에서 시작한 여정 만 지원</li><li>Campaign에서 보낸 메시지에서는 의사 결정 관리가 지원되지 않습니다.</li></ul> |

<br>

## 필요 조건

Adobe [!DNL Experience Platform]:

- [!DNL Journey Optimizer] 데이터 원본을 구성하려면 먼저 시스템에서 스키마와 데이터 집합을 구성해야 합니다.
- XDM 경험 이벤트 클래스 기반 스키마의 경우 규칙 기반 이벤트가 아닌 이벤트가 트리거되도록 하려면 &#39;Orchestration eventID 필드 그룹을 추가합니다.
- XDM 개별 프로필 클래스 기반 스키마의 경우 [!DNL Journey Optimizer]에서 사용할 테스트 프로필을 로드할 수 있도록 &#39;프로필 테스트 세부 정보&#39; 필드 그룹을 추가하십시오.

<br>

이메일:

- 메시지 보내기에 사용할 하위 도메인이 있어야 합니다.
- 하위 도메인을 Adobe에 완전히 위임하거나(권장) CNAME을 사용하여 Adobe 전용 DNS 서버(사용자 정의)를 가리킬 수 있습니다.
- 전달성 보장을 위해 각 하위 도메인에 대해 Google TXT 기록이 있어야 합니다.

<br>

모바일 푸시:

- 고객은 앱을 빌드할 수 있는 모바일 개발자가 있어야 합니다.
- Adobe Experience Platform Mobile SDK

<br>

## 가드레일

[[!DNL Journey Optimizer] 보호 기능 제품 링크](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/guardrails.html)

[보호 기능 및 전체 지연 지침](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 관련 설명서

- [[!DNL Experience Platform] 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
- [[!DNL Experience Platform] 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
- [[!DNL Experience Platform Mobile SDK] 설명서](https://experienceleague.adobe.com/docs/mobile.html)
- [[!DNL Journey Optimizer] 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)
- [[!DNL Journey Optimizer] 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)