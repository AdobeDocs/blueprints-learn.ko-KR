---
title: 통신 업계 - 트리거된 메시지용 Journey Optimizer
description: 고객은 장기 충성도를 위해 효율적인 고객 온보딩과 동시에 실시간으로 맞춤 거래를 제공할 수 있습니다.
solution: Experience Platform, Journey Optimizer
kt: 9486
source-git-commit: c393d73d2fa7acd4e5c2d99c098503b023b6115d
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 12%

---


# 통신 업계 비즈니스 과제

이 블루프린트를 구현하기 전에 전기통신회사의 &quot;새 라인 추가&quot; 이메일 캠페인은 사용자가 7일 대기 기간 후에 전환했는지 여부와 이에 대한 확인을 기반으로 했습니다. 이러한 기준이 충족되면 추가적인 터치 포인트가 개시됩니다.

사용자가 현재 상태 7일 대기 시간 보다 빠른 라인을 추가하고 싶어했던 타임리어 후속 작업을 시작하기 위해 이 제한을 해결해야만 했다.

## Adobe 방법

* 새 행을 추가하도록 전환하지 못한 사용자를 식별하는 Adobe Analytics 데이터는 Adobe Journey Optimizer에서 사용할 데이터 소스로 포함됩니다.
* Adobe Journey Optimizer은 고객이 계정에 새 줄을 추가하여 전환하도록 유도하기 위해 고안된 사용자 지정된 &quot;포기&quot; 메시지를 받을 때까지의 규칙을 사용합니다.


## 전달된 비즈니스 가치

| 목표 | 전술 | 값 잠금 해제됨 |
|---|---|---|
| **더 높은 캠페인 전환율 유도&#x200B;**<br></br>**연간 계정 매출 증대**</ul> | <ul><li>라인 추가에 관심이 있지만 아직 전환되지 않은 사용자를 위해 거의 실시간으로 새 세그먼트를 만듭니다.</li><li>전환되지 않은 고객을 위해 관심 있는 비변환자를 위한 두 번째 터치포인트를 사용하여 후속 조치를 수행하십시오. </li><li>테스트 전략을 사용하여 여정 성능을 측정하고 이메일을 통한 전환을 최적화합니다.</li></ul> | <ul><li><strong>고품질 관련 경험:</strong> 이때 여정 오케스트레이션이 적용되면 고객이 보다 연관성 있는 메시지를 경험하여 이메일 목록 이탈을 줄일 수 있습니다.</li><li><strong>규모에 맞게 Journey Orchestration:</strong>개인화된 시간별 여정을 만들어 전환율과 총 매출을 높일 수 있습니다.</li></ul> |

## 기본 블루프린트: Experience Cloud 애플리케이션을 사용한 고객 및 활성화

### 설명

<ul><li>Adobe Experience Platform을 데이터, 고객 프로필 및 세분화 스트리밍의 중심 허브로 사용하고 Journey Orchestration으로 여정 오케스트레이션 및 메시지 게재를 스트리밍하여 트리거 및 스트리밍 메시지를 실행합니다.</li></ul>

### Experience Cloud 애플리케이션

<ul><li>Adobe Journey Optimizer</li></ul>

### 블루프린트 아키텍처

<a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=ko"><img alt="텔레커뮤니케이션 비즈니스를 위한 축소판 이미지는 장기적인 충성도를 위해 효율적인 고객 온보딩과 동시에 실시간으로 맞춤 거래를 제공합니다." src="https://experienceleague.adobe.com/docs/blueprints-learn/assets/journey-optimizer.png?lang=en"/></a>





