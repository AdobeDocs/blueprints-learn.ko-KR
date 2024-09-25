---
title: Real-time Customer Data Platform 블루프린트로 Customer Journey Analytics
description: Customer Journey Analytics에서 고객 여정 전반에 걸친 데이터 및 고객 행동을 통합하고 분석하여 대상자를 CJA에서 RTCDP로 게시
solution: Customer Journey Analytics
kt: null
thumbnail: null
exl-id: 9e1ba723-63f2-4622-ba67-f2a315c3ba0c
source-git-commit: 9fe44d93dcc05711c77ce1325b6549bb6c27a860
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 94%

---

# Real-time Customer Data Platform 블루프린트로 Customer Journey Analytics

고객 타겟팅 및 개인화를 위해 CJA(Customer Journey Analytics)에서 식별한 대상자를 만들어 Adobe Experience Platform의 실시간 고객 프로필에 게시합니다. 내역 데이터를 사용하여 대상자를 만들거나 Customer Journey Analytics의 세분화된 필터링 및 계산된 필드로 보다 정교한 대상자를 만드는 데 적합합니다.

## Customer Journey Analytics 대상자 게시 안내서

Customer Journey Analytics에서 Real-time Customer Data Platform으로 대상자를 게시하기 위한 구현 및 구성에 대한 지침은 다음 설명서를 참조하십시오. [사용자 가이드](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko)

## Customer Journey Analytics 블루프린트의 아키텍처

![아키텍처 다이어그램](assets/CJA.svg){zoomable="yes"}

## Customer Journey Analytics 블루프린트의 가드레일 다이어그램

* 자세한 가드레일 및 엔드 투 엔드 지연 시간에 대해서는 [배포 가드레일 문서](../experience-platform/deployment/guardrails.md)를 참조하십시오.

![가드레일 다이어그램](../experience-platform/deployment/assets/CJA_guardrails.svg){zoomable="yes"}

## 자주 하는 질문

* CJA가 보낸 RTCDP에 해당 프로필이 존재하지 않는 경우 새 프로필을 만드나요, 아니면 이미 있는 프로필에 대해서만 CJA에서 대상자를 기록하나요? 새 프로필을 만듭니다. 따라서 알려진 고객만을 대상으로 하는 RTCDP 구현의 경우 CJA 대상자 규칙을 작성하여 알려진 신원이 있는 프로필만 필터링해야 합니다. 이를 통해 원하지 않는 경우 익명 프로필에서 RTCDP 프로필 카운트가 증가하지 않도록 할 수 있습니다.

* CJA는 어떤 신원을 보내나요? CJA는 CJA 구성 시 [개인 ID]로 구성된 신원을 전송합니다.

* 기본 신원으로 설정되는 것은 무엇인가요? 사용자가 CJA를 설정할 때 기본 [개인] ID로 설정한 모든 신원입니다.

* 신원 서비스는 CJA 메시지도 처리하나요? 즉, CJA가 대상자 공유를 통해 프로필 아이덴티티 그래프에 신원을 추가할 수 있나요? 아니요. 신원 서비스는 CJA 메시지를 처리하지 않습니다.