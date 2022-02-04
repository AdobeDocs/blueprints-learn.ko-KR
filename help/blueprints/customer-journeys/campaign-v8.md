---
title: Campaign v8 블루프린트
description: Adobe Campaign v8은 이메일 및 DM과 같은 기존 마케팅 채널을 위해 만들어진 차세대 캠페인 도구입니다. 완벽한 캠페인을 제작 및 조정하는 데 도움이 되는 강력한 ETL 및 데이터 관리 기능을 제공합니다. 오케스트레이션 엔진은 배치 기반 여정에 핵심 포커스를 둔 풍부한 멀티 터치 마케팅 프로그램을 제공합니다.  또한 마케팅 팀이 암호 재설정, 주문 확인, 전자 수신 등의 작업에 대해 모든 IT 시스템의 모든 포함 페이로드를 기반으로 사전 정의된 메시지를 전송할 수 있도록 해주는 확장 가능한 실시간 메시징 서버와 나란히 제공됩니다.
solution: Campaign v8
source-git-commit: 1c46cbdfc395de4fc9139966cf869ba1feeceaaa
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 3%

---

# Campaign v8 블루프린트

Adobe Campaign v8은 이메일 및 DM과 같은 기존 마케팅 채널을 위해 만들어진 차세대 캠페인 도구입니다. 완벽한 캠페인을 제작 및 조정하는 데 도움이 되는 강력한 ETL 및 데이터 관리 기능을 제공합니다. 오케스트레이션 엔진은 배치 기반 여정에 핵심 포커스를 둔 풍부한 멀티 터치 마케팅 프로그램을 제공합니다.  또한 마케팅 팀이 암호 재설정, 주문 확인, 전자 수신 등의 작업에 대해 모든 IT 시스템의 모든 포함 페이로드를 기반으로 사전 정의된 메시지를 전송할 수 있도록 해주는 확장 가능한 실시간 메시징 서버와 나란히 제공됩니다.

<br>

## 사용 사례

* 매우 복잡한 일괄 처리 기반 메시징 프로그램
* 캠페인 시작 및 재실행
* DM 광고, 브로셔 및 매거진 캠페인
* 간단한 트랜잭션 메시지(예: 암호 재설정, 이메일 영수증, 주문 확인 등)

<br>

## 아키텍처

<img src="assets/campaign-v8-architecture.svg" alt="Campaign v8 블루프린트에 대한 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 통합 패턴

| 시나리오 | 설명 | 기능 |
| :-- | :--- | :--- |
| [Journey Optimizer과 Adobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizer을 사용하여 실시간 고객 프로필을 활용하여 1:1 경험을 조정하고 기본 Adobe Campaign 트랜잭션 메시지 시스템을 활용하여 메시지를 보내는 방법을 보여줍니다 | Journey Optimizer의 실시간 고객 프로필 및 기능을 활용하여 현재 경험을 조정하고 Adobe Campaign의 기본 실시간 메시징 기능을 활용하여 마지막 마일 커뮤니케이션을 수행합니다<br><br>고려 사항:<br><ul><li>실시간 메시지 서버를 통해 시간당 최대 1M개의 메시지를 전송할 수 있습니다<li>Pre-Sales Enterprise Architect에서 기술 검토를 위해 Journey Optimizer에서 제한이 수행되지 않습니다.</li><li>offer decisioning은 Campaign v8의 페이로드에서 지원되지 않습니다</li></ul> |

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

* 최대 1B 프로필까지 확장할 수 있으며 최대 2,000M의 프로필로 스토리지를 확장할 수 있습니다
* Adobe Admin Console을 통한 사용자 액세스 설정 및 제어
* Campaign에 데이터를 로드하려면 배치 파일을 통해 해야 합니다
   * API 데이터 로드 지원은 주로 데이터베이스 내의 프로필 또는 단순 개체(예: 만들기 및 업데이트)를 관리하는 데 사용됩니다. 대량의 데이터 또는 일괄 처리 등과 같은 작업을 로드하는 데 사용되지 않습니다.
   * API를 사용하여 사용자 지정 애플리케이션 용도로 데이터를 읽을 수 없습니다
   * API를 통해 로드된 데이터는 애플리케이션 데이터베이스에서 준비된 다음 매시간마다 클라우드 데이터베이스에 복제됩니다
* API 호출은 초당 15개 또는 크기가 150k로 제한됩니다

### 배치 메시징 서버 크기 조정

* 시간당 최대 2,000만 개의 메시지를 처리하도록 확장 가능

### 실시간 메시징 서버 크기 조정

* 시간당 최대 1M개의 메시지를 전송할 수 있습니다
* 기본적으로 하나의 (1) 실시간 메시징 서버만 제공됩니다. 이는 서버와의 통신이 24시간 후에 만료되는 세션 토큰을 통해 수행되도록 하기 위한 것입니다
* 선택적으로 최대 8개의 실시간 메시징 서버를 배포할 수 있지만 인증은 사용자/전달만 지원합니다
* 가능하면 세션 토큰 기반 인증을 활용하기 위해 항상 하나의 실시간 메시징 서버를 사용하는 것이 좋습니다

### SMS 구성

* Campaign은 SMS 공급자와 통합하는 기능을 제공합니다. 공급자가 고객이 조달하고 SMS 기반 메시지 전송 캠페인과 통합됩니다
* SMPP 프로토콜을 통해 지원
* Adobe이 지원할 수 있는 세 가지 유형의 SMS가 있습니다.
   * SMS MT(모바일 종료됨): Adobe Campaign에서 SMPP 공급자를 통해 휴대폰에 내보내는 SMS입니다.
   * SMS MO(모바일이 시작됨): smpp 공급자를 통해 모바일에서 Adobe Campaign으로 전송되는 SMS입니다.
   * SMS SR(상태 보고서) 또는 DR 또는 DLR(게재 확인): sms를 성공적으로 수신했음을 나타내는 SMPP 공급자를 통해 모바일이 Adobe Campaign으로 보낸 반환 수신입니다. Adobe Campaign은 메시지를 배달할 수 없음을 나타내는 SR을 받을 수도 있으며, 이는 종종 오류에 대한 설명과 함께 제공됩니다.

### 모바일 푸시 구성

* Campaign v8에는 Campaign SDK만 지원됩니다. 액세스 권한을 얻으려면 Adobe 고객 지원 센터에 문의하십시오
* 다음 내용을 따르십시오 [Campaign SDK 설명서](https://experienceleague.adobe.com/docs/campaign-classic/using/sending-messages/sending-push-notifications/integrating-campaign-sdk-into-the-mobile-application.html?lang=en) sdk 설치 및 구성 방법을 알아봅니다.

   >[!IMPORTANT]
   >다른 Experience Cloud 애플리케이션에는 데이터 수집을 위해 Experience Platform Mobile SDK를 사용해야 합니다. 다른 SDK이므로 Campaign SDK와 함께 설치해야 합니다

<br>

## 구현 단계

시작 안내서 참조 [Adobe Campaign v8 구현](https://experienceleague.adobe.com/docs/campaign/campaign-v8/implement/implement.html?lang=en)


## 관련 설명서

* [Campaign v8 설명서](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=en)
* [Campaign v8 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-campaign-managed-cloud-services.html)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
