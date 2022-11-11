---
title: Customer Journey Analytics와 Real-time Customer Data Platform
description: Customer Journey Analytics에서 고객 여정 전반에 걸친 데이터 및 고객 행동을 통합하고 분석하여 대상자를 CJA에서 RTCDP로 게시
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 985f7320db7c77b8541ec4ef76b1eb7ad0caae56
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 44%

---

# Customer Journey Analytics와 Real-time Customer Data Platform

고객 타겟팅 및 개인화를 위해 CJA(Customer Journey Analytics)에서 식별한 대상자를 만들어 Adobe Experience Platform의 실시간 고객 프로필에 게시합니다. 내역 데이터를 사용하여 대상자를 만들거나 Customer Journey Analytics의 세분화된 필터링 및 계산된 필드로 보다 정교한 대상자를 만드는 데 적합합니다.

## Customer Journey Analytics 대상자 게시 안내서

Customer Journey Analytics에서 Real-time Customer Data Platform으로 대상자를 게시하기 위한 구현 및 구성에 대한 지침은 다음 설명서를 참조하세요. [사용자 가이드](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko)

## Customer Journey Analytics 블루프린트의 아키텍처

![아키텍처 다이어그램](assets/CJA_RTCDP.svg)

## Customer Journey Analytics 블루프린트의 가드레일 다이어그램

* 자세한 보호 기능 및 종료 대기 시간은 [배포 가드 레일 문서](../experience-platform/deployment/guardrails.md)

![가드레일 다이어그램](../experience-platform/assets/CJA_guardrails.svg)

## FAQ

* CJA가 보낸 RTCDP에 해당 프로필이 존재하지 않거나, 새 프로필을 만들거나, 이미 있는 프로필에만 CJA에서 대상을 기록합니까? 예. 새 프로필이 만들어집니다. 따라서 RTCDP 구현이 알려진 고객만을 대상으로 하는 경우 CJA 대상 규칙을 작성하여 알려진 ID가 있는 프로필만 필터링해야 합니다. 원하지 않는 경우 익명 프로필에서 RTCDP 프로필 카운트가 증가하지 않도록 합니다.

* CJA는 대상 데이터를 파이프라인 이벤트나 데이터 레이크로도 이동하는 플랫 파일로 전송합니까? CJA 대상은 파이프라인을 통해 RTCDP 프로필 서비스로 스트리밍되지만 데이터 레이크에도 데이터 세트로 저장됩니다.

* CJA는 어떤 ID를 전송합니까? CJA는 CJA 구성 중에 &quot;개인 ID&quot;로 구성된 ID를 전송합니다.

* 기본 ID로 설정되는 것은 무엇입니까? CJA를 기본 &quot;개인&quot; ID로 설정할 때 사용자가 선택한 모든 ID입니다.

* ID 서비스는 CJA 메시지도 처리합니까? 즉, CJA가 대상 공유를 통해 프로필 ID 그래프에 ID를 추가할 수 있습니까? 아니요. ID 서비스는 CJA 메시지를 처리하지 않습니다.

## 관련 블로그 게시물

* [[!DNL Blueprint for Multi-Channel Orchestration in Adobe Experience Platform]](https://medium.com/adobetech/blueprint-for-multi-channel-orchestration-in-adobe-experience-platform-c68317e94184)
* [[!DNL Leveraging External Data Platforms in Adobe Experience Platform Journey Orchestration]](https://medium.com/adobetech/leveraging-external-data-platforms-in-adobe-experience-platform-journey-orchestration-54fc6134fe17)
* [[!DNL Event-Based Triggering on Adobe Experience Platform Orchestration Service using Apache Airflow]](https://medium.com/adobetech/event-based-triggering-on-adobe-experience-platform-orchestration-service-using-apache-airflow-8607b28251f1)
* [[!DNL Adobe Campaign Classic Integration with Journey Orchestration]](https://medium.com/adobetech/adobe-campaign-classic-integration-with-journey-orchestration-ae577653281)
* [[!DNL Demonstrating the Power of Adobe’s New Journey Orchestration Service to Build Personalized Omnichannel Experiences in Real-Time]](https://medium.com/adobetech/demonstrating-the-power-of-adobes-new-journey-orchestration-service-to-build-personalized-aa60d88cd34)
* [[!DNL Journey Orchestration in an Omnichannel World]](https://medium.com/adobetech/journey-orchestration-in-an-omnichannel-world-3a2d32d556d9)
