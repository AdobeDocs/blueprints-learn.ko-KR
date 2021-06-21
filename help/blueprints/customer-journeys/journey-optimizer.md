---
title: Journey Optimizer - 트리거된 메시징 및 Adobe Experience Platform 블루프린트
description: Adobe Experience Platform을 스트리밍 데이터, 고객 프로필 및 세분화의 중앙 허브로 사용하여 트리거된 메시지 및 경험을 실행합니다.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: dc13a1fe9a32f70497c5c73485618e6989b7a644
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 49%

---

# Journey Optimizer

Adobe Journey Optimizer은 마케팅 팀이 고객 행동에 실시간으로 반응하여 현재 위치에 충족하는 데 사용할 수 있도록 내장된 목적 시스템입니다. 데이터 관리 기능이 Adobe Experience Platform으로 이동되었으므로 마케팅 팀은 다음 중 가장 좋은 작업에 집중할 수 있습니다.세계 최고 수준의 고객 여정과 개인화된 대화를 만들어 내고 있습니다.  이 블루프린트는 애플리케이션의 기술 기능을 간략하게 설명하고 Adobe Journey Optimizer을 구성하는 다양한 아키텍처 구성 요소에 대해 자세히 살펴봅니다.

## 사용 사례

* 트리거 메시지
* 등록 확인
* 장바구니 및 애플리케이션 양식 버리기
* 장소 트리거 메시지

## 아키텍처

<img src="assets/journey-optimizer.png" alt="트리거 메시지와 Adobe Experience Platform 블루프린트를 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 통합 패턴

* Adobe Experience Platform -> Journey Optimizer

## 필요 조건

1. 고객에게 유효한 IMS 조직이 있는 Experience Cloud이 제공되어야 합니다
1. 모바일 푸시

* 고객은 앱을 빌드할 수 있는 모바일 개발자가 있어야 합니다
* Adobe Experience Platform Mobile SDK
* Adobe 실행
   * 모바일 속성
      * 확장:
         * Adobe Journey Optimizer 확장
         * Adobe Experience Platform Edge Network
         * ID
         * Mobile Core
         * 프로필
   * 앱 구성
   * 데이터 스트림
      * Experience Platform 사용
      * 이벤트 데이터 세트 - 일반적인 모바일 동작을 수집하는 데 사용됩니다.
      * 프로필 데이터 세트 - AJO 푸시 프로필 데이터 세트(다를 수 없음)

## 가드레일

* 제한 사항에 대한 자세한 내용은 링크를 참조하세요.
* 배치 세그먼트 - 자격이 있는 사용자의 일별 볼륨을 이해하고 대상 시스템이 여정 및 모든 여정에 대해 버스트 처리량을 처리할 수 있는지 확인해야 합니다
* 스트리밍 세그먼트 - 프로필 자격의 초기 버스트를 여정 당 및 모든 여정에서 일별 스트리밍 자격 볼륨과 함께 처리할 수 있도록 해야 합니다
* 프로필 업데이트 활동 - 실시간 고객 프로필은 여정 내에서 기본적으로 업데이트할 수 있습니다.  프로필 스토어로 업데이트를 처리하는 데 최대 1분이 지연됩니다
* 비즈니스 이벤트 - JO 시스템으로의 외부 호출을 기반으로 하여 읽기 세그먼트 기반 여정을 시작하도록 트리거할 수 있습니다
* 기본적으로 메시지 Offer decisioning만 지원합니다. 기본 작업을 통한 향후 지원
* 지원되는 채널:
   * 이메일
   * 푸시(FCM/APNS)
   * Rest API 엔드포인트
* 수평 크기 조절을 사용하여 초당 5k 이벤트를 처리합니다(전자 지갑은 제한).
* A/B 테스트는 두 개의 게재를 사용하여 수행하며 QS 또는 CJA를 사용하여 결과를 확인합니다
* Litmus 통합 - 통합을 활용하려면 Litmus와 계정이 있어야 합니다.

## 구현 단계

### Adobe Experience Platform

#### 스키마/데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html?lang=ko)
1. broadLog, trackingLog, 게재 불가 주소 및 프로필 환경 설정에 대하여 Adobe Campaign 스키마를 만듭니다(선택 사항).
1. Experience Platform에서 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 거버넌스를 위해 Experience Platform에서 데이터 세트에 [데이터 사용 레이블을 추가](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ko)합니다.
1. 대상 관리 [정책을 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ko)

#### 프로필/ID

1. [고객용 네임스페이스를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [스키마에 ID를 추가합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. [!UICONTROL Real-time Customer Profile]의 서로 다른 보기에 대한 [병합 규칙](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko)을 만듭니다(선택 사항).
1. 캠페인 사용량에 대한 세그먼트를 만듭니다.

#### 소스/대상

1. 스트리밍 API와 소스 커넥터를 사용하여 [데이터를 Experience Platform으로 수집합니다](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko).1. Adobe Campaign에서 사용할 [!DNL Azure] Blob 스토리지 대상을 구성합니다.

#### 모바일 앱 배포

1. Adobe Campaign Classic의 경우 Adobe Campaign SDK, Adobe Campaign Standard의 경우 Experience Platform SDK를 구현합니다. Experience Platform Launch가 있는 경우 Experience Platform SDK의 Adobe Campaign Classic 또는 Adobe Campaign Standard 확장을 사용하는 것을 추천합니다.


### Journey Orchestration

1. 고객 여정을 시작하는 데 사용되는 스트리밍 데이터는 먼저 Journey Optimizer 내에서 구성해야 오케스트레이션 ID를 가져올 수 있습니다. 이 오케스트레이션 ID는 데이터 수집에 사용할 수 있도록 개발자에게 제공됩니다.
1. 외부 데이터 소스를 구성합니다.
1. 사용자 정의 행동을 구성합니다.

## 관련 설명서

* [Adobe Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=ko)
* [Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
