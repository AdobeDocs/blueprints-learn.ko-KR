---
title: 서버측 엔터프라이즈 데이터 수집 블루프린트
description: Experience Platform SDK를 통해 대상으로 스트리밍 수집한 데이터
solution: Data Collection
kt: 7202
exl-id: 8d6f0705-628b-44e4-a3fc-da6c5e308a5b
source-git-commit: 1d286f4dabe71f359c14a88c91f306ea443646a6
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 서버측 엔터프라이즈 데이터 수집 블루프린트

서버측 엔터프라이즈 데이터 수집 블루프린트에서는 Adobe Experience Platform 웹 및 모바일 SDK로 수집한 데이터를 Experience Platform Edge Network에서 원하는 대상으로 전달하는 방법을 설명합니다. SDK에서 수집한 원 데이터 전체를 전달하거나 태그 속성(이전 Launch)에서 구성한 바에 따라 이벤트 및 규칙을 기반으로 특정 데이터를 전달할 수 있습니다.

## 사용 사례

* 웹 또는 모바일에서 단일 수집 태그를 사용하여 데이터를 수집함으로써 클라이언트 브라우저 및 앱에 대한 코드 권한 요구를 줄입니다. 단일 데이터 수집 소스에서 수집한 데이터를 다양한 종점으로 전파합니다.
* 수집한 데이터와 비교하여 인사이트 및 애플리케이션을 구축할 수 있도록 수집한 데이터를 파트너 애플리케이션 또는 데이터 저장 위치로 전달합니다.

## 애플리케이션

* Adobe Experience Platform 수집

## 아키텍처

<img src="assets/enterprise_collection.svg" alt="엔터프라이즈 데이터 수집을 위한 참조 아키텍처" style="width:80%; border:1px solid #4a4a4a" />

## 관련 설명서

* [이벤트 전달 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko)
* [이벤트 전달 비디오](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=ko)
* 웹 SDK의 [이벤트 전달 레슨](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=ko) 튜토리얼

## 관련 블로그 게시물

* [[!DNL Boosting Website Performance with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [[!DNL Solving Implementation Pain Points with Adobe Experience Platform Web SDK and Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Adobe Experience Platform Web SDK — Adobe Target]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [[!DNL Adobe Experience Platform Web SDK Migration Scenarios for Adobe Analytics]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [[!DNL Unify Your Adobe Experience Platform Services with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [[!DNL Accelerate Your Mobile Application Development with Adobe Experience Platform Mobile SDK and Launch]](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [[!DNL Simplifying Customer Workflows with Adobe Experience Platform Web SDK]](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
