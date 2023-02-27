---
title: 통신 업계 - Journey Optimizer를 통한 트리거 메시지
description: 고객에게 실시간으로 맞춤형 딜을 제공하는 한편 장기적 충성도를 확보하기 위한 효율적 고객 온보딩을 진행합니다.
solution: Journey Optimizer
kt: 9486
exl-id: fa4a6569-3972-4b97-91f1-7ca8ffd3c5b3
source-git-commit: 1a0ce987fc615080bb78fb8ecf60c96e362a95c0
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 통신 업계 비즈니스 과제

이 블루프린트를 구현하기 전에 해당 통신 회사의 &quot;새 회선 추가&quot; 이메일 캠페인은 사용자의 전환 여부를 기반으로 했으며, 대기 기간 7일 이후에만 이를 확인할 수 있었습니다. 이 기준이 충족되야만 접점이 추가되었습니다.

이와 같은 제한을 해결해 기존 7일의 대기 기간 이전에 회선을 추가해 사용자에게 보다 시의적절한 후속 조치를 해야 했습니다.

## Adobe의 접근 방식

* 새 회선을 추가하도록 전환하지 못한 사용자를 식별하는 Adobe Analytics 데이터를 Adobe Journey Optimizer에서 사용할 수 있는 데이터 소스로 포함했습니다.
* Adobe Journey Optimizer에서는 고객이 사용자 정의된 &quot;포기&quot; 메시지를 받을 시간을 정하는 규칙을 사용합니다. 이 메시지는 고객이 자신의 계정에 새로운 회선을 추가함으로써 전환을 이루도록 유도합니다.


## 제공한 비즈니스 가치

| 목표 | 전략 | 발견한 가치 |
|---|---|---|
| **보다 높은 캠페인 전환율 유도&#x200B;**<br></br>**연간 계정 매출 증대**</ul> | <ul><li>회선 추가에 관심을 보였지만 아직 전환되지 않은 사용자에 대한 새 세그먼트를 거의 실시간으로 만듭니다.</li><li>비전환 고객에 대한 후속 조치를 진행하여 관심이 있는 비전환자를 위한 두 번째 접점을 제공합니다. </li><li>테스트 전략을 통해 여정의 수행을 측정하고 이메일을 통한 전환을 최적화합니다.</li></ul> | <ul><li><strong>높은 품질, 관련성 높은 경험:</strong> 적절한 여정 오케스트레이션을 통해 고객에게 보다 관련성 높은 메시지 경험을 제공하여 이메일 목록 이탈을 줄일 수 있습니다.</li><li><strong>규모에 맞는 Journey Orchestration:</strong> 개인화되고 시의적절한 여정을 만들어 전환율과 총 매출을 높일 수 있습니다.</li></ul> |

## 기본 블루프린트: Experience Cloud 애플리케이션을 사용한 대상자 및 활성화

### 설명

<ul><li>Adobe Experience Platform을 데이터, 고객 프로필 및 세분화 스트리밍의 중심 허브로 사용하고 Journey Orchestration으로 여정 오케스트레이션 및 메시지 게재를 스트리밍하여 트리거 및 스트리밍 메시지를 실행합니다.</li></ul>

### Experience Cloud 애플리케이션

<ul><li>Adobe Journey Optimizer</li></ul>

### 블루프린트 아키텍처

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=ko"><img alt="텔레커뮤니케이션 비즈니스를 위한 이미지는 장기적인 충성도에 대한 효율적인 고객 온보딩과 동시에 실시간 맞춤 거래를 제공합니다." src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/ajo-architecture.svg"/></a>
