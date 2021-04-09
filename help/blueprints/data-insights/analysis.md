---
title: 데이터 분석 및 인텔리전스 블루프린트
description: 이 블루프린트는 Adobe Experience Platform 내에서 데이터 호수에 있는 데이터의 탐구적 쿼리 및 분석을 수행할 수 있는 기능을 보여줍니다.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: 3b22dfdd-3fbe-40b3-b798-1ee983723039,a972ea56-d1c8-45da-9044-ed31222a2441
translation-type: tm+mt
source-git-commit: 009a55715b832c3167e9a3413ccf89e0493227df
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 데이터 분석 및 인텔리전스 블루프린트

Data Analysis and Intelligence는 Adobe Experience Platform 내에서 데이터 호수에 있는 데이터의 탐구적 쿼리와 분석을 수행하는 기능으로 구성됩니다.

Experience Platform [!UICONTROL 쿼리 서비스]에서는 데이터에 대해 SQL 쿼리를 수행할 수 있습니다. [!UICONTROL Data Science ] Workspaces를 사용하면 데이터에 대한 데이터 분석, 데이터 과학 및 머신 러닝 워크로드를 수행할 수 있습니다.

또한 Experience Platform을 사용하면 타사 SQL 클라이언트, 인터페이스 및 Business Intelligence(BI) 도구에 연결하여 [!DNL PostgreSQL] 프로토콜을 사용하여 Experience Platform 내의 데이터에 직접 연결하고 액세스 및 쿼리할 수 있습니다.

블루프린트 세부 정보에 설명된 대로 쿼리 시간 초과와 쿼리 결과에 포함된 데이터의 양에 대해 특정 단속이 적용됩니다.

## 사용 사례

* 인터랙티브한 쿼리 및 데이터 집계
* 탐색 및 유효성 검사를 위해 인제스트된 데이터에 대한 행 및 열 액세스
* Business Intelligence 툴을 통한 대시보드 및 데이터 시각화

## 애플리케이션

* Adobe Experience Platform

## 아키텍처

<img src="assets/dataexplore.svg" alt="엔터프라이즈 데이터 탐색 및 보고 청사진을 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

* 인터랙티브한 쿼리의 10분 제한
* UI에서 반환된 레코드 제한 100개
* SQL 커넥터를 통해 50,000개의 레코드 제한 반환

## 구현 단계

1. 데이터 호수로 데이터를 수집하기 위한 데이터 집합 및 스키마를 구성합니다.
1. 데이터 인제스트
1. 원시 액세스 및 쿼리를 위해 [!UICONTROL 쿼리 서비스] 및 [!UICONTROL 데이터 과학 작업 공간]에 데이터를 사용할 수 있는지 확인합니다.
1. 시각화, 데이터 쿼리 및 탐색을 위해 Business Intelligence 도구 및 SQL 클라이언트를 [!UICONTROL 쿼리 서비스]에 연결합니다.

## 관련 설명서

* [Adobe Experience Platform Intelligence 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL 쿼리 ] 서비스 설명서](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=en)
