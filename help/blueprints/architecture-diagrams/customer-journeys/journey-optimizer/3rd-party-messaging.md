---
title: Journey Optimizer - 서드파티 메시징
description: Adobe Journey Optimizer을 서드파티 메시징 시스템과 함께 사용하여 개인화된 통신을 전송하는 방법을 보여 줍니다.
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
TQID: https://experienceleague.adobe.com/dlCwgPnHuoU0IGois2Yy3e9wPELIQsLkStzTBVl5M1M
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
    internal-label: Journey Optimizer
feature_v2:
  - id: a653cc2e-bc85-4353-a306-399e5b247978
    internal-label: Journey Optimizer campaigns
  - id: d556b755-390a-43f0-be32-a08cf6236126
    internal-label: Configuration
  - id: d998adac-2f81-400b-a669-d07bb196e4eb
    internal-label: Journeys
subfeature_v2:
  - id: af7571a6-3ddb-4c1c-abdf-4d4dde592140
    internal-label: Source connectors
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
    internal-label: Customer profiles
source-git-commit: 79738031788419872e32b8f754febacbfd18cc06
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 15%
---
# 서드파티 메시징

>[!TIP]
>이 아키텍처는 Campaign Management &amp; Orchestration 아래에 [사용 사례 패턴](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md)으로도 설명되어 있습니다.

Adobe Journey Optimizer을 서드파티 메시징 시스템과 함께 사용하여 개인화된 통신을 전송하는 방법을 보여 줍니다.

<br>

## 아키텍처

![참조 아키텍처 Journey Optimizer](images/ajo-third-party-messaging.png){width="1000" zoomable="yes"}

<br>

토폴로지에는 서드파티로 트랜잭션 페이로드를 보내는 [!DNL Journey Optimizer]이(가) 표시됩니다.
사용자 지정 작업 또는 REST API 통합을 통한 메시징 애플리케이션. [타사 메시징 사용 사례 패턴 사용](/help/blueprints/use-case-patterns/campaign-management-orchestration/third-party-messaging.md)
사전 요구 사항, 보호 및 구현 지침을 확인하십시오.

<br>

## 관련 설명서

* [Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
* [Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko)
* [Journey Optimizer 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)
