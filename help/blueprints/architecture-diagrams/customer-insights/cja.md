---
title: Real-time Customer Data Platform이 포함된 Customer Journey Analytics
description: Customer Journey Analytics에서 고객 여정 전반에 걸친 데이터 및 고객 행동을 통합하고 분석하여 대상자를 CJA에서 RTCDP로 게시
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
TQID: https://experienceleague.adobe.com/gbNXsco0cQIcn5O83ofB-rb0PF65v7kaTZ7mTngqHks
product_v2:
  - id: e98b7246-966c-4318-9e95-cad2f7a17dc7
    internal-label: Customer Journey Analytics
feature_v2:
  - id: ce577701-5b9e-4fe4-8fa3-4eedea976da4
    internal-label: Components
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 8%
---

# Adobe Customer Journey Analytics

Adobe Customer Journey Analytics은 Adobe Experience Platform 및 기타 소스의 고객 상호 작용 데이터를 여정 기반 분석 서비스로 통합합니다. 이 아키텍처는 크로스 채널 분석, B2B CJA 도출 및 CJA 대상을 Real-Time CDP에 게시하기 위한 핵심 참조를 제공합니다.

## Customer Journey Analytics 아키텍처

이 다이어그램은 연결, 데이터 보기, 분석 및 대상 생성을 위해 Customer Journey Analytics으로 고객 상호 작용 데이터의 핵심 흐름을 보여 줍니다.

![Adobe Customer Journey Analytics 핵심 아키텍처](assets/cja.png){width="1000" zoomable="yes"}

## 아키텍처 도출

- B2B Customer Journey Analytics은 계정 기반 분석을 위해 계정, 기회, 구매 그룹 및 개인 차원을 통해 핵심 아키텍처를 확장합니다.
- CJA 대상 공유는 활성화 및 다운스트림 여정 실행을 위해 Customer Journey Analytics에서 Real-Time CDP으로 만든 대상을 게시합니다.

## 기본 데이터 흐름 및 통합 지점

- 고객 상호 작용 데이터는 웹, 모바일, 상거래, CRM 및 기타 소스에서 Adobe Experience Platform으로 수집됩니다.
- Experience Platform 데이터 세트는 Customer Journey Analytics 연결에서 선택됩니다.
- 데이터 보기에는 채널 간 분석을 위한 지표, 차원 및 계산된 필드가 표시됩니다.
- Customer Journey Analytics 대상은 활성화를 위해 Real-Time CDP에 게시할 수 있습니다.
- Customer Journey Analytics insights는 전용 통합 아키텍처를 통해 Journey Optimizer과 함께 사용할 수 있습니다.

## 지원되는 사용 사례 패턴

- [B2B 분석](/help/blueprints/use-case-patterns/b2b/account-analytics.md) - B2B 차원을 사용하여 계정, 영업 기회 및 사용자 수준 여정을 분석합니다.
- [Customer analytics 및 insight 생성](/help/blueprints/use-case-patterns/analysis/customer-analytics-insight-generation.md) - 크로스 채널 동작을 분석하고 여정 통찰력을 생성합니다.

## 추가 읽기

- [Customer Journey Analytics 개요](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview)
- [Customer Journey Analytics 연결](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-connections/create-connection)
- [Customer Journey Analytics 대상 게시](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/audiences/publish)
