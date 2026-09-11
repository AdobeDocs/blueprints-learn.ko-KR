---
title: 주문 이벤트 스트리밍
description: 샘플 주문 이벤트를 보내고 기존 고객 프로필에 연결하는 HTTP API 스트리밍 데이터 흐름 구축을 연습합니다.
doc-type: article
solution: Experience Platform
exl-id: 558c21d1-f9b7-489b-9153-5f10d0b8448a
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 주문 이벤트 스트리밍

## 필요 조건

1. [샘플 파일](../sample-files.md)을 다운로드하고 이름이 —> **Lab\_Single\_Order\_sample.json**&#x200B;인 파일을 확인합니다.
1. [데이터 랜딩 영역 사용](./using-data-landing-zone/overview.md) 실습을 완료했으며 가져올 올바른 매핑이 설정되어 있습니다.

## 과제

이전 실습에서와 마찬가지로 다음 작업 세트를 수행합니다.

1. HTTP API 소스 커넥터를 사용하여 새 계정 만들기
1. 새 계정을 사용하여 데이터 흐름을 설정하여 데이터를 고유한 고객 주문 데이터 세트로 스트리밍합니다
1. [데이터 랜딩 영역 사용](./using-data-landing-zone/overview.md) 랩에서 매핑 세트를 다시 사용합니다.
1. Postman에서 데이터를 성공적으로 스트리밍하고 이전에 만든 고객 계정 레코드에 연결하는 데 필요한 정보로 **주문 이벤트 만들기**&#x200B;를 채웁니다
1. 주문이 프로필에 연결되어 있는지 확인합니다.

>[!TIP]
>
>행운을 빌어 Adobe Experience Platform 신들이 너와 함께 하길!
