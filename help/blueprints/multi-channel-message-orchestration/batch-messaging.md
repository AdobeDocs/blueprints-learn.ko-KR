---
title: 일괄 메시징 및 Adobe Experience Platform 블루프린트
description: 고객 프로필 및 세분화를 위한 중앙 허브로 Adobe Experience Platform을 사용하여 예약 및 일괄 메시징 캠페인을 실행합니다.
solution: Experience Platform, Campaign
kt: 7196
exl-id: 4e55218c-c158-4f78-9f0b-c03528d992fa
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# 일괄 메시징 및 Adobe Experience Platform 블루프린트

고객 프로필 및 세분화를 위한 중앙 허브로 Adobe Experience Platform을 사용하여 예약 및 일괄 메시징 캠페인을 실행합니다.

## 사용 사례

* 예약된 이메일 캠페인
* 온보딩 및 재마케팅 캠페인

## 애플리케이션

* Adobe Experience Platform
* Adobe Campaign Classic 또는 Standard

## 통합 패턴

* Adobe Experience Platform → Adobe Campaign Classic
* Adobe Experience Platform → Adobe Campaign Standard

## 아키텍처

<img src="assets/aepbatch.svg" alt="배치 메시징 및 Adobe Experience Platform Blueprint에 대한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

* 캠페인 단일 조직 단위 배포만 지원
* 캠페인은 모든 활성 프로필에 대한 진실 소스입니다. 즉, 프로필은 Campaign에 있어야 하며 새 프로필은 Experience Platform 세그먼트를 기반으로 만들지 않아야 합니다.
* Experience Platform의 세그먼트 회원 실현은 일괄 처리(하루 1회)와 스트리밍(약 5분) 모두에 걸쳐 지연됩니다.

**[!UICONTROL 실시간 고객 데이터 플랫폼 세그먼트] 를 캠페인에 공유:**

* 20개 세그먼트 제한 권장 사항
* 정품 인증은 24시간 단위로 제한됩니다
* 활성화할 수 있는 공용 스키마 특성만 사용할 수 있습니다(배열/맵/경험 이벤트에 대한 지원 없음).
* 세그먼트당 20개 이하의 속성 권장 사항
* &quot;실현된&quot; 세그먼트 멤버십이 있는 모든 프로필의 세그먼트당 하나의 파일 또는 세그먼트 멤버십이 &quot;실현됨&quot; 및 &quot;종료한&quot; 프로필 모두에 속성으로 추가된 경우
* 증분 또는 전체 세그먼트 내보내기가 지원됩니다.
* 파일 암호화는 지원되지 않습니다.
* 최대 4시간마다 캠페인 내보내기 워크플로우 실행
* Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html)에 대한 [프로필 및 데이터 통합 지침을 참조하십시오.

## 구현 단계

### Adobe Experience Platform

#### 스키마/데이터 집합

1. 고객이 제공한 데이터를 기반으로 Experience Platform에서 개별 프로필, 경험 이벤트 및 다중 엔터티 스키마를 구성합니다.
1. broadLog, trackingLog, 배달할 수 없는 주소 및 프로필 환경 설정에 대한 캠페인 스키마를 만듭니다(선택 사항).
1. 거버넌스를 위해 데이터 세트에 데이터 사용 레이블을 추가합니다.
1. 대상에 대한 거버넌스를 적용하는 정책을 만듭니다.

#### 프로필/ID

1. 고객별 네임스페이스를 만듭니다.
1. 스키마에 ID를 추가합니다.
1. 프로필에 대한 스키마 및 데이터 세트를 활성화합니다.
1. [!UICONTROL 실시간 고객 프로필](선택 사항)의 다른 보기에 대한 병합 규칙을 설정합니다.
1. 캠페인 사용을 위한 세그먼트를 만듭니다.

#### 소스/대상

1. 스트리밍 API 및 소스 커넥터를 사용하여 데이터를 Experience Platform에 인제스트합니다.
1. [!DNL Azure] Blob 저장소 대상을 캠페인과 함께 사용하도록 구성합니다.

#### 모바일 앱 배포

1. Campaign Standard용 Campaign Classic 또는 Experience Platform SDK용 캠페인 SDK를 구현합니다. Experience Platform Launch이 있는 경우 Campaign Classic/표준 확장을 Experience Platform SDK와 함께 사용하는 것이 좋습니다.

#### Campaign

1. 프로필, 조회 데이터 및 관련 전달 개인화 데이터에 대한 스키마를 구성합니다.

>[!IMPORTANT]
>
>이 시점에서 프로필 및 이벤트 데이터의 Experience Platform 내에 있는 데이터 모델을 파악하여 Campaign에서 어떤 데이터가 필요한지 아는 것이 중요합니다.

#### 워크플로우 가져오기

1. 간소화된 프로필 데이터를 Campaign sFTP에 로드하고 인제스트합니다.
1. 캠페인 FTP에 오케스트레이션 및 메시징 개인화 데이터를 로드하고 인제스트합니다.
1. 워크플로우를 통해 [!DNL Azure] blob의 Experience Platform 세그먼트를 인제스트합니다.

#### 내보내기 워크플로우

1. 4시간마다 워크플로우(broadLog, trackingLog, 배달할 수 없는 주소)를 통해 캠페인 로그를 Experience Platform으로 다시 보냅니다.
1. 4시간마다 컨설팅 방식의 워크플로우를 통해 프로파일 환경 설정을 Experience Platform으로 다시 보낼 수 있습니다(선택 사항).


## 관련 설명서

* [Adobe Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Campaign Classic 설명서](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard 설명서](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
