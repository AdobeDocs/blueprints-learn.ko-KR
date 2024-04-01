---
title: Journey Optimizer와 Adobe Campaign v8 블루프린트
description: Adobe Journey Optimizer를 Adobe Campaign과 함께 사용하여 앱 내에서 메시지를 보내는 방법을 설명합니다. Campaign의 실시간 메시지 서버를 활용합니다.
solution: Journey Optimizer, Campaign, Campaign v8 Client Console
exl-id: 447a1b60-f217-4295-a0df-32292c4742b0
source-git-commit: 60a7785ea0ec4ee83fd9a1e843f0b84fc4cb1150
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Journey Optimizer와 Adobe Campaign v8 블루프린트

Adobe 방법을 보여 줍니다 [!DNL Journey Optimizer] Adobe과 함께 사용할 수 있습니다. [!DNL Campaign] 의 실시간 메시징 서버를 사용하여 메시지를 기본적으로 전송합니다. [!DNL Campaign].

## 아키텍처

<img src="assets/ajo-campaign-architecture.svg" alt="Journey Optimizer 블루프린트 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

>[!IMPORTANT]
>Journey Optimizer와 Campaign을 둘 다 사용하여 별도로 메시지를 보낼 수 있지만, 고민해야 하는 몇 가지 기술적 고려 사항이 있습니다. 이 방법을 사용하려면 영업 전 단계 기업 아키텍트와 협력하여 구현을 지원하는 데 필요한 사항을 이해해야 합니다.

## 필요 조건

각 애플리케이션에 대한 다음 사전 요구 사항을 검토하십시오.

### Adobe Experience Platform      

* Journey Optimizer 데이터 소스를 구성하려면 먼저 시스템에서 스키마와 데이터 세트를 구성해야 합니다.
* [경험 이벤트] 클래스 기반 스키마의 경우 규칙 기반 이벤트가 아닌 이벤트를 트리거하려면 [Orchestration eventID 필드 그룹]을 추가해야 합니다.
* [개별 프로필] 클래스 기반 스키마의 경우 Journey Optimizer에서 사용할 테스트 프로필을 로드할 수 있도록 하려면 [프로필 테스트 세부 정보] 필드 그룹을 추가해야 합니다.
* Journey Optimizer와 Campaign은 동일한 IMS 조직에 공급됩니다.

### Campaign v8

* 실시간 메시지 서비스(=[메시지 센터])의 실행 인스턴스는 Adobe Managed Cloud Services에서 호스팅해야 합니다.
* 모든 메시지 작성은 Campaign 인스턴스 자체에서 수행합니다.

## 가드레일

* [Journey Optimizer Guarrails 제품 제한 사항](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ko)

* [보호 및 완벽한 지연 지침](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 구현 단계

아래에 설명된 각 애플리케이션에 대한 구현을 따르십시오.

### Adobe Experience Platform  

#### 스키마/데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ko)
1. (선택 사항) Adobe Campaign broadLog, trackingLog 및 전달할 수 없는 주소 테이블에 대한 경험 이벤트 클래스 기반 스키마를 만듭니다.
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

1. [데이터 수집 대상 [!DNL Experience Platform]](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko) 스트리밍 API 및 소스 커넥터 사용.

### Journey Optimizer   

1. 구성 [!DNL Experience Platform] 데이터 소스 및 프로필의 일부로 캐시할 필드 결정고객 여정을 시작하는 데 사용되는 스트리밍 데이터를 오케스트레이션 ID를 가져오려면 먼저 Journey Optimizer 내에서 구성해야 합니다. 이 오케스트레이션 ID는 데이터 수집에 사용할 수 있도록 개발자에게 제공됩니다.
1. 외부 데이터 소스를 구성합니다.
1. Campaign 인스턴스에 대한 사용자 지정 작업을 구성합니다.

### Campaign v8

* 메시징 템플릿은 적절한 개인화 컨텍스트로 구성해야 합니다.
* 대상 [!DNL Campaign] 표준: 트랜잭션 메시지 로그를 다시 Experience Platform으로 내보내려면 내보내기 워크플로우를 구성해야 합니다. 최대 4시간마다 실행하는 것이 좋습니다.
* 대상 [!DNL Campaign] v8.4 Adobe 활용 가능 [!DNL Campaign] Experience Platform의 Managed Services 소스 커넥터를 사용하여 Campaign의 게재 및 추적 이벤트를 Experience Platform에 동기화할 수 있습니다. 다음을 참조하십시오. [소스 커넥터](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ko) 자세한 내용은 설명서를 참조하십시오.

### 모바일 푸시 구성(선택 사항)

1. 구현 [!DNL Experience Platform] Mobile SDK를 사용하여 푸시 토큰 및 로그인 정보를 수집하여 알려진 고객 프로필에 다시 연결합니다.
1. 다음 확장을 사용하여 Adobe 태그를 활용하고 모바일 속성을 만들 수 있습니다.
   * Adobe [!DNL Journey Optimizer] | Adobe [!DNL Campaign Classic] | Adobe [!DNL Campaign Standard]
   * Adobe [!DNL Experience Platform] [!DNL Edge Network]
   * 다음에 대한 ID [!DNL Edge Network]
   * Mobile Core
1. 모바일 앱 배포와 웹 배포를 위한 전용 데이터스트림이 있는지 확인합니다.
1. 자세한 내용은 [Adobe Journey Optimizer Mobile 안내서](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer).

   >[!IMPORTANT]
   >Journey Optimizer를 통해 실시간 커뮤니케이션을 보내고 Campaign을 통해 일괄 푸시 알림을 보내려는 경우 Journey Optimizer와 Campaign 양쪽에서 모바일 토큰을 수집해야 할 수 있습니다. Campaign v8에서 푸시 토큰을 캡처하려면 Campaign SDK를 단독으로 사용해야 합니다.

## 관련 설명서

* [Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko)
* [Journey Optimizer 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)
* [Campaign v8 설명서](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=ko)
