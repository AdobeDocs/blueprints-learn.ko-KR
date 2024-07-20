---
title: 데이터 수집 및 준비
description: ' [!DNL Experience Platform] Adobe에서 데이터를 수집하고 준비할 수 있는 방법을 알아봅니다.'
solution: Data Collection
kt: 7204
thumbnail: null
exl-id: 5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 61%

---

# 데이터 수집 및 준비 블루프린트

데이터 수집 및 준비는 데이터를 준비하고 Adobe [!DNL Experience Platform]에 수집할 수 있는 모든 방법을 포함합니다. 데이터를 Adobe [!DNL Experience Platform Edge Network]에 수집하는 기능과 Side 전달을 통해 데이터를 엔터프라이즈 대상으로 전달하는 후속 기능입니다.

데이터를 준비할 때는 소스 데이터를 XDM(Experience Data Model) 스키마로 매핑하게 됩니다. 또한 데이터에 날짜 포맷 정리, 필드 분할/연결/전환 및 기록 연결/병합/재입력 등의 변환을 수행합니다. 데이터 준비를 통해 고객 데이터를 단일화하면 종합적이고 필터링된 분석 제공에 도움이 됩니다. 보고 시에나 고객 프로필 집합/데이터 과학/활성화 등을 위해 데이터를 준비할 때 유용합니다.

| 블루프린트 | 설명 | Experience Cloud 애플리케이션 |
|---|---|---|
| **[데이터 준비 및 수집](ingestion.md)** | <ul><li>데이터 준비 및 수집 블루프린트는 데이터를 준비하고 Adobe [!DNL Experience Platform]에 수집할 수 있는 모든 방법을 포함합니다.</ul></li> | <ul><li> Adobe [!DNL Experience Platform] </ul></li> |
| **[서버측 엔터프라이즈 데이터 수집](server-side-collection.md)** | <ul><li>이메일 공급자, 소셜 네트워크 및 광고 대상 등 알려진 프로필 기반 대상으로 활성화합니다. </li><li>오프라인 주문, 거래, CRM 또는 충성도 데이터 등 오프라인 특성 및 이벤트와 온라인 행동을 함께 사용하여 온라인 타겟팅과 개인화를 수행합니다.</li></ul> | <ul><li>Adobe [!DNL Experience Platform]</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager(선택 사항)</li></ul> |
