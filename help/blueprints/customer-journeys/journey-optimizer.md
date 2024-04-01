---
title: "[!DNL Journey Optimizer] - 트리거된 메시징 및 Adobe Experience Platform 블루프린트"
description: Adobe Experience Platform을 스트리밍 데이터, 고객 프로필 및 세분화의 중앙 허브로 사용하여 트리거된 메시지 및 경험을 실행합니다.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: a1f3aef5b508575019bd651b9706efc7d6db5306
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Journey Optimizer] 블루프린트

Adobe [!DNL Journey Optimizer] 은 마케팅 팀이 고객 행동에 실시간으로 반응하고 현재 위치에서 이를 충족하기 위해 특별히 빌드된 시스템입니다. 데이터 관리 기능이 Adobe으로 이동되었습니다. [!DNL Experience Platform] 마케팅 팀이 가장 잘하는 것, 즉 세계적 수준의 고객 여정과 개인화된 대화를 만드는 것에 집중할 수 있도록 합니다.

이 블루프린트는 애플리케이션의 기술 기능에 대해 간략히 설명하고 를 구성하는 다양한 아키텍처 구성 요소에 대해 자세히 설명합니다 [!DNL Journey Optimizer].

## 사용 사례

* 트리거 메시지
* 시작 및 등록 확인
* 장바구니 및 애플리케이션 양식 버리기
* 장소 트리거 메시지
* 운동 경기장 내 경험
* 여행 및 숙박업의 도착 전 및 숙박 시 경험

## 아키텍처

<img src="assets/ajo-architecture.svg" alt="Journey Optimizer 블루프린트 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

## 블루프린트 시나리오

| 시나리오 | 설명 | 기능 |
| :-- | :--- | :--- |
| [서드파티 메시지](3rd-party-messaging.md) | Adobe 방법을 보여 줍니다 [!DNL Journey Optimizer] 은 서드파티 메시징 시스템과 함께 활용하여 개인화된 커뮤니케이션을 통합 및 전송할 수 있습니다 | 고객이 브랜드나 회사와 상호 작용할 때 1:1로 즉각적인 개인화 커뮤니케이션을 제공합니다.<br><br>고려 사항:<br><ul><li>인증을 위해 서드파티 시스템이 베어러 토큰을 지원해야 합니다.</li><li>멀티테넌트 아키텍처로 인해 고정 IP를 지원하지 않습니다.</li><li>서드파티 시스템의 아키텍처에 따른 초당 API 호출 제한을 알고 있어야 합니다.  고객이 서드파티 공급업체로부터 볼륨을 추가로 구입하여 다음 제품의 볼륨을 지원할 필요가 있을 수 있음 [!DNL Journey Optimizer]</li><li>메시지나 페이로드에 의사 결정 관리를 지원하지 않습니다.</li></ul> |

<br>

## 통합 패턴

| 통합 | 설명 | 기능 |
| :-- | :--- | :--- |
| [[!DNL Journey Optimizer] Adobe Campaign 사용](ajo-and-campaign.md) | Adobe 사용 방법을 보여 줍니다. [!DNL Journey Optimizer] 실시간 고객 프로필을 활용하여 1:1 경험을 조정하고 기본 Adobe Campaign 트랜잭션 메시지 시스템을 활용하여 메시지를 전송합니다 | 의 실시간 고객 프로필 및 기능 활용 [!DNL Journey Optimizer] Adobe Campaign의 기본 실시간 메시징 기능을 활용하여 라스트 마일 통신을 수행하면서 즉각적인 경험을 조율합니다.<br><br>고려 사항:<br><ul><li>Campaign 애플리케이션이 v7 빌드 21.1 이후 또는 v8 버전이어야 합니다.</li><li>메시지 처리량</li><ul><li>Campaign v7 - 시간당 최대 5만</li><li>Campaign v8 - 시간당 최대 100만</li><li>Campaign Standard - 시간당 최대 5만</li></ul><li>스로틀링을 수행하지 않으므로 사용 사례에 대해 기업 아키텍트의 기술 점검을 받아야 합니다.</li><li>Campaign에서 보내는 메시지에 대한 의사 결정 관리 활용은 지원하지 않습니다.</li></ul> |

<br>

## 필요 조건

Adobe [!DNL Experience Platform]:

* 를 구성하려면 먼저 시스템에서 스키마 및 데이터 세트를 구성해야 합니다 [!DNL Journey Optimizer] 데이터 소스
* [경험 이벤트] 클래스 기반 스키마의 경우 규칙 기반 이벤트가 아닌 이벤트를 트리거하려면 [Orchestration eventID 필드 그룹]을 추가해야 합니다.
* 개별 프로필 클래스 기반 스키마의 경우 &quot;프로필 테스트 세부 정보&quot; 필드 그룹을 추가하여 사용할 테스트 프로필을 로드할 수 있습니다. [!DNL Journey Optimizer]

이메일:

* 메시지 보내기에 사용할 하위 도메인이 있어야 합니다.
* 하위 도메인을 Adobe에 완전히 위임하거나(권장) CNAME을 사용하여 Adobe 전용 DNS 서버(사용자 정의)를 가리킬 수 있습니다.
* 전달성 보장을 위해 각 하위 도메인에 대해 Google TXT 기록이 있어야 합니다.

모바일 푸시:

* 고객은 앱을 빌드할 수 있는 모바일 개발자가 있어야 합니다.
* Adobe Experience Platform Mobile SDK

## 가드레일

[[!DNL Journey Optimizer] 보호 제품 링크](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[보호 및 전체 지연 지침](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 관련 설명서

* [[!DNL Experience Platform] 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [[!DNL Experience Platform] 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
* [[!DNL Experience Platform Mobile SDK] 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
* [[!DNL Journey Optimizer] 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko)
* [[!DNL Journey Optimizer] 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)
