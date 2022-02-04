---
title: Journey Optimizer - 타사 메시징 블루프린트
description: Adobe Journey Optimizer을 타사 메시징 시스템과 함께 사용하여 개인화된 커뮤니케이션을 오케스트레이션 및 전송하는 방법을 보여줍니다.
solution: Experience Platform, Journey Optimizer
hidefromtoc: true
source-git-commit: a86df4a1b2de38bcb244a6afe1cea87adc7e26fa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 35%

---

# 타사 메시징

Adobe Journey Optimizer을 타사 메시징 시스템과 함께 사용하여 개인화된 커뮤니케이션을 오케스트레이션 및 전송하는 방법을 보여줍니다.

<br>

## 아키텍처

<img src="assets/3rd-party-messaging-architecture.svg" alt="참조 아키텍처 Journey Optimizer 블루프린트" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 필요 조건

Adobe Experience Platform

* Journey Optimizer 데이터 소스를 구성하려면 먼저 시스템에서 스키마 및 데이터 세트를 구성해야 합니다
* 규칙 기반 이벤트가 아닌 이벤트를 트리거하려면 Experience Event 클래스 기반 스키마의 경우 &#39;Orchestration eventID 필드 그룹&#39;을 추가합니다
* 개별 프로필 클래스 기반 스키마의 경우 Journey Optimizer에서 사용할 테스트 프로필을 로드할 수 있도록 &#39;프로필 테스트 세부 정보&#39; 필드 그룹을 추가합니다

타사 메시징 응용 프로그램

* 트랜잭션 페이로드 전송을 위한 REST API 호출을 지원해야 합니다.

<br>

## 가드레일

[Journey Optimizer 보호 제품 링크](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ko)

추가 Journey Optimizer 보호 기능:

* 캡핑은 API를 통해 사용할 수 있으므로 대상 시스템이 장애 시기까지 포화되지 않습니다. 이것은 캡을 초과하는 메시지가 완전히 삭제되고 전송되지 않음을 의미합니다. 조절이 지원되지 않습니다.
   * 최대 연결 수 - 대상이 처리할 수 있는 최대 http/s 연결 수
   * 최대 호출 수 - periodInMs 매개 변수에서 수행할 최대 호출 수
   * perienceInMs - 시간(밀리초)
* 세그먼트 멤버십에서 시작한 여정은 두 가지 모드로 작동할 수 있습니다.
   * 배치 세그먼트(24시간 간격으로 새로 고침)
   * 스트리밍 세그먼트(&lt;5분 자격)
* 세그먼트 일괄 처리: 인증 사용자의 일별 볼륨을 이해해야 하며, 대상 시스템이 각 여정 및 모든 여정의 발생 처리량을 처리할 수 있어야 합니다.
* 세그먼트 스트리밍: 프로필 인증 첫 발생을 각 여정 및 모든 여정에 대한 일별 스트리밍 인증 볼륨과 함께 처리할 수 있어야 합니다.
* 지원되지 않는 의 offer decisioning
* 타사 시스템에 대한 아웃바운드 통합
   * 인프라가 멀티 테넌트이므로 단일 정적 IP를 지원하지 않습니다(모든 데이터 센터 IP를 허용 목록 해야 함).
   * 사용자 지정 작업에는 POST 및 PUT 메서드만 지원됩니다
   * 인증 지원: 토큰 | 암호 | OAuth2
* 다양한 샌드박스 간에 Adobe Experience Platform 또는 Journey Optimizer의 개별 구성 요소를 패키징하여 이동할 수 없습니다. 새 환경에서 다시 구현해야 함

<br>

타사 메시징 시스템

* 시스템이 트랜잭션 API 호출에 대해 지원할 수 있는 로드를 이해해야 합니다
   * 초당 허용되는 호출 수
   * 연결 수
* API 호출을 수행하는 데 필요한 인증을 이해해야 합니다
   * 인증 유형:  토큰 | 암호 | OAuth2는 Journey Optimizer을 통해 지원됩니다
   * 인증 캐시 기간:  토큰은 얼마나 유효합니까? 
* 일괄 처리가 만 지원되는 경우 Amazon Kinesis 또는 Azure Event Grid와 같은 클라우드 저장소 엔진으로 스트리밍되어야 합니다
   * 이러한 클라우드 스토리지 엔진에서 데이터를 일괄 처리하여 타사에 공급할 수 있습니다
   * 필요한 모든 미들웨어는 고객 또는 타사에서 제공하는 책임입니다

<br>

## 구현 단계

### Adobe Experience Platform

#### 스키마/데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. Experience Platform에서 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 거버넌스를 위해 Experience Platform에서 데이터 세트에 [데이터 사용 레이블을 추가](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ko)합니다.
1. 대상 관리 [정책을 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ko)

#### 프로필/ID

1. [고객용 네임스페이스를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [스키마에 ID를 추가합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. [!UICONTROL Real-time Customer Profile]의 서로 다른 보기에 대한 [병합 규칙](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko)을 만듭니다(선택 사항).
1. 여정 사용을 위한 세그먼트를 만듭니다.

#### 소스/대상

1. 스트리밍 API 및 소스 커넥터를 사용하여 [Experience Platform으로 데이터를 수집해 옵니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)

### Journey Optimizer

1. Experience Platform 데이터 소스를 구성하고 프로필 일부로 캐시해야 하는 필드를 결정합니다. 고객 여정을 시작하는 데 사용되는 스트리밍 데이터는 먼저 Journey Optimizer 내에서 구성하여 오케스트레이션 ID를 받아야 합니다. 이 오케스트레이션 ID는 데이터 수집에 사용할 수 있도록 개발자에게 제공됩니다
1. 외부 데이터 소스를 구성합니다
1. 타사 애플리케이션에 대한 사용자 지정 작업 구성

### 모바일 푸시 구성(타사에서 토큰을 수집할 수 있는 옵션)

1. Experience Platform Mobile SDK를 구현하여 푸시 토큰 및 로그인 정보를 수집하여 알려진 고객 프로필에 다시 연결합니다
1. Adobe 태그를 활용하고 다음 확장을 사용하여 모바일 속성을 만듭니다.
   * Adobe Journey Optimizer
   * Adobe Experience Platform Edge Network
   * ID 에지 네트워크용
   * Mobile Core
1. 모바일 앱 배포와 웹 배포를 위한 전용 데이터 스트림이 있는지 확인합니다.
1. 자세한 내용은 [Adobe Journey Optimizer Mobile 안내서](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

<br>

## 관련 설명서

* [Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
* [Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko)
* [Journey Optimizer 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
