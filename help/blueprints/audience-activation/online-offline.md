---
title: 온라인/오프라인 Audience Activation 블루프린트
description: 온라인/오프라인 Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
translation-type: tm+mt
source-git-commit: 2f35195b875d85033993f31c8cef0f85a7f6cccc
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 35%

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

### 세그먼트 평가 및 활성화 보장

| 세그멘테이션 유형 | 빈도 | 처리량 | 지연(세그먼트 평가) | 지연(세그먼트 활성화) | 활성화 페이로드 |
|-|-|-|-|-||
| 가장자리 세그멘테이션 | Edge 세그멘테이션은 현재 베타 버전으로 제공되고 있으며 Adobe Target 및 Adobe Journey Optimizer을 통해 실시간으로 동일한 페이지 의사 결정을 위해 Experience Platform 에지 네트워크에서 유효한 실시간 세그멘테이션을 평가할 수 있습니다. |  | ~100ms | Adobe Target의 개인화, 에지 프로필의 프로필 조회 및 쿠키 기반 대상을 통한 활성화를 위해 즉시 사용할 수 있습니다. | 에지 사이트에서 프로필 조회 및 쿠키 기반 대상에 대한 대상 멤버십을 사용할 수 있습니다.<br>대상 멤버십 및 프로필 속성은 Adobe Target 및 Journey Optimizer에서 사용할 수 있습니다.  |
| 스트리밍 세그멘테이션 | 새로운 스트리밍 이벤트 또는 레코드를 실시간 고객 프로파일에 인제스트할 때마다 세그먼트 정의가 유효한 스트리밍 세그먼트입니다. <br>스트리밍 세그먼트  [기준에 ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko) 대한 지침은 세그멘테이션 설명서를 참조하십시오. | 초당 최대 1,500개의 이벤트.  | ~ p95 &lt;5분 | 스트리밍 대상:스트리밍 대상 멤버십은 약 10분 이내에 활성화되거나 대상의 요구 사항에 따라 마이크로 일괄적으로 활성화됩니다.<br>예약된 대상:스트리밍 대상 멤버십은 예약된 대상 배달 시간에 따라 일괄 활성화됩니다. | 스트리밍 대상:대상 멤버십 변경 사항, ID 값 및 프로필 속성.<br>예약된 대상:대상 멤버십 변경 사항, ID 값 및 프로필 속성. |
| 증분 세그먼테이션 | 마지막 증분 또는 일괄 세그먼트 평가 이후 실시간 고객 프로필로 인제스트한 새 데이터에 대해 시간당 한 번. |  |  | 스트리밍 대상:증분 대상 멤버십은 약 10분 이내에 활성화되거나 대상의 요구 사항에 따라 미시적 일괄 처리됩니다.<br>예약된 대상:예약된 대상 배달 시간에 따라 증분 대상 멤버십이 일괄적으로 활성화됩니다. | 스트리밍 대상:대상 멤버십 변경 및 ID 값만 가능합니다.<br>예약된 대상:대상 멤버십 변경 사항, ID 값 및 프로필 속성. |
| 일괄 세그먼테이션 | 미리 결정된 시스템 세트 일정을 기준으로 하루에 한 번 또는 API를 통해 수동으로 시작한 애드혹. |  | 최대 10TB의 프로필 스토어 크기에 대해 작업당 약 1시간, 10TB에서 100TB까지의 프로필 스토어 크기에 대해 작업당 2시간. 일괄 세그먼트 작업 성능은 평가 중인 세그먼트 수 프로필, 프로필 크기 및 수에 따라 달라집니다. | 스트리밍 대상:배치 대상 멤버십은 대상의 요구 사항에 따라 세그먼테이션 평가가 약 10일 이내에 활성화되거나 미시적 일괄 처리됩니다.<br>예약된 대상:예약된 대상 배달 시간에 따라 일괄 대상 멤버십이 활성화됩니다. | 스트리밍 대상:대상 멤버십 변경 및 ID 값만 가능합니다.<br>예약된 대상:대상 멤버십 변경 사항, ID 값 및 프로필 속성. |

### 애플리케이션 간 대상 공유를 위한 보장

| 고객 애플리케이션 통합 | 빈도 | 처리량/볼륨 | 지연(세그먼트 평가) | 지연(세그먼트 활성화) |
|-|-|-|-||
| 실시간 고객 데이터 플랫폼-Audience Manager | 세그멘테이션 유형에 따라 - 위의 세그멘테이션 가리기 테이블을 참조하십시오. | 세그멘테이션 유형에 따라 - 위의 세그멘테이션 가리기 테이블을 참조하십시오. | 세그멘테이션 유형에 따라 - 위의 세그멘테이션 가리기 테이블을 참조하십시오. | 세그먼트 평가가 완료된 후 몇 분 이내에<br>실시간 고객 데이터 플랫폼과 Audience Manager 간의 초기 고객 구성 동기화는 약 4시간이 소요됩니다.<br>4시간 동안 실현된 모든 고객 멤버십은 후속 배치 세그먼테이션 작업의 Audience Manager에 &quot;기존&quot; 대상 멤버십으로 기록됩니다. |
| Adobe Analytics에서 Audience Manager으로 |  | 기본적으로 각 Adobe Analytics 보고서 세트에 대해 최대 75명의 대상을 공유할 수 있습니다. Audience Manager 라이선스를 사용하는 경우 Adobe Analytics 및 Adobe Target 또는 Adobe Audience Manager과 Adobe Target 간에 공유할 수 있는 대상 수에 제한이 없습니다. |  |  |
| Adobe Analytics에서 실시간 고객 데이터 플랫폼으로 | 현재 사용할 수 없음 | 현재 사용할 수 없음 | 현재 사용할 수 없음 | 현재 사용할 수 없음 |





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
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ko)

## 관련 비디오 및 튜토리얼

* [Real-time Customer Data Platform 개요 ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ko)
* [[!UICONTROL Real-time Customer Data Platform 데모]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ko)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)
