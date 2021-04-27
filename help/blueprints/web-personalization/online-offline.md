---
title: 온라인/오프라인 웹 개인화 블루프린트
description: 웹 개인화를 이메일 및 기타 알려지거나 알려지지 않은 채널 개인화와 동기화합니다.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7194thumb-web-personalization-scenario2.jpg
exl-id: 29667c0e-bb79-432e-af3a-45bd0b3b43bb
translation-type: tm+mt
source-git-commit: 2f35195b875d85033993f31c8cef0f85a7f6cccc
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 48%

---

# 온라인/오프라인 웹/모바일 개인화 블루프린트

웹 개인화를 이메일 및 기타 알려지거나 알려지지 않은 채널 개인화와 동기화합니다.

## 사용 사례

* 랜딩 페이지 최적화
* 행동 및 오프라인 프로필 타겟팅
* 이전 제품/콘텐츠 조회, 제품/콘텐츠 관련성, 환경 요인, 서드파티 대상자 데이터 및 인적 특성과 더불어 거래, 충성도 및 CRM 데이터 등 오프라인 인사이트와 모델에서 도출한 인사이트를 기반으로 한 개인화

## 애플리케이션

* [!UICONTROL Real-time Customer Data Platform]
* Adobe Target
* Adobe Audience Manager(선택 사항): 서드파티 대상자 데이터, co-op 기반 디바이스 그래프, Platform 세그먼트를 Adobe Analytics로 표면화하는 기능 및 Adobe Analytics 세그먼트를 Platform에서 표면화하는 기능 제공
* Adobe Analytics(선택 사항): 과거 행동 데이터 및 Adobe Analytics 데이터의 세밀한 세분화를 기반으로 세그먼트를 작성하는 기능 제공

## 아키텍처

<img src="assets/onoff.svg" alt="온라인/오프라인 웹 개인화 청사진을 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

### 세그먼트 평가 및 활성화 보장

| 세그멘테이션 유형 | 빈도 | 처리량 | 지연(세그먼트 평가) | 지연(세그먼트 활성화) |
|-|-|-|-||
| 가장자리 세그멘테이션 | Edge 세그멘테이션은 현재 베타 버전으로 제공되고 있으며 Adobe Target 및 Adobe Journey Optimizer을 통해 실시간으로 동일한 페이지 의사 결정을 위해 Experience Platform 에지 네트워크에서 유효한 실시간 세그멘테이션을 평가할 수 있습니다. |  | ~100ms | Adobe Target의 개인화, 에지 프로필의 프로필 조회 및 쿠키 기반 대상을 통한 활성화를 위해 즉시 사용할 수 있습니다. |
| 스트리밍 세그멘테이션 | 새로운 스트리밍 이벤트 또는 레코드를 실시간 고객 프로파일에 인제스트할 때마다 세그먼트 정의가 유효한 스트리밍 세그먼트입니다. <br>스트리밍 세그먼트  [기준에 ](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko) 대한 지침은 세그멘테이션 설명서를 참조하십시오. | 초당 최대 1,500개의 이벤트.  | ~ p95 &lt;5분 | 이러한 세그먼트 합산이 발생하면 몇 분 내에 Audience Manager 및 고객 공유 서비스에 공유되고 Adobe Target에서 동일한/다음 페이지 개인화에 사용할 수 있습니다. |
| 증분 세그먼테이션 | 마지막 증분 또는 일괄 세그먼트 평가 이후 실시간 고객 프로필로 인제스트한 새 데이터에 대해 시간당 한 번. |  |  | 이러한 세그먼트 멤버십이 실현되면 Audience Manager 및 고객 공유 서비스에 몇 분 내에 공유되고 Adobe Target에서 동일한/다음 페이지 개인화를 위해 사용할 수 있습니다. |
| 일괄 세그먼테이션 | 미리 결정된 시스템 세트 일정을 기준으로 하루에 한 번 또는 API를 통해 수동으로 시작한 애드혹. |  | 최대 10TB의 프로필 스토어 크기에 대해 작업당 약 1시간, 10TB에서 100TB까지의 프로필 스토어 크기에 대해 작업당 2시간. 일괄 세그먼트 작업 성능은 평가 중인 세그먼트 수 프로필, 프로필 크기 및 수에 따라 달라집니다. | 이러한 세그먼트 멤버십이 실현되면 Audience Manager 및 고객 공유 서비스에 몇 분 내에 공유되고 Adobe Target에서 동일한/다음 페이지 개인화를 위해 사용할 수 있습니다. |

### 애플리케이션 간 공유를 위한 보장


| 고객 공유 통합 패턴 | 세부 사항 | 빈도 | 처리량 | 지연(세그먼트 평가) | 지연(세그먼트 활성화) |
|-|-|-|-|-||
| 실시간 고객 데이터 플랫폼-Audience Manager |  | 세그멘테이션 유형에 따라 - 위의 세그멘테이션 가리기 테이블을 참조하십시오. | 세그멘테이션 유형에 따라 - 위의 세그멘테이션 가리기 테이블을 참조하십시오. | 세그멘테이션 유형에 따라 - 위의 세그멘테이션 가리기 테이블을 참조하십시오. | 세그먼트 평가가 완료된 후 몇 분 이내에<br>실시간 고객 데이터 플랫폼과 Audience Manager 간의 초기 고객 구성 동기화는 약 4시간이 소요됩니다.<br>4시간 동안 실현된 모든 고객 멤버십은 후속 배치 세그먼테이션 작업의 Audience Manager에 &quot;기존&quot; 대상 멤버십으로 기록됩니다. |
| Adobe Analytics에서 Audience Manager으로 | 기본적으로 각 Adobe Analytics 보고서 세트에 대해 최대 75명의 대상을 공유할 수 있습니다. Audience Manager 라이선스를 사용하는 경우 Adobe Analytics 및 Adobe Target 또는 Adobe Audience Manager과 Adobe Target 간에 공유할 수 있는 대상 수에 제한이 없습니다. |  |  |  |  |
| Adobe Analytics에서 실시간 고객 데이터 플랫폼으로 | 현재 사용할 수 없습니다. |  |  |  |  |

## 구현 패턴

웹/모바일 개인화 청사진은 아래에 설명된 다음 접근 방식을 통해 구현할 수 있습니다.

1. [!UICONTROL 플랫폼 웹 SDK] 또는 [!UICONTROL 플랫폼 모바일 SDK] 및 [!UICONTROL 에지 네트워크] 사용
1. 기존의 애플리케이션별 SDK 사용(예: AppMeasurement.js)

### 1. 플랫폼 웹/모바일 SDK 및 Edge 방식

<img src="assets/websdkflow.svg" alt="[!UICONTROL Platform Web SDK] 또는 [!UICONTROL Platform Mobile SDK] 및 [!UICONTROL Edge Network] 접근 방식에 대한 참조 아키텍처" style="border:1px solid #4a4a4a" />

### 2. 애플리케이션별 SDK 방식

<img src="assets/appsdkflow.png" alt="특정 애플리케이션용 SDK를 사용할 때의 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 구현 필요 조건

| 애플리케이션/서비스 | 필요한 라이브러리 | 참고 사항 |
|---|---|---|
| Adobe Target | [!UICONTROL 플랫폼 웹 SDK]*, at.js 0.9.1+ 또는 mbox.js 61+ | mbox.js는 더 이상 개발되지 않으므로 at.js 사용을 추천합니다. |
| Adobe Audience Manager(선택 사항) | [!UICONTROL 플랫폼 웹 SDK]* 또는 dil.js 5.0+ |  |
| Adobe Analytics(선택 사항) | [!UICONTROL 플랫폼 웹 SDK]* 또는 AppMeasurement.js 1.6.4+ | Adobe Analytics 추적에는 RDC(지역 단위 데이터 수집)를 사용해야 합니다. |
| Experience Cloud ID 서비스 | [!UICONTROL 플랫폼 웹 SDK]* 또는 VisitorAPI.js 2.0+ | (추천)ID 서비스 배포에 Experience Platform Launch를 사용하여 반드시 애플리케이션 호출 발생 이전에 ID가 설정되도록 합니다. |
| Experience Platform 모바일 SDK(선택 사항) | iOS 및 Android™용 4.11 이상 |  |
| Experience Platform 웹 SDK | 1.0, 현재 Experience Platform SDK 버전에는 [아직 Experience Cloud 애플리케이션에서 지원하지 않는 다양한 사용 사례](https://github.com/adobe/alloy/projects/5)가 있습니다. |  |


## 구현 단계

1. 웹 또는 모바일 애플리케이션에 [Adobe Target 구현](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html?lang=ko)
1. [Adobe Audience Manager 구현](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html?lang=ko)(선택 사항)
1. [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=ko)(선택 사항)
1. [[!UICONTROL Experience Platform 및 Real-time Customer Profile 구현]](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=ko)
1. [Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html?lang=ko) 또는 [Experience Platform 웹 SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ko) 구현
   >[!NOTE]
   >
   >애플리케이션 간에 대상자를 공유하려면 각 애플리케이션이 Experience Cloud ID를 사용해야 하며 동일한 Experience Cloud 조직의 일부여야 합니다.
1. [Experience Platform과 Adobe Target 간 대상자 공유를 위한 제공 요청(공유 대상자)](https://www.adobe.com/go/audiences)

## 관련 설명서

* [Experience Platform 세그먼트를 Audience Manager 및 기타 Experience Cloud 솔루션에 공유하기](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=ko)
* [Experience Platform 세분화 개요](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ko)
* [세분화 스트리밍](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Experience Platform 세분화 작성기 개요](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=ko)
* [Audience Manager 소스 커넥터](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ko)
* [Adobe Audience Manager을 통한 Adobe Analytics 세그먼트 공유](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html?lang=ko)
* [Experience Platform 웹 SDK 설명서](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Experience Cloud ID 서비스 설명서](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=ko)
* [Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=ko)

## 관련 블로그 게시물

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL Adobe Experience Platform’s Identity Service — How to Solve the Customer Identity Conundrum]](https://medium.com/adobetech/adobe-experience-platforms-identity-service-how-to-solve-the-customer-identity-conundrum-f95e22d16ea9)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
* [[!DNL Build an Optimal Online Experience: Enrich Unified Profile with Query Service]](https://medium.com/adobetech/build-an-optimal-online-experience-enrich-unified-profile-with-query-service-8027c196ab33)
