---
title: Experience Cloud 애플리케이션을 사용한 대상자 및 프로필 활성화 블루프린트
description: Experience Platform의 프로필 및 대상자를 관리하고 Experience Cloud 애플리케이션에 공유합니다.
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services
kt: 7722
exl-id: f36014e8-170d-47e1-b4ec-10c0ea70612d
source-git-commit: 16ca42fdb944e658bfc1fb3e960e81cd67be049c
workflow-type: ht
source-wordcount: '896'
ht-degree: 100%

---

# Experience Cloud 애플리케이션을 사용한 대상자 및 프로필 활성화 블루프린트

Experience Platform의 프로필 및 대상자를 관리하고 Experience Cloud 애플리케이션에 공유합니다. Experience Platform에서 풍부한 고객 세그먼트와 인사이트를 작성 및 공유하고 이를 Experience Cloud 애플리케이션에 공유합니다.

Experience Cloud 애플리케이션에서의 활성화는 [알려진 고객 활성화 블루프린트](known.md)의 내용과 유사합니다.

## 사용 사례

* Experience Cloud를 기반으로 하는 고객 상호 작용 채널 전체에 걸친 개인화 및 타겟팅을 수행합니다.
* Experience Platform과 Experience Cloud 애플리케이션 간에 대상자 및 프로필 데이터를 공유합니다.
* 온라인 행동 데이터 및 데이터 과학 모델을 포함한 다중 채널 데이터에서 풍부한 인사이트를 끌어내어 Experience Platform의 실시간 고객 프로필을 보강한 다음 이를 Experience Cloud 애플리케이션에 공유할 수 있습니다.

## 애플리케이션

* Adobe Experience Platform    
* [!UICONTROL Real-time Customer Data Platform]
* Experience Platform Activation
* Experience Cloud 애플리케이션
   * Adobe Audience Manager
   * Adobe Target
   * Adobe Campaign
   * Journey Optimizer
   * Marketo Engage
   * Adobe Commerce
   * Customer Journey Analytics

## 아키텍처

Experience Platform과 Experience Cloud 애플리케이션 통합과 관련된 아키텍처 다이어그램을 더 확인하려면 [Experience Platform과 애플리케이션 아키텍처 섹션](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=ko)을 참조하세요.

### Experience Cloud 애플리케이션을 사용한 대상자 및 프로필 활성화

<img src="../experience-platform/assets/aep+apps.svg" alt="Experience Cloud 애플리케이션을 사용한 대상자 및 프로필 활성화의 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />
<br>

## 가드레일

[대상자 및 프로필 활성화 개요 페이지의 가드레일](overview.md)을 참조하세요.    또한 [배포 가드레일](../experience-platform/deployment/guardrails.md) 페이지도 참조하실 수 있습니다.

## 구현 시 고려 사항

* 대상에 프로필 데이터를 공유하려면 대상 페이로드에 대상이 사용하는 특정 ID 값을 포함해야 합니다. 목표 대상에 필요한 ID는 모두 Platform으로 수집하여 [!UICONTROL Real-time Customer Profile] ID로 구성해야 합니다.

### Real-time Customer Data Platform에서 Audience Manager로 대상 공유하기

* 자세한 내용은 다음 설명서를 참조하세요. [Experience Platform 세그먼트를 Audience Manager 및 기타 Experience Cloud 솔루션에 공유하기](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ko).

* 세그먼트 평가가 일괄 처리인지 스트리밍인지에 관계없이 세그먼트 평가가 완료되고 실시간 고객 프로필에 작성되는 즉시 RT-CDP의 대상 멤버십이 스트리밍 방식으로 Audience Manager에 공유됩니다.
* 자격이 있는 프로필에 관련 프로필 장치에 대한 지역 라우팅 정보가 포함되어 있는 경우 RTCDP의 대상 멤버십이 연결된 Audience Manager Edge에서 스트리밍 방식으로 검증됩니다. 타임스탬프 기준 최근 14일 내 프로필에 지역 라우팅 정보가 적용된 경우 Audience Manager Edge에서 스트리밍 방식으로 평가합니다. RTCDP의 프로필에 지역 라우팅 정보가 없거나 지역 라우팅 정보가 14일보다 전에 적용된 경우, 해당 RTCDP 대상자 멤버십을 Audience Manager 허브 위치로 다시 보내어 배치 기반 평가 및 활성화 처리를 합니다.
* 지역 라우팅 정보가 있으면 이 프로필은 Edge 활성화를 사용할 수 있으며 RTCDP에서 몇 분 내로 세그먼트 인증 후 활성화됩니다. Edge 활성화를 사용할 수 없는 프로필은 Audience Manager 허브를 통해 자격을 얻어야 하며, 여기에는 12~24시간 정도의 처리 시간이 걸릴 수 있습니다.
* 어느 Edge에 Audience Manager 프로필을 저장할지에 대한 지역 라우팅 정보는 Audience Manager, 방문자 ID 서비스, Analytics, Launch에서, 또는 Web SDK에서 직접 Experience Platform에 [데이터 캡처 지역 정보] XDM 필드 그룹을 사용하여 별도의 프로필 기록 클래스 데이터 세트로 수집할 수 있습니다. 자세한 내용은 [링크](https://experienceleague.adobe.com/docs/id-service/using/reference/regions.html?lang=ko)의 지역 정보 가져오기 문서를 참조하세요.
* Experience Platform에서 Audience Manager로 대상자를 공유하는 활성화 시나리오의 경우 자동으로 공유되는 ID에는 ECID, IDFA, GAID, 해시 이메일 주소(EMAIL_LC_SHA256), AdCloud ID가 있습니다. 현재 사용자 지정 네임스페이스는 공유되지 않습니다.
* Experience Platform의 대상자는 필요한 대상 ID가 [!UICONTROL Real-time Customer Profile]에 포함된 경우 또는 [!UICONTROL Real-time Customer Profile]의 ID가 Audience Manager에서 필요 대상 ID와 연결된 경우에 Audience Manager 대상을 통해 공유할 수 있습니다.

### Real-time Customer Data Platform에서 Target으로 대상 공유하기

* [알려진 고객 개인화 - Target 및 RTCDP 블루프린트](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/web-personalization/known-personalization.html?lang=ko)에서 Real-time Customer Data Platform의 프로필 및 대상자를 Target으로 공유하는 방법에 대한 자세한 내용을 확인할 수 있습니다.

### Real-time Customer Data Platform에서 Campaign 및 Journey Optimizer으로 대상 공유

* [고객 여정 블루프린트](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=ko)에서 프로필 및 대상자를 Real-time Customer Data Platform에서 Campaign 및 Journey Optimizer으로 공유하는 방법에 대해 자세히 살펴볼 수 있습니다.

### Real-time Customer Data Platform에서 Marketo Engage로 대상자 공유하기

* Real-time Customer Data Platform에서 Marketo Engage로 프로필 및 대상자를 공유하는 자세한 방법은 [B2B 활성화 블루프린트](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=ko)를 참조하세요.

### Real-time Customer Data Platform에서 Customer Journey Analytics로 대상자 공유하기

* Real-time Customer Data Platform 대상자를 Customer Journey Analytics로 공유하는 자세한 방법은 [RTCDP 대상자를 Customer Journey Analytics에 공유하기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/ingest-aep-segments.html?lang=ko)를 참조하세요.

## 관련 설명서

* [[!UICONTROL Real-time Customer Data Platform] 제품 설명 ](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html)
* [프로필 및 세분화 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)
* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ko)

## 관련 비디오 및 튜토리얼

* [[!UICONTROL Real-time Customer Data Platform] 개요 ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ko)
* [[!UICONTROL Real-time Customer Data Platform] 데모](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ko)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)
