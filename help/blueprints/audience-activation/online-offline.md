---
title: 온라인/오프라인 Audience Activation 블루프린트
description: 온라인/오프라인 Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 76fe52d8e83e075f9e7ce6e8596880181b01a7fd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 79%

---

# 온라인/오프라인 Audience Activation 블루프린트

오프라인 주문, 거래, CRM 또는 충성도 데이터 등 오프라인 특성 및 이벤트와 온라인 행동을 함께 사용하여 온라인 타겟팅과 개인화를 수행합니다.

대상자를 이메일 공급자, 소셜 네트워크 및 광고 대상 등 알려진 프로필 기반 대상으로 활성화합니다.

## 사용 사례

* 소셜 및 광고 대상의 알려진 대상자 타겟팅
* 온라인 및 오프라인 특성을 활용한 온라인 개인화
* 대상자를 이메일 및 SMS 등 알려진 채널로 활성화합니다.

## 애플리케이션

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]

## 아키텍처

<img src="assets/online_offline_activation.svg" alt="온라인/오프라인 Audience Activation 청사진을 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

대상 및 프로필 활성화 개요 페이지에 나와 있는 지침을 참조하십시오. [LINK](overview.md)

## 구현 단계

1. Experience Platform에서 스키마와 데이터 세트를 구성합니다.
1. 수집한 데이터를 통합 프로필로 결합할 수 있도록 스키마에 올바른 ID와 ID 네임스페이스를 구성합니다.
1. 프로필에 대해 스키마와 데이터 세트를 활성화합니다.
1. 데이터를 Platform으로 수집합니다.
1. Audience Manager에 공유될 Experience Platform에 정의된 대상에 대해 Experience Platform과 Audience Manager 간에 실시간 고객 데이터 플랫폼] 세그먼트 공유를 프로비저닝합니다.[!UICONTROL 
1. Experience Platform에서 일괄 처리 또는 스트리밍 시 평가할 세그먼트를 작성합니다. 세그먼트를 일괄 처리로 평가할지 스트리밍으로 평가할지는 시스템에서 자동으로 결정합니다.
1. 프로필 특성과 대상자 멤버십을 공유할 대상을 원하는 대상으로 구성합니다.

## 구현 시 고려 사항

* 대상에 프로필 데이터를 공유하려면 대상 페이로드에 대상이 사용하는 특정 ID 값을 포함해야 합니다. 대상 대상에 필요한 모든 ID를 플랫폼으로 인제스트하고 [!UICONTROL 실시간 고객 프로필]에 대한 ID로 구성해야 합니다.

* Experience Platform에서 Audience Manager로 대상자를 공유하는 활성화 시나리오에서는 [!UICONTROL Real-time Customer Profile]에 포함된 ID를 모두 Audience Manager로 공유합니다. Experience Platform의 대상자는 필요한 대상 ID가 [!UICONTROL Real-time Customer Profile]에 포함된 경우 또는 [!UICONTROL Real-time Customer Profile]의 ID가 Audience Manager에서 필요 대상 ID와 연결된 경우에 Audience Manager 대상을 통해 공유할 수 있습니다.

## 관련 설명서

* [Real-time Customer Data Platform 제품 설명 ](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html)
* [프로필 및 세그멘테이션 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)
* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ko)

## 관련 비디오 및 튜토리얼

* [Real-time Customer Data Platform 개요 ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ko)
* [[!UICONTROL Real-time Customer Data Platform 데모]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ko)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)
