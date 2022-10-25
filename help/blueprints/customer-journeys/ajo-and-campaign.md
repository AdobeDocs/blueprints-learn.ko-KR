---
title: Journey Optimizer와 Adobe Campaign 블루프린트
description: Adobe Journey Optimizer를 Adobe Campaign과 함께 사용하여 앱 내에서 메시지를 보내는 방법을 설명합니다. Campaign의 실시간 메시지 서버를 활용합니다.
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 076446a9-dfb9-464c-a04f-6864b8cb7b48
source-git-commit: 6901596cbb661ffa8cf57c6ae958db1978bf1520
workflow-type: ht
source-wordcount: '504'
ht-degree: 100%

---

# Journey Optimizer와 Adobe Campaign

Adobe Journey Optimizer를 Adobe Campaign과 함께 사용하여 앱 내에서 메시지를 보내는 방법을 설명합니다. Campaign의 실시간 메시지 서버를 활용합니다.

<br>

## 아키텍처

<img src="assets/ajo-campaign-architecture.svg" alt="Journey Optimizer 블루프린트 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>Journey Optimizer와 Campaign을 둘 다 사용하여 별도로 메시지를 보낼 수 있지만, 고민해야 하는 몇 가지 기술적 고려 사항이 있습니다. 이 방법을 사용하려면 영업 전 단계 기업 아키텍트와 협력하여 구현을 지원하는 데 필요한 사항을 이해해야 합니다.

<br>

## 필요 조건

### Adobe Experience Platform

* Journey Optimizer 데이터 소스를 구성하려면 먼저 시스템에서 스키마와 데이터 세트를 구성해야 합니다.
* [경험 이벤트] 클래스 기반 스키마의 경우 규칙 기반 이벤트가 아닌 이벤트를 트리거하려면 [Orchestration eventID 필드 그룹]을 추가해야 합니다.
* [개별 프로필] 클래스 기반 스키마의 경우 Journey Optimizer에서 사용할 테스트 프로필을 로드할 수 있도록 하려면 [프로필 테스트 세부 정보] 필드 그룹을 추가해야 합니다.
* Journey Optimizer와 Campaign은 동일한 IMS 조직에 공급됩니다.

### Campaign v7/v8 또는 Campaign Standard

* 실시간 메시지 서비스(=[메시지 센터])의 실행 인스턴스는 Adobe Managed Cloud Services에서 호스팅해야 합니다.
* 모든 메시지 작성은 Campaign 인스턴스 자체에서 수행합니다.

<br>

## 가드레일

[Journey Optimizer 가드레일 제품 링크](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ko)

### 그 외의 Journey Optimizer 가드레일

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
* 비즈니스 이벤트는 지원하지 않습니다.
* 서드파티 시스템으로의 아웃바운드 통합
   * 멀티 테넌트 인프라를 사용하므로 단일 고정 IP를 지원하지 않습니다(모든 데이터 센터의 IP를 허용 목록에 추가해야 함).
   * 사용자 정의 작업에는 POST 및 PUT 메서드만 지원됩니다.
   * 인증 지원: 토큰 | 암호 | OAuth2
* 다양한 샌드박스 간에 Adobe Experience Platform 또는 Journey Optimizer의 개별 구성 요소를 패키징하여 이동할 수 없습니다. 새로운 환경에서는 다시 구현해야 합니다.

<br>

### Campaign 통합

사용하시는 Adobe Campaign 버전과 Adobe Journey Optimizer와의 통합에 대한 지침은 각 Adobe Campaign 버전별로 해당하는 안내서를 참조하세요.

* [Adobe Journey Optimizer와 Campaign v7](ajo-and-campaign-v7.md)
* [Adobe Journey Optimizer와 Campaign v8](ajo-and-campaign-v8.md)