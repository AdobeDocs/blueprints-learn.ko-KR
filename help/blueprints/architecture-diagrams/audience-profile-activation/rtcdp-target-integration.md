---
title: Adobe Real-Time CDP 및 Adobe Target 통합
description: Real-Time Customer Data Platform 대상 및 프로필 컨텍스트가 Edge Network을 통해 Adobe Target과 통합되는 방법을 이해합니다.
landing-page-description: Real-Time Customer Data Platform 대상 및 프로필 컨텍스트가 Edge Network을 통해 Adobe Target과 통합되는 방법을 이해합니다.
short-description: Real-Time Customer Data Platform 대상 및 프로필 컨텍스트가 Edge Network을 통해 Adobe Target과 통합되는 방법을 이해합니다.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
TQID: https://experienceleague.adobe.com/1ti2SqfAFOgnKbaJ70xwGI-xHDE1WXJ7-oTStcJJy1E
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
    internal-label: Real-Time Customer Data Platform
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
    internal-label: Segmentation
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: ba929a52-9339-4154-9487-317dc875a3c7
    internal-label: Use cases
  - id: c132d929-fa62-4271-803e-b823be07b914
    internal-label: Profile
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
    internal-label: Implementation
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
    internal-label: Segments
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
    internal-label: B2B
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
    internal-label: Audiences
  - id: ee602049-8a18-43df-9299-a689a025a371
    internal-label: Use cases
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 17%
---
# Adobe Real-Time CDP 및 Adobe Target 통합

이 아키텍처는 [!DNL Real-Time Customer Data Platform]과(와) [!DNL Adobe Target]이(가) Edge Network을 통해 통합하는 방법을 보여 줍니다. 에지에서의 실시간 대상 평가와 Target과의 스트리밍 또는 배치 대상 공유 중에서 선택하는 데 도움이 됩니다.

## 애플리케이션

* [!DNL Real-Time Customer Data Platform]
* [!DNL Adobe Target]
* [!DNL Experience Platform] Edge Network
* Experience Platform Web SDK 또는 Edge Network Server API

## 통합 접근 방식 선택

### 가장자리에서 실시간 대상 평가

[!DNL Adobe Target]에 동일한 페이지 또는 다음 페이지 개인화에 대해 에지 평가 대상 및 프로필 특성이 필요한 경우 이 방법을 사용하십시오. [!DNL Adobe Target] 및 [!DNL Experience Platform] 서비스를 사용하도록 설정한 상태에서 웹 SDK 또는 Edge Network Server API를 구현하고 데이터 스트림을 구성하십시오.

### Target에 스트리밍 및 일괄 처리 대상 공유

[!DNL Real-Time Customer Data Platform]에서 평가된 대상을 실시간 에지 평가 없이 [!DNL Adobe Target]에서 사용할 수 있어야 하는 경우 이 방법을 사용하십시오. 기본 프로덕션 샌드박스에서 [!DNL Adobe Target] 대상을 구성합니다. 웹 SDK 또는 Edge Network Server API 구현은 실시간 에지 평가 또는 사용자 지정 ID 네임스페이스 조회에만 필요합니다.

## 아키텍처 다이어그램

이 다이어그램은 데이터 수집, Edge Network, [!DNL Real-Time Customer Data Platform] 및 [!DNL Adobe Target] 간의 기본 통합 지점을 보여 줍니다.

![Real-Time Customer Data Platform 및 Adobe Target 통합을 위한 아키텍처](assets/real_time_cdp_target.png){zoomable="yes"}

## 데이터 흐름 다이어그램

이 시퀀스는 클라이언트 요청이 Edge Network에 도달하고, 대상자와 프로필 컨텍스트를 평가하고, [!DNL Adobe Target]에 개인화 요청을 보내고, 결과 경험을 클라이언트에 반환하는 방법을 보여 줍니다.

![Real-Time Customer Data Platform 및 Adobe Target 통합을 위한 데이터 흐름](assets/real_time_cdp_target_data_flow_detail.png){zoomable="yes"}

## 구현 시 고려 사항

* [!DNL Adobe Target] 및 [!DNL Real-Time Customer Data Platform]은(는) 동일한 IMS 조직을 사용해야 합니다.
* [!DNL Adobe Target] 대상은 [!DNL Real-Time Customer Data Platform]에서 기본 프로덕션 샌드박스를 지원합니다.
* 가장자리에서 사용자 지정 ID 네임스페이스 조회의 경우 Web SDK 또는 Edge Network Server API를 사용하고 ID 맵에 각 ID를 포함합니다.
* at.js를 사용하는 경우 프로필 통합은 ECID ID 네임스페이스만 지원합니다.

## 관련 설명서

### 통합 구성

* [실시간 고객 데이터 플랫폼을 위한 Adobe Target 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ko)
* [Edge 데이터스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ko)

### 에지에서 구현

* [Experience Platform 웹 SDK 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
* [Experience Cloud ID 서비스 설명서](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ko)

### 대상자 평가

* [Experience Platform 세그멘테이션 개요](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ko)
* [실시간 세분화](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=ko)
* [스트리밍 세분화](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)
* [병합 정책 구성](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=ko#create-a-merge-policy)
