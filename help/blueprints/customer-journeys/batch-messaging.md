---
title: 일괄 처리 메시지와 Adobe Experience Platform 블루프린트
description: Adobe Experience Platform을 고객 프로필 및 세분화의 중심 허브로 사용하여 예약 및 일괄 처리 메시지 캠페인을 실행합니다.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
source-git-commit: 3c950cebaa25901ae50433775c510ed834d8bcd5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 일괄 처리 메시지와 Adobe Experience Platform 블루프린트

Adobe Experience Platform을 고객 프로필 및 세분화의 중심 허브로 사용하여 예약 및 일괄 처리 메시지 캠페인을 실행합니다.

## 사용 사례

* 예약 이메일 캠페인
* 캠페인 시작 및 재실행

## 애플리케이션

* Adobe Experience Platform
* Adobe Campaign Classic 또는 Standard

## 통합 패턴

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## 아키텍처

<img src="assets/aepbatch.svg" alt="일괄 처리 메시지와 Adobe Experience Platform 블루프린트를 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

* Adobe Campaign 단일 조직 유닛 배포만 지원
* Adobe Campaign이 전체 활성 프로필에 대한 단일 정보 저장소입니다. 따라서 프로필이 Adobe Campaign 내에 존재해야 하며 Experience Platform 기반으로 새로운 프로필을 만들면 안 됩니다.
* Experience Platform의 세그먼트 멤버십 실현은 일괄 처리(하루에 하나) 및 스트리밍(최대 5분) 모두에서 잠복기를 가집니다.

**[!UICONTROL Real-time Customer Data Platform] 세그먼트를 Adobe Campaign에 공유할 때:**

* 최대 20 세그먼트 제한 추천
* 활성화는 매 24시간으로 제한
* 통합 스키마 속성만 활성화할 수 있습니다(배열/맵/경험 이벤트 미지원).
* 세그먼트 당 최대 속성 20개 제한 추천
* 세그먼트 당 한 파일(&quot;실현&quot; 세그먼트 멤버십을 가진 전체 프로필, 또는 파일에 세그먼트 멤버십을 속성으로 추가한 경우 &quot;실현&quot; 및 &quot;탈퇴&quot; 프로필 모두)
* 증분 또는 전체 세그먼트 가져오기 지원
* 파일 암호화 미지원
* Adobe Campaign 내보내기 워크플로우는 4시간에 한 번 이하로 실행
* [Experience Platform 프로필 및 데이터 수집 가드레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)을 참조하세요.

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

#### 모바일 앱 배포

1. Adobe Campaign Classic의 경우 Adobe Campaign SDK, Adobe Campaign Standard의 경우 Experience Platform SDK를 구현합니다. Experience Platform Launch가 있는 경우 Experience Platform SDK의 Adobe Campaign Classic 또는 Adobe Campaign Standard 확장을 사용하는 것을 추천합니다.

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


## 관련 설명서

* [Adobe Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Campaign Classic 설명서](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ko)
* [Campaign Standard 설명서](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ko)
* [Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
