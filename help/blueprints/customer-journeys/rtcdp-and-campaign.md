---
title: Real-Time CDP과 Adobe Campaign 블루프린트
description: Adobe Campaign에서 Adobe Experience Platform 및 그 실시간 고객 프로필 및 중앙 집중식 세그멘테이션 도구를 사용하여 개인화된 대화를 제공하는 방법을 소개합니다.
solution: Experience Platform, Campaign v8, Campaign Classic v7, Campaign Standard
source-git-commit: 1c46cbdfc395de4fc9139966cf869ba1feeceaaa
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 58%

---

# Real-Time CDP과 Adobe Campaign 블루프린트

Adobe Campaign에서 Adobe Experience Platform 및 그 실시간 고객 프로필 및 중앙 집중식 세그멘테이션 도구를 사용하여 개인화된 대화를 제공하는 방법을 소개합니다.

<br>

## 애플리케이션

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v7 또는 Campaign Standard

<br>

## 아키텍처

<img src="assets/rtcdp-campaign-architecture.svg" alt="일괄 처리 메시지와 Adobe Experience Platform 블루프린트를 위한 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 필요 조건

* Experience Platform 및 Campaign은 동일한 IMS 조직에 프로비저닝되어 사용자 액세스를 위해 Adobe Admin Console을 활용하는 것이 좋습니다. 또한 고객이 마케팅 UI 내에서 솔루션 전환기를 활용할 수 있습니다

<br>

## 가드레일

### Adobe Campaign

* Adobe Campaign 단일 조직 단위 배포만 지원합니다
* Adobe Campaign이 전체 활성 프로필에 대한 단일 정보 저장소입니다. 따라서 프로필이 Adobe Campaign 내에 존재해야 하며 Experience Platform 기반으로 새로운 프로필을 만들면 안 됩니다.
* Campaign 내보내기 워크플로우는 4시간에 한 번 이하로 실행
* Adobe Campaign broadLog, trackingLogs 및 비제공 주소를 위한 XDM 스키마 및 데이터 세트는 즉시 사용할 수 없으며 설계 및 구축되어야 합니다

### Experience Platform CDP 세그먼트 공유

* 20개 세그먼트 제한 권장 사항
* 활성화는 24시간 간격으로 제한됩니다
* 통합 스키마 속성만 활성화할 수 있습니다(배열/맵/경험 이벤트 미지원)
* 세그먼트당 20개 이하의 속성에 대한 권장 사항
* 세그먼트 당 한 파일(&quot;실현&quot; 세그먼트 멤버십을 가진 전체 프로필, 또는 파일에 세그먼트 멤버십을 속성으로 추가한 경우 &quot;실현&quot; 및 &quot;탈퇴&quot; 프로필 모두)
* 증분 및 전체 세그먼트 내보내기가 지원됩니다
* 파일 암호화 미지원

<br>

## 구현 단계

### Adobe Experience Platform

#### 스키마 / 데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. broadLog, trackingLog, 게재 불가 주소 및 프로필 환경 설정에 대하여 Adobe Campaign 스키마를 만듭니다(선택 사항).
1. Experience Platform에서 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 거버넌스를 위해 Experience Platform에서 데이터 세트에 [데이터 사용 레이블을 추가](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ko)합니다.
1. 대상 관리 [정책을 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ko)

#### 프로필 / ID

1. [고객용 네임스페이스를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [스키마에 ID를 추가합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. [!UICONTROL Real-time Customer Profile]의 서로 다른 보기에 대한 [병합 규칙](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko)을 만듭니다(선택 사항).
1. Adobe Campaign에서 사용하기 위한 세그먼트를 만듭니다.

#### 소스 / 대상

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

* 푸시 알림에 대해 모바일 장치와 통합하기 위해 지원되는 두 가지 방법:
   * Experience Platform Mobile SDK
   * Campaign Mobile SDK
* Experience Platform Mobile SDK 경로:
   * Experience Platform Mobile SDK와의 통합을 설정하기 위해 Adobe 태그 및 Campaign Classic 확장 활용
   * Adobe 태그 및 데이터 수집에 대한 실무 지식 필요
   * SDK를 배포하고 FCM(Android) 및 APNS(iOS)과 통합하여 푸시 토큰을 가져오고, 푸시 알림을 수신하고, 푸시 상호 작용을 처리하도록 앱을 구성하려면 Android 및 iOS 모두에서 푸시 알림과 함께 모바일 개발 경험이 필요합니다
* Campaign Mobile SDK
   * 다음 내용을 따르십시오 [Campaign SDK 설명서](Campaign Mobile SDK 여기에 설명된 배포 설명서를 따르십시오.)

   >[!IMPORTANT]
   >Campaign SDK를 배포하고 다른 Experience Cloud 애플리케이션과 작업하는 경우, 사용자는 데이터 수집을 위해 Campaign Mobile SDK를 사용해야 합니다. 이렇게 하면 장치에서 중복 클라이언트 측 호출이 만들어집니다.

## 관련 설명서

* [Adobe Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Campaign Classic 설명서](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ko)
* [Campaign Standard 설명서](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ko)
* [Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
