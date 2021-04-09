---
title: 트리거된 메시지 및 Adobe Experience Platform 블루프린트
description: Adobe Experience Platform을 중앙 허브 스트리밍 데이터, 고객 프로파일 및 세그먼테이션으로 사용하여 트리거된 메시지와 경험을 실행할 수 있습니다.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
translation-type: tm+mt
source-git-commit: 2404d871a852df8fed3adb97a79cc15e994db762
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---

# 트리거된 메시지 및 Adobe Experience Platform 블루프린트

Adobe Experience Platform을 중앙 허브 스트리밍 데이터, 고객 프로파일 및 세그먼테이션으로 사용하여 트리거된 메시지와 경험을 실행할 수 있습니다.

## 사용 사례

* 트리거된 메시지
* 등록 확인
* 장바구니 및 애플리케이션 양식 포기
* 위치 트리거된 메시지

## 아키텍처

<img src="assets/triggered.svg" alt="트리거된 메시징 및 Adobe Experience Platform 시나리오에 대한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 통합 패턴

* Adobe Experience Platform -> Journey Orchestration

## 사전 요구 사항

* Adobe Experience Platform
* Journey Orchestration

## 가드레일

### Journey Orchestration

* 제한 사항](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en#starting-with-journeys)에 대한 자세한 내용은 [링크를 참조하십시오.
* 호출은 API 설정을 통해 사용할 수 있으므로 대상 시스템의 채도가 실패 지점까지 도달하지 않습니다. 캡처한 것은 캡을 초과하는 메시지가 완전히 삭제되고 전송되지 않음을 의미합니다. 조절이 아직 지원되지 않습니다.
   * 최대 연결:대상이 처리할 수 있는 최대 http/s 연결 수
   * 최대 호출 수:periodInMs 매개 변수에서 수행할 최대 호출 수
   * periodInMs:시간(밀리초)
* 세그먼트 멤버십에서 시작된 여정은 다음 두 가지 모드에서 작동할 수 있습니다.
   * 일괄 세그먼트(24시간마다 새로 고침)
   * 스트리밍 세그먼트(5분 자격 조건)
* 세그먼트 일괄 처리:자격이 있는 사용자의 일별 볼륨을 이해하고 대상 시스템이 여정과 모든 여정에 대해 버스트 처리량을 처리할 수 있는지 확인합니다.
* 스트리밍 세그먼트:프로파일 자격 증명의 초기 버스트를 여정당 일일 스트리밍 자격 볼륨 및 모든 여정에서 처리할 수 있는지 확인
* 최종 대상은 REST API 및 JSON 페이로드를 지원해야 합니다.
* 현재 Offer decisioning을 지원하지 않음
* Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)에 대한 [프로필 및 데이터 통합 지침을 참조하십시오.

### Campaign Standard

* 처리량에서 14tps(시간당 50k)만 지원할 수 있습니다.
* 세그먼트 멤버십으로 시작된 여정은 지원되지 않습니다.
* 트랜잭션 메시지 열기/클릭에 대한 반응 이벤트는 Journey Orchestration 내에서 지원됩니다.
* 트랜잭션 메시지 로그는 현재 Experience Platform에 기본적으로 동기화되지 않으므로 수동으로 구성해야 합니다. 4시간마다 로그를 내보내는 것이 좋습니다.


## 구현 단계

### Adobe Experience Platform

#### 스키마/데이터 집합

1. 고객이 제공한 데이터를 기반으로 Experience Platform에서 개별 프로필, 경험 이벤트 및 다중 엔터티 스키마를 구성합니다.
1. 다음에 대한 캠페인 스키마 만들기:broadLog, trackingLog, 비제공 주소 및 프로필 환경 설정(선택 사항).
1. 거버넌스를 위해 데이터 세트에 데이터 사용 레이블을 추가합니다.
1. 대상에 대한 거버넌스를 적용할 정책을 만듭니다.

#### 프로필/ID

1. 고객별 네임스페이스를 만듭니다.
1. 스키마에 ID를 추가합니다.
1. 프로필에 대한 스키마 및 데이터 세트를 활성화합니다.
1. [!UICONTROL 실시간 고객 프로필](선택 사항)의 다른 보기에 대한 병합 규칙을 설정합니다.
1. 캠페인 사용을 위한 세그먼트를 만듭니다.

#### 소스/대상

1. 스트리밍 API 및 소스 커넥터를 사용하여 데이터를 Experience Platform에 인제스트합니다.
1. [!DNL Azure] Blob 저장소 대상을 캠페인과 함께 사용하도록 구성합니다.

#### 모바일 앱 배포

1. Campaign Standard용 Campaign Classic 또는 Experience Platform SDK용 캠페인 SDK를 구현합니다. Experience Platform Launch이 있는 경우 Campaign Classic/표준 확장을 Experience Platform SDK와 함께 사용하는 것이 좋습니다.


### Journey Orchestration

1. 오케스트레이션 ID를 얻으려면 먼저 Journey Orchestration 내에 고객 여정을 시작하는 데 사용되는 스트리밍 데이터를 구성해야 합니다. 그런 다음 통합 작업에 사용할 수 있도록 이 통합 ID를 개발자에게 제공합니다.
1. 외부 데이터 소스를 구성합니다.
1. 사용자 지정 작업을 구성합니다.

### Campaign Standard

1. 적절한 개인화 설정으로 메시징 템플릿을 구성합니다.
1. 트랜잭션 메시지 로그를 내보내는 내보내기 워크플로우를 구성합니다. 권장 사항은 4시간마다 실행되어야 합니다.


## 관련 설명서

* [Adobe Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Orchestration 설명서](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Campaign Classic 설명서](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard 설명서](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
