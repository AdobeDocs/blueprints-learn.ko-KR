---
title: 파일 및 엔터프라이즈 스트리밍 대상에 대한 대상자 및 프로필 활성화 블루프린트
description: 엔터프라이즈 대상에 대한 대상자 및 프로필 활성화
solution: Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
source-git-commit: 05666e35eebe81fa5a061250528b1c2f4a7376a6
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 73%

---

# 파일 및 엔터프라이즈 스트리밍 대상에 대한 대상자 및 프로필 활성화 블루프린트

스트리밍 또는 일괄 처리에서 프로필 및 대상 변경 사항 및 이벤트 공유 [!UICONTROL Real-time Customer Data Platform] 엔터프라이즈 데이터 저장소 및 응용 프로그램에 연결할 수 있습니다. 이러한 프로필 및 대상 이벤트를 사용하여 중단된 애플리케이션 프로세스 또는 웨비나 등록을 처리하는 등 고객에게 판매 또는 지원 조치를 시작하거나 최신 고객 속성 및 인텔리전스로 엔터프라이즈 애플리케이션을 업데이트하는 데 사용할 수 있습니다. [!UICONTROL Real-time Customer Data Platform].

## 사용 사례

* 클라우드 스토리지 대상에 대한 프로필 및 대상자 활성화 또는 대상 스트리밍을 통한 엔터프라이즈 추적, 저장, 분석 및 고객 데이터와 인사이트 활성화.

## 애플리케이션

* Adobe Experience Platform    Activation

## 아키텍처

<img src="assets/enterprise_destination_activation.svg" alt="엔터프라이즈 활성화 시나리오를 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" zoomable="yes" />


## 가드레일

[대상자 및 프로필 활성화 개요 페이지의 가드레일 설명을 참조하세요.](overview.md)

## 구현 단계

1. 수집할 데이터를 위한 [스키마를 만듭니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ko)
1. 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 수집한 데이터를 통합 프로필로 결합할 수 있도록 스키마에 [올바른 ID와 ID 네임스페이스를 구성합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. 데이터를 Experience Platform으로 [수집합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)
1. [프로비저닝 [!UICONTROL Real-time Customer Data Platform] 세그먼트 공유](https://www.adobe.com/go/audiences) Audience Manager에 공유할 Experience Platform에 정의된 대상에 대한 Experience Platform과 Audience Manager 간.
1. Experience Platform에서 [세그먼트를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko). 세그먼트를 일괄 처리로 평가할지 스트리밍으로 평가할지는 시스템에서 자동으로 결정합니다.
1. 프로필 특성과 대상자 멤버십을 공유할 대상을 원하는 대상으로 [구성합니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html?lang=ko)

## 관련 설명서

* [대상 설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=ko)
* [클라우드 스토리지 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=ko#catalog)
* [HTTP 대상](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=ko#overview)
* [[!UICONTROL Real-time Customer Data Platform] 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html)
* [프로필 및 세분화 지침](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [세분화 설명서](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html?lang=ko)

## 관련 비디오 및 튜토리얼

* [[!UICONTROL Real-time Customer Data Platform] 개요](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=ko)
* [데모 [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html?lang=ko)
* [세그먼트 만들기](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)
