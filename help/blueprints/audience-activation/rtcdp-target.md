---
title: Target을 사용하는 알려진 고객 Personalization
description: RTCDP 프로필과 대상자를 Adobe Target과 통합합니다.
landing-page-description: RTCDP 프로필과 대상자를 Adobe Target과 통합합니다.
short-description: RTCDP 프로필과 대상자를 Adobe Target과 통합합니다.
solution: Real-Time Customer Data Platform, Target, Experience Platform
kt: 7194
thumbnail: thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
TQID: https://experienceleague.adobe.com/1ti2SqfAFOgnKbaJ70xwGI-xHDE1WXJ7-oTStcJJy1E
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: ba929a52-9339-4154-9487-317dc875a3c7
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
  - id: ee602049-8a18-43df-9299-a689a025a371
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 213e2d7d73d91fa7b487289dfe62685bc32d5029
workflow-type: tm+mt
source-wordcount: 735
ht-degree: 37%

---

# Target을 사용하는 알려진 고객 Personalization

>[!TIP]
>이 블루프린트는 Personalization에서 [사용 사례 패턴](/help/blueprints/use-case-patterns/personalization/audience-sharing-with-target.md)(으)로도 사용할 수 있습니다.

## 사용 사례

* 알려진 고객 데이터를 사용한 온라인 개인화
* 랜딩 페이지 최적화
* 이전 제품/콘텐츠 조회, 제품/콘텐츠 관련성, 환경 요인 및 인적 속성과 더불어 거래, 충성도 및 CRM 데이터 등 오프라인 인사이트와 모델에서 도출한 인사이트를 기반으로 한 개인화.
* Adobe Target을 사용하여 웹 사이트 및 모바일 앱에서 실시간 고객 데이터 플랫폼에 정의된 대상을 공유하고 타깃팅할 수 있습니다

## 애플리케이션

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target

### 참조 설명서

* [실시간 고객 데이터 플랫폼을 위한 Adobe Target 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html)
* [Edge 데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=ko)

## 통합 패턴

| 통합 패턴 | 기능 | 필요 조건 |
|--------------------|------------|---------------|
| **실시간 고객 데이터 플랫폼에서 Target으로 공유되는 Edge에 대한 실시간 세그먼트 평가** | - Edge에서 동일한 페이지 또는 다음 페이지 개인화에 대해 실시간으로 대상자를 평가합니다. <br>- 스트리밍 또는 일괄 처리 방식으로 평가된 모든 세그먼트는 에지 세그먼트 평가 및 개인화에 포함되도록 Edge Network에도 투영됩니다. | - 웹/모바일 SDK을 구현하거나 Edge Network Server API를 구현해야 합니다. <br>- Target 및 Experience Platform 확장이 활성화된 Experience Edge에서 데이터 스트림을 구성해야 합니다. <br>- Target 대상은 Real-time Customer Data Platform 대상에 구성해야 합니다. <br>- Target과 통합하려면 Experience Platform 인스턴스와 동일한 IMS 조직이어야 합니다. |
| **Edge 접근 방식을 통해 Real-time Customer Data Platform에서 Target으로 스트리밍 및 일괄 대상자 공유** | - Edge 네트워크를 통해 Real-time Customer Data Platform에서 Target으로 스트리밍 및 배치 대상자를 공유합니다. <br>- 실시간으로 평가되는 대상에는 웹 SDK 및 Edge Network 구현이 필요합니다. | - Target의 웹/모바일 SDK 또는 Edge API 구현은 Target에 스트리밍 및 일괄 RTCDP 대상을 공유하는 데 필요하지 않지만 실시간 에지 세그먼트 평가를 활성화하는 데 필요합니다. <br>- AT.js를 사용하는 경우 ECID ID 네임스페이스에 대한 프로필 통합만 지원합니다. <br>- Edge에서 사용자 지정 ID 네임스페이스 조회를 수행하려면 웹 SDK/Edge API를 배포해야 하며 각 ID는 ID 맵에서 ID로 설정해야 합니다. <br>- Target 대상은 Real-time Customer Data Platform 대상에 구성해야 합니다. RTCDP의 기본 프로덕션 샌드박스만 지원됩니다. <br>- Target과 통합하려면 Experience Platform 인스턴스와 동일한 IMS 조직이어야 합니다. |
| **대상 공유 서비스 접근 방식을 통해 Real-time Customer Data Platform에서 Target 및 Audience Manager으로 대상 공유 스트리밍 및 일괄 처리** | - 이 통합 패턴은 Audience Manager의 서드파티 데이터 및 대상의 추가 보강이 필요한 경우 활용할 수 있습니다. | - 웹/모바일 SDK은 Target에 스트리밍 및 배치 대상을 공유하는 데 필요하지 않지만 실시간 에지 세그먼트 평가를 활성화하는 데 필요합니다. <br>- AT.js를 사용하는 경우 ECID ID 네임스페이스에 대한 프로필 통합만 지원합니다. <br>- Edge에서 사용자 지정 ID 네임스페이스 조회를 수행하려면 웹 SDK/Edge API를 배포해야 하며 각 ID는 ID 맵에서 ID로 설정해야 합니다. <br>- 대상 공유 서비스를 통한 대상 프로젝션을 구축해야 합니다. <br>- Target과 통합하려면 Experience Platform 인스턴스와 동일한 IMS 조직이어야 합니다. <br>- 기본 프로덕션 샌드박스의 대상자만 핵심 서비스를 공유하는 대상을 지원합니다. |

## Adobe Target으로 실시간, 스트리밍, 배치 대상자 공유하기

아키텍처

![온라인/오프라인 웹 Personalization 블루프린트에 대한 참조 아키텍처](assets/RTCDP+Target.png)

시퀀스 세부 사항

![온라인/오프라인 웹 Personalization 블루프린트에 대한 참조 아키텍처](assets/RTCDP+Target_flow.png)

아키텍처 개요

![온라인/오프라인 웹 Personalization 블루프린트에 대한 참조 아키텍처](assets/personalization_with_apps.png)

## 관련 설명서

### SDK 설명서

* [Experience Platform 웹 SDK 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
* [Experience Cloud ID 서비스 설명서](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ko)

### 세분화 설명서

* [Experience Platform 세그멘테이션 개요](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ko)
* [실시간 세분화](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html?lang=ko)
* [스트리밍 세분화](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)
* [Adobe Audience Manager을 통한 Adobe Analytics 세그먼트 공유](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ko)
* [병합 정책 구성](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/ui-guide.html?lang=ko#create-a-merge-policy)

### 튜토리얼

* [Real-Time CDP 및 Adobe Target을 사용한 다음 히트 개인화](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=ko)
