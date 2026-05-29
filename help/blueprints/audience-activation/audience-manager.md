---
title: 장치 기반 - Audience Manager을 사용한 익명 대상 타깃팅
description: 고객의 익명 행동 데이터를 기반으로 여러 웹과 광고 채널에 걸쳐 대상자를 타겟팅하는 방법을 알아봅니다. 이를 통해 전 디바이스에 걸쳐 개인화되고 일관적인 실시간 고객 경험을 제공할 수 있습니다.
landing-page-description: 고객의 익명 행동 데이터를 기반으로 여러 웹과 광고 채널에 걸쳐 대상자를 타겟팅하는 방법을 알아봅니다.
short-description: 고객의 익명 행동 데이터를 기반으로 여러 웹과 광고 채널에 걸쳐 대상자를 타겟팅하는 방법을 알아봅니다.
solution: Audience Manager
kt: 7211
thumbnail: null
exl-id: f17599f1-2e75-4cbe-841a-9fd1dae71ada
TQID: https://experienceleague.adobe.com/weUxfDND0nBp0iQbCU5gYydUBcKn-Zk2unQ05Ett44k
product_v2:
  - id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
feature_v2:
  - id: a8b0238e-1d43-4679-a3b4-5ba1bad83baa
  - id: baaa0dd2-d27e-4921-aae3-7888623a5fa5
  - id: c814092e-2730-45e8-a12d-e084529f52cb
subfeature_v2:
  - id: e8a4c7eb-7254-4984-ac46-e651a57c7e39
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 213e2d7d73d91fa7b487289dfe62685bc32d5029
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 86%

---

# 장치 기반 - Audience Manager을 사용한 익명 대상 타깃팅

>[!TIP]
>이 블루프린트는 Personalization에서 [사용 사례 패턴](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md)(으)로도 사용할 수 있습니다.

익명 대상자 활성화는 익명의 디바이스 및 행동 데이터를 기반으로 웹, 모바일, 광고 채널 전반에 걸쳐 대상자를 타겟팅하고 대상자에 맞추어 개인화하는 기능입니다.

## 사용 사례

* 웹 사이트, 모바일 앱 또는 지원되는 광고 채널에서 익명의 디지털 대상자에 대한 타겟팅 및 개인화를 수행합니다.
* 알려진 디바이스 및 행동 특성을 기반으로 랜딩 페이지 및 사전 인증 경험을 최적화합니다.
* Audience Manager 서드파티 데이터 네트워크를 활용하여 타겟팅을 위해 대상자를 개선 및 확장합니다.


## 애플리케이션

* Audience Manager
* Real-time Customer Data Platform

온사이트 및 광고 대상에 대한 익명 대상자 활성화에는 Audience Manager와 Real-time Customer Data Platform 모두 활용할 수 있습니다. 단, Real-time Customer Data Platform의 경우 광고 대상 중 [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/overview.html?lang=ko)에서 설명하는 익명 디바이스 식별자가 있는 일부만 지원합니다.

## 아키텍처

![익명 Audience Activation 블루프린트에 대한 참조 아키텍처](assets/anonymous_activation.png)

<br>

## Audience Manager 구현 단계

* Audience Manager 구현에 대한 자세한 내용은 다음 [설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ko)를 참조하세요.