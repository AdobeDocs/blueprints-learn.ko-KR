---
title: Journey Optimizer - 트리거 메시지와 Adobe Experience Platform 블루프린트
description: Adobe Experience Platform을 스트리밍 데이터, 고객 프로필 및 세분화의 중앙 허브로 사용하여 트리거된 메시지 및 경험을 실행합니다.
solution: Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 5f9384abe7f29ec764428af33c6dd1f0a43f5a89
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 97%

---

# Journey Optimizer 블루프린트

Adobe Journey Optimizer는 고객 행동에 실시간으로 반응하여 즉각적인 고객 만족을 이끌어 낼 수 있도록 고안된 시스템입니다. 데이터 관리 기능이 Adobe Experience Platform으로 이동하여 마케팅 팀은 중요한 업무에 집중할 수 있습니다. 바로 세계 최고 수준의 고객 여정과 개인화된 소통을 이끌어 내는 데에 초점을 맞출 수 있습니다.  이 블루프린트는 애플리케이션의 기술 기능을 간략하게 설명하고 Adobe Journey Optimizer을 구성하는 다양한 아키텍처 구성 요소에 대해 자세히 살펴봅니다.

<br>

## 사용 사례

* 트리거 메시지
* 시작 및 등록 확인
* 장바구니 및 애플리케이션 양식 버리기
* 장소 트리거 메시지
* 운동 경기장 내 경험
* 여행 및 숙박업의 도착 전 및 숙박 시 경험

<br>

## 아키텍처

<img src="assets/ajo-architecture.svg" alt="Journey Optimizer 블루프린트 참조 아키텍처" style="width:100%; border:1px solid #4a4a4a" class="modal-image" />

<br>

## 블루프린트 시나리오

| 시나리오 | 설명 | 기능 |
| :-- | :--- | :--- |
| [서드파티 메시지](3rd-party-messaging.md) | Adobe Journey Optimizer를 서드파티 메시지 시스템과 함께 사용하여 개인화된 메시지를 오케스트레이션하고 보내는 방법을 설명합니다. | 고객이 브랜드나 회사와 상호 작용할 때 1:1로 즉각적인 개인화 커뮤니케이션을 제공합니다.<br><br>고려 사항:<br><ul><li>인증을 위해 서드파티 시스템이 베어러 토큰을 지원해야 합니다.</li><li>멀티테넌트 아키텍처로 인해 고정 IP를 지원하지 않습니다.</li><li>서드파티 시스템의 아키텍처에 따른 초당 API 호출 제한을 알고 있어야 합니다.  Journey Optimizer에서 보내는 데이터의 양을 지원하기 위해 고객이 서드파티 공급업체로부터 추가 용량을 구매해야 할 수도 있습니다.</li><li>메시지나 페이로드에 의사 결정 관리를 지원하지 않습니다.</li></ul> |

<br>

## 통합 패턴

| 통합 | 설명 | 기능 |
| :-- | :--- | :--- |
| [Journey Optimizer와 Adobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizer를 통해 [실시간 고객 프로필]을 활용하여 1:1 경험을 오케스트레이션하고 Adobe Campaign의 기본 제공 트랜잭션 메시지 시스템을 활용하여 메시지를 보내는 방법을 보여 줍니다. | [실시간 고객 프로필]과 Journey Optimizer의 기능을 활용하여 실시간 경험을 오케스트레이션하는 한편 Adobe Campaign의 기본 제공 실시간 메시지 기능을 사용하여 라스트 마일 커뮤니케이션을 수행합니다.<br><br>고려 사항:<br><ul><li>Campaign 애플리케이션이 v7 빌드 21.1 이후 또는 v8 버전이어야 합니다.</li><li>메시지 처리량</li><ul><li>Campaign v7 - 시간당 최대 5만</li><li>Campaign v8 - 시간당 최대 100만</li><li>Campaign Standard - 시간당 최대 5만</li></ul><li>스로틀링을 수행하지 않으므로 사용 사례에 대해 기업 아키텍트의 기술 점검을 받아야 합니다.</li><li>Campaign에서 보내는 메시지에 대한 의사 결정 관리 활용은 지원하지 않습니다.</li></ul> |

<br>

## 필요 조건

Adobe Experience Platform

* Journey Optimizer 데이터 소스를 구성하려면 먼저 시스템에서 스키마와 데이터 세트를 구성해야 합니다.
* [경험 이벤트] 클래스 기반 스키마의 경우 규칙 기반 이벤트가 아닌 이벤트를 트리거하려면 [Orchestration eventID 필드 그룹]을 추가해야 합니다.
* [개별 프로필] 클래스 기반 스키마의 경우 Journey Optimizer에서 사용할 테스트 프로필을 로드할 수 있도록 하려면 [프로필 테스트 세부 정보] 필드 그룹을 추가해야 합니다.

이메일

* 메시지 보내기에 사용할 하위 도메인이 있어야 합니다.
* 하위 도메인을 Adobe에 완전히 위임하거나(권장) CNAME을 사용하여 Adobe 전용 DNS 서버(사용자 정의)를 가리킬 수 있습니다.
* 전달성 보장을 위해 각 하위 도메인에 대해 Google TXT 기록이 있어야 합니다.

모바일 푸시

* 고객은 앱을 빌드할 수 있는 모바일 개발자가 있어야 합니다.
* Adobe Experience Platform Mobile SDK

<br>

## 가드레일

[Journey Optimizer 가드레일 제품 링크](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html)

[보호 및 전체 지연 지침](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html)

## 관련 설명서

* [Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
* [Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko)
* [Journey Optimizer 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-journey-optimizer.html)
