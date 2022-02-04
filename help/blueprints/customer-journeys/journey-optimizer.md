---
title: Journey Optimizer - 트리거 메시지와 Adobe Experience Platform 블루프린트
description: Adobe Experience Platform을 스트리밍 데이터, 고객 프로필 및 세분화의 중앙 허브로 사용하여 트리거된 메시지 및 경험을 실행합니다.
solution: Experience Platform, Journey Optimizer
exl-id: 97831309-f235-4418-bd52-28af815e1878
source-git-commit: 2ead62f94e761cd9453be284a9fde3c5803879eb
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 42%

---

# Journey Optimizer

Adobe Journey Optimizer는 고객 행동에 실시간으로 반응하여 즉각적인 고객 만족을 이끌어 낼 수 있도록 고안된 시스템입니다. 데이터 관리 기능이 Adobe Experience Platform으로 이동하여 마케팅 팀은 중요한 업무에 집중할 수 있습니다. 바로 세계 최고 수준의 고객 여정과 개인화된 소통을 이끌어 내는 데에 초점을 맞출 수 있습니다.  이 블루프린트는 애플리케이션의 기술 기능을 간략하게 설명하고 Adobe Journey Optimizer을 구성하는 다양한 아키텍처 구성 요소에 대해 자세히 살펴봅니다.

<br>

## 사용 사례

* 트리거 메시지
* 시작 및 등록 확인
* 장바구니 및 애플리케이션 양식 버리기
* 장소 트리거 메시지
* 경기장 내 경험
* 도착 전 여행 및 숙박 및 숙박 경험

<br>

## 아키텍처

<img src="assets/ajo-architecture.svg" alt="참조 아키텍처 Journey Optimizer 블루프린트" style="width:100%; border:1px solid #4a4a4a" />

<br>

## 블루프린트 시나리오

| 시나리오 | 설명 | 기능 |
| :-- | :--- | :--- |
| [타사 메시징](3rd-party-messaging.md) | Adobe Journey Optimizer을 타사 메시징 시스템과 함께 사용하여 개인화된 커뮤니케이션을 오케스트레이션 및 전송하는 방법을 보여줍니다 | 고객이 브랜드 또는 회사와 상호 작용할 때 고객에게 개인화된 커뮤니케이션을 즉시 제공<br><br>고려 사항:<br><ul><li>타사 시스템은 인증을 위해 베어러 토큰을 지원해야 합니다</li><li>다중 임차인 아키텍처로 인해 정적 IP를 지원하지 않음</li><li>초당 API 호출과 관련하여 타사 시스템에 대한 아키텍처 제한 사항을 알고 있어야 합니다.  고객이 Journey Optimizer에서 제공하는 볼륨을 지원하기 위해 타사 공급업체로부터 추가 볼륨을 구입해야 할 필요가 있을 수 있습니다</li><li>메시지 또는 페이로드의 Offer decisioning을 지원하지 않습니다</li></ul> |

<br>

## 통합 패턴

| 통합 | 설명 | 기능 |
| :-- | :--- | :--- |
| [Journey Optimizer과 Adobe Campaign](ajo-and-campaign.md) | Adobe Journey Optimizer을 사용하여 실시간 고객 프로필을 활용하여 1:1 경험을 조정하고 기본 Adobe Campaign 트랜잭션 메시지 시스템을 활용하여 메시지를 보내는 방법을 보여줍니다 | Journey Optimizer의 실시간 고객 프로필 및 기능을 활용하여 현재 경험을 조정하고 Adobe Campaign의 기본 실시간 메시징 기능을 활용하여 마지막 마일 커뮤니케이션을 수행합니다<br><br>고려 사항:<br><ul><li>Campaign 애플리케이션은 v7 빌드 21.1 또는 v8에 있어야 합니다.</li><li>메시징 처리량</li><ul><li>Campaign v7 - 시간당 최대 5만 개</li><li>Campaign v8 - 시간당 최대 1M</li><li>Campaign Standard - 시간당 최대 50k</li></ul><li>조절이 수행되지 않으므로 사용 사례에서 Enterprise Architect의 기술 검증이 필요합니다</li><li>Campaign에서 보낸 메시지에 Offer decisioning을 활용하는 데 대한 지원이 없습니다</li></ul> |

<br>

## 필요 조건

Adobe Experience Platform

* Journey Optimizer 데이터 소스를 구성하려면 먼저 시스템에서 스키마 및 데이터 세트를 구성해야 합니다
* 규칙 기반 이벤트가 아닌 이벤트를 트리거하려면 Experience Event 클래스 기반 스키마의 경우 &#39;Orchestration eventID 필드 그룹&#39;을 추가합니다
* 개별 프로필 클래스 기반 스키마의 경우 Journey Optimizer에서 사용할 테스트 프로필을 로드할 수 있도록 &#39;프로필 테스트 세부 정보&#39; 필드 그룹을 추가합니다

이메일

* 메시지 보내기에 사용할 하위 도메인이 있어야 합니다
* 하위 도메인을 Adobe에 완전히 위임하거나(권장) CNAME을 사용하여 Adobe 특정 DNS 서버(사용자 지정)를 가리킬 수 있습니다
* Google TXT 레코드는 배달이 잘 되도록 각 하위 도메인에 필요합니다

모바일 푸시

* 고객은 앱을 빌드할 수 있는 모바일 개발자가 있어야 합니다.
* Adobe Experience Platform Mobile SDK

<br>

## 가드레일

[Journey Optimizer 보호 제품 링크](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=ko)

위의 링크에는 나열되지 않은 사항에 유의하십시오.

* 세그먼트 일괄 처리: 인증 사용자의 일별 볼륨을 이해해야 하며, 대상 시스템이 각 여정 및 모든 여정의 발생 처리량을 처리할 수 있어야 합니다.
* 세그먼트 스트리밍: 프로필 인증 첫 발생을 각 여정 및 모든 여정에 대한 일별 스트리밍 인증 볼륨과 함께 처리할 수 있어야 합니다.
* 기본적으로 메시지에서만 Offer decisioning 지원(사용자 지정 작업 없음)
* 지원되는 메시지 유형:
   * 이메일
   * 푸시(FCM/APNS)
   * 사용자 지정 작업(Rest API 사용)
* 타사 시스템에 대한 아웃바운드 통합
   * 인프라가 멀티 테넌트이므로 단일 정적 IP를 지원하지 않습니다(모든 데이터 센터 IP를 허용 목록 해야 함).
   * 사용자 지정 작업에는 POST 및 PUT 메서드만 지원됩니다
   * 사용자/전달 또는 인증 토큰을 통한 인증
* 다양한 샌드박스 간에 Adobe Experience Platform 또는 Journey Optimizer의 개별 구성 요소를 패키징하여 이동할 수 없습니다. 새 환경에서 다시 구현해야 함

### 데이터 수집 가드 레일

<img src="assets/aep-data-ingestion-details-latency.svg" alt="참조 아키텍처 Journey Optimizer 블루프린트" style="width:80%; border:1px solid #4a4a4a" />

<br>

### 활성화 보호 기능

<img src="assets/ajo-activation-details-latency.svg" alt="참조 아키텍처 Journey Optimizer 블루프린트" style="width:80%; border:1px solid #4a4a4a" />

<br>

## 구현 단계

### Adobe Experience Platform

#### 스키마/데이터 세트

1. 고객 제공 데이터를 기반으로 Experience Platform에서 [개인 프로필, 경험 이벤트 및 다중 항목 스키마를 구성합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)
1. Experience Platform에서 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 거버넌스를 위해 Experience Platform에서 데이터 세트에 [데이터 사용 레이블을 추가](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html?lang=ko)합니다.
1. 대상 관리 [정책을 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html?lang=ko)

#### 프로필/ID

1. [고객용 네임스페이스를 만듭니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [스키마에 ID를 추가합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. [!UICONTROL Real-time Customer Profile]의 서로 다른 보기에 대한 [병합 규칙](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko)을 만듭니다(선택 사항).
1. 여정 사용을 위한 세그먼트를 만듭니다.

#### 소스/대상

1. 스트리밍 API 및 소스 커넥터를 사용하여 [Experience Platform으로 데이터를 수집해 옵니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)

### Journey Optimizer

1. Experience Platform 데이터 소스를 구성하고 프로필 일부로 캐시해야 하는 필드를 결정합니다. 고객 여정을 시작하는 데 사용되는 스트리밍 데이터는 먼저 Journey Optimizer 내에서 구성하여 오케스트레이션 ID를 받아야 합니다. 이 오케스트레이션 ID는 데이터 수집에 사용할 수 있도록 개발자에게 제공됩니다
1. 외부 데이터 소스를 구성합니다.
1. 사용자 정의 행동을 구성합니다.

### 모바일 푸시 구성

1. Experience Platform Mobile SDK를 구현하여 푸시 토큰 및 로그인 정보를 수집하여 알려진 고객 프로필에 다시 연결합니다
1. Adobe 태그를 활용하고 다음 확장을 사용하여 모바일 속성을 만듭니다.
1. Adobe Journey Optimizer
1. Adobe Experience Platform Edge Network
1. ID 에지 네트워크용
1. Mobile Core
1. 모바일 앱 배포와 웹 배포를 위한 전용 데이터 스트림이 있는지 확인합니다.
1. 자세한 내용은 [Adobe Journey Optimizer Mobile 안내서](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)


## 관련 설명서

* [Experience Platform 설명서](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Experience Platform 태그 설명서](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK 설명서](https://experienceleague.adobe.com/docs/mobile.html?lang=ko)
* [Journey Optimizer 설명서](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=ko)
* [Journey Optimizer 제품 설명](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
