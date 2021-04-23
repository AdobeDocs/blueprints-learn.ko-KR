---
title: 온라인/오프라인 Audience Activation 블루프린트
description: 온라인/오프라인 Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 81%

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

<img src="assets/onoff.svg" alt="온라인/오프라인 Audience Activation 청사진을 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

* [프로필 및 세분화 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* 세그먼트 일괄 처리 작업은 기존에 정한 예약 일정에 따라 하루 한 번 실행됩니다. 그 다음에는 예약한 대상 게재에 앞서 세그먼트 내보내기 작업이 실행됩니다. 참고: 세그먼트 일괄 처리 작업과 대상 게재 작업은 별도로 실행됩니다. 세그먼트 일괄 처리 작업과 내보내기 작업의 속도는 평가하는 프로필의 수와 규모 및 세그먼트의 수에 따라 달라집니다.
* 세그먼트 스트리밍 작업은 프로필에 도착할 데이터를 스트리밍하는 몇 분 안에 평가되며, 즉시 프로필에 세그먼트 멤버십을 쓰고 구독할 애플리케이션에 이벤트를 보냅니다.
* 세그먼트 멤버십 스트리밍이 스트리밍 대상에서 즉각 실행되며, 대상의 수집 패턴에 따라 단일 세그먼트 멤버십 이벤트 또는 여러 프로필 이벤트의 소규모 일괄 처리 단위로 게재됩니다. 예약된 세그먼트 일괄 처리를 통해 게재하여 스트리밍 시 평가하는 모든 세그먼트에 대해, 예약한 대상이 게재에 앞서 프로필로부터 세그먼트 내보내기 작업을 시작합니다.
* Audience Manager에 실시간 고객 데이터 플랫폼] 세그먼트 멤버십을 공유하는 경우 세그먼트 스트리밍에 대해 몇 분 내에, 일괄 세그먼테이션에 대한 일괄 세그먼트 평가가 완료되면 몇 분 내에 발생합니다.[!UICONTROL 
* Experience Platform에서 Audience Manager로 공유한 세그먼트는 스트리밍과 일괄 처리 평가 방법 중 어떤 방식을 사용하든 세그먼트 실현 몇 분 이내에 공유됩니다. 세그먼트가 처음 만들어지면 Experience Platform과 Audience Manager 간에 초기 세그먼트 구성 동기화가 있으며 약 4시간 후 Experience Platform 세그먼트 멤버십이 Audience Manager 프로필에서 구현될 수 있습니다. Experience Platform과 Audience Manager 대상자 구성 전이나 대상자 메타데이터를 Experience Platform에서 Audience Manager로 동기화하기 전에 실현된 대상자 멤버십의 경우 &quot;기존&quot; 세그먼트 멤버십이 공유되는 후속 세그먼트 작업 전까지는 실현되지 않습니다.
* 세그먼트 일괄 처리 작업에서 시작된 대상 일괄 처리 또는 스트리밍 작업에서는 프로필 특성 업데이트와 세그먼트 멤버십을 공유할 수 있습니다.
* 스트리밍 대상에 대한 세분화 스트리밍 작업은 세그먼트 멤버십 업데이트만 공유합니다.

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
* [프로필 및 세그멘테이션 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)
* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ko)

## 관련 비디오 및 튜토리얼

* [Real-time Customer Data Platform 개요 ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ko)
* [[!UICONTROL Real-time Customer Data Platform 데모]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ko)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)
