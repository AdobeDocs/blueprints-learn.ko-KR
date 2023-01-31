---
title: Customer Journey Analytics 블루프린트
description: 고객 여정 전체에 걸쳐 수집한 데이터와 고객 행동의 통합 및 분석
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 3bb2dada-f4cd-43f7-a0d0-f276510ad224
source-git-commit: 8355a36a235d847a6faf2398f3fadbed28ccac37
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 90%

---

# Customer Journey Analytics 블루프린트

Customer Journey Analytics를 통해 브랜드가 다양한 소통 채널 및 소스에서 수집한 고객 데이터와 행동을 통합하여 모든 고객 상호 작용에 대한 여정 기반 관점을 만들 수 있는 방법을 확인할 수 있습니다. Customer Journey Analytics 애플리케이션 서비스에서 보고와 분석을 수행하여 고객 상호 작용과 행동 패턴을 평가하고 인사이트를 얻을 수 있습니다.

Customer Journey Analytics 사용 사례의 전체 목록은 Customer Journey Analytics 설명서에서 확인할 수 있습니다.

## Customer Journey Analytics 사용 사례

[일반적인 사용 사례는 다음과 같습니다.](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cja-usecases.html?lang=ko)

* Real-time Customer Data Platform에 대상자 만들기 및 게시
* 최대/최소 전환 경로
* 채널 참여 및 전환
* 가장 많이 본 콘텐츠
* 많이 본 카테고리와 제품
* 전환과 참여 증가로 이어진 캠페인
* 도구 사용량 분석으로 셀프 서비스 경험 최적화

## Customer Journey Analytics 아키텍처

![아키텍처 다이어그램](assets/CJA.svg)

기본 사용 사례의 예시는 다음과 같습니다.
| 블루프린트 | 설명 |  Experience Cloud 애플리케이션 |
|---|---|---|
| **[크로스 채널 여정 분석](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/cross-channel.html?lang=ko)**  | <ul><li>다양한 웹, 모바일 및 오프라인 속성에서 수집한 데이터를 통합하여 전 채널에 걸친 고객 행동을 통합된 단일 관점으로 분석합니다.</li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li><li>Adobe Analytics(선택 사항)</li></ul>| | **[Real-time Customer Data Platform에 대상 게시](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko)** | <ul><li>고객 타겟팅 및 개인화를 위해 CJA(Customer Journey Analytics)에서 식별한 대상자를 만들어 Adobe Experience Platform의 실시간 고객 프로필에 게시합니다. 내역 데이터를 사용하여 대상자를 만들거나 Customer Journey Analytics의 세분화된 필터링 및 계산된 필드로 보다 정교한 대상자를 만드는 데 적합합니다.</li></ul> | <ul><li>Real-time Customer Data Platform</li><li>Customer Journey Analytics</li> |
| **[통화 전환 여정 분석](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/call-center.html?lang=ko)** | <ul><li>콜센터 데이터를 웹, 모바일 및 다른 상호작용 데이터와 함께 분석하여 어떤 행동이 가장 콜센터 문의로 이어질 확률이 높은지를 확인합니다.</li><li>이 인사이트를 활용하여 고객 경험을 최적화할 수 있으며, 셀프 서비스 콘텐츠 및 도구를 최적화하여 콜센터 문의로 이어지는 경로를 줄일 수 있습니다.  </li></ul> | <ul><li>Adobe Experience Platform</li><li>Customer Journey Analytics</li> |

## Customer Journey Analytics 블루프린트에 대한 보호 다이어그램

* 자세한 가드레일 및 엔드 투 엔드 지연 시간에 대해서는 [배포 가드레일 문서](../experience-platform/deployment/guardrails.md)를 참조하세요.

![가드레일 다이어그램](../experience-platform/assets/CJA_guardrails.svg)

## 관련 블로그 게시물

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184){target="_blank"}
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17){target="_blank"}
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1){target="_blank"}
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281){target="_blank"}
* [[!DNL Demonstrating the Power of Adobe's New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34){target="_blank"}
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9){target="_blank"}
