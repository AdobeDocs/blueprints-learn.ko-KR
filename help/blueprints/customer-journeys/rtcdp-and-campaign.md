---
title: Real-Time CDP와 Adobe Campaign v7 및 Campaign Standard 통합 패턴
description: Adobe Experience Platform의 [실시간 고객 프로필]과 그 중앙 집중식 세분화 도구를 Adobe Campaign과 함께 활용하여 개인화된 대화를 게재하는 방법을 소개합니다.
solution: Real-Time Customer Data Platform, Campaign
exl-id: a15e8304-2763-42fc-9978-11f2482ea8b8
source-git-commit: 5f9384abe7f29ec764428af33c6dd1f0a43f5a89
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 100%

---

# Real-Time CDP와 Adobe Campaign 통합 패턴

Adobe Experience Platform의 [실시간 고객 프로필]과 그 중앙 집중식 세분화 도구를 Adobe Campaign과 함께 활용하여 개인화된 대화를 게재하는 방법을 소개합니다.

<br>

## 애플리케이션

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v7 또는 Campaign Standard

<br>

## 아키텍처

<img src="assets/rtcdp-campaign-architecture.svg" alt="일괄 처리 메시지와 Adobe Experience Platform 통합 패턴의 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 필요 조건

* Experience Platform 및 Campaign을 동일한 IMS 조직에서 프로비저닝하고 사용자 액세스를 위해 Adobe Admin Console을 활용하는 것이 좋습니다. 이렇게 하면 고객이 마케팅 UI 내에서 솔루션 전환기를 활용할 수 있습니다.

<br>

## 가드레일

### Adobe Campaign

* Adobe Campaign 단일 조직 유닛 배포만 지원
* Adobe Campaign이 전체 활성 프로필에 대한 단일 정보 저장소입니다. 따라서 프로필이 Adobe Campaign 내에 존재해야 하며 Experience Platform 기반으로 새로운 프로필을 만들면 안 됩니다.
* Campaign 내보내기 워크플로우는 4시간에 한 번 이하로 실행
* Adobe Campaign broadLog, trackingLogs, 게재 불가 주소에 대한 XDM 스키마 및 데이터 세트는 기본 제공되지 않으며 설계 및 작성해야 합니다.

### Experience Platform CDP 세그먼트 공유

* RTCDP Campaign 대상 커넥터를 참조하세요. [RTCDP Campaign 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=ko)

* AEP의 프로필 및 데이터 수집 가드레일을 참조하세요. [링크](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)

## 구현 단계

### Adobe Experience Platform  

#### 스키마/데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ko)
1. broadLog, trackingLog, 게재 불가 주소 및 프로필 환경 설정에 대하여 Adobe Campaign 스키마를 만듭니다(선택 사항).
1. Experience Platform에서 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 거버넌스를 위해 Experience Platform에서 데이터 세트에 [데이터 사용 레이블을 추가](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ko)합니다.
1. 대상 관리 [정책을 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ko)

#### 프로필/신원

1. [고객용 네임스페이스를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [스키마에 신원을 추가합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. [!UICONTROL Real-time Customer Profile]의 서로 다른 보기에 대한 [병합 규칙](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko)을 만듭니다(선택 사항).
1. Adobe Campaign에서 사용하기 위한 세그먼트를 만듭니다.

#### 소스/대상

1. [Experience Platform과 Campaign Standard 소스 및 대상](https://experienceleague.adobe.com/docs/campaign-standard/using/integrating-with-adobe-cloud/adobe-experience-platform/aep-sources-destinations/get-started-sources-destinations.html?lang=ko)
1. [Experience Platform과 Campaign v7 소스 및 대상](https://experienceleague.adobe.com/docs/campaign-classic/using/integrating-with-adobe-experience-cloud/aep-sources-destinations/get-started-sources-destinations.html?lang=ko)
1. 스트리밍 API 및 소스 커넥터를 사용하여 [Experience Platform으로 데이터를 수집해 옵니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)
1. Adobe Campaign에서 사용할 [!DNL Azure] Blob 스토리지 대상을 구성합니다.

#### Adobe Campaign

1. 프로필, 룩업 데이터 및 관련 게재 개인화 데이터에 대하여 스키마를 구성합니다.

>[!IMPORTANT]
>
>이때 Experience Platform 내에 프로필 및 이벤트 데이터에 대한 데이터 모델에는 어떤 것이 있는지를 이해하여 Adobe Campaign에서 어떤 데이터가 필요할지 알아 두는 것이 중요합니다.

#### 가져오기 워크플로우

1. 간략화된 프로필 데이터를 Adobe Campaign sFTP로 로드 및 수집합니다.
1. 오케스트레이션 및 메시지 개인화 데이터를 Adobe Campaign sFTP로 로드 및 수집합니다.
1. 워크플로우를 통해 [!DNL Azure] Blob에서 Experience Platform 세그먼트를 수집합니다.

#### 내보내기 워크플로우

1. 네 시간마다 워크플로우를 통해 Adobe Campaign 로그를 다시 Experience Platform으로 보냅니다(broadLog, trackingLog, 게재 불가 주소).
1. 네 시간마다 컨설팅으로 작성한 워크플로우를 통해 프로필 환경 설정을 다시 Experience Platform으로 보냅니다(선택 사항).


### 모바일 푸시 구성

* 모바일 디바이스와 통합하여 푸시 알림을 보내는 방법으로는 두 가지를 지원합니다.
   * Experience Platform Mobile SDK
   * Campaign Mobile SDK
* Experience Platform Mobile SDK 방법:
   * Adobe 태그와 Campaign Classic 확장을 활용하여 Experience Platform Mobile SDK와의 통합을 설정합니다.
   * Adobe 태그 및 데이터 수집에 대한 실무 지식이 필요합니다.
   * Android와 iOS 모두에서 푸시 알림 모바일 개발 경험이 필요합니다. SDK를 배포하고, FCM(Android) 및 APNS(iOS)와 통합하여 푸시 토큰을 가져오고, 앱이 푸시 알림을 수신하고 푸시 상호 작용을 처리하도록 구성할 수 있어야 합니다.
* Campaign Mobile SDK
   * [Campaign SDK 설명서] 를 따르세요(Campaign Mobile SDK의 경우
여기에서 설명하는 배포 설명서를 따르세요).

  >[!IMPORTANT]
  >Campaign SDK를 배포하고 다른 Experience Cloud 애플리케이션으로 작업하는 경우, 데이터 수집을 위해 Experience Platform Mobile SDK를 사용해야 합니다. 이렇게 하면 디바이스에 중복 클라이언트 측 호출이 만들어집니다.

## 관련 설명서

* [Adobe Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Campaign Classic 설명서](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ko)
* [Campaign Standard 설명서](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ko)
* [Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
