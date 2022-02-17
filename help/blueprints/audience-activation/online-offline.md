---
title: 온라인 및 오프라인 데이터 블루프린트를 사용한 활성화
description: 온라인/오프라인 대상자 활성화.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
source-git-commit: 53ef83cbaa9dde0793e379c0044f449cfca078ab
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 온라인 및 오프라인 데이터 블루프린트를 사용한 활성화

오프라인 주문, 거래, CRM 또는 충성도 데이터 등 오프라인 특성 및 이벤트와 온라인 행동을 함께 사용하여 온라인 타겟팅과 개인화를 수행합니다.

대상자를 이메일 공급자, 소셜 네트워크 및 광고 대상 등 알려진 프로필 기반 대상으로 활성화합니다.

[Experience Cloud 애플리케이션을 사용한 대상자 및 프로필 활성화 블루프린트](platform-and-applications.md)에서 Experience Platform와 Experience Cloud 애플리케이션 간 통합에 대하여 더 자세하게 설명합니다.

## 사용 사례

* 소셜 및 광고 대상의 알려진 대상자 타겟팅
* 온라인 및 오프라인 특성을 활용한 온라인 개인화
* 대상자를 이메일 및 SMS 등 알려진 채널로 활성화합니다.

## 애플리케이션

* Adobe Experience Platform     
* [!UICONTROL Real-time Customer Data Platform]

## 아키텍처

### 대상을 사용한 온라인 및 오프라인 데이터로 활성화

<img src="assets/online_offline_activation.svg" alt="온라인/오프라인 대상자 활성화 블루프린트를 위한 참조 아키텍처" style="width:80%; border:1px solid #4a4a4a" />
<br>

## 가드레일

[대상자 및 프로필 활성화 개요 페이지의 가드레일 설명을 참조하세요.](overview.md)

## 구현 단계

1. 수집할 데이터를 위한 [스키마를 만듭니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 수집한 데이터를 통합 프로필로 결합할 수 있도록 스키마에 [올바른 ID와 ID 네임스페이스를 구성합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. 데이터를 Experience Platform으로 [수집합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)
1. [Experience Platform에서 정의한 대상자를 Audience Manager로 공유할 수 있도록 Experience Platform과 Audience Manager 간 [!UICONTROL Real-time Customer Data Platform] 세그먼트 공유를 제공합니다.](https://www.adobe.com/go/audiences)
1. Experience Platform에서 [세그먼트를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko). 세그먼트를 일괄 처리로 평가할지 스트리밍으로 평가할지는 시스템에서 자동으로 결정합니다.
1. 프로필 특성과 대상자 멤버십을 공유할 대상을 원하는 대상으로 [구성합니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=ko)

## 구현 시 고려 사항

* 대상에 프로필 데이터를 공유하려면 대상 페이로드에 대상이 사용하는 특정 ID 값을 포함해야 합니다. 목표 대상에 필요한 ID는 모두 Platform으로 수집하여 [!UICONTROL Real-time Customer Profile] ID로 구성해야 합니다.

### Real-time Customer Data Platform에서 Audience Manager로 대상 공유하기

* 세그먼트 평가가 일괄 처리인지 스트리밍인지에 관계없이 세그먼트 평가가 완료되고 실시간 고객 프로필에 작성되는 즉시 RT-CDP의 대상 멤버십이 스트리밍 방식으로 Audience Manager에 공유됩니다. 자격이 있는 프로필에 관련 프로필 장치에 대한 지역 라우팅 정보가 포함되어 있는 경우 RTCDP의 대상 멤버십이 연결된 Audience Manager Edge에서 스트리밍 방식으로 검증됩니다. 지난 14일 동안 타임스탬프가 있는 프로필에 지역 라우팅 정보가 적용된 경우 스트리밍의 Audience Manager 에지에서 평가됩니다. RTCDP의 프로필에 지역 라우팅 정보가 포함되어 있지 않거나 지역 라우팅 정보가 14일 이상 오래된 경우 프로필 멤버십이 배치 기반 평가 및 활성화를 위해 Audience Manager 허브 위치로 전송됩니다. Edge 활성화를 사용할 수 있는 프로필은 RTCDP에서 세그먼트 자격 몇 분 내에 활성화되고 Edge 활성화를 사용할 수 없는 프로필은 Audience Manager 허브에서 자격을 얻으며 12~24시간 처리 시간이 있을 수 있습니다.

* Audience Manager 프로필이 저장되는 Edge에 대한 지역 라우팅 정보는 Audience Manager, 방문자 ID 서비스, Analytics, Launch 또는 웹 SDK에서 직접 Experience Platform에 수집하여 &quot;데이터 캡처 영역 정보&quot; XDM 필드 그룹을 사용하여 별도의 프로필 레코드 클래스 데이터 세트로 사용할 수 있습니다.

* Experience Platform에서 Audience Manager으로 대상을 공유하는 활성화 시나리오의 경우 다음 ID가 자동으로 공유됩니다: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. 현재 사용자 지정 네임스페이스는 공유되지 않습니다.

Experience Platform의 대상자는 필요한 대상 ID가 [!UICONTROL Real-time Customer Profile]에 포함된 경우 또는 [!UICONTROL Real-time Customer Profile]의 ID가 Audience Manager에서 필요 대상 ID와 연결된 경우에 Audience Manager 대상을 통해 공유할 수 있습니다.

## 관련 설명서

* [[!UICONTROL Real-time Customer Data Platform] 제품 설명 ](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html)
* [프로필 및 세분화 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)
* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ko)

## 관련 비디오 및 튜토리얼

* [[!UICONTROL Real-time Customer Data Platform] 개요 ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ko)
* [[!UICONTROL Real-time Customer Data Platform] 데모](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ko)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
