---
title: 데이터 준비 및 수집 블루프린트
description: 이 블루프린트에서는 Adobe Experience Platform에서 데이터를 수집하고 준비하는 방법을 모두 다룹니다.
solution: Experience Platform,Data Collection
kt: 7204
thumbnail: null
exl-id: 21f8a73e-6be7-448e-8cd3-ebee9fc848e1,5c3c94b6-c928-4d93-8b38-f8bd2aad2e68
source-git-commit: 45e47c3ac88a67069485952aaa57741820c37143
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 100%

---

# 데이터 준비 및 수집 블루프린트

데이터 준비 및 수집 블루프린트는 데이터를 준비하고 Adobe Experience Platform으로 수집하는 방법을 모두 포함합니다.

데이터를 준비할 때는 소스 데이터를 XDM(Experience Data Model) 스키마로 매핑하게 됩니다. 또한 데이터에 날짜 포맷 정리, 필드 분할/연결/전환 및 기록 연결/병합/재입력 등의 변환을 수행합니다. 데이터 준비를 통해 고객 데이터를 단일화하면 종합적이고 필터링된 분석 제공에 도움이 됩니다. 보고 시에나 고객 프로필 집합/데이터 과학/활성화 등을 위해 데이터를 준비할 때 유용합니다.

## 아키텍처

<img src="assets/data_ingestion.png" alt="데이터 준비 및 수집 블루프린트의 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 데이터 수집 방법

| 수집 방법 | 설명 |
|------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 웹/모바일 SDK | 대기 시간:<ul><li>실시간 - Edge Network와 동일한 페이지 수집</li><li>프로필로 스트리밍 수집 1분 이내</li><li>데이터 레이크로 스트리밍 수집(소규모 일괄 처리 15분 이내)</ul>사용자 가이드: <ul><li>[웹 SDK](https://experienceleague.adobe.com/docs/web-sdk.html?lang=ko)</li><li>[모바일 SDK](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)</li></ul> |
| 스트리밍 소스 | 대기 시간:<ul><li>실시간 - Edge Network와 동일한 페이지 수집</li><li>프로필로 스트리밍 수집 1분 이내</li><li>데이터 레이크로 스트리밍 수집(소규모 일괄 처리 15분 이내)</li></ul>[사용자 가이드](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ko#connectors) |
| 스트리밍 API | 대기 시간:<ul><li>실시간 - Edge Network와 동일한 페이지 수집</li><li>프로필로 스트리밍 수집 1분 이내</li><li>데이터 레이크로 스트리밍 수집(소규모 일괄 처리 15분 이내)</li><li>7GB/시간</li></ul>[사용자 가이드](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=ko#what-can-you-do-with-streaming-ingestion%3F) |
| ETL 도구 사용 | ETL 도구를 사용하여 엔터프라이즈 데이터를 Experience Platform으로 수집하기 전에 수정 및 변환합니다.<br><br>대기 시간:<ul><li>시간은 외부 ETL 도구의 예약 설정에 따라 달라지며, 수집에 사용하는 방법을 기반으로 표준 수집 가드레일이 적용됩니다.</li></ul> |
| 일괄 처리 소스 | 소스 예약 호출<br>대기 시간: 최대 200GB/시간<br><br>[설명서](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=en#connectors)<br>[비디오 튜토리얼](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/overview.html?lang=ko) |
| 일괄 처리 API | 대기 시간:<ul><li>프로필로 일괄 수집하는 경우 규모 및 트래픽 부하에 따라 달라지며 45분 이내</li><li>데이터 레이크로 일괄 수집하는 경우 규모 및 트래픽 부하에 따라 다름</li></ul>[사용자 가이드](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=ko#batch) |
| Adobe 애플리케이션 커넥터 | Adobe Experience Cloud 애플리케이션을 소스로 하는 데이터를 자동으로 수집<ul><li>Adobe Analytics: [설명서](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ko#connectors) 및 [비디오 튜토리얼](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=ko)</li><li>Audience Manager: [설명서](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ko#connectors) 및 [비디오 튜토리얼](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-aam.html?lang=ko)</li></ul> |


## 데이터 준비 방법

| 데이터 준비 방법 | 설명 |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!UICONTROL Data Science Workspace] - 데이터 준비 | 모델 기반 변환, 스크립트 변환.<br>[사용자 가이드](https://experienceleague.adobe.com/docs/experience-platform/data-science-workspace/home.html?lang=ko) |
| 외부 ETL 도구([!DNL Snaplogic], [!DNL Mulesoft], [!DNL Informatica] 등) | ETL 도구에서 복잡한 변환을 수행하고 표준 Experience Platform [!UICONTROL 플로우 서비스] API 또는 소스 커넥터를 사용하여 결과 데이터를 수집합니다. |
| [!UICONTROL 쿼리 서비스] - 데이터 준비 | 데이터를 새 데이터 세트와 연결, 분할, 병합, 변환, 쿼리 및 필터링합니다. CTAS(Create Table as Selec) 사용 <br>[설명서](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=ko#sql) |
| XDM 매핑 및 데이터 준비 함수(스트리밍 및 일괄 처리) | Experience Platform 수집 시 CSV 또는 JSON 포맷의 소스 특성을 XDM 특성에 매핑합니다.<br>수집하는 데이터의 함수 계산(데이터 형식 지정, 분할, 연결 등)<br>[사용자 가이드](https://experienceleague.adobe.com/docs/experience-platform/data-prep/home.html?lang=ko) |

## 관련 블로그 게시물

* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17?source=your_stories_page-------------------------------------)
* [[!DNL High Throughput Ingestion with Iceberg]](https://medium.com/adobetech/high-throughput-ingestion-with-iceberg-ccf7877a413f?source=your_stories_page-------------------------------------)
* [[!DNL Query Service Tricks in Adobe Experience Platform (Writing Queries and Storing Derived Datasets)]](https://medium.com/adobetech/query-service-tricks-in-adobe-experience-platform-writing-queries-and-storing-derived-datasets-eaee0d6d683e?source=your_stories_page-------------------------------------)
* [[!DNL Digging into Adobe Experience Platform’s Experience Data Model to More Fully Understand the Power of Real-time Customer Profile]](https://medium.com/adobetech/digging-into-adobe-experience-platforms-experience-data-model-to-more-fully-understand-the-power-3e109271e04f?source=your_stories_page-------------------------------------)
* [[!DNL An Introductory Look at Exploratory Data Analysis on Adobe Experience Platform]](https://medium.com/adobetech/an-introductory-look-at-exploratory-data-analysis-on-adobe-experience-platform-1bfce7501d9a?source=your_stories_page-------------------------------------)
* [[!DNL Modeling XDM Data for Data Science at Scale on Adobe Experience Platform]](https://medium.com/adobetech/modeling-xdm-data-for-data-science-at-scale-on-adobe-experience-platform-222bb2a6dbf7?source=your_stories_page-------------------------------------)
