---
title: Adobe Experience Platform Web SDK 및 [!DNL Edge Network]
description: 이 아키텍처 다이어그램은 Experience Platform 웹 및 모바일 SDK 및 [!DNL Edge Network]을(를) 통한 수집을 보여 줍니다
solution: Experience Platform,Data Collection
kt: null
thumbnail: null
exl-id: 3cc9e849-a75d-40ad-a604-6acf4c2c9f89
TQID: https://experienceleague.adobe.com/s56Vkgc-UvIUNPhcB8x3WFlzhfeEUpRxXZCMu0zf58Y
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
    internal-label: Implementation
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
    internal-label: Data collection
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: 79738031788419872e32b8f754febacbfd18cc06
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 60%
---
# Adobe Experience Platform Web SDK 및 [!DNL Edge Network]

웹 및 모바일 SDK 및 [!DNL Edge Network] Server API에 대한 개요와 자세한 내용은 다음을 참조하십시오.

* [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
* [모바일 SDK 개요](https://developer.adobe.com/client-sdks/documentation/)
* [[!DNL Edge Network] 서버 API](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ko)

WebSDK에서 지원하는 애플리케이션 기능에 대한 자세한 개요는 다음 설명서를 참조하세요.

* [웹 SDK 애플리케이션 기능 지원](https://github.com/orgs/adobe/projects/18/views/1)

애플리케이션별 SDK에서 Web 및 Mobile SDK로 마이그레이션하는 작업과 관련된 자세한 내용은 다음 설명서를 참조하세요.

* [ID 서비스](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=ko)
* [Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/analytics-overview.html?lang=ko)
* [Target](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=ko)
* [Target용 Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/a4t/overview.html?lang=ko)

## Experience Platform Web/Mobile SDK 또는 [!DNL Edge Network] Server API 배포

아래 아키텍처 다이어그램은 Experience Platform Web SDK를 활용하는 배포 및 데이터 수집을 보여줍니다.

![Experience Platform 웹 및 모바일 SDK을 사용하는 구현을 위한 참조 아키텍처](assets/sdk_data_flow_diagram.png){width="1000" zoomable="yes"}

Experience Edge, Experience Platform 서비스, 애플리케이션의 시퀀스 다이어그램

![온라인/오프라인 웹 Personalization 시나리오에 대한 참조 아키텍처](assets/sdk_sequence_diagram.png){width="1000" zoomable="yes"}

## 참조 설명서

* [Web SDK 튜토리얼을 통해 Adobe Experience Cloud 구현](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko)
* [모바일 앱에서 Adobe Experience Cloud 구현 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=ko)
