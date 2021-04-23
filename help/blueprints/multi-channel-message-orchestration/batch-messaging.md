---
title: 일괄 메시징 및 Adobe Experience Platform 블루프린트
description: Adobe Experience Platform을 고객 프로필 및 세분화의 중심 허브로 사용하여 예약 및 일괄 처리 메시지 캠페인을 실행합니다.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 37416aafc997838888edec2658d2621d20839f94
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 59%

---

# 일괄 메시징 및 Adobe Experience Platform 블루프린트

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

<img src="assets/aepbatch.svg" alt="배치 메시징 및 Adobe Experience Platform Blueprint에 대한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

* Adobe Campaign 단일 조직 구성 단위 배포만 지원
* Adobe Campaign은 모든 활성 프로파일에 대한 진실의 소스입니다. 즉, Adobe Campaign에 프로파일이 있어야 하며 Experience Platform 세그먼트를 기반으로 새 프로파일을 만들 수 없습니다.
* Experience Platform의 세그먼트 멤버십 실현은 일괄 처리(하루에 하나) 및 스트리밍(최대 5분) 모두에서 잠복기를 가집니다.

**[!UICONTROL Adobe Campaign에 대한 실시간 고객 데이터 플랫폼 ] 세그먼트 공유:**

* 최대 20 세그먼트 제한 추천
* 활성화는 매 24시간으로 제한
* 통합 스키마 속성만 활성화할 수 있습니다(배열/맵/경험 이벤트 미지원).
* 세그먼트 당 최대 속성 20개 제한 추천
* 세그먼트 당 한 파일(&quot;실현&quot; 세그먼트 멤버십을 가진 전체 프로필, 또는 파일에 세그먼트 멤버십을 속성으로 추가한 경우 &quot;실현&quot; 및 &quot;탈퇴&quot; 프로필 모두)
* 증분 또는 전체 세그먼트 가져오기 지원
* 파일 암호화 미지원
* 4시간마다 Adobe Campaign 내보내기 워크플로우 실행
* [Experience Platform 프로필 및 데이터 수집 가드레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)을 참조하세요.

## 구현 단계

### Adobe Experience Platform

#### 스키마 / 데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.
1. 광범위한 로그, trackingLog, 배달할 수 없는 주소 및 프로필 환경 설정에 대한 Adobe Campaign 스키마를 만듭니다(선택 사항).
1. 관리를 위해 데이터 세트에 데이터 사용량 레이블을 추가합니다.
1. 대상 관리 정책을 만듭니다.

#### 프로필 / ID

1. 고객용 네임스페이스를 만듭니다.
1. 스키마에 ID를 추가합니다.
1. 프로필에 대해 스키마와 데이터 세트를 활성화합니다.
1. [!UICONTROL 실시간 고객 프로필](선택 사항)의 다른 보기에 대한 병합 규칙을 설정합니다.
1. Adobe Campaign 사용을 위한 세그먼트를 만듭니다.

#### 소스 / 대상

1. 스트리밍 API 및 소스 커넥터를 사용하여 Experience Platform으로 데이터를 수집해 옵니다.
1. Adobe Campaign에서 사용할 [!DNL Azure] Blob 저장소 대상을 구성합니다.

#### 모바일 앱 배포

1. Adobe Campaign Classic용 Adobe Campaign SDK 또는 Adobe Campaign Standard용 Experience Platform SDK 구현 Experience Platform Launch이 있는 경우 Experience Platform SDK와 함께 Adobe Campaign Classic 또는 Adobe Campaign Standard 확장을 사용하는 것이 좋습니다.

#### Adobe Campaign

1. 프로필, 룩업 데이터 및 관련 게재 개인화 데이터에 대하여 스키마를 구성합니다.

>[!IMPORTANT]
>
>이때 프로필 및 이벤트 데이터의 Experience Platform 내에 있는 데이터 모델을 이해하여 Adobe Campaign에서 어떤 데이터가 필요한지 파악하는 것이 중요합니다.

#### 가져오기 워크플로우

1. Adobe Campaign sFTP에 간소화된 프로필 데이터를 로드하고 인제스트합니다.
1. Adobe Campaign sFTP에서 오케스트레이션 및 메시징 개인화 데이터를 로드하고 인제스트할 수 있습니다.
1. 워크플로우를 통해 [!DNL Azure] Blob에서 Experience Platform 세그먼트를 수집합니다.

#### 내보내기 워크플로우

1. 4시간마다 워크플로우(broadLog, trackingLog, 배달할 수 없는 주소)를 통해 Adobe Campaign 로그를 Experience Platform으로 다시 보냅니다.
1. 네 시간마다 컨설팅으로 작성한 워크플로우를 통해 프로필 환경 설정을 다시 Experience Platform으로 보냅니다(선택 사항).


## 관련 설명서

* [Adobe Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Campaign Classic 설명서](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ko)
* [Campaign Standard 설명서](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=ko)
* [Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
