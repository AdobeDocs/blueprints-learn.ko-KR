---
title: 스키마 작성
description: 이전에 완료한 매핑 시트를 사용하여 클래스 및 여러 필드 그룹에서 연결 5G 고객 계정 스키마를 어셈블합니다.
doc-type: overview-page
solution: Experience Platform
exl-id: 6a935c42-0446-43f7-8abc-442ee696a6cf
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 스키마 작성

## 스키마 어셈블리

XDM의 일부인 모든 스키마는 동일한 방식으로 구성됩니다.  스키마는 항상 하나의 클래스와 하나 이상의 필드 그룹으로만 구성됩니다. 또한 스키마의 클래스는 Experience Platform 내의 다른 시스템이 데이터를 해석하는 방법(예: 레코드 기반 또는 시계열)을 나타냅니다.

![한 클래스와 하나 이상의 필드 그룹으로 구성된 스키마를 보여 주는 다이어그램](assets/overview-schema-assembly.jpeg "스키마 어셈블리")


## 귀하의 목표

이 실습에서는 이전에 작성하신 매핑 시트를 활용하여 Connection 5G 고객 계정 스키마를 구축하게 됩니다. 랩의 이 부분을 완료하면 다음과 유사한 스키마가 표시됩니다.

![클래스 및 필드 그룹이 결합된 연결 5G 고객 계정 스키마 완료](assets/overview-connection-5g-customer-account-schema.png "연결 5G - 고객 계정 스키마")



![연결 5G 고객 계정 스키마에 대한 매핑 시트 완료됨](assets/overview-final-connection-5g-customer-mapping-sheet.png "최종 연결 5G 고객 매핑 시트")
