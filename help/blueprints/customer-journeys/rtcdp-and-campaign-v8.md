---
title: Real-Time CDP와 Adobe Campaign v8 통합 패턴
description: Adobe Experience Platform의 [실시간 고객 프로필]과 그 중앙 집중식 세분화 도구를 Adobe Campaign v8과 함께 활용하여 개인화된 대화를 게재하는 방법을 소개합니다.
solution: Real-time Customer Data Platform, Campaign
exl-id: d0291088-02ed-4e7e-b538-018ea40e38c6
source-git-commit: 05666e35eebe81fa5a061250528b1c2f4a7376a6
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 90%

---

# Real-Time CDP와 Adobe Campaign v8 통합 패턴

Adobe Experience Platform의 [실시간 고객 프로필]과 그 중앙 집중식 세분화 도구를 Adobe Campaign과 함께 활용하여 개인화된 대화를 게재하는 방법을 소개합니다.

<br>

## 애플리케이션

* Adobe Experience Platform Real-Time CDP
* Adobe Campaign v8

<br>

## 아키텍처

<img src="assets/rtcdp-campaignv8-architecture.svg" alt="일괄 처리 메시지와 Adobe Experience Platform 통합 패턴의 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 필요 조건

* 고객은 유효한 IMS 조직이 있는 Experience Cloud에 프로비전되어야 합니다.
* 단일 로그인 URL을 사용할 수 있도록 Adobe Experience Platform과 Campaign을 동일한 IMS 조직에 프로비저닝하기를 권장합니다.
* 고객에 대해 Campaign의 V8 인스턴스를 프로비저닝해야 합니다.
* 고객에게 RTCDP, 소스, 대상에 대한 액세스 권한이 있어야 합니다.
* Adobe Campaign 제품 컨텍스트가 있어야 합니다.

<br>

## 구현 단계

Adobe Experience Platform에 Campaign v8 소스 커넥터를 구성하고 Real-time Customer Data Platform 대상 커넥터를 Campaign v8에 구성하는 방법에 대한 다음 설명서를 참조하십시오.
[Campaign과 AEP 커넥터](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html?lang=ko)

## 가드레일

### Adobe Campaign

* Campaign 소스 커넥터 설명서를 참조하세요. [Campaign 소스 커넥터](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/campaign.html?lang=ko)
* Adobe Campaign 단일 조직 유닛 배포만 지원
* Adobe Campaign이 전체 활성 프로필에 대한 단일 정보 저장소입니다. 따라서 프로필이 Adobe Campaign 내에 존재해야 하며 Experience Platform 기반으로 새로운 프로필을 만들면 안 됩니다.


### Real-time Customer Data Platform 세그먼트 공유 Experience Platform

* RTCDP Campaign 대상 커넥터를 참조하세요. [RTCDP Campaign 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/adobe-campaign-managed-services.html?lang=ko)
* 최대 50 세그먼트 제한 추천
* AEP의 세그먼트 멤버십 실현은 일괄 처리(하루에 1회)와 스트리밍(~5분) 모두에 대해, 세그먼트 평가 일정에 따라 지연 처리됩니다.
* 활성화 지연 시간은 최소 3시간입니다
* 통합 스키마 속성만 활성화할 수 있습니다(배열/맵/경험 이벤트 미지원)
* 세그먼트 당 최대 속성 20개 제한 추천
* 세그먼트 당 한 파일(&quot;실현&quot; 세그먼트 멤버십을 가진 프로필 전체의 세그먼트, 또는 파일에 세그먼트 멤버십을 속성으로 추가한 경우 &quot;실현&quot; 및 &quot;탈퇴&quot; 프로필 전체의 세그먼트)
* 증분 및 전체 세그먼트 가져오기 지원
* 파일 암호화 미지원
* AEP의 프로필 및 데이터 수집 가드레일을 참조하세요. [링크](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
