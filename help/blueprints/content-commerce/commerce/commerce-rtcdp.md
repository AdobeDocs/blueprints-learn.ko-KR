---
title: Adobe Commerce - RTCDP 블루프린트
description: Adobe Experience Platform과 Adobe Commerce을 통합하여 고객에 대한 단일 뷰를 제작하고 디지털 상점 및 여러 채널에서 경험을 지능적으로 개인화할 수 있습니다.
solution: Real-Time Customer Data Platform, Commerce
exl-id: e2fc5e1c-c865-4c24-9b82-861a34aba487
source-git-commit: 80a4716a7ed64ec30b9c60b3444affc5bd8984e4
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 1%

---

# Adobe Commerce 및 RTCDP

[!DNL Data Connection] 확장을 사용하면 Adobe Commerce 고객이 Adobe Experience Platform과 원활하게 통합하여 고객 프로필을 강화하고 디지털 상점 및 기타 채널에서 경험을 개인화할 수 있습니다.

## 기술 기능 활성화됨

* 모든 Adobe Experience Cloud 제품으로 수집 및 전송된 상점 데이터(장바구니에 추가, 장바구니 포기 등과 같은 클라이언트측)입니다.
* 모든 Adobe Experience Cloud 제품에 대한 백오피스 주문 상태
* 백오피스 내역 주문을 Adobe Experience Platform으로 전송할 수 있습니다.
* Adobe Commerce에 RTCDP 대상 공유 및 개인화

## 필요 조건

[!DNL Data Connection] 확장을 사용하려면 다음 항목이 있어야 합니다.

* Adobe Commerce 2.4.4 이상
* Adobe ID 및 조직 ID
* Adobe Experience Platform/RTCDP
* [ACDL(Adobe 클라이언트 데이터 레이어)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=ko). ACDL은 상점 이벤트 데이터를 수집하는 데 필요합니다.

## 온보딩 단계

### Adobe Commerce에서 Adobe Experience Platform으로 데이터 수집

* [!DNL Data Connection] 확장을 [설치](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html?lang=ko)합니다.
* 조직 ID를 확인하려면 Adobe 계정에 [로그인](https://helpx.adobe.com/kr/manage-account/using/access-adobe-id-account.html)하고 보세요. 조직 ID 는 공급된 Experience Cloud 회사와 연결된 ID입니다. 이 ID는 24자의 영숫자 문자열과 @AdobeOrg(포함 필수)로 구성됩니다.
* Commerce 관련 필드 그룹으로 XDM 스키마를 [만들거나 업데이트](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html?lang=ko)합니다.
* 만들거나 업데이트한 스키마를 기준으로 [데이터 집합을 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=ko#create-a-dataset). 이 데이터 세트에는 전송하는 Commerce 데이터가 포함됩니다.
* [데이터 스트림을 만들고](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/overview.html?lang=ko) Commerce 관련 필드 그룹이 포함된 XDM 스키마를 선택합니다.
* [Commerce 서비스에 연결](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=ko).
* [Adobe Experience Platform에 연결](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html?lang=ko).

### 대상 공유를 위해 Adobe Experience Platform에서 Commerce 대상에 연결

Adobe Commerce 대상에 연결하려면 다음 작업을 수행하십시오.

* [Adobe Experience Platform 인터페이스](https://experience.adobe.com/platform/)에서 대상 > 카탈로그로 이동합니다.
* Personalization을 선택합니다.
* Adobe Commerce 대상을 선택하여 강조 표시한 다음 설정을 선택합니다.
* [대상 구성 자습서](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=ko)에 설명된 단계를 따르십시오.

## 기본 데이터

* Storefront(브라우저/앱) 이벤트
* 백오피스 이벤트
* 이전 순서 데이터

지원되는 전체 이벤트 목록은 [Commerce 이벤트](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/event-forwarding/events.html?lang=ko)를 참조하십시오.

## 아키텍처

<img src="../commerce/assets/commerce_rtcdp.png" alt="Adobe Commerce RTCDP 아키텍처" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 관련 구현 안내서

| 안내서 | 링크 |
|:----|:----|
| 플랫폼 커넥터 | [Adobe Commerce Experience Platform 커넥터 개요](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/overview.html?lang=ko) |
| Commerce 대상 | [RTCDP의 Adobe Commerce 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-commerce.html?lang=ko) |
| Edge Personalization | [Edge 개인화 대상에 대상 활성화](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations.html?lang=ko) |
