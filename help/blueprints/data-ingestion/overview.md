---
title: 데이터 수집 및 준비
description: 이 블루프린트에서는 Adobe Experience Platform에서 데이터를 수집하고 준비하는 방법을 모두 다룹니다.
solution: Data Collection
kt: 7204
thumbnail: null
exl-id: 5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 98%

---

# 데이터 수집 및 준비  블루프린트

데이터 준비 및 수집에서는 데이터를 준비하고 Adobe Experience Platform으로 수집하는 방법을 모두 다룹니다. 또한 Adobe Experience Platform의 Edge Network로 데이터를 수집하고 사이드 포워딩을 통해 엔터프라이즈 대상으로 이 데이터를 전달하는 기능도 다룹니다.

데이터를 준비할 때는 소스 데이터를 XDM(Experience Data Model) 스키마로 매핑하게 됩니다. 또한 데이터에 날짜 포맷 정리, 필드 분할/연결/전환 및 기록 연결/병합/재입력 등의 변환을 수행합니다. 데이터 준비를 통해 고객 데이터를 단일화하면 종합적이고 필터링된 분석 제공에 도움이 됩니다. 보고 시에나 고객 프로필 집합/데이터 과학/활성화 등을 위해 데이터를 준비할 때 유용합니다.

| 블루프린트 | 설명 | Experience Cloud 애플리케이션 |
|---|---|---|
| **[데이터 준비 및 수집](ingestion.md)** | <ul><li>데이터 준비 및 수집 블루프린트는 데이터를 준비하고 Adobe Experience Platform으로 수집하는 방법을 모두 포함합니다.</ul></li> | <ul><li> Adobe Experience Platform </ul></li> |
| **[서버측 엔터프라이즈 데이터 수집](server-side-collection.md)** | <ul><li>이메일 공급자, 소셜 네트워크 및 광고 대상 등 알려진 프로필 기반 대상으로 활성화합니다. </li><li>오프라인 주문, 거래, CRM 또는 충성도 데이터 등 오프라인 특성 및 이벤트와 온라인 행동을 함께 사용하여 온라인 타겟팅과 개인화를 수행합니다.</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager(선택 사항)</li></ul> |
