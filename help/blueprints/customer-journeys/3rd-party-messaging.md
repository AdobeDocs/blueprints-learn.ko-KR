---
title: Journey Optimizer - 서드파티 메시지 블루프린트
description: Adobe Journey Optimizer를 서드파티 메시지 시스템과 함께 사용하여 개인화된 메시지를 오케스트레이션하고 보내는 방법을 설명합니다.
solution: Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
source-git-commit: a1421a47da2c84635ef904096a6036cfe488d763
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 99%

---

# 서드파티 메시지 블루프린트

Adobe Journey Optimizer를 서드파티 메시지 시스템과 함께 사용하여 개인화된 메시지를 오케스트레이션하고 보내는 방법을 설명합니다.

<br>

## 아키텍처

<img src="assets/3rd-party-messaging-architecture.svg" alt="Journey Optimizer 블루프린트 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 필요 조건

Adobe Experience Platform

* Journey Optimizer 데이터 소스를 구성하려면 먼저 시스템에서 스키마와 데이터 세트를 구성해야 합니다.
* [경험 이벤트] 클래스 기반 스키마의 경우 규칙 기반 이벤트가 아닌 이벤트를 트리거하려면 [Orchestration eventID 필드 그룹]을 추가해야 합니다.
* [개별 프로필] 클래스 기반 스키마의 경우 Journey Optimizer에서 사용할 테스트 프로필을 로드할 수 있도록 하려면 [프로필 테스트 세부 정보] 필드 그룹을 추가해야 합니다.

서드파티 메시지 애플리케이션

* 트랜잭션 페이로드를 보내기 위해 REST API 호출을 지원해야 합니다.

<br>

## 가드레일

[Journey Optimizer 가드레일 제품 링크](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ko)

그 외의 Journey Optimizer 가드레일:

* 현재는 대상 시스템이 과부하로 수신에 실패하지 않도록 API 설정을 통해 용량 제한을 사용할 수 있습니다. 이는 최대 용량을 초과하는 메시지를 완전히 없애서 보내지 않는 것을 말합니다. 스로틀링(트래픽 조절)은 지원하지 않습니다.
   * 최대 연결 수- 대상에서 처리할 수 있는 최대 http/s 연결 수
   * 최대 호출- periodInMs 매개 변수 내에 실행할 수 있는 최대 호출 수
   * periodInMs- 밀리세컨드(ms)로 표기한 시간
* 세그먼트 멤버십에서 시작한 여정은 두 가지 모드로 작동할 수 있습니다.
   * 세그먼트 일괄 처리(24시간마다 새로 고침)
   * 세그먼트 스트리밍(5분 미만의 인증)
* 세그먼트 일괄 처리: 인증 사용자의 일별 볼륨을 이해해야 하며, 대상 시스템이 각 여정 및 모든 여정의 발생 처리량을 처리할 수 있어야 합니다.
* 세그먼트 스트리밍: 프로필 인증 첫 발생을 각 여정 및 모든 여정에 대한 일별 스트리밍 인증 볼륨과 함께 처리할 수 있어야 합니다.
* 의사 결정 관리는 지원하지 않음
* 서드파티 시스템으로의 아웃바운드 통합
   * 멀티 테넌트 인프라를 사용하므로 단일 고정 IP를 지원하지 않습니다(모든 데이터 센터의 IP를 허용 목록에 추가해야 함).
   * 사용자 정의 작업에는 POST 및 PUT 메서드만 지원됩니다.
   * 인증 지원: 토큰 | 암호 | OAuth2
* 다양한 샌드박스 간에 Adobe Experience Platform 또는 Journey Optimizer의 개별 구성 요소를 패키징하여 이동할 수 없습니다. 새로운 환경에서는 다시 구현해야 합니다.

<br>

서드파티 메시지 시스템

* 시스템이 트랜잭션 API 호출에 지원할 수 있는 로드를 파악해야 합니다.
   * 초당 허용되는 호출 수
   * 연결 수
* API 호출에 필요한 인증을 이해해야 합니다.
   * 인증 유형: Journey Optimizer를 통해 토큰 | 암호 | OAuth2 지원
   * 인증 캐시 기간: 토큰의 유효성이 지속되는 기간
* 일괄 수집만 지원되는 경우 먼저 Amazon Kinesis나 Azure Event Grid 등 클라우드 스토리지 엔진으로 스트리밍해야 합니다.
   * 그 뒤 데이터를 이 클라우드 스토리지 엔진에서 일괄 처리하여 서드파티에 공급하게 됩니다.
   * 필요한 미들웨어에 대한 제공 책임은 모두 고객 또는 서드파티에 있습니다.

<br>

## 구현 단계

### Adobe Experience Platform  

#### 스키마/데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ko)
1. Experience Platform에서 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 거버넌스를 위해 Experience Platform에서 데이터 세트에 [데이터 사용 레이블을 추가](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ko)합니다.
1. 대상 관리 [정책을 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ko)

#### 프로필/신원

1. [고객용 네임스페이스를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [스키마에 신원을 추가합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. [!UICONTROL Real-time Customer Profile]의 서로 다른 보기에 대한 [병합 규칙](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko)을 만듭니다(선택 사항).
1. Journey에서 사용할 세그먼트를 만듭니다.

#### 소스/대상

1. 스트리밍 API 및 소스 커넥터를 사용하여 [Experience Platform으로 데이터를 수집해 옵니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)

### Journey Optimizer

1. Experience Platform 데이터 소스를 구성하고 프로필의 일부로 캐시할 필드를 정합니다. 고객 여정을 시작하는 데 사용할 스트리밍 데이터는 먼저 Journey Optimizer 내에서 구성하여 오케스트레이션 ID를 설정해야 합니다. 이 오케스트레이션 ID는 데이터 수집에 사용할 수 있도록 개발자에게 제공됩니다
1. 외부 데이터 소스를 구성합니다
1. 서드파티 애플리케이션에 대한 사용자 정의 작업 구성

### 모바일 푸시 구성(선택 사항. 서드파티에서 토큰을 수집할 수 있음)

1. Experience Platform Mobile SDK를 구현하여 푸시 토큰 및 로그인 정보를 수집하고 이를 알려진 고객 프로필에 다시 연결합니다.
1. 다음 확장을 사용하여 Adobe 태그를 활용하고 모바일 속성을 만들 수 있습니다.
   * Adobe Journey Optimizer
   * Adobe Experience Platform Edge Network
   * ID           Edge 네트워크의 경우
   * Mobile Core
1. 모바일 앱 배포와 웹 배포 각각에 대해 전용 데이터 스트림이 있는지 확인합니다.
1. 자세한 내용은 [Adobe Journey Optimizer Mobile 안내서](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer/)를 참조하세요.

<br>

## 관련 설명서

* [Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
* [Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko)
* [Journey Optimizer 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)
