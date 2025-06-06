---
title: ' [!DNL Campaign] v7 및 Campaign Standard 통합 패턴이 포함된 Real-Time CDP'
description: Adobe Experience Platform 및 실시간 고객 프로필과 중앙 집중식 세분화 도구를 Adobe [!DNL Campaign] 과(와) 함께 사용하여 개인 맞춤화된 대화를 제공하는 방법을 소개합니다.
solution: Real-Time Customer Data Platform, [!DNL Campaign]
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 258aea64f6ff2f620b1adaa0c9ba4b02b47acce9
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 42%

---

# [!DNL Campaign] 통합 패턴을 사용하는 [!DNL Real-Time Customer Data Platform]

[!DNL Experience Platform] Adobe과 실시간 고객 프로필 및 중앙 집중식 세분화 도구를 [!DNL Campaign] Adobe과 함께 사용하여 개인 맞춤화된 대화를 제공하는 방법을 소개합니다.

## 애플리케이션

* Adobe [!DNL Experience Platform Real-Time Customer Data Platform]
* Adobe [!DNL Campaign] v7 또는 [!DNL Campaign Standard]

## 아키텍처

<img src="assets/rtcdp-campaign-architecture.svg" alt="일괄 처리 메시지와 Adobe Experience Platform 통합 패턴의 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 필요 조건

* Experience Platform 및 [!DNL Campaign]은(는) 동일한 IMS 조직에서 프로비저닝하고 사용자 액세스에 Adobe Admin Console을 사용하는 것이 좋습니다. 이렇게 하면 고객이 마케팅 UI 내에서 솔루션 전환기를 활용할 수 있습니다.

## 가드레일

다음 섹션에서는 이 통합의 보호 기능에 대해 설명합니다.

### Adobe [!DNL Campaign]

* Adobe [!DNL Campaign] 단일 조직 단위 배포만 지원합니다.
* Adobe [!DNL Campaign]은(는) 모든 활성 프로필에 대한 신뢰할 수 있는 소스입니다. 즉, 프로필이 Adobe [!DNL Campaign]에 있어야 하며 Experience Platform 세그먼트를 기반으로 새 프로필을 만들지 않아야 합니다.
* [!DNL Campaign] 내보내기 워크플로를 최대 4시간마다 실행
* Adobe [!DNL Campaign] broadLog, trackingLogs 및 전달할 수 없는 주소에 대한 XDM 스키마 및 데이터 세트는 기본 제공되지 않으며 디자인 및 빌드되어야 합니다.

### Real-time Customer Data Platform 세그먼트 공유

* RTCDP [!DNL Campaign] 대상 커넥터([RTCDP Campaign 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=ko))를 참조하세요.

* [기본 보호 기능 [!DNL Real-Time Customer Profile Data] 및 세분화](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)을 참조하세요.

## 구현 단계

다음 섹션에서는 각 애플리케이션에 대한 구현 단계를 설명합니다.

### Adobe Experience Platform  

#### 스키마/데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/?lang=ko&recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ko)
1. broadLog, trackingLog, 전달할 수 없는 주소 및 프로필 환경 설정에 대해 [!DNL Campaign] Adobe 스키마를 만듭니다(선택 사항).
1. Experience Platform에서 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 거버넌스를 위해 Experience Platform에서 데이터 세트에 [데이터 사용 레이블을 추가](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ko)합니다.
1. 대상 관리 [정책을 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ko)

#### 프로필/신원

1. [고객용 네임스페이스를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [스키마에 신원을 추가합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. [!UICONTROL Real-time Customer Profile]의 서로 다른 보기에 대한 [병합 규칙](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko)을 만듭니다(선택 사항).
1. Adobe [!DNL Campaign] 사용에 대한 세그먼트를 만듭니다.

#### 소스/대상

1. [Experience Platform 및 [!DNL Campaign] 표준 소스 및 지정](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=ko)
1. [Experience Platform 및 [!DNL Campaign] v7 원본 및 지정](https://experienceleague.adobe.com/docs/campaign-classic/using/integrating-with-adobe-experience-cloud/aep-sources-destinations/get-started-sources-destinations.html?lang=ko)
1. 스트리밍 API 및 소스 커넥터를 사용하여 [Experience Platform으로 데이터를 수집해 옵니다.](https://experienceleague.adobe.com/?lang=ko&recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)
1. [!DNL Campaign] Adobe에 사용할 [!DNL Azure] blob 저장소 대상을 구성합니다.

#### Adobe [!DNL Campaign]

1. 프로필, 룩업 데이터 및 관련 게재 개인화 데이터에 대하여 스키마를 구성합니다.

>[!IMPORTANT]
>
>이 시점에서 프로필 및 이벤트 데이터에 대한 Experience Platform 내에 데이터 모델이 무엇인지 파악하여 Adobe [!DNL Campaign]에서 어떤 데이터가 필요한지 알아야 합니다.

#### 가져오기 워크플로우

1. 간소화된 프로필 데이터를 Adobe [!DNL Campaign] sFTP에 로드하고 수집합니다.
1. 오케스트레이션 및 메시징 개인화 데이터를 Adobe [!DNL Campaign] sFTP로 로드하고 수집합니다.
1. 워크플로우를 통해 [!DNL Azure] Blob에서 Experience Platform 세그먼트를 수집합니다.

#### 내보내기 워크플로우

1. 워크플로우를 통해 4시간마다 [!DNL Campaign] Adobe 로그를 다시 Experience Platform으로 보냅니다(broadLog, trackingLog, 전달할 수 없는 주소).
1. 네 시간마다 컨설팅으로 작성한 워크플로우를 통해 프로필 환경 설정을 다시 Experience Platform으로 보냅니다(선택 사항).

### 모바일 푸시 구성

* 모바일 디바이스와 통합하여 푸시 알림을 보내는 방법으로는 두 가지를 지원합니다.
   * Experience Platform Mobile SDK
   * [!DNL Campaign] Mobile SDK
* Experience Platform Mobile SDK 방법:
   * Experience Platform Mobile SDK와의 통합을 설정하기 위해 Adobe 태그와 [!DNL Campaign Classic] 확장 사용
   * Adobe 태그 및 데이터 수집에 대한 실무 지식이 필요합니다.
   * Android와 iOS 모두에서 푸시 알림 모바일 개발 경험이 필요합니다. SDK를 배포하고, FCM(Android) 및 APNS(iOS)와 통합하여 푸시 토큰을 가져오고, 앱이 푸시 알림을 수신하고 푸시 상호 작용을 처리하도록 구성할 수 있어야 합니다.
* [!DNL Campaign] Mobile SDK
   * [Campaign Classic SDK 설명서](https://developer.adobe.com/client-sdks/solution/adobe-campaign-classic/) 보기

>[!IMPORTANT]
>
>[!DNL Campaign] SDK를 배포하고 다른 Experience Cloud 응용 프로그램과 함께 작업하는 경우 데이터 수집을 위해 Experience Platform Mobile SDK를 사용해야 합니다. 이렇게 하면 디바이스에 중복 클라이언트 측 호출이 만들어집니다.

## 관련 설명서

* [Adobe [!DNL Experience Platform] 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [[!DNL Campaign Classic] 설명서](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ko)
* [[!DNL Campaign Standard] 설명서](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ko)
* [[!DNL Experience Platform] 시작 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=ko)
* [[!DNL Experience Platform] Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
