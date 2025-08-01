---
title: Experience Platform 및 애플리케이션 가드레일
description: 가드레일은 Adobe Experience Platform 및 애플리케이션 내 구성 요소와 서비스의 성능 기대치 및 영향을 정의합니다.
solution: Experience Platform
thumbnail: null
exl-id: b64cf3e4-cc5d-4984-8a0f-4736d432b8e1
source-git-commit: 75a0f2a77f39a4320dc4c4b0db918879be099dd3
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 13%

---


# 가드레일

가드레일은 시스템 제한, 예상 대기 시간 및 성능 기대치를 반영하여 고객 아키텍처 및 사용 사례 성능을 최적화하고 안정성을 보장하고 오류나 예상치 못한 결과를 방지하는 데 도움이 됩니다.

## 보호 기능 유형

| 보호 유형 | 설명 |
|---|---|
| 성능 보호(소프트 제한) | 성능 보호는 사용 사례의 범위와 관련된 사용 제한이며 일반적인 조건에서 예상되는 성능을 요약합니다. 초과되면 성능 저하와 지연이 발생할 수 있습니다. 성능 보호 기능은 아래 설명된 대로 각 솔루션에 대한 보호 섹션 아래의 Experience League 문서에 설명되어 있습니다. |
| 정적 제한(엄격한 제한) | 이는 초과할 수 없는 시스템 적용 제한입니다. 정적 제한은 일반적으로 계약상으로 연결되며 고객 계약과 [제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions.html)에 요약되어 있습니다. |

>[!NOTE]
>
> 보호 기능은 SLA(서비스 수준 계약)가 아니라 최적의 구성과 예상되는 시스템 동작을 위한 지침입니다. 시스템 또는 계약 제한 또는 SLA(서비스 수준 계약)에 해당하는 모든 보호 기능은 고객 계약 및 제품 설명에 자세히 설명되어 있습니다. 사용자 지정 제한에 대한 자세한 내용은 고객 지원 센터에 문의하십시오.

>[!NOTE]
>
> 지연 시간 또는 성능 요구 사항이 엄격한 사용 사례의 경우 Adobe은 Adobe 계정 팀 및 구현 파트너와 세부 사항에 대해 논의할 것을 제안합니다. 각 고객 설정은 데이터 수집 패턴, 프로필 수 및 풍부성, 세그먼트 규칙 및 활성화 채널에 따라 다를 수 있습니다. 따라서 성능을 최적화하고 예상 성능 특성을 완전히 파악하려면 사용 사례를 설계하고 테스트하는 것이 중요합니다.

## Adobe Experience Platform 및 애플리케이션 가드레일 참조 설명서

다음 페이지에서는 Adobe Experience Platform 기능, 서비스 및 응용 프로그램의 보호 기능에 대한 정보를 제공합니다.

**Experience Platform 응용 프로그램**

* [Real-Time CDP 보호 개요](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/guardrails/overview.html?lang=ko)
* [보호 기능을 공유하는 Customer Journey Analytics 대상자](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko#latency)
* [Customer Journey Analytics 데이터 수집 보호](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ko#what-is-the-expected-latency-for-analytics-data-on-platform%3F)
* [Journey Optimizer 보호](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=ko)

**Experience Platform 서비스**

* [데이터 수집 가드레일](https://experienceleague.adobe.com/docs/experience-platform/ingestion/guardrails.html?lang=ko)
* [[!DNL Edge Network] API 보호](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/guardrails.html?lang=ko)
* [실시간 고객 프로필 및 세그먼테이션 보호](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [신원 가드레일](https://experienceleague.adobe.com/docs/experience-platform/identity/guardrails.html?lang=ko)
* [쿼리 서비스 가드레일](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ko)
* [대상 활성화 가드레일](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ko)

## 엔드투엔드 지연 다이어그램 {#end-to-end-latency}

### Experience Platform Edge Network 및 Hub 기본 관찰 지연 시간 {#edge-hub-latencies}

다음 다이어그램은 Experience Platform 및 애플리케이션에서 사용 사례를 설계할 때 알아야 하는 기본 에지 및 허브의 관찰된 대기 시간을 보여 줍니다.

![Experience Platform [!DNL Edge Network] 및 허브 기본 대기 시간이 관찰되었습니다.](/help/blueprints/experience-platform/assets/aep_edge_hub_latency_v1.svg "Experience Platform Edge Network 및 허브 기본 대기 시간이 관찰됨"){width="1000" zoomable="yes"}