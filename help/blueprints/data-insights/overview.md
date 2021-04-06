---
title: 엔터프라이즈 데이터 탐색 및 보고 블루프린트
description: 이 블루프린트는 Adobe Experience Platform 내에서 데이터 호수에 있는 데이터의 탐구적 쿼리 및 분석을 수행할 수 있는 기능을 보여줍니다.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039
translation-type: tm+mt
source-git-commit: 3f27f27159d9fb07124f289164dd85941ec58a25
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# 엔터프라이즈 데이터 탐색 및 보고 블루프린트

엔터프라이즈 데이터 탐색 및 보고는 Adobe Experience Platform 내에서 데이터 호수에 있는 데이터에 대한 탐구적 쿼리 및 분석을 수행하는 기능으로 구성됩니다.

Experience Platform 쿼리 서비스를 사용하면 데이터에 대해 SQL 쿼리를 수행할 수 있습니다. 데이터 과학 작업 공간을 사용하면 데이터에 대한 데이터 탐색, 데이터 과학 및 머신 러닝 워크로드를 수행할 수 있습니다.

또한 Experience Platform을 사용하면 타사 SQL 클라이언트, 인터페이스 및 Business Intelligence(BI) 도구에 연결하여 PostgreSQL 프로토콜을 사용하여 Experience Platform 내의 데이터에 직접 연결하고 액세스 및 쿼리할 수 있습니다.

시나리오 세부 정보에 명시된 대로 쿼리 시간 초과 및 쿼리 결과에 포함된 데이터의 양에 대해 특정 단락이 적용됩니다.

## 사용 사례

* 인터랙티브한 쿼리 및 데이터 집계
* 탐색 및 유효성 검사를 위해 인제스트된 데이터에 대한 행 및 열 액세스
* Business Intelligence 툴을 통한 대시보드 및 데이터 시각화

## 애플리케이션

* Adobe Experience Platform

## 시나리오

| 시나리오 | 설명 | Experience Cloud 애플리케이션/서비스 |
|---|---|---|
| **데이터 탐색 - 데이터의 원시 쿼리** | <ul><li>대화형 쿼리 사용자 인터페이스 또는 연결된 SQL 클라이언트를 사용하여 데이터 레이크에서 SQL 쿼리를 작성하고 수행합니다. 또한 데이터 과학 작업 공간을 사용하여 Experience Platform의 원시 데이터를 쿼리하고 통찰력을 얻을 수 있습니다.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |
| **엔터프라이즈 대시보드** | <ul><li>Business Intelligence 툴을 Experience Platform에 연결하여 대시보드 및 보고 사용 사례용 데이터를 시각화할 수 있습니다.</li></ul> | <ul><li>Adobe Experience Platform</li></ul> |

## 아키텍처

<img src="assets/dataexplore.svg" alt="엔터프라이즈 데이터 탐색 및 보고 청사진을 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

* 인터랙티브한 쿼리의 10분 제한
* UI에서 반환된 레코드 제한 100개
* SQL 커넥터를 통해 50,000개의 레코드 제한 반환

## 구현 단계

1. 데이터 호수로 데이터를 수집하기 위한 데이터 집합 및 스키마를 구성합니다.
1. 데이터 인제스트
1. 원시 액세스 및 쿼리를 위해 쿼리 서비스 및 데이터 과학 작업 공간에 데이터를 사용할 수 있는지 확인합니다.
1. 시각화, 데이터 쿼리 및 탐색을 위해 Business Intelligence 도구 및 SQL 클라이언트를 쿼리 서비스에 연결합니다.

## 관련 설명서

* [Adobe Experience Platform Intelligence 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [쿼리 서비스 설명서](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
