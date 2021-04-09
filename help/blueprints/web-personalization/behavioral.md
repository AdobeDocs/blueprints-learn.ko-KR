---
title: 행동 웹 개인화 블루프린트
description: 온라인 행동 및 고객 데이터를 기반으로 개인화
solution: Experience Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7085thumb-web-personalization-scenario1.jpg
exl-id: b9882c2c-cb45-4efa-a85c-8fe48f641a12
translation-type: tm+mt
source-git-commit: 2343151a1ed5374c299fb9317f6282c232d5d23b
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# 행동 웹 개인화 블루프린트

온라인 행동 및 고객 데이터를 기반으로 개인화

## 사용 사례

* 랜딩 페이지 최적화
* 행동 타깃팅
* 이전 제품/컨텐츠 보기, 제품/컨텐츠 선호도, 환경 특성, 제3자 고객 데이터 및 인구 통계학적 정보를 기반으로 개인화

## 애플리케이션

* Adobe Target
* Adobe Analytics(선택 사항)
* Adobe Audience Manager(선택 사항)

## 아키텍처

<img src="assets/personalization.svg" alt="행동 웹 개인화 시나리오에 대한 참조 아키텍처" style="border:1px solid #4a4a4a" />


## 가드레일

기본적으로 세그먼트 공유 서비스를 사용하면 각 Adobe Analytics 보고서 세트에 대해 최대 75명의 대상을 공유할 수 있습니다. 대상 공유에 Audience Manager이 사용되는 경우 공유할 수 있는 대상 수에 제한이 없습니다. 

## 구현 패턴

웹/모바일 개인화 청사진은 아래에 설명된 다음 접근 방식을 통해 구현할 수 있습니다.

1. 플랫폼 웹 SDK/모바일 SDK 및 Edge 네트워크 사용.
1. 기존의 애플리케이션별 SDK 사용(예: AppMeasurement.js)

### 1. 플랫폼 웹/모바일 SDK 및 Edge 방식

<img src="assets/websdkflow.svg" alt="플랫폼 웹 SDK/모바일 SDK 및 Edge 네트워크 접근 방식을 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

### 2. 애플리케이션별 SDK 방식

<img src="assets/appsdkflow.png" alt="애플리케이션별 SDK 접근 방식의 참조 아키텍처" style="border:1px solid #4a4a4a" />




## 구현 전제 조건

| 애플리케이션/서비스 | 필수 라이브러리 | 참고 사항 |
|---|---|---|
| Adobe Target | 플랫폼 웹 SDK*, at.js 0.9.1+ 또는 mbox.js 61+ | mbox.js가 더 이상 개발되지 않으므로 at.js가 선호됩니다. |
| Adobe Audience Manager(선택 사항) | 플랫폼 웹 SDK* 또는 dil.js 5.0+ |  |
| Adobe Analytics(선택 사항) | 플랫폼 웹 SDK* 또는 AppMeasurement.js 1.6.4+ |  |
| Experience Cloud ID 서비스 | 플랫폼 웹 SDK* 또는 VisitorAPI.js 2.0+ |  |
| Experience Platform Mobile SDK(선택 사항) | iOS 및 Android™의 경우 4.11 이상 |  |
| Experience Platform 웹 SDK | 1.0, 현재 Experience Platform SDK 버전에는 Experience Cloud 응용 프로그램에 대해 아직 지원되지 않는 다양한 사용 사례가 있습니다](https://github.com/adobe/alloy/projects/5)[ |  |

## 구현 단계

1. [웹 또는 모바일 ](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) 애플리케이션에 대한 Adobe 타게팅을 구현합니다.

   Audience Manager 또는 Analytics를 사용하는 경우:

1. [Adobe Audience Manager 구현](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html)
1. [Adobe Analytics 구현](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
1. [Experience Cloud ID 서비스 구현](https://experienceleague.adobe.com/docs/id-service/using/implementation/implementation-guides.html)

   >[!NOTE]
   >
   >각 응용 프로그램은 Experience Cloud ID를 사용하고 동일한 Experience Cloud 조직에 속해 있어야 응용 프로그램 간에 대상 공유를 허용할 수 있습니다.

1. [사람 및 대상 공유 서비스에 대한 프로비저닝 요청(공유 대상)](https://www.adobe.com/go/audiences)
1. [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-build.html) 또는 [Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html) 및 [에서 세그먼트를 작성하고 Experience Cloud](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)(Audience Manager 또는 Adobe Analytics을 사용하는 경우)에 공유할 대상 구성
1. Adobe Target에서 대상을 사용할 수 있게 되면 Adobe Target](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)이 있는 [타깃팅 경험에 사용할 수 있습니다.

## 관련 설명서

* [Experience Cloud 대상](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html)
* [Adobe Target과 Audience Manager 통합](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-other-solutions/aam-target-integration.html)
* [Adobe Audience Manager을 통한 Adobe Analytics 세그먼트 공유](https://experienceleague.adobe.com/docs/analytics/components/segmentation/segmentation-workflow/seg-publish.html)


## 관련 블로그 게시물

* [[!DNL Blueprint for Web Personalization using Adobe Experience Platform Real-Time Customer Profile]](https://medium.com/adobetech/blueprint-for-web-personalization-using-adobe-experience-platform-real-time-customer-profile-fef2ce7a4b2f)
* [[!DNL Integrating Adobe Experience Platform Decisioning Engine with AEM Websites]](https://jaeness.medium.com/integrating-adobe-experience-platform-decisioning-engine-with-aem-websites-9c222acd12e2)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [[!DNL Implementing Adobe Experience Platform Real-Time Customer Profile through our “Customer Zero” Program]](https://medium.com/adobetech/implementing-adobe-experience-platform-real-time-customer-profile-through-our-customer-zero-32e7cd952896)
* [[!DNL How Adobe Experience Platform Can Help Customers Personalize Their Mobile Messaging in Real-Time with Journey Orchestration Service and a Mobile Messaging Vendor]](https://medium.com/adobetech/how-adobe-experience-platform-helped-a-client-personalize-their-mobile-messaging-in-real-time-with-7d634aefa098)
* [[!DNL Segmentation in Seconds: How Adobe Experience Platform Made Real-time Customer Profiles a Reality]](https://medium.com/adobetech/segmentation-in-seconds-how-adobe-experience-platform-made-real-time-customer-profiles-a-reality-a7a8552b0847)
