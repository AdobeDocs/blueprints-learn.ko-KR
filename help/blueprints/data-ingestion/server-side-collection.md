---
title: 이벤트 전달 블루프린트
description: 수집된 데이터 스트리밍 기준 [!DNL Experience Platform] 대상에 대한 SDK
solution: Data Collection
kt: 7202
exl-id: 8d6f0705-628b-44e4-a3fc-da6c5e308a5b
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 55%

---

# 이벤트 전달 블루프린트

이벤트 전달 블루프린트는 Adobe으로 데이터가 수집되는 방식을 보여 줍니다 [!DNL Experience Platform] 웹 및 모바일 SDK는에서 전달할 수 있습니다. [!DNL Experience Platform] [!DNL Edge Network] 원하는 대상으로 이동합니다. SDK에서 수집한 원 데이터 전체를 전달하거나 태그 속성(이전 Launch)에서 구성한 바에 따라 이벤트 및 규칙을 기반으로 특정 데이터를 전달할 수 있습니다.

## 사용 사례

* 웹 또는 모바일에서 단일 수집 태그를 사용하여 데이터를 수집함으로써 클라이언트 브라우저 및 앱에 대한 코드 권한 요구를 줄입니다. 단일 데이터 수집 소스에서 수집한 데이터를 다양한 종점으로 전파합니다.
* 수집한 데이터와 비교하여 인사이트 및 애플리케이션을 구축할 수 있도록 수집한 데이터를 파트너 애플리케이션 또는 데이터 저장 위치로 전달합니다.

## 애플리케이션

* Adobe [!DNL Experience Platform] 데이터 수집

## 아키텍처

<img src="assets/enterprise_collection.svg" alt="엔터프라이즈 데이터 수집을 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" class="modal-image" />

## 관련 설명서

* [이벤트 전달 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko)
* [이벤트 전달 비디오](https://experienceleague.adobe.com/docs/launch-learn/tutorials/server-side/overview.html?lang=ko)
* 웹 SDK의 [이벤트 전달 레슨](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html?lang=ko) 튜토리얼

## 관련 블로그 게시물

* [Adobe을 통한 웹 사이트 성능 향상 [!DNL Experience Platform] Web SDK 및 [!DNL Edge Network]](https://medium.com/adobetech/boosting-website-performance-with-adobe-experience-platform-web-sdk-and-edge-network-329fcf70fdf9)
* [Adobe을 통한 구현 불만 사항 해결 [!DNL Experience Platform] Web SDK 및 [!DNL Edge Network]](https://medium.com/adobetech/solving-implementation-pain-points-with-adobe-experience-platform-web-sdk-and-edge-network-880b635e6819)
* [Adobe [!DNL Experience Platform] Audience Management용 Web SDK](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
* [Adobe [!DNL Experience Platform] Web SDK - Adobe Target](https://medium.com/adobetech/adobe-experience-platform-web-sdk-adobe-target-9b9f621d271)
* [Adobe [!DNL Experience Platform] Adobe Analytics용 웹 SDK 마이그레이션 시나리오](https://medium.com/adobetech/adobe-experience-platform-web-sdk-migration-scenarios-for-adobe-analytics-91c255ec82b0)
* [Adobe 통합 [!DNL Experience Platform] Adobe이 있는 서비스 [!DNL Experience Platform] 웹 SDK](https://medium.com/adobetech/unify-your-adobe-experience-platform-services-with-adobe-experience-platform-web-sdk-75cf6851a9fc)
* [Adobe을 통해 모바일 애플리케이션 개발 가속화 [!DNL Experience Platform] Mobile SDK 및 Launch](https://medium.com/adobetech/accelerate-your-mobile-application-development-with-adobe-experience-platform-mobile-sdk-and-launch-ed023536d611)
* [Adobe을 통해 고객 워크플로우 단순화 [!DNL Experience Platform] 웹 SDK](https://medium.com/adobetech/simplifying-customer-workflows-with-adobe-experience-platform-web-sdk-4e54fe134f4a)
