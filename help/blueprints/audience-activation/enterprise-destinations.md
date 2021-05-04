---
title: 엔터프라이즈 대상 블루프린트에 대한 고객 및 프로필 활성화
description: 엔터프라이즈 대상 고객 및 프로필 활성화
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: da21d1796eb9a2c9c0f087d82606874ca55bd4ea
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 39%

---

# 엔터프라이즈 대상 블루프린트에 대한 고객 및 프로필 활성화

[!UICONTROL 실시간 고객 데이터 플랫폼]에서 엔터프라이즈 데이터 저장소 및 애플리케이션으로 스트리밍하거나 일괄적으로 프로필 및 대상 변경 사항과 이벤트를 공유할 수 있습니다. 이러한 프로필 및 대상 이벤트를 사용하여 중단된 응용 프로그램 프로세스나 웨비나 등록을 팔로우하는 것과 같은 고객에 대한 판매 또는 지원 작업을 시작하거나 [!UICONTROL 실시간 고객 데이터 플랫폼]에서 최신 고객 속성 및 인텔리전스로 기업 애플리케이션을 업데이트할 수 있습니다.

## 사용 사례

* 고객 데이터와 인사이트의 엔터프라이즈 추적, 스토리지, 분석 및 활성화를 위해 클라우드 스토리지 대상 또는 스트리밍 대상에 대한 프로파일 및 고객 활성화.

## 애플리케이션

* Adobe Experience Platform 활성화

## 아키텍처

<img src="assets/enterprise_destination_activation.svg" alt="기업 활성화 시나리오를 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />


## 가드레일

대상 및 프로필 활성화 개요 페이지에 나와 있는 지침을 참조하십시오. [LINK](overview.md)

## 구현 단계

1. 인제스트할 데이터에 대한 스키마를 만듭니다.
1. 수집할 데이터를 위한 데이터 세트를 만듭니다.
1. 수집한 데이터를 통합 프로필로 결합할 수 있도록 스키마에 올바른 ID와 ID 네임스페이스를 구성합니다.
1. 프로필 처리를 위해 스키마 및 데이터 세트를 활성화합니다.
1. 데이터 수집에 대한 모든 소스를 구성합니다.
1. Experience Platform에서 세그먼트를 작성하여 일괄 또는 스트리밍으로 평가할 수 있습니다. 세그먼트를 일괄 처리로 평가할지 스트리밍으로 평가할지는 시스템에서 자동으로 결정합니다.
1. 프로필 특성과 대상자 멤버십을 공유할 대상을 원하는 대상으로 구성합니다.

## 관련 설명서

* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ko)
* [클라우드 스토리지 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP 대상](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [Real-time Customer Data Platform 제품 설명 ](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html)
* [프로필 및 세그멘테이션 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)

## 관련 비디오 및 튜토리얼

* [Real-time Customer Data Platform 개요 ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ko)
* [[!UICONTROL Real-time Customer Data Platform 데모]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ko)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)
