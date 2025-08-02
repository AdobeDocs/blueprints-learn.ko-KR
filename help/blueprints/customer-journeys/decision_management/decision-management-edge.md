---
title: Edge의 의사 결정 관리 블루프린트
description: 실시간 웹 및 모바일 경험을 포함하여 다양한 채널의 소비자에게 개인화된 오퍼를 제공합니다.
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 68%

---

# Journey Optimizer - Edge 블루프린트의 [!DNL Decision Management]

[!DNL Decision Management]은(는) [!DNL Journey Optimizer]의 일부로 제공된 서비스입니다. 이 블루프린트에서는 애플리케이션의 사용 사례 및 기술적 기능을 간략하게 훑어보고 의사 결정 관리의 다양한 아키텍처 구성 요소와 고려할 사항을 자세히 설명합니다.

>[!MORELIKETHIS]
>
>[!DNL Decision Management]에 대한 자세한 내용은 [블루프린트 개요](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-overview.html?lang=ko)를 참조하거나 [제품 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ko)를 참조하세요.

[!DNL Decision Management]은(는) 다음 두 가지 방법 중 하나로 배포할 수 있습니다. 첫 번째 방법은 단일 데이터 센터 아키텍처인 [!DNL Experience Platform] 허브를 사용하는 것입니다. [허브] 접근 방식에서는 오퍼를 실행, 개인화하여 초 단위의 지연 시간을 두고 게재합니다 따라서 허브 아키텍처는 지연 시간이 초 미만 단위일 필요가 없는 고객 경험에 가장 적합합니다. 예를 들면 콜센터 또는 대면 상호 작용 등의 상담원 지원 경험이나 키오스크에서 제공하는 오퍼 의사 결정이 있습니다.

두 번째 방법은 Experience Platform [!DNL Edge Network]을(를) 사용하는 것입니다. 이 인프라는 빠르게 초당 밀리초 미만의 경험을 제공할 수 있도록 지리적으로 분산된 인프라입니다. 지연을 최소화하기 위해 소비자 지리적 위치에 가장 가까운 Edge 인프라에서 최종 소비자 경험을 실행하고 있습니다. Edge의 [!DNL Decision Management]은(는) 실시간 소비자 경험을 제공하도록 설계되었습니다. 여기에는 웹 또는 모바일 인바운드 개인화 요청 등의 경험이 포함됩니다.

이 블루프린트는 Edge에서의 의사 결정 관리에 대해 구체적인 정보를 다룹니다.

허브의 의사 결정 관리에 대한 자세한 내용은 [허브의 의사 결정 관리](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/decision-management/decision-management-hub.html?lang=ko) 블루프린트를 참조하세요.

## Edge의 의사 결정 관리 사용 사례

* 프로필 컨텍스트 지연 시간이 15분 미만으로 엄격하고 의사 결정 관리 실행이 1초 미만인 스트리밍 사용 사례입니다.
* 웹 또는 모바일 인바운드 경험을 통한 온라인 개인화.
* 크로스 채널 여정 실행 - Adobe Journey Optimizer를 통한 웹, 모바일, 이메일, 기타 상호 작용 채널 간 오퍼 일관성.

## 아키텍처

<img src="../assets/offers_edge.svg" alt="참조 아키텍처: Edge의 의사 결정 관리 블루프린트" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 통합 패턴

| 통합 | 설명 |
| :-- | :--- |
| [의사 결정 관리와 Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html?lang=ko) | 의사 결정 관리를 Adobe Target과 통합하여 오퍼를 테스트하고 Target 경험으로 게재할 수 있습니다. |

## 가드레일

* Journey Optimizer의 가드레일에 대해서는 다음의 [Journey Optimizer 가드레일](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html?lang=ko)을 참조하세요.

* 의사 결정 관리의 가드레일은 다음 [의사 결정 관리 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/offer-decisioning-app-service.html)을 참조하세요.

[보호 기능 및 전체 지연 지침](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/guardrails.html?lang=ko)

## 관련 설명서

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ko)
* [Adobe Journey Optimizer 의사 결정 관리](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ko)
* [ Adobe Journey Optimizer 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe 의사 결정 관리 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/offer-decisioning-app-service.html)
