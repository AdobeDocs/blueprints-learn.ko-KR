---
title: 다중 샌드박스 이벤트 전달 데이터 수집 블루프린트
description: 이벤트 전달을 사용하여 Experience Platform SDK에서 수집한 데이터를 여러 샌드박스로 스트리밍합니다
solution: Data Collection
kt: 7202
source-git-commit: 8ea7041103f86f034740f00a607ae36ca0b358cf
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 18%

---

# 다중 샌드박스 이벤트 전달 데이터 수집 블루프린트

다중 샌드박스 이벤트 전달 데이터 수집 블루프린트는 Adobe Experience Platform Web 및 Mobile SDK로 수집된 데이터를 구성하여 단일 이벤트를 수집하고 여러 AEP 샌드박스로 전달하는 방법을 보여줍니다. 이 블루프린트는 Adobe 태그의 이벤트 전달 기능을 사용하는 특정 사용 사례입니다.

이벤트를 복제하는 것 외에도 이벤트 전달 기능을 사용하여 다른 샌드박스의 요구 사항을 충족하는 수집된 원래 데이터에 추가, 필터링 또는 조작할 수 있습니다. 예를 들어 샌드박스 A는 모든 이벤트 데이터 요소를 수신해야 하며 샌드박스 B는 PII 이외의 데이터만 수신해야 합니다.

이벤트 전달에서는 데이터 요구 사항에 필요한 데이터 요소, 규칙 및 확장을 포함하는 별도의 태그 속성을 사용합니다. 수신 이벤트를 사용하여 이벤트 전달 속성은 데이터를 수집하고 필요에 따라 전달하기 전에 관리할 수 있습니다.

대상 샌드박스에는 이벤트 전달 HTTPS 확장에서 사용할 HTTP 스트리밍 종료 포인트가 필요합니다.



## 사용 사례

* 전역 데이터 보고 - 여러 샌드박스를 사용하여 운영 환경을 격리하고 교차 샌드박스 보고를 위해 데이터 수집을 하나의 샌드박스로 통합해야 하는 경우. 보고 샌드박스로 이벤트 전달 을 사용하면 각 샌드박스 운영 환경에서 실시간으로 수집되는 데이터를 보고 샌드박스로 전송할 수 있습니다
* 각 샌드박스 운영 환경에 대한 다양한 데이터 규칙을 기반으로 샌드박스 간 데이터 수집을 관리합니다. 의료 및 금융 서비스와 같은 중요한 데이터를 필터링해야 하는 운영 환경

## 애플리케이션

* Adobe Experience Platform 수집

## 아키텍처

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="다중 샌드박스 이벤트 전달을 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" />

1. 태그 작성자는 태그 속성과 이벤트 전달 속성을 모두 정의합니다. 여기에서 작성자는 데이터 수집을 관리하는 데이터 요소, 규칙 및 작업을 정의합니다. 태그 속성 코드는 클라이언트에서 실행되며 CDN 호스트에 의해 배포됩니다. 이벤트 전달 속성 코드는 Adobe Edge 서버에서 실행됩니다.

1. 클라이언트에서 수집된 데이터는 Edge Server로 전송됩니다. 또한 고객은 서버 측 수집 방법으로 먼저 데이터를 자체 서버로 전송하는 옵션을 사용할 수 있습니다.
WebSDK는 서버에 서버 수집 기능을 제공할 수 있습니다. 그러나 이를 구현하려면 다른 프로그래밍 모델이 필요합니다. 설명서를 참조하십시오 **Edge Network Server API 개요** 아래

1. Platform Edge Server는 데이터 수집 페이로드를 수신하고 Target 및 Analytics와 같은 필수 시스템으로 데이터 흐름을 오케스트레이션합니다.

1. 이벤트 전달 속성 데이터 요소는 페이로드에 도착하는 이벤트 데이터에 액세스하는 데 사용됩니다. 규칙을 사용하여 전달하기 전에 필요에 따라 이벤트 데이터를 조작할 수도 있습니다. 스트리밍 데이터 수집을 위해 필요한 XDM에 데이터 형식 지정 등의 작업을 수행합니다

1. 이벤트 전달은 이벤트 데이터를 HTTPS 종료 지점에 전달하는 기능을 제공하는 HTTPS 확장 기능을 제공합니다.

1. 샌드박스 2는 전달된 이벤트를 받는 스트리밍 종료 지점으로 구성됩니다.

## 관련 설명서

* [이벤트 전달 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko)
* [이벤트 전달 비디오](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=ko)
* 웹 SDK의 [이벤트 전달 레슨](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=ko) 튜토리얼
* [Experience Platform WebSDK 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko)
* [Edge Network Server API 개요](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ko)

## 관련 블로그 게시물

* [[!DNL Boosting Website Performance with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [[!DNL Solving Implementation Pain Points with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Adobe Experience Platform Web SDK — Adobe Target]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [[!DNL Adobe Experience Platform Web SDK Migration Scenarios for Adobe Analytics]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [[!DNL Unify Your Adobe Experience Platform Services with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [[!DNL Accelerate Your Mobile Application Development with Adobe Experience Platform Mobile SDK and Launch]](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [[!DNL Simplifying Customer Workflows with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
