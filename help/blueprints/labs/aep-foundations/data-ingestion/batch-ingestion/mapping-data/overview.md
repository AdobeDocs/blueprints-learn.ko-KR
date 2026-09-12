---
title: 데이터 매핑
description: 소스 필드와 스키마 필드 간의 AI/ML 생성 패스스루 매핑에 수집 전 주의 깊은 검사가 필요한 이유를 이해합니다.
doc-type: overview-page
solution: Experience Platform
exl-id: 6c61093d-de03-4b76-9b4b-3e36962047da
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# 데이터 매핑

## 개요

매핑 화면에서 AI/ML 추천 엔진은 소스 데이터 세트의 필드와 스키마 필드 사이에 여러 속성을 자동으로 매핑합니다. 이러한 자동화된 매핑을 통과 매핑이라고 하지만 오류와 잘못된 매핑이 자주 발생하므로 **주의 깊은 검사**&#x200B;가 필요합니다.



![통과 매핑에 대한 AI/ML 기반 상황별 권장 사항을 표시하는 매핑 화면](assets/overview-ai-ml-based-contextual-recommendations.png "AI/ML 기반 상황별 권장 사항")

>[!NOTE]
>
>AI/ML 권장 사항은 컨텍스트를 기반으로 하며 위의 스크린샷과 다르게 보이거나 이웃과 다를 수 있습니다

>[!NOTE]
>
>모든 소스 열은 항상 문자열로 처리됩니다
