---
title: 지원 및 판매 시나리오를 위한 실시간 프로필 액세스
description: 직원이 관여하는 지원 및 영업의 맥락을 제공하는 [!UICONTROL Real-time Customer Profile] 확인 블루프린트입니다.
solution: Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
TQID: https://experienceleague.adobe.com/Ci9pUbGCLQ9uhlQ9l1na7A2NiI9CpCRMLrUSN6lSOnU
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: a075b2c1-7748-4328-b7f6-343aa314616a
  - id: b12f6872-9271-4369-85e5-86969a0b99a2
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: ba929a52-9339-4154-9487-317dc875a3c7
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
  - id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 95ba7aa681e67efb136adac15dc7894cb413a4f0
workflow-type: tm+mt
source-wordcount: 368
ht-degree: 54%

---

# 지원 및 판매 시나리오를 위한 실시간 프로필 액세스

>[!TIP]
>이 블루프린트는 Audience Building &amp; Activation에서 [사용 사례 패턴](/help/blueprints/use-case-patterns/audience-building-activation/real-time-profile-lookup.md)으로도 사용할 수 있습니다.

지원 및 판매 시나리오를 위한 실시간 프로필 액세스 블루프린트는 외부 애플리케이션이 Adobe Experience Platform의 [!UICONTROL 실시간 고객 프로필]에 액세스하는 방법을 보여 줍니다.

외부 애플리케이션에서는 API GET 요청을 통해 프로필에 액세스할 수 있습니다. 이렇게 하면 해당 프로필 내에 저장된 속성, 이벤트, 세그먼트 멤버십 및 모델 기반 특성을 해당 Adobe 외부 애플리케이션에서 사용할 수 있습니다.

이를 통해 고객의 콜센터 문의에 대해 풍부한 맥락을 표면화할 수 있습니다. 예를 들면 지원 담당자가 고객의 생애 가치, 이탈 경향 또는 어떤 마케팅 캠페인에 노출되었는지 등을 확인할 수 있습니다. 영업 담당자도 고객에 대해 맥락 또는 인사이트를 얻어 활용할 수 있습니다.

>[!NOTE]
>
>허브에서의 프로필 조회는 웹/모바일 인바운드 개인화와 같이 높은 처리량, 짧은 지연 사용 사례를 위한 것이 아닙니다. 허브에 대한 프로필 조회는 에이전트 지원 지원 또는 판매 상호 작용과 같은 지연 시간이 짧은 시나리오를 위한 것입니다. 웹/모바일 개인화 또는 실시간 오퍼 의사 결정과 같이 지연 시간이 짧고 처리량이 많은 시나리오의 경우 Edge 프로필을 활용해야 합니다. Edge 프로필을 사용하면 Real-time Customer Data Platform의 [사용자 지정 Personalization 연결](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/personalization/custom-personalization)을 통해 실시간으로 액세스할 수 있습니다.

## 사용 사례

* 지원 및 영업 경험 등 직원이 관여하는 상호 작용에 대해 보다 자세한 고객의 맥락을 제공합니다. Experience Platform에서 프로필 확인 기능을 사용하면 담당자가 소비자에 대해 실시간 고객 프로필에 저장된 최근 구매, 캠페인 상호 작용, 성향, 대상자 멤버십 및 기타 속성과 인사이트 등 더 많은 맥락을 확인할 수 있습니다.

## 아키텍처

<img src="assets/customer_activity_hub.svg" alt="고객 활동 허브 블루프린트를 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## 가드레일

* [[!UICONTROL 실시간 고객 프로필] 데이터의 보호 기능](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)

## 관련 설명서

* [Adobe Experience Platform Activation 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL 실시간 고객 프로필] 설명서](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ko)
* [프로필 보호](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [프로필 조회 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
