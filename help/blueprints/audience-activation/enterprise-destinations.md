---
title: 엔터프라이즈 대상 블루프린트에 대한 고객 및 프로필 활성화
description: 엔터프라이즈 대상 고객 및 프로필 활성화
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
translation-type: tm+mt
source-git-commit: a63da7d5da3038cf66b5f2c99e117d4aa5b21cc1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# 엔터프라이즈 대상 블루프린트에 대한 고객 및 프로필 활성화

기업 데이터 저장소에 대한 프로필 및 대상 변경 사항을 복제 및 업데이트하여 활성화 및 보고 사용 사례를 제공합니다.<!-- This sentence is difficult to mentally process because there's no verb. Describe what the customer can do with this feature. The first paragraph on a page should not be an abstract description.-->

기업 시스템 및 애플리케이션에 대한 [!UICONTROL 실시간 고객 데이터 플랫폼]의 고객 행동에 대한 알림을 통해 고객에게 판매 또는 지원 조치를 시작합니다.<!-- What kinds of sales or support actions? You might add a "For example...." The content in these blueprints should be more simple and friendly.-->

## 사용 사례

* 고객 데이터와 인사이트의 엔터프라이즈 추적, 스토리지, 분석 및 활성화를 위해 클라우드 스토리지 대상 또는 스트리밍 대상에 대한 프로파일 및 고객 활성화.

## 애플리케이션

* Adobe Experience Platform 활성화

## 아키텍처

<img src="assets/enterprise_destination.svg" alt="기업 활성화 시나리오를 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

[프로필 및 세그멘테이션 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

지연 및 처리량 임계값:

스트리밍 세분화:

* 스트리밍 세분화를 위해 최대 5분, 초당 최대 1500개의 이벤트
* 스트리밍 활성화를 위한 최대 11분

일괄 세분화:
하루에 한 번 또는 API를 통해 수동으로 애드혹 시작

* 최대 10TB의 프로파일 저장소 크기에 대해 작업당 약 1시간
* 10TB에서 100TB 프로파일 저장소 크기에 대해 작업당 약 2시간

## 구현 단계

1. 인제스트할 데이터에 대한 스키마를 만듭니다.<!-- Cross-references to these topics would be helpful -->
1. 수집할 데이터를 위한 데이터 세트를 만듭니다.
1. 스키마의 올바른 ID 및 ID 네임스페이스를 구성하여 인제스트된 데이터가 통합 프로파일로 연결될 수 있도록 합니다.
1. 프로필 처리를 위해 스키마 및 데이터 세트를 활성화합니다.
1. 데이터 수집에 대한 모든 소스를 구성합니다.
1. Experience Platform에서 세그먼트를 작성하여 일괄 또는 스트리밍으로 평가할 수 있습니다. 시스템에서 자동으로 세그먼트가 일괄 처리로 평가되는지 아니면 스트리밍으로 평가되는지를 결정합니다.
1. 원하는 대상에 프로필 속성 및 대상 멤버십을 공유할 대상을 구성합니다.

## 구현 고려 사항

특성 및 ID 활성화

* [!UICONTROL 실시간 고객 데이터 플랫폼] 은 고객 멤버쉽뿐만 아니라 활성화를 위해 선택한 세그먼트의 구성원인 프로파일에 대한 속성 및 ID 변경을 활성화할 수 있습니다. 특성 또는 ID를 활성화하는 것이 목표인 경우 속성 및 ID 업데이트가 전송되는 모든 프로파일을 포함하는 글로벌 세그먼트를 정의해야 합니다. 이 시점에서 세그먼트 및 원하는 속성을 선택하여 대상 구성의 일부로 활성화할 수 있습니다.
* 배치 대상은 특성 전용 변경 이벤트 활성화를 지원하지 않습니다. 정품 인증을 위해 선택한 속성과 함께 전체 또는 증분 대상 멤버십이 전송될 수 있지만 배치 대상을 통해 속성 전용 변경 이벤트를 활성화할 수 없습니다.

스트리밍 대상에 일괄 세그먼트 활성화

* 스트리밍 대상에 대한 일괄 세그먼트 정품 인증이 지원됩니다. 세그먼트 일괄 처리 작업은 스트리밍 활성화를 위해 세그먼트 작업이 완료된 후 파이프라인에 메시지를 배치합니다.

일괄 처리 대상으로 스트리밍 세그먼트 활성화

* 일괄 처리 대상에 대한 스트리밍 세그먼트 활성화가 지원됩니다. 배치 대상 일정은 배치 대상 일정을 기준으로 프로필 세그먼트 멤버십을 내보냅니다. 여기에는 스트리밍과 일괄 처리 방법을 통해 결정된 세그먼트 멤버십이 모두 포함됩니다.

경험 이벤트 활성화

* 원시 경험 이벤트 활성화는 지원되지 않습니다. 경험 이벤트에 대해 활성화하려면 경험 이벤트 논리를 포함하거나 제외하는 필수 규칙을 사용하여 세그먼트를 만들어야 합니다. 경험 이벤트에 대해 정의된 세그먼트를 만들고, 세그먼트 멤버십을 원시 경험 이벤트를 활성화하기 위한 프록시로 활성화할 수 있습니다. 또한 [!UICONTROL Launch Server Side]을 사용하여 SDK를 통해 수집된 원시 경험 이벤트를 활성화하십시오.

## 관련 설명서

* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [클라우드 스토리지 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP 대상](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [[!UICONTROL 실시간 고객 데이터 ] 플랫폼제품 설명](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [프로필 및 세그멘테이션 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## 관련 비디오 및 Tutorials

* [[!UICONTROL 실시간 고객 데이터 플랫폼 ] 개요](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [실시간  [!UICONTROL 고객 데이터 플랫폼 데모]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
