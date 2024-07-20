---
title: 웹/모바일 SDK, [!DNL Edge Network] 배포 아키텍처 다이어그램
description: 이 블루프린트는 Experience Platform 웹 및 모바일 SDK 및  [!DNL Edge Network]을(를) 통한 아키텍처 및 수집을 보여 줍니다.
solution: Experience Platform,Data Collection
kt: null
thumbnail: null
exl-id: 3cc9e849-a75d-40ad-a604-6acf4c2c9f89
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 69%

---


# Experience Platform 웹 SDK 및 [!DNL Edge Network] 아키텍처 다이어그램

웹 및 모바일 SDK와 [!DNL Edge Network] Server API에 대한 개요와 자세한 내용은 다음을 참조하십시오.

* [Web SDK 개요](https://experienceleague.adobe.com/docs/web-sdk.html?lang=ko)
* [Mobile SDK 개요](https://developer.adobe.com/client-sdks/documentation/)
* [[!DNL Edge Network] 서버 API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ko)

WebSDK에서 지원하는 애플리케이션 기능에 대한 자세한 개요는 다음 설명서를 참조하세요.

* [Web SDK 애플리케이션 기능 지원](https://github.com/orgs/adobe/projects/18/views/1)

애플리케이션별 SDK에서 Web 및 Mobile SDK로 마이그레이션하는 작업과 관련된 자세한 내용은 다음 설명서를 참조하세요.

* [신원 서비스](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=ko)
* [Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/analytics-overview.html?lang=ko)
* [Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=ko)
* [Analytics for Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/a4t/overview.html?lang=ko)

## 웹/모바일 SDK 또는 [!DNL Edge Network] 서버 API 배포 Experience Platform

아래 아키텍처 다이어그램은 Experience Platform Web SDK를 활용하는 배포 및 데이터 수집을 보여줍니다.

<img src="assets/web_sdk_flow.svg" alt="Experience Platform Web 및 Mobile SDK를 사용하여 구현할 때 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

Experience Edge, Experience Platform 서비스, 애플리케이션의 시퀀스 다이어그램

<img src="assets/web_sdk_sequence.svg" alt="온라인/오프라인 웹 개인화 블루프린트를 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## 참조 설명서

* [Web SDK를 사용하여 Adobe Experience Cloud 구현하기 튜토리얼](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko)
* [모바일 앱에서 Adobe Experience Cloud 구현 튜토리얼](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=ko)
