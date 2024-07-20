---
title: 데이터 분석 및 인텔리전스 블루프린트
description: Adobe  [!DNL Experience Platform] (AEM)을(를) 사용하여 데이터 레이크에 있는 데이터에 대한 탐색적 쿼리 및 분석을 수행합니다.
solution: Experience Platform
kt: 7207
thumbnail: null
exl-id: a972ea56-d1c8-45da-9044-ed31222a2441
source-git-commit: 7f3bc307f74aa88a7a73f3e50cc48bd16f58b37f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 59%

---

# 데이터 분석 및 인텔리전스 블루프린트

데이터 분석 및 인텔리전스는 [!DNL Experience Platform] 내에서 데이터 레이크에 있는 데이터에 대한 탐색적 쿼리 및 분석을 수행하는 기능으로 구성됩니다.

[!DNL Experience Platform]의 [!UICONTROL 쿼리 서비스]를 사용하면 데이터에 대해 SQL 쿼리를 수행할 수 있습니다.

[!DNL Experience Platform]을(를) 사용하면 [!DNL PostgreSQL] 프로토콜을 사용하여 [!DNL Experience Platform] 내의 데이터에 직접 연결하고, 액세스하고, 쿼리할 수 있도록 서드파티 SQL 클라이언트, 인터페이스 및 Business Intelligence(BI) 도구와의 연결을 허용합니다.

## 사용 사례

* 데이터에 인터랙티브한 쿼리 및 병합 적용
* 수집한 데이터에 행과 열로 액세스하여 탐색 및 유효성 검사
* Business Intelligence 도구를 통한 데이터 대시보드화 및 시각화

쿼리 서비스에 대한 일반적 사용 사례를 [쿼리 서비스 사용 사례](https://experienceleague.adobe.com/docs/experience-platform/query/use-cases/abandoned-browse.html?lang=ko)에서 추가로 확인하실 수 있습니다.

## 애플리케이션

* Adobe [!DNL Experience Platform]

## 아키텍처

<img src="assets/data_exploration.svg" alt="엔터프라이즈 데이터 탐색 및 보고 블루프린트를 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" />

## 가드레일

모범 사례 및 가드레일에 대한 자세한 설명은 Query Service 제품 설명서를 참조하세요.
[쿼리 서비스 안내](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ko)

## 구현 단계

1. 수집할 데이터를 위한 [스키마를 만듭니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ko)
1. 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. [데이터를 [!DNL Experience Platform]에 수집](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko).
1. 데이터를 [[!UICONTROL 쿼리 서비스]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=ko)에서 사용할 수 있는지 확인합니다.
1. [시각화, 데이터 쿼리 및 탐색을 위해 Business Intelligence 도구 및 SQL 클라이언트를 [!UICONTROL 쿼리 서비스]](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=ko)에 연결합니다.

## 관련 설명서

* [Adobe [!DNL Experience Platform] 인텔리전스 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [[!UICONTROL 쿼리 서비스] 설명서](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ko)
