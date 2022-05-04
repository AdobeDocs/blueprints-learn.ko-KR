---
title: 에지 offer decisioning
description: 실시간 웹 및 모바일 경험을 포함하여 다양한 채널의 소비자에게 개인화된 오퍼를 제공합니다.
solution: Experience Platform, Journey Optimizer
exl-id: 31e5f624-5578-49e1-ab92-5cabd596a632
source-git-commit: bedfce6f9ded6c168656e8c37c59f85f250481a1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Journey Optimizer - Offer decisioning

Adobe 결정 관리는 Adobe Journey Optimizer의 일부로 제공되는 서비스입니다. 이 블루프린트는 애플리케이션의 사용 사례 및 기술 기능을 간략하게 설명하고 Offer decisioning을 구성하는 다양한 아키텍처 구성 요소 및 고려 사항을 자세히 설명합니다.

의사 결정 관리를 두 가지 방법 중 하나로 배포할 수 있습니다. 첫 번째 단계는 단일 데이터 센터 아키텍처인 Adobe Experience Platform 허브를 통해 입니다. &quot;hub&quot; 접근 방식에서는 두 번째 지연 시 오퍼가 실행, 개인화 및 전달됩니다. 따라서 허브 아키텍처는 초 미만의 지연을 요구하지 않는 고객 경험에 가장 적합합니다. 예를 들면 콜센터 또는 개인 상호 작용과 같은 키오스크 또는 에이전트 지원 경험에 대해 제공되는 오퍼 결정 등이 있습니다.

두 번째 방법은 Experience Edge Network를 통한 것입니다. Experience Edge Network는 빠른 초 및 밀리초 경험을 제공하기 위해 지리적으로 분산된 인프라입니다. 최종 소비자 경험은 지연을 최소화하기 위해 지리적 위치에 가장 가까운 에지 인프라에 의해 실행됩니다. Edge의 의사 결정 관리는 실시간 고객 경험을 제공하도록 설계되었습니다. 여기에는 웹 또는 모바일 인바운드 개인화 요청과 같은 경험이 포함됩니다.

이 블루프린트는 Edge에서 의사 결정 관리의 세부 사항을 다룹니다.

허브에서 의사 결정 관리에 대한 자세한 내용은 [허브의 의사 결정 관리](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer/offer-decisioning/offers-hub.html?lang=en) 블루프린트.

의사 결정 관리에 대한 자세한 내용은 제품 설명서를 참조하십시오 [여기](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)

## 사용 사례

* 웹 또는 모바일을 통한 온라인 개인화.
* 인바운드 offer decisioning 및 오퍼 포지션.
* 크로스 채널 여정 실행 - Adobe Journey Optimizer을 통해 웹, 모바일, 이메일 및 기타 상호 작용 채널 간에 일관성을 제공합니다.

<br>

## 아키텍처

<img src="../assets/offers_edge.svg" alt="Edge 블루프린트에서 참조 아키텍처 Offer decisioning" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 통합 패턴

| 통합 | 설명 |
| :-- | :--- |
| [Adobe Target으로 offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | offer decisioning은 Adobe Target과 통합될 수 있으므로 오퍼를 Target 경험으로 테스트 및 전달할 수 있습니다. |

## 필요 조건

Adobe Experience Platform

* Journey Optimizer 데이터 소스를 구성하려면 먼저 시스템에서 스키마와 데이터 세트를 구성해야 합니다.
* [경험 이벤트] 클래스 기반 스키마의 경우 규칙 기반 이벤트가 아닌 이벤트를 트리거하려면 [Orchestration eventID 필드 그룹]을 추가해야 합니다.
* [개별 프로필] 클래스 기반 스키마의 경우 Journey Optimizer에서 사용할 테스트 프로필을 로드할 수 있도록 하려면 [프로필 테스트 세부 정보] 필드 그룹을 추가해야 합니다.

<br>

## 가드레일

* Journey Optimizer 보호 기능의 경우 다음을 참조하십시오 [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/limitations.html).
* offer decisioning 보호 기능은 다음을 참조하십시오 [offer decisioning 제품 설명](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html).

### 데이터 수집 가드 레일

<img src="../assets/aep-data-ingestion-details-latency.svg" alt="Journey Optimizer 블루프린트 참조 아키텍처" style="width:80%; border:1px solid #4a4a4a" />

<br>

### 활성화 가드레일

<img src="../assets/ajo-activation-details-latency.svg" alt="Journey Optimizer 블루프린트 참조 아키텍처" style="width:80%; border:1px solid #4a4a4a" />

<br>

## 구현 패턴

* 웹 사이트 및 모바일 애플리케이션에서 배포하기 위해 Web 또는 Mobile SDK를 사용하여 SDK가 배포된 Offer decisioning을 구현합니다.
   * [웹/모바일 SDK 블루프린트](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/data-ingestion/websdk.html?lang=ko)
   * [WebSDK](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/offer-decisioning/offer-decisioning-overview.html)
   * [MobileSDK](https://aep-sdks.gitbook.io/docs/)

또는

* API 서버 간 서버 기반 구현의 경우 서버 간 직접 Offer decisioning 구현을 위해 Edge Network Service API를 사용하십시오.
   * [Edge Network Server API](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/api-reference/offer-delivery/deliver-offers.html)

<br>

## 구현 단계

### Adobe Experience Platform

#### 스키마/데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. Experience Platform에서 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 거버넌스를 위해 Experience Platform에서 데이터 세트에 [데이터 사용 레이블을 추가](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ko)합니다.
1. 대상 관리 [정책을 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ko)

#### 프로필/ID

1. [고객용 네임스페이스를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [스키마에 ID를 추가합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. [!UICONTROL Real-time Customer Profile]의 서로 다른 보기에 대한 [병합 규칙](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko)을 만듭니다(선택 사항).
1. Journey에서 사용할 세그먼트를 만듭니다.

#### 소스/대상

1. 스트리밍 API 및 소스 커넥터를 사용하여 [Experience Platform으로 데이터를 수집해 옵니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)

## 관련 설명서

* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html)
* [Adobe Journey Optimizer 의사 결정 관리](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html)
* [Adobe Journey Optimizer 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
* [Adobe Offer decisioning 제품 설명](https://helpx.adobe.com/legal/product-descriptions/offer-decisioning-app-service.html)
