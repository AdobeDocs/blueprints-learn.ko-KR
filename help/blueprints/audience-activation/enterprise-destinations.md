---
title: 파일 및 엔터프라이즈 스트리밍 대상 블루프린트의 대상 및 프로필 활성화
description: 엔터프라이즈 대상에 대한 고객 및 프로필 활성화
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
source-git-commit: dd01bd48f2bb5a250ead4b4b28b6228c0cbd2517
workflow-type: ht
source-wordcount: '415'
ht-degree: 100%

---

# 파일 및 엔터프라이즈 스트리밍 대상 블루프린트의 대상 및 프로필 활성화

[!UICONTROL Real-time Customer Data Platform]에서 프로필 및 대상자의 변경 사항과 이벤트를 스트리밍이나 일괄 처리로 엔터프라이즈 데이터 저장소 및 애플리케이션에 공유합니다. 이 프로필 및 대상자 이벤트는 고객에 대한 영업 또는 지원 동작을 시작하는 데 사용할 수 있습니다. 예를 들어 중지된 애플리케이션 프로세스나 웨비나 등록을 팔로우업하거나 [!UICONTROL Real-time Customer Data Platform]의 최신 고객 특성과 인텔리전스로 엔터프라이즈 애플리케이션을 업데이트할 수 있습니다.

## 사용 사례

* 클라우드 스토리지 대상에 대한 프로필 및 대상자 활성화 또는 대상 스트리밍을 통한 엔터프라이즈 추적, 저장, 분석 및 고객 데이터와 인사이트 활성화.

## 애플리케이션

* Adobe Experience Platform      Activation

## 아키텍처

<img src="assets/enterprise_destination_activation.svg" alt="엔터프라이즈 활성화 시나리오를 위한 참조 아키텍처" style="width:80%; border:1px solid #4a4a4a" />


## 가드레일

[대상자 및 프로필 활성화 개요 페이지의 가드레일 설명을 참조하세요.](overview.md)

## 구현 단계

1. 수집할 데이터를 위한 [스키마를 만듭니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 수집한 데이터를 통합 프로필로 결합할 수 있도록 스키마에 [올바른 ID와 ID 네임스페이스를 구성합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. 데이터를 Experience Platform으로 [수집합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)
1. [Experience Platform에서 정의한 대상자를 Audience Manager로 공유할 수 있도록 Experience Platform과 Audience Manager 간 [!UICONTROL Real-time Customer Data Platform] 세그먼트 공유를 제공합니다.](https://www.adobe.com/go/audiences)
1. Experience Platform에서 [세그먼트를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko). 세그먼트를 일괄 처리로 평가할지 스트리밍으로 평가할지는 시스템에서 자동으로 결정합니다.
1. 프로필 특성과 대상자 멤버십을 공유할 대상을 원하는 대상으로 [구성합니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=ko)

## 관련 설명서

* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ko)
* [클라우드 스토리지 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=ko#catalog)
* [HTTP 대상](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=ko#overview)
* [[!UICONTROL Real-time Customer Data Platform] 제품 설명 ](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html)
* [프로필 및 세분화 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)

## 관련 비디오 및 튜토리얼

* [[!UICONTROL Real-time Customer Data Platform] 개요 ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ko)
* [[!UICONTROL Real-time Customer Data Platform] 데모](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ko)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)
