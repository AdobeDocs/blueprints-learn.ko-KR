---
title: CreateDate에 대한 MAPPER 오류 수정
description: 빈 필드로 변환되던 잘못된 형식의 createDate 값으로 인해 발생한 MAPPER 오류 문제를 해결하고 해결합니다.
doc-type: article
solution: Experience Platform
exl-id: e3f7ef23-6fd1-4f7a-8dc7-db82445322b0
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# CreateDate에 대한 MAPPER 오류 수정

이 연습에서는 일괄 처리 수집 랩에서 보았던 MAPPER 오류를 제거하는 방법을 파악해야 합니다. createDate가 필수 필드가 아님에도 불구하고 형식이 잘못된 날짜가 빈 필드로 변환되기 때문에 레코드가 계속 수집되므로 오류를 수정해야 합니다.

![잘못된 형식의 createDate 값으로 인해 MAPPER 오류 발생](assets/fix-mapper-errors-for-createdate-invalid-format-mapper-error.png)
