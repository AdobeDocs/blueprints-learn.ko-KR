---
title: Experience Platform 및 애플리케이션 가드레일
description: 가드레일은 Adobe Experience Platform 및 애플리케이션 내 구성 요소와 서비스의 성능 기대치 및 영향을 정의합니다.
solution: Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 4379f372241248ea6c70c766f13a182783fcac0c
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 64%

---

# 가드레일

보호 기능은 Adobe Experience Platform 및 애플리케이션에서 데이터 및 시스템 사용에 대한 지침을 제공하는 권장 임계값입니다. 보호 기능은 시스템 제한 사항과 성능 기대치를 반영하여 고객 아키텍처 및 사용 사례 성능을 최적화하고 오류 또는 예상치 못한 결과를 방지하는 데 도움이 됩니다. 보호 기능은 SLA(서비스 수준 계약)가 아닙니다.

애플리케이션 및 기능에 대한 특정 SLA에 대한 자세한 내용은 [애플리케이션 및 기능 설명](#application-feature-descriptions) 섹션에 있는 마지막 항목이 될 필요가 없습니다.


## Adobe Experience Platform 및 애플리케이션 가드레일 참조 설명서

다음 페이지에서는 Adobe Experience Platform 기능, 서비스 및 응용 프로그램의 보호 기능에 대한 정보를 제공합니다.

**Experience Platform 애플리케이션**

* [Real-Time CDP 보호 개요](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html)
* [보호 기능 공유 Customer Journey Analytics 대상자](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko-KR#latency)
* [Customer Journey Analytics 데이터 수집 보호](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ko-KR#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizer 보호 기능](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=ko)

**Experience Platform 서비스**

* [데이터 수집 가드레일](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=ko)
* [Edge Network API 가드레일](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html?lang=ko)
* [Real-time Customer Profile 가드레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [신원 가드레일](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=ko)
* [쿼리 서비스 가드레일](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ko)
* [대상 활성화 가드레일](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ko)



## 엔드투엔드 지연 다이어그램

### 데이터 수집

<img src="assets/aep_data_flow_guardrails.svg" alt="Experience Platform 데이터 흐름" style="border:1px solid #4a4a4a" width="85%" />

<br>

### 세분화

<img src="assets/segmentation_guardrails.svg" alt="Experience Platform 세분화 가드레일" style="border:1px solid #4a4a4a" width="85%" />

<br>

### Real-time Customer Data Platform 및 Adobe Target

<img src="assets/RTCDP_Target_guardrails.svg" alt="RTCDP 및 Target 가드레일" style="border:1px solid #4a4a4a" width="85%" />

<br>

### Customer Journey Analytics

<img src="assets/CJA_guardrails.svg" alt="CJA 가드레일" style="border:1px solid #4a4a4a" width="85%" />

<br>

### Journey Optimizer

<img src="assets/AJO_guardrails.svg" alt="Journey Optimizer 블루프린트 참조 아키텍처" style="width:85%; border:1px solid #4a4a4a" />

<br>

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
