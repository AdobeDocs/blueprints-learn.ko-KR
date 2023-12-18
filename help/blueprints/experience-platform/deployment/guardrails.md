---
title: Experience Platform 및 애플리케이션 가드레일
description: 가드레일은 Adobe Experience Platform 및 애플리케이션 내 구성 요소와 서비스의 성능 기대치 및 영향을 정의합니다.
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 5a4827244b7d8414b1f1a0bf9b3cd8308bde8c60
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 18%

---

# 가드레일

보호 기능은 Adobe Experience Platform 및 애플리케이션에서 데이터, 관찰된 대기 시간 및 시스템 사용에 대한 지침을 제공하는 권장 임계값입니다. 보호 기능은 시스템 제한 사항과 성능 기대치를 반영하여 고객 아키텍처 및 사용 사례 성능을 최적화하고 오류 또는 예상치 못한 결과를 방지하는 데 도움이 됩니다. 보호 기능은 SLA(서비스 수준 계약)가 아니며, SLA(서비스 수준 계약)는 아래 링크된 제품 설명 및 고객 라이선스 계약에 문서화되어 있습니다. 보호 기능은 안정성과 실행을 보장하기 위해 특정 고객 사용 사례에 대한 솔루션 설계 지침을 제공하기 위한 것입니다.

애플리케이션 및 기능에 대한 특정 SLA에 대한 자세한 내용은 [애플리케이션 및 기능 설명](#application-feature-descriptions) 섹션에 있는 마지막 항목이 될 필요가 없습니다.

지연 또는 볼륨 요구 사항이 엄격한 고객 사용 사례의 경우 Adobe은 Adobe 계정 팀 및 구현 파트너와 함께 사용 사례를 자세히 검토할 것을 권장합니다. 특정 경우에 사용 사례의 프로덕션 시작 전에 주어진 사용 사례 구현을 테스트하고 관찰하여 예상 동작을 관찰하고 이해하는 것이 좋습니다. 각 고객 구현에는 데이터 수집의 특성 및 케이던스, 빌드 중인 세그먼트 규칙의 세부 사항, 다양한 활성화 문제 및 페이로드를 비롯한 다양한 요소가 있으므로 각 사용 사례 구현에는 관찰된 성능이 달라질 것입니다. 따라서 사용 사례의 지연 시간 및 성능 요구 사항에 따라 적절한 아키텍처 및 구현을 보장하기 위해 예상되는 성능을 미리 설정하고 테스트하는 것이 가장 좋습니다.


## Adobe Experience Platform 및 애플리케이션 가드레일 참조 설명서

다음 페이지에서는 Adobe Experience Platform 기능, 서비스 및 응용 프로그램의 보호 기능에 대한 정보를 제공합니다.

**Experience Platform 애플리케이션**

* [Real-Time CDP 보호 개요](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [보호 기능 공유 Customer Journey Analytics 대상자](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html#latency)
* [Customer Journey Analytics 데이터 수집 보호](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html)

**Experience Platform 서비스**

* [데이터 수집 가드레일](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html)
* [Edge Network API 가드레일](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html)
* [실시간 고객 프로필 및 세그멘테이션 가드 레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [신원 가드레일](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=ko)
* [쿼리 서비스 가드레일](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ko)
* [대상 활성화 가드레일](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ko)

## 엔드투엔드 지연 다이어그램 {#end-to-end-latency}

### 데이터 수집 {#data-ingestion}

아래 다이어그램은 다음을 통해 예상되는 데이터 수집 지연 값을 표시합니다. [스트리밍 수집](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html) 및 [일괄 처리 수집](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/getting-started.html?lang=ko) 데이터를 Real-Time CDP으로 가져올 때. 고해상도 버전을 보려면 이미지를 클릭하십시오.

![데이터 수집 높은 수준의 시각적 개요.](/help/blueprints/experience-platform/deployment/assets/aep_data_flow_guardrails.svg "데이터 수집 높은 수준의 시각적 개요 및 지연 시간 값"){width="1000" zoomable="yes"}

### 세분화 {#segmentation}

아래 다이어그램은 의 대상자로 작업할 때 예상되는 지연 값을 표시합니다. [Real-Time CDP 세그멘테이션 서비스](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=ko). 고해상도 버전을 보려면 이미지를 클릭하십시오.

![세그먼테이션의 높은 수준의 시각적 개요.](/help/blueprints/experience-platform/deployment/assets/segmentation_guardrails.svg "세그먼테이션 높은 수준의 시각적 개요 및 지연 값"){width="1000" zoomable="yes"}

### Real-time Customer Data Platform 및 Adobe Target {#adobe-target-latency}

아래 다이어그램은 Real-Time CDP에서 로 대상을 내보낼 때 예상되는 지연 값을 표시합니다 [Adobe Target](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ko). 고해상도 버전을 보려면 이미지를 클릭하십시오.

![Adobe Target으로 내보내기의 높은 수준 시각적 개요.](/help/blueprints/experience-platform/deployment/assets/RTCDP_Target_guardrails.svg "Adobe Target으로 대상 내보내기 높은 수준의 시각적 개요 및 지연 시간 값"){width="1000" zoomable="yes"}

### Customer Journey Analytics      {#customer-journey-analytics}

아래 다이어그램은 를 사용하여 작업할 때 예상되는 지연 값을 표시합니다 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=en). 고해상도 버전을 보려면 이미지를 클릭하십시오.

![Customer Journey Analytics 높은 수준의 시각적 개요 작업](/help/blueprints/experience-platform/deployment/assets/CJA_guardrails.svg "Customer Journey Analytics의 높은 수준의 시각적 개요 및 지연 시간 값 작업"){width="1000" zoomable="yes"}

### Journey Optimizer    {#journey-optimizer}

아래 다이어그램은 를 사용하여 작업할 때 예상되는 지연 값을 표시합니다 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en). 고해상도 버전을 보려면 이미지를 클릭하십시오.

![Adobe Journey Optimizer을 사용한 작업 고급 시각적 개요.](/help/blueprints/experience-platform/deployment/assets/AJO_guardrails.svg "Adobe Journey Optimizer의 높은 수준의 시각적 개요 및 지연 시간 값 작업"){width="1000" zoomable="yes"}

## 애플리케이션 및 기능 설명 {#application-feature-descriptions}

기능별 SLA에 대한 자세한 내용은 아래 제품 설명을 참조하십시오.

* [Experience Platform 컬렉션 기업용](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform-collection-enterprise.html)
* [Real-time Customer Data Platform](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform.html)
* [B2B Customer Data Platform](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform-b2b.html)
* [Experience Platform Activation](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform0.html)
* [Experience Platform Intelligence](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html)
* [인텔리전트 서비스](https://helpx.adobe.com/kr/legal/product-descriptions/intelligent-services.html)
* [Data Distiller](https://helpx.adobe.com/kr/legal/product-descriptions/data-distiller.html)
* [Customer Journey Analytics](https://helpx.adobe.com/kr/legal/product-descriptions/customer-journey-analytics.html)
* [Journey Optimizer](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)
* [Journey Orchestration](https://helpx.adobe.com/kr/legal/product-descriptions/journey-orchestration.html)
* [Offer Decisioning](https://helpx.adobe.com/kr/legal/product-descriptions/offer-decisioning-app-service.html)
