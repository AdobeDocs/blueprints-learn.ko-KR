---
title: 의사 결정 관리 개요
description: 고객 여정 간에 개인화된 오퍼를 제공합니다.
solution: Experience Platform, Journey Optimizer
source-git-commit: 5b2f7531cc05178127fb08d3fdafcbce70192ecd
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 40%

---

# Journey Optimizer - 의사 결정 관리 개요

의사 결정 관리에 대한 자세한 내용은 [여기](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=ko)에 있는 제품 설명서를 참조하세요.

Adobe 의사 결정 관리는 Adobe Journey Optimizer의 일부로 제공되는 서비스입니다. 이 블루프린트는 애플리케이션의 사용 사례 및 기술 기능에 대해 간략하게 설명하고 결정 관리를 구성하는 다양한 아키텍처 구성 요소 및 고려 사항을 자세히 설명합니다.

Journey Optimizer은 모든 터치 포인트를 적시에 걸쳐 고객에게 최상의 오퍼와 경험을 전달하는 데 사용됩니다. 의사 결정 관리를 사용하면 마케팅 오퍼의 중앙 라이브러리 및 Adobe Experience Platform에서 만든 풍부한 실시간 프로필에 규칙과 제한을 적용하여 고객에게 적합한 오퍼를 적시에 보낼 수 있도록 하는 의사 결정 엔진을 통해 개인화를 쉽게 수행할 수 있습니다.

결정 관리 기능은 다음 두 가지 주요 구성 요소로 구성됩니다.

* 오퍼를 구성하는 여러 요소를 만들고 관리하고, 규칙과 제한을 정의하는 인터페이스인 중앙 오퍼 라이브러리.
* 오퍼 라이브러리와 함께 Adobe Experience Platform 데이터 및 실시간 고객 프로필을 활용하여 오퍼가 전달될 고객 및 채널을 선택할 수 있는 오퍼 결정 엔진입니다.

<img src="../assets/offers_overview.png" alt="의사 결정 관리" style="width:100%; border:1px solid #4a4a4a" />

의사 결정 관리는 에지 또는 허브를 통해 두 가지 방법 중 하나로 배포할 수 있습니다. 이러한 각 방법에는 아래에서 참조되는 각 청사진에 설명된 대로 서비스를 운영하기 위한 특정 인터페이스 및 프로토콜 세트가 있습니다. 자세한 내용은 결정 관리 설명서에서 확인할 수 있습니다 [여기](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery-api/decisioning-vs-edge-apis.html).

## 허브의 의사 결정 관리

첫 번째 방법은 중앙 데이터 센터 아키텍처인 Adobe Experience Platform 허브를 통해 배포하는 것입니다. [허브] 접근 방식에서는 오퍼를 실행, 개인화하여 500ms 이상의 지연 시간을 두고 게재합니다. 따라서 허브 아키텍처는 지연 시간이 초 미만 단위일 필요가 없는 고객 경험에 가장 적합합니다. 예를 들면 콜센터 또는 대면 상호 작용 등의 상담원 지원 경험이나 키오스크에서 제공하는 오퍼 의사 결정이 있습니다. 이메일, SMS 메시지 또는 푸시 알림 및 기타 아웃바운드 캠페인에 삽입되는 오퍼도 허브 접근 방식으로 제공됩니다. 허브의 의사 결정 관리에 대한 자세한 내용은 [허브의 의사 결정 관리](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-hub.html?lang=en) 블루프린트를 참조하세요.

* 오퍼 자격 은 모든 속성 및 경험 이벤트를 포함하여 전체 실시간 고객 프로필에 대해 작동할 수 있습니다

### 허브의 의사 결정 관리에 사용 사례

* 키오스크 및 매장 경험의 개인화 오퍼.
* 콜센터나 세일즈 상호 작용 등 상담원 지원 경험의 개인화 오퍼.
* 이메일, SMS 또는 기타 아웃바운드 상호 작용에 포함된 오퍼.
* 크로스 채널 여정 실행 - Adobe Journey Optimizer를 통한 웹, 모바일, 이메일, 기타 상호 작용 채널 간 오퍼 일관성.

### 허브 기술 고려 사항에 대한 의사 결정 관리

* 초당 요청 수 = 2000입니다.
* 응답 지연 시간이 500ms 미만입니다.
* 대상 멤버십, 특성 및 경험 이벤트를 포함한 전체 실시간 고객 프로필에 액세스합니다.

## 최상의 의사 결정 관리

두 번째 방법은 Experience Edge Network를 통한 것입니다. Experience Edge Network는 1초 미만, 밀리초 단위의 빠른 경험을 제공하기 위해 지리적 위치를 전 세계에 분산시킨 인프라입니다. 지연을 최소화하기 위하여 최종 소비자 경험은 소비자의 지리적 위치에서 가장 가까운 Edge 인프라에 의해 실행됩니다. Edge의 의사 결정 관리는 웹 또는 모바일 인바운드 개인화 요청과 같은 실시간 고객 경험을 제공하는 용도로 설계되었습니다. Edge의 의사 결정 관리에 대한 자세한 내용은 [Edge의 의사 결정 관리](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/decision-management-edge.html?lang=en) 블루프린트를 참조하세요.

### 에지에서 의사 결정 관리에 사용 사례

* 웹 또는 모바일 인바운드 경험을 통한 온라인 개인화.
* 크로스 채널 여정 실행 - Adobe Journey Optimizer를 통한 웹, 모바일, 이메일, 기타 상호 작용 채널 간 오퍼 일관성.

### 에지 기술 고려 사항에 대한 의사 결정 관리

* 초당 요청 수 = 5000입니다.
* 응답 지연 시간이 250ms 미만입니다.
* Edge 실시간 프로필에 대한 액세스. 에지 예상 대상 및 프로필 속성만 프로필에서 사용할 수 있습니다.
* 처음 경험에서 개인화가 필요한 경우 전체 프로필을 사용할 수 있으므로 허브가 이상적입니다. Edge 프로필은 처음 Edge 경험을 위해 허브에서 동기화되어야 합니다. 따라서 Edge의 첫 번째 경험에는 이전에 업로드된 프로필 데이터가 허브에 포함되지 않습니다.

## 관련 설명서

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=ko)
* [Adobe Journey Optimizer 의사 결정 관리](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [ Adobe Journey Optimizer 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe 결정 관리 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/offer-decisioning-app-service.html)