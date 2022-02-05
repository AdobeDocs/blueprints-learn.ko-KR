---
title: Campaign v7 블루프린트
description: Adobe Campaign v7는 이메일 및 DM과 같은 기존 마케팅 채널을 위한 캠페인 도구입니다. 완벽한 캠페인을 제작 및 조정하는 데 도움이 되는 강력한 ETL 및 데이터 관리 기능을 제공합니다. 오케스트레이션 엔진은 배치 기반 여정에 핵심 포커스를 둔 풍부한 멀티 터치 마케팅 프로그램을 제공합니다.  또한 마케팅 팀이 암호 재설정, 주문 확인, 전자 수신 등의 작업에 대해 모든 IT 시스템의 모든 포함 페이로드를 기반으로 사전 정의된 메시지를 전송할 수 있도록 해주는 실시간 메시징 서버와 나란히 제공됩니다.
solution: Campaign Classic v7
exl-id: 71c808f5-59e6-4f49-a6ba-581ed508bc04
source-git-commit: 0c072465c2cac954631fe3a8dbdcef280ee397ab
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 3%

---

# Campaign v7 블루프린트

Adobe Campaign v7는 이메일 및 DM과 같은 기존 마케팅 채널을 위한 캠페인 도구입니다. 완벽한 캠페인을 제작 및 조정하는 데 도움이 되는 강력한 ETL 및 데이터 관리 기능을 제공합니다. 오케스트레이션 엔진은 배치 기반 여정에 핵심 포커스를 둔 풍부한 멀티 터치 마케팅 프로그램을 제공합니다.  또한 마케팅 팀이 암호 재설정, 주문 확인, 전자 수신 등의 작업에 대해 모든 IT 시스템의 모든 포함 페이로드를 기반으로 사전 정의된 메시지를 전송할 수 있도록 해주는 실시간 메시징 서버와 나란히 제공됩니다.

<br>

## 사용 사례

* 일괄 처리 기반 메시징 프로그램
* 캠페인 시작 및 재실행
* DM 광고, 브로셔 및 매거진 캠페인
* 낮은 볼륨 단순 트랜잭션 메시지(예: 암호 재설정, 이메일 영수증, 주문 확인 등)

<br>

## 아키텍처

<img src="assets/campaign-v7-architecture.svg" alt="Campaign v7 블루프린트에 대한 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 통합 패턴

| 시나리오 | 설명 | 기능 |
| :-- | :--- | :--- |
| [Journey Optimizer과 Adobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizer을 사용하여 실시간 고객 프로필을 활용하여 1:1 경험을 조정하고 기본 Adobe Campaign 트랜잭션 메시지 시스템을 활용하여 메시지를 보내는 방법을 보여줍니다 | Journey Optimizer의 실시간 고객 프로필 및 기능을 활용하여 현재 경험을 조정하고 Adobe Campaign의 기본 실시간 메시징 기능을 활용하여 마지막 마일 커뮤니케이션을 수행합니다<br><br>고려 사항:<br><ul><li>실시간 메시지 서버를 통해 시간당 최대 5만 개의 메시지를 전송할 수 있습니다<li>Pre-Sales Enterprise Architect에서 기술 검토를 위해 Journey Optimizer에서 제한이 수행되지 않습니다.</li><li>offer decisioning은 Campaign v7 실시간 메시징 서버에 대한 페이로드에서 지원되지 않습니다</li></ul> |
| [Real-Time CDP과 Adobe Campaign](rtcdp-and-campaign.md) | Adobe Experience Platform의 Real-Time CDP 및 중앙 집중식 세그멘테이션 도구를 Adobe Campaign과 사용하여 개인화된 대화를 제공하는 방법을 소개합니다 | <ul><li>클라우드 스토리지 파일 교환 및 Adobe Campaign 수집 워크플로우를 사용하여 Real-Time CDP에서 Adobe Campaign으로 대상 공유 </li><li>고객 대화의 전달 및 상호 작용 데이터를 Adobe Campaign에서 실시간 CDP로 쉽게 공유하여 실시간 고객 프로필을 향상시키고 메시징 캠페인에 대한 크로스 채널 보고를 제공합니다</li></ul> |

<br>

## 필요 조건

### 응용 프로그램 서버 및 실시간 메시징 서버

* Campaign v8 소프트웨어를 상호 작용하고 사용하려면 Adobe Campaign 클라이언트 콘솔이 필요합니다. Windows 기반 클라이언트이며 표준 인터넷 프로토콜(SOAP, HTTP 등)을 사용합니다. 소프트웨어를 배포, 설치 및 실행하기 위해 조직에서 필요한 권한을 사용하도록 설정해야 합니다

* IP 주소 허용 목록
   * 클라이언트 콘솔에 액세스하는 동안 모든 사용자가 활용할 IP 범위를 식별합니다
   * 실시간 메시징 서버에 연결할 수 있는 엔터프라이즈 시스템을 확인하고 사용자가 허용 목록할 수 있는 정적으로 할당된 IP 또는 범위가 있는지 확인합니다
   * Campaign Campaign 컨트롤 패널을 통해 설정하고 제어할 수 있습니다
* sFTP 키 관리
   * 제공된 sFTP에서 Campaign에 사용할 수 있는 SSH 공개 키가 있습니다. Campaign Campaign 컨트롤 패널을 통해 설정하고 제어할 수 있습니다.

### 이메일

* 메시지 보내기에 사용할 하위 도메인을 준비하십시오
* 하위 도메인을 Adobe에 완전히 위임하거나(권장) CNAME을 사용하여 Adobe 특정 DNS 서버(사용자 지정)를 가리킬 수 있습니다
* Google TXT 레코드는 배달이 잘 되도록 각 하위 도메인에 필요합니다

### 모바일 푸시

* 모바일 앱을 배포, 구성 및 구축할 수 있는 모바일 개발자가 있습니까?
* Adobe은 FCM(Android) 및 APNS(iOS)에서 필요한 정보를 수집하여 메시지 페이로드를 해당 서버에 전송하는 SDK만 제공합니다. 모바일 앱의 코딩, 배포, 관리 및 디버깅을 수행하는 방법은 고객의 책임입니다

### 웹 앱(선택 사항)

* Campaign에서 호스팅하는 구독 취소 및 랜딩 페이지에 대한 추가 하위 도메인을 위임할 수 있습니다
* SSL 인증서가 적극 권장됩니다

<br>

## 가드레일

### 응용 프로그램 서버 크기 조정

* 최대 100M의 프로필로 스토리지 확장 가능
* Adobe Admin Console(권장)를 통해 또는 애플리케이션 자체에서 로컬로 사용자 액세스를 설정하고 제어합니다
* Campaign에 데이터를 로드하려면 배치 파일을 통해 해야 합니다
   * API 데이터 로드 지원은 주로 데이터베이스 내의 프로필 또는 단순 개체(예: 만들기 및 업데이트)를 관리하는 데 사용됩니다. 대량의 데이터 또는 일괄 처리 등과 같은 작업을 로드하는 데 사용되지 않습니다.
   * API를 사용하여 사용자 지정 애플리케이션 용도로 데이터를 읽을 수 없습니다
* API 호출은 초당 15개 또는 크기가 150k로 제한됩니다

### 배치 메시징 서버 크기 조정

* 시간당 최대 250만 개의 메시지를 처리하도록 확장 가능

### 실시간 메시징 서버 크기 조정

* 시간당 최대 5만 개의 메시지를 전송할 수 있습니다
* 기본적으로 두 개의 실시간 메시징 서버가 제공됩니다. 최대 8개의 실시간 메시징 서버를 확장할 수 있습니다.

### SMS 구성

* Campaign은 SMS 공급자와 통합하는 기능을 제공합니다. 공급자가 고객이 조달하고 SMS 기반 메시지 전송 캠페인과 통합됩니다
* SMPP 프로토콜을 통해 지원
* Adobe이 지원할 수 있는 세 가지 유형의 SMS가 있습니다.
   * SMS MT(모바일 종료됨): Adobe Campaign에서 SMPP 공급자를 통해 휴대폰에 내보내는 SMS입니다.
   * SMS MO(모바일이 시작됨): smpp 공급자를 통해 모바일에서 Adobe Campaign으로 전송되는 SMS입니다.
   * SMS SR(상태 보고서) 또는 DR 또는 DLR(게재 확인): sms를 성공적으로 수신했음을 나타내는 SMPP 공급자를 통해 모바일이 Adobe Campaign으로 보낸 반환 수신입니다. Adobe Campaign은 메시지를 배달할 수 없음을 나타내는 SR을 받을 수도 있으며, 이는 종종 오류에 대한 설명과 함께 제공됩니다.

### 모바일 푸시 구성

* 푸시 알림에 대해 모바일 장치와 통합하기 위해 지원되는 두 가지 방법:
   * Experience Platform Mobile SDK(권장)
   * Campaign Mobile SDK
* Experience Platform Mobile SDK 경로:
   * Experience Platform Mobile SDK와의 통합을 설정하기 위해 Adobe 태그 및 Campaign Classic 확장 활용
   * Adobe 태그 및 데이터 수집에 대한 실무 지식 필요
   * SDK를 배포하고 FCM(Android) 및 APNS(iOS)과 통합하여 푸시 토큰을 가져오고, 푸시 알림을 수신하고, 푸시 상호 작용을 처리하도록 앱을 구성하려면 Android 및 iOS 모두에서 푸시 알림과 함께 모바일 개발 경험이 필요합니다
* Campaign Mobile SDK
   * 액세스 권한을 얻으려면 Adobe 고객 지원 센터에 문의하십시오
   * 다음 내용을 따르십시오 [Campaign SDK 설명서](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=en) sdk 설치 및 구성 방법을 알아봅니다.

   >[!IMPORTANT]
   >Campaign SDK를 배포하고 다른 Experience Cloud 애플리케이션과 작업하는 경우, 사용자는 데이터 수집을 위해 Campaign Mobile SDK를 사용해야 합니다. 다른 SDK이므로 Campaign SDK와 함께 설치해야 합니다

<br>

## 구현 단계

자세한 내용은 [시작 안내서](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=en) Adobe Campaign v7 구현


## 관련 설명서

* [Campaign v7 설명서](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=ko)
* [Campaign v7 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
