---
title: Adobe Customer Journey Analytics 및 Adobe Journey Optimizer 통합
description: Adobe Customer Journey Analytics에서 Adobe Journey Optimizer 캠페인 및 여정 통찰력을 분석하고 여정 실행을 위해 대상자를 다시 게시하기 위한 아키텍처입니다.
solution: Customer Journey Analytics, Journey Optimizer, Experience Platform
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%
---
# Adobe Customer Journey Analytics 및 Adobe Journey Optimizer 통합

이 아키텍처는 Adobe Journey Optimizer 전달 및 상호 작용 데이터가 캠페인 및 여정 통찰력을 위해 Adobe Experience Platform을 통해 Customer Journey Analytics으로 어떻게 이동하는지를 보여 줍니다. Customer Journey Analytics에서 만든 대상은 Journey Optimizer 실행에 사용할 수 있도록 Real-Time CDP을 통해 게시할 수 있습니다.

## Campaign 및 여정 통찰력 아키텍처

아키텍처는 보고, 분석 및 대상 생성을 위해 Journey Optimizer 전달 및 상호 작용 데이터를 Experience Platform 및 Customer Journey Analytics과 연결합니다.

![Adobe Customer Journey Analytics 및 Adobe Journey Optimizer 통합 아키텍처](assets/cja_ajo_integration.png){width="1000" zoomable="yes"}

## 기본 데이터 흐름 및 통합 지점

- Journey Optimizer 게재, 상호 작용 및 효율성 데이터는 Experience Platform 데이터 서비스에 공유됩니다.
- Experience Platform 데이터는 CJA 연결을 통해 Customer Journey Analytics에 수집됩니다.
- Customer Journey Analytics 데이터 보기 및 분석은 campaign 및 여정 insight을 제공합니다.
- Customer Journey Analytics에서 작성된 대상은 Real-Time CDP에 게시됩니다.
- Real-Time CDP 대상은 Journey Optimizer 여정 실행 및 개인화에 사용할 수 있습니다.

## 지원되는 사용 사례 패턴

- [Customer analytics 및 insight 생성](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md) - 채널 전반의 캠페인 및 여정 동작을 분석합니다.
- [이벤트 트리거 메시지](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) - 고객 및 여정 신호를 사용하여 오케스트레이션된 메시지를 지원합니다.

## 추가 읽기

- [Journey Optimizer 보고](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/reporting/reports/sharing-overview)
- [Customer Journey Analytics 개요](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-overview/cja-overview)
- [Customer Journey Analytics 대상 게시](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/cja-components/audiences/publish)
