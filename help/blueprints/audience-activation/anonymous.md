---
title: 익명 Audience Activation 블루프린트
description: 고객의 익명 행동 데이터를 기반으로 여러 웹과 광고 채널에 걸쳐 대상자를 타겟팅하는 방법을 알아봅니다. 이를 통해 전 디바이스에 걸쳐 개인화되고 일관적인 실시간 고객 경험을 제공할 수 있습니다.
landing-page-description: 고객의 익명 행동 데이터를 기반으로 여러 웹과 광고 채널에 걸쳐 대상자를 타겟팅하는 방법을 알아봅니다.
solution: Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 63%

---

# 익명 Audience Activation 블루프린트

익명 대상자 활성화는 익명의 디바이스 및 행동 데이터를 기반으로 웹, 모바일, 광고 채널 전반에 걸쳐 대상자를 타겟팅하고 대상자에 맞추어 개인화하는 기능입니다.

## 사용 사례

* 웹 사이트, 모바일 앱 또는 지원되는 광고 채널에서 익명의 디지털 대상자에 대한 타겟팅 및 개인화를 수행합니다.
* 알려진 디바이스 및 행동 특성을 기반으로 랜딩 페이지 및 사전 인증 경험을 최적화합니다.
* Audience Manager 서드파티 데이터 네트워크를 활용하여 타겟팅을 위해 대상자를 개선 및 확장합니다.


## 애플리케이션

* Audience Manager
* Real-time Customer Data Platform

Audience Manager과 Real-time Customer Data Platform을 모두 활용하여 온사이트 및 광고 대상을 위한 익명의 Audience Activation을 강화할 수 있습니다. Real-time Customer Data Platform은 Analytics Mobile Apps 또는 Analytics Premium에서 카탈로그로 지정된 익명 장치 식별자가 있는 광고 대상의 하위 집합만 지원합니다 [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=ko).

Microsoft Bing, Google DV360 및 TradeDesk는 익명 장치 기반 타깃팅을 위해 지원되는 기본 Real-time Customer Data Platform 광고 대상입니다. 이 외에도 Real-time Customer Data Platform은 [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=ko) 및 [알려진 고객 활성화 블루프린트](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ko).

## 아키텍처

<img src="assets/anonymous_activation.svg" alt="익명 대상자 활성화 블루프린트를 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" />

<br>

## Audience Manager 구현 단계

* Audience Manager 구현에 대한 자세한 내용은 다음 [설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ko)를 참조하세요.

## Real-time Customer Data Platform 구현 단계

* Real-time Customer Data Platform의 구현 단계는 다음을 참조하십시오 [설명서](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ko).

## 관련 설명서

* [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html?lang=ko)
* [Experience Cloud [!UICONTROL 대상]](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=ko)
* [Audience Manager와 Target 통합](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html?lang=ko)
* [Adobe Analytics 세그먼트를 Audience Manager를 통해 공유](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ko)
* [알려진 고객 활성화 블루프린트](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ko).
* [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=ko)
