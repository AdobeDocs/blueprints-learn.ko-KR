---
title: B2B Customer Journey Analytics 블루프린트
description: 계정 기반 보고 및 여정 분석을 위해 Customer Journey Analytics의 B2B 계정, 기회 및 구매 그룹 데이터를 포함합니다.
solution: Customer Journey Analytics
source-git-commit: 10e54d97082143b61e43bae56250a524d1759d45
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 7%

---


# B2B Customer Journey Analytics 블루프린트

Customer Journey Analytics B2B edition을 통해 B2B 조직을 위한 계정 기반 보고 및 분석을 사용할 수 있습니다. 사용자 중심의 B2C 분석과 달리 이 블루프린트는 **account**&#x200B;을 데이터 모델의 중심에 배치하므로 여러 관련자, 구매 그룹 및 판매 주기에 걸쳐 복잡한 B2B 구매 여정을 분석할 수 있습니다. [!DNL Customer Journey Analytics]을(를) 사용하여 행동 데이터를 여정 기반 통찰력 및 대상자 생성을 위한 B2B 차원(계정, 기회, 캠페인 및 마케팅 목록)과 통합합니다.

## 애플리케이션

* Adobe [!DNL Customer Journey Analytics]&#x200B;(B2B edition)
* Adobe Experience Platform (B2B 및 이벤트 데이터용)

## 사용 사례

* **계정 마케팅 최적화** - 캠페인, 채널 및 콘텐츠 전반에서 계정 내 구매 그룹, 파이프라인 진행 및 상향 판매/교차 판매 기회에 대한 마케팅 영향을 분석합니다.
* **주요 계정 성장** - 주요 계정 내 구매 그룹 간 고가치 접점을 식별하여 마케팅 및 판매 작업을 알리고 계정 수준에서 고객 생애 가치를 계산합니다.
* **제품 가치 구축** — 계정 및 사용자 수준에서 제품 릴리스 및 사용이 고객 만족에 미치는 영향을 측정하여 기능을 최적화하고 개발에 알릴 수 있습니다.
* **개인 기반 B2B 분석** — 계정 및 영업 기회 컨텍스트와 잠재 고객 점수, 참여 및 여정 분석을 위한 개별 사용자 행동을 결합합니다.

## 필요 조건

* [!DNL Customer Journey Analytics] B2B edition 권한.
* Adobe Experience Platform의 B2B 및 행동 데이터: B2B 데이터 세트(계정, 기회, 개인, 캠페인, 마케팅 목록, B2B 활동) 및 이벤트 데이터(웹, 모바일 또는 기타 채널)는 [CJA 연결](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=ko)에서 사용할 수 있습니다.
* [CJA에 대한 B2B 이름 지정](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/b2b.html): 연결에 대해 구성된 B2B 관련 데이터 보기 설정(계정 ID, 영업 기회 ID 및 관련 차원)입니다.

## 아키텍처

![여정 분석을 위해 통합된 B2B 계정 및 영업 기회 데이터가 있는 Customer Journey Analytics 아키텍처](assets/CJA.svg){zoomable="yes"}

CJA 연결을 통해 Experience Platform(B2B 및 이벤트 데이터 세트)에서 [!DNL Customer Journey Analytics]&#x200B;(으)로 데이터 흐름. B2B 차원은 데이터 보기에 표시되므로 계정, 기회 및 개인 수준에서 분석 및 대상을 구축할 수 있습니다.

## 가드레일

* B2B edition 제품 제한 및 사용 권한에 대해서는 [Customer Journey Analytics B2B 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/customer-journey-analytics-b2b.html)을 참조하세요.
* Analytics Platform 및 CJA 기술 제한에 대해서는 [Analytics Platform 보호](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/technotes/guardrails)를 참조하십시오.
* CJA 데이터 수집 및 연결 제한에 대해서는 [Customer Journey Analytics 데이터 수집 보호](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ko#what-is-the-expected-latency-for-analytics-data-on-platform%3F)를 참조하십시오.
* CJA 대상을 Real-time Customer Data Platform에 게시하는 경우 [보호 기능을 공유하는 Customer Journey Analytics 대상](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko#latency)을 참조하십시오.
* 전체 대기 시간 및 플랫폼 보호 기능은 [배포 보호 기능 문서](../experience-platform/guardrails.md)를 참조하세요.

## 구현 단계

1. **B2B 및 이벤트 데이터를 Experience Platform으로 수집** - [소스](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=ko)&#x200B;(예: [!DNL Marketo Engage], CRM 또는 기타 B2B 커넥터)를 사용하여 계정, 기회, 개인, 캠페인, 활동 데이터와 행동 이벤트를 가져옵니다.
2. **CJA 연결 만들기** — [관련 Experience Platform 데이터 세트 추가](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=ko)&#x200B;(B2B 및 이벤트)를 Customer Journey Analytics 연결에 추가합니다.
3. **데이터 보기에서 B2B 구성** — [B2B 이름 지정 및 키 차원 사용](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/b2b.html)&#x200B;(계정 ID, 영업 기회 ID 등) 를 참조하십시오.
4. **계정 기반 분석 및 대상 구축** — [CJA B2B 사용 사례 및 보고](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/b2b.html?lang=ko)를 사용하여 계정 및 기회 수준에서 보고서, 분류 및 대상을 만듭니다. 활성화를 위해 [실시간 CDP에 대상을 게시](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko)할 수도 있습니다.

## 관련 설명서

### Customer Journey Analytics B2B edition

* [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition.html?lang=ko)
* [B2B 사용 사례](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/b2b.html?lang=ko)
* [B2B edition 사용 사례 개요](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/b2b/b2b-edition/use-cases-overview.html?lang=ko)
* [예제 사용자 기반 B2B 프로젝트](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/b2b/example.html?lang=ko)

### 연결 및 데이터 보기

* [연결 만들기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=ko)
* [B2B 데이터 보기 설정](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/b2b.html)

### 대상자 및 보호 기능

* [Real-time CDP에 CJA 대상 게시](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko)
* [Experience Platform 및 애플리케이션 보호](../experience-platform/guardrails.md)
