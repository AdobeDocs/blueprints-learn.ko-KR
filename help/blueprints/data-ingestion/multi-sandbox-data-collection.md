---
title: 다중 샌드박스 이벤트 전달 데이터 수집 블루프린트
description: 수집된 데이터 스트리밍 기준 [!DNL Experience Platform] (AEP) 이벤트 전달을 사용하여 여러 샌드박스에 대한 SDK
solution: Data Collection
kt: 7202
exl-id: c24a47fe-b3da-4170-9416-74d2b6a18f32
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 60%

---

# 다중 샌드박스 이벤트 전달 데이터 수집 블루프린트

다중 샌드박스 이벤트 전달 데이터 수집 블루프린트는 Adobe으로 데이터가 수집되는 방식을 보여 줍니다. [!DNL Experience Platform] 웹 및 모바일 SDK는 단일 이벤트를 수집하고 여러 이벤트에 전달하도록 구성할 수 있습니다 [!DNL Experience Platform] (AEP) 샌드박스. 이 블루프린트는 Adobe 태그의 이벤트 전달 기능을 사용하는 특수한 사용 사례입니다.

이벤트를 복제하는 것 외에도 이벤트 전달 기능을 사용하면 기존에 수집한 데이터 중 다른 샌드박스의 요구 사항을 충족하는 데이터를 추가하거나 필터링하거나 조정할 수 있습니다. 예를 들면 샌드박스 A는 모든 이벤트 데이터 요소를 수신하고 샌드박스 B는 PII 외의 데이터만 수신해야 하는 경우가 있습니다.

이벤트 전달에서는 데이터 요구 사항에 필요한 데이터 요소, 규칙 및 확장이 포함된 별도의 태그 속성을 사용합니다. 이벤트 전달 속성은 들어오는 이벤트에 대해 필요에 따라 데이터를 수집하고 관리할 수 있습니다.

대상 샌드박스에 이벤트 전달 HTTPS 확장에서 사용할 HTTP 스트리밍 끝점 이 구성되어 있어야 합니다.

## 사용 사례

* 전역 데이터 보고 - 여러 샌드박스를 사용하여 운영 환경을 분리하고 있으며 여러 샌드박스에 걸친 보고를 위해 데이터 수집을 단일 샌드박스로 통합해야 하는 경우. 보고 샌드박스로 이벤트를 전달하면 각 샌드박스 운영 환경에서 실시간으로 수집한 데이터를 보고 샌드박스로 보낼 수 있습니다.
* 각 샌드박스 운영 환경에 대한 다양한 데이터 규칙을 기반으로 샌드박스 간 데이터 수집을 관리합니다. 의료 및 금융 서비스 등 중요한 데이터를 필터링해야 하는 운영 환경.

## 애플리케이션

* Adobe [!DNL Experience Platform] 데이터 수집

## 아키텍처

<img src="assets/multi-Sandbox-Data-Collection.svg" alt="다중 샌드박스 이벤트 전달을 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

1. 태그 작성자가 태그 속성과 이벤트 전달 속성을 모두 정의합니다. 여기에서 작성자는 데이터 요소, 규칙 및 데이터 수집을 관리하는 작업을 정의합니다. 태그 속성 코드는 클라이언트에서 실행되며 CDN 호스트에 의해 배포된다는 점에 유의하세요. 다음 [!UICONTROL 이벤트 전달 속성] 코드가 Adobe에서 실행됩니다. [!DNL Edge Server].

1. 클라이언트에서 수집된 데이터는 [!DNL Edge Network]. 또한 고객은 서버측 수집의 방법으로 먼저 데이터를 자체 서버에 보낼 수 있는 옵션이 있습니다. Web SDK가 서버에서 서버로의 수집 기능을 제공할 수 있습니다. 그러나 이를 구현하려면 다른 프로그래밍 모델이 필요합니다. 설명서 참조 **[!DNL Edge Network]서버 API 개요** 아래

1. 플랫폼 [!DNL Edge Network] 데이터 수집 페이로드를 수신하고 Target 및 Analytics와 같은 필수 시스템에 대한 데이터 흐름을 조정합니다.

1. 페이로드에 도착하는 이벤트 데이터에 액세스하는 데에는 이벤트 전달 속성 데이터 요소를 사용합니다. 필요에 따라 규칙을 사용하여 이벤트 데이터를 전달 전에 조정할 수도 있습니다. 가령 스트리밍 데이터 수집을 위해 데이터 형식을 필요한 XDM에 맞추는 등의 조정 작업을 할 수 있습니다.

1. 이벤트 전달은 이벤트 데이터를 HTTPS 엔드포인트로 전달하는 기능이 있는 HTTPS 확장을 제공합니다.

1. 샌드박스 2를 구성할 때는 전달한 이벤트를 수신하는 스트리밍 엔드포인트를 사용합니다.

## 관련 설명서

* [이벤트 전달 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko)
* [이벤트 전달 비디오](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=ko)
* 웹 SDK의 [이벤트 전달 레슨](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=ko) 튜토리얼
* [[!DNL Experience Platform] Web SDK 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko)
* [[!DNL Edge Network] 서버 API 개요](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ko)

## 관련 블로그 게시물

* [Adobe을 통한 웹 사이트 성능 향상 [!DNL Experience Platform] Web SDK 및 [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [Adobe을 통한 구현 불만 사항 해결 [!DNL Experience Platform] Web SDK 및 [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Adobe [!DNL Experience Platform] Audience Management용 Web SDK](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe [!DNL Experience Platform] Web SDK - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Adobe [!DNL Experience Platform] Adobe Analytics용 웹 SDK 마이그레이션 시나리오](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [Adobe 통합 [!DNL Experience Platform] Adobe이 있는 서비스 [!DNL Experience Platform] 웹 SDK](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Adobe을 통해 모바일 애플리케이션 개발 가속화 [!DNL Experience Platform] Mobile SDK 및 Launch](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Adobe Experience Platform 웹 SDK를 통한 고객 워크플로우 간소화](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
