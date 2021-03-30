---
title: 멀티채널 메시지 통합 계획
description: 다양한 화면에서 개인화된 적시에 고객 경험을 제공할 수 있습니다.
solution: Experience Platform
kt: null
thumbnail: null
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# 멀티채널 메시지 통합 계획

멀티채널 메시지 통합 운영 청사진은 고객이 이메일, SMS 및 모바일 알림과 같은 채널을 통해 사전에 고객의 참여를 유도하고 고객과 소통하는 방법을 보여줍니다.

통합 운영 툴은 대상 상태를 다른 채널의 의사 결정 엔진과 공유하여 웹 및 모바일 개인화를 위해 인바운드 채널과 같은 다른 인터랙션 채널과 통합할 수 있습니다. 고객 인터랙션이 트리거 기반인지 예약적인지, 타깃팅 및 개인화에 필요한 데이터 등과 같이 사용할 애플리케이션 및 배포 옵션을 결정하는 데 다양한 요소가 도움이 됩니다. 이러한 요소는 메시지 통합 기능을 빌드할 때 다양한 가능한 시나리오 및 배포 옵션을 초래합니다.

## 시나리오


| 시나리오 | 설명 | Experience Cloud 애플리케이션 |
|---|---|---|
| **일괄 처리 및 트랜잭션 메시지** | <ul><li>예약된 아웃바운드 및 일괄적으로 아웃바운드 캠페인 작성 및 실행</li><li>트랜잭션 메시지 전달</li></ul> | <ul><li>Adobe Campaign Classic 및 Managed Services</li><li>Adobe Campaign Standard</li></ul> |
| **[일괄 메시징 및 Adobe Experience Platform](batch-messaging.md)** | <ul><li>고객 프로필 및 세분화를 위한 중앙 허브로 Adobe Experience Platform을 사용하여 예약 및 일괄 메시징 캠페인 실행</li></ul> | <ul><li>실시간 고객 데이터 플랫폼</li><li>Adobe Campaign Classic, Managed Services 또는 Campaign Standard</li><li>지원되는 타사 메시징 공급자</li></ul> |
| **[트리거된 메시지 및 Adobe Experience Platform](triggered-messaging.md)** | <ul><li>스트리밍 여정 통합 및 메시지 전달을 위한 Journey Orchestration과 함께 스트리밍 데이터, 고객 프로파일 및 세그멘테이션을 위한 중앙 허브로 Adobe Experience Platform을 사용하여 트리거 및 스트리밍 메시지를 실행할 수 있습니다</li></ul> | <ul><li>Adobe Experience Platform</li><li>Journey Orchestration</li><li>메시지 전달을 위한 Adobe Campaign 또는 기타 타사 애플리케이션</li></ul> |
