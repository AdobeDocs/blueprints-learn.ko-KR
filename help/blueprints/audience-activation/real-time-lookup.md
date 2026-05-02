---
title: 웹 및 모바일 Personalization용 실시간 Edge 프로필 액세스
description: '[!UICONTROL 실시간 고객 프로필] 실시간 웹 및 모바일 개인화에 대한 컨텍스트를 제공하기 위해 가장자리에서 액세스합니다.'
solution: Real-Time Customer Data Platform, Data Collection
kt: 719
exl-id: 61b81d00-c4bd-41b2-8161-683814947b56
TQID: https://experienceleague.adobe.com/H59c3UBbNCQFs3H0VL5iVDKKZ5D3CFt4ri2RVwNlq7s
product_v2:
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: ba929a52-9339-4154-9487-317dc875a3c7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 631
ht-degree: 8%

---

# 웹 및 모바일 Personalization용 실시간 Edge 프로필 액세스

>[!TIP]
>이 블루프린트는 Personalization에서 [사용 사례 패턴](/help/blueprints/use-case-patterns/personalization/edge-profile-access.md)(으)로도 사용할 수 있습니다.

웹 및 모바일 Edge에 대한 실시간 Personalization 프로필 액세스 블루프린트는 웹 및 모바일 애플리케이션이 가장자리에 있는 Adobe Experience Platform의 [!UICONTROL 실시간 고객 프로필]에 액세스하여 처리량이 높고 대기 시간이 짧은 개인화를 수행하는 방법을 보여 줍니다.

애플리케이션은 밀리초 단위의 지연 시간으로 에지(edge)의 실시간 프로필 속성 및 대상자에 액세스할 수 있습니다. 프로필에 속성으로 저장된 속성, 대상자 멤버십 및 모델 기반 기능은 웹 및 모바일 채널에서 동일한 페이지 및 다음 페이지 개인화를 위해 실시간으로 액세스할 수 있습니다.

이 기능을 사용하면 실시간 행동, 실시간 고객 프로필에 수집된 속성 및 계산된 통찰력을 포함하여 실시간 고객 프로필을 기반으로 웹 사이트 및 모바일 애플리케이션에서 고도로 개인화된 경험을 제공할 수 있습니다.

>[!NOTE]
>
>Edge 프로필 액세스는 웹/모바일 인바운드 개인화 및 실시간 오퍼 의사 결정과 같이 높은 처리량, 짧은 지연 시간 사용 사례를 위해 특별히 설계되었습니다. 에이전트 지원 지원 또는 판매 상호 작용과 같은 낮은 처리량 시나리오의 경우 Hub 프로필 조회 API가 더 적절합니다. 허브 기반 프로필 액세스는 [지원 및 판매 시나리오에 대한 실시간 프로필 액세스 블루프린트](customer-activity.md)를 참조하십시오.

## 애플리케이션

* Real-time Customer Data Platform
* Adobe Experience Platform 데이터 수집 (웹 SDK / 모바일 SDK)
* Edge Network 서버 API

## 사용 사례

* 알려진 고객 경험을 위한 웹 및 모바일 채널에서의 실시간 개인화
* 실시간 프로필 속성 및 대상자를 기반으로 하는 동일 페이지 및 다음 페이지 개인화
* 실시간 행동 데이터, 속성 및 계산된 통찰력을 포함한 고객 프로필을 기반으로 하는 콘텐츠 및 오퍼 개인화
* 실시간 의사 결정을 위한 개인화 엔진, 콘텐츠 관리 시스템 및 외부 애플리케이션과 통합
* 실시간 프로필 컨텍스트를 통한 테스트 및 콘텐츠 최적화

## 아키텍처 다이어그램

<img src="assets/real-time-edge-lookup.svg" alt="웹 및 모바일 Personalization용 Edge 프로필 액세스에 대한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## 가드레일

* [[!UICONTROL 실시간 고객 프로필] 데이터의 보호 기능](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [Edge Network 가드 레일](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* Edge 프로필에는 14일 TTL(time-to-live)이 있습니다. 사용자가 14일 동안 에지에서 활성화되지 않은 경우 에지 프로필이 만료되어 허브에서 가져와야 하며, 이는 첫 페이지 개인화에 영향을 줄 수 있습니다.
* Edge 개인화는 에지 세분화 기준을 충족하는 대상에 대해 실시간 대상 멤버십 평가를 지원합니다. 적절한 구성으로 허브에서 대상자 일괄 처리 및 스트리밍을 에지에서 사용할 수도 있습니다.

## 관련 설명서

### 대상 구성

* [사용자 지정 Personalization 연결](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/custom-personalization) - 기본 구현 안내서
* [Personalization 대상 개요](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/overview)
* [Edge 개인화 대상에 대한 대상자 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations)
* [에지에서 실시간으로 프로필 속성 조회](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-profile-lookup)

### SDK 설명서

* [Experience Platform 웹 SDK 설명서](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/home.html)
* [Experience Platform Mobile SDK 설명서](https://developer.adobe.com/client-sdks/home/)
* [Edge Network Server API 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ko)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
* [웹 SDK의 명령 응답](https://experienceleague.adobe.com/docs/experience-platform/web-sdk/commands/command-responses.html)

### 프로필 및 세그멘테이션 설명서

* [[!UICONTROL 실시간 고객 프로필] 설명서](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html)
* [프로필 보호](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)

### 튜토리얼

* [Real-Time CDP 및 Adobe Target을 사용한 다음 히트 개인화](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* [데이터 스트림 구성](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html)
