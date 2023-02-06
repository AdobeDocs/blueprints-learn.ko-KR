---
title: 데이터 액세스 및 내보내기 블루프린트
description: 이 블루프린트는 Adobe Experience Platform 및 애플리케이션에서 데이터에 액세스하고 데이터를 내보낼 수 있는 모든 방법을 제시하고 개괄적으로 설명합니다.
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-time Customer Data Platform, Tags
exl-id: 2ca51a29-2db2-468f-8688-fc8bc061b47b
source-git-commit: 5110ee2a7a079945475055cbcfdabf7cdcaa0ab5
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 98%

---

# 데이터 액세스 및 내보내기 블루프린트

데이터 액세스 및 내보내기 블루프린트는 Adobe Experience Platform 및 애플리케이션에서 데이터에 액세스하거나 데이터를 내보낼 수 있는 모든 방법을 간략하게 설명합니다.

이 블루프린트는 Experience Platform과 애플리케이션에서 데이터에 액세스하는 방법에 대한 두 카테고리로 분류됩니다. 먼저 Experience Platform 및 애플리케이션에서 데이터를 내보낼 때의 접근 방법으로, 데이터 전송의 푸시 유형 방법이라 할 수 있습니다. 그 다음은 Experience Platform 및 애플리케이션에서 데이터에 액세스할 때의 접근 방법으로, 데이터 액세스의 풀 유형 방법이라 할 수 있습니다.

데이터 액세스 접근 방법:

* [실시간 고객 프로필 액세스 API](#rtcp-profile-access-api)
* [데이터 액세스 API](#data-access-api)
* [쿼리 서비스](#query-service)

데이터 내보내기 접근 방법:

* [클라이언트 측 태그](#client-side-tags-extensions)
* [이벤트 전달](#event-forwarding)
* [Real-time Customer Data Platform 대상](#RTCDP-destinations)
* [Journey Optimizer 사용자 정의 작업](#jo-custom-actions)

## 데이터 액세스 및 내보내기 개요 아키텍처

<img src="../experience-platform/assets/aep_data_flow.svg" alt="데이터 준비 및 수집 블루프린트의 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a; margin-bottom: 15px;" class="modal-image" />

## 데이터 액세스 접근 방법

### 실시간 고객 프로필 액세스 API {#rtcp-profile-access-api}

고객은 실시간 고객 프로필 액세스 API를 사용하여 모든 프로필 신원, 대상자 멤버십, 속성, 경험 이벤트 등을 포함하는 실시간 고객 프로필 저장소의 단일 통합 프로필에 액세스할 수 있습니다.

자세한 내용은 [실시간 고객 프로필 액세스 API](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=ko) 설명서를 참조하세요.

#### 사용 사례

* 단일 프로필을 검색하여 채팅 및 콜센터를 통한 지원 상호 작용 또는 판매 시점의 영업 상호 작용 등 상담원과 고객의 상호 작용에 배경 정보를 추가합니다.
* 웹 개인화 시스템이나 오퍼 결정 시스템 등 외부 시스템에서 수행한 개인화 결정에 배경 정보 추가를 허용합니다.

#### 고려할 사항

* Real-time Customer Profile [가드레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)이 적용됩니다.
* 한 번에 한 개의 프로필을 검색하는 용도로 설계되었습니다. 분석 또는 데이터 과학 용도의 대규모 프로필 액세스 또는 전체 프로필 모집단의 다운로드에 사용하지 않습니다.
* 프로필 검색 응답 시간은 프로필 가드레일을 지킵니다. 실시간 처리, 낮은 지연 시간이 필요한 경우(예: 동일 페이지 개인화가 필요한 경우) 브라우저 내 및 앱 내 개인화에 필요한 실시간 프로필 액세스를 위해 [Adobe Target 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=ko) 또는 [사용자 지정 개인화 연결](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=ko)로 Edge 프로필을 활용해야 합니다.

### 데이터 액세스 API {#data-access-api}

고객은 데이터 액세스 API를 사용하여 Experience Platform 데이터 레이크에 저장된 미가공 데이터 세트 파일에 직접 액세스할 수 있습니다.

* 데이터 액세스 API 사용에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=ko)를 참조하세요.

#### 사용 사례

* 엔터프라이즈 환경에서의 저장 및 평가를 위해 Experience Platform에서 미가공 및 가공 데이터 파일을 가져옵니다.

#### 고려할 사항

* 데이터에 일괄적, 비동기 상태로 액세스하므로 태그의 활용, 이벤트 전송, RTCDP 대상 등 같은 스트리밍 데이터 전송 접근 방법에 비해 데이터 액세스에 시간이 더 걸립니다.
* 데이터 파일은 Experience Platform으로 처리할 때 일괄적으로 파일 컬렉션으로 저장 및 압축된 후 parquet 포맷으로 저장됩니다. 따라서 파일에 액세스하여 다른 환경으로 다운로드할 때는 전체 데이터 세트가 아닌 배치 및 파일 단위로 체계적으로 액세스해야 하며, 데이터를 처리할 때에는 파일이 parquet 포맷으로 압축된다는 점을 고려해야 합니다.

### 쿼리 서비스 {#query-service}

고객은 Experience Platform 쿼리 서비스를 사용하여 Experience Platform 내 데이터 세트를 쿼리하고 쿼리 결과를 유지할 수 있습니다. SQL 클라이언트를 활용하여 SQL 클라이언트가 지원할 수 있는 저장소 대상 중 원하는 곳에 쿼리하고 쿼리 응답을 유지할 수 있습니다. 쿼리 서비스 UI를 사용하여 SQL 결과를 Experience Platform의 대상 데이터 세트에 저장하거나 로컬 컴퓨터에 저장할 수 있습니다.

* SQL 클라이언트에 연결하여 Experience Platform 쿼리 서비스에서 가져온 SQL 결과를 유지하는 자세한 방법은 다음 [설명서](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=ko)를 참조하세요.

#### 사용 사례

* Experience Platform 데이터 세트의 미가공 데이터를 쿼리하고 쿼리 결과를 유지합니다.
* 프로필 스냅샷 데이터 세트를 쿼리하여 실시간 고객 프로필에 대한 인사이트를 끌어냅니다. [설명서](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=ko#profile-attribute-datasets).
* 쿼리 결과를 별도의 데이터 세트에 저장하여 액세스하거나, 프로필을 사용하는 데이터 세트에 저장하여 나중에 RTCDP 및 다른 실시간 고객 프로필에 액세스하는 Experience Cloud 애플리케이션을 통해 보낼 수 있습니다.

#### 고려할 사항

* 데이터에 일괄적, 비동기 상태로 쿼리하므로 태그의 활용, 이벤트 전송, RTCDP 대상 등 같은 스트리밍 데이터 전송 접근 방법에 비해 데이터 액세스에 시간이 더 걸립니다.
* 쿼리 서비스로는 Experience Platform 데이터 레이크에서 사용할 수 있는 데이터만 쿼리할 수 있습니다. 실시간 고객 프로필 저장소, 아이덴티티 그래프, Customer Journey Analytics는 쿼리 서비스로 직접 쿼리할 수 없습니다. 해당 데이터 세트는 프로필 스냅샷 데이터 세트의 예시와 같이 데이터 세트를 데이터 레이크로 내보내야만 쿼리할 수 있습니다.
* [쿼리 서비스 가드레일](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=ko) 설명서에 나온 바와 같이 쿼리 결과 수 및 쿼리 시간 초과에 대한 가드레일이 적용됩니다.

## 데이터 내보내기 접근 방법

### 클라이언트측 태그 확장 {#client-side-tags-extensions}

Adobe의 태그 솔루션을 사용하여 확장을 배포할 수 있습니다. 확장을 배포하고 나면 클라이언트 브라우저 또는 애플리케이션에 직접 데이터 요청을 배포하고 요청을 호출하여 원하는 대상에 데이터 및 요청을 보낼 수 있습니다.

자세한 내용은 [태그 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko) 설명서를 참조하세요.

#### 사용 사례

* 태깅을 사용하여 클라이언트 측 환경에서 직접 미가공 스트리밍 정보를 수집합니다.

#### 고려할 사항

* Experience Platform 실시간 고객 프로필과 대상자 멤버십 등 서버 측 정보에 직접 액세스할 수 없습니다.
* 페이지에 데이터 수집 태그를 더 추가하면 페이지 로드 시간이 늘어날 수 있습니다.
* 특정 기준이 충족되는 경우에만 데이터를 요청하도록 규칙을 설정할 수 있습니다.
* 데이터를 클라이언트로부터 직접 수집하므로 데이터 수집 전에 수행할 수 있는 변환 및 보강 유형에 제한이 있습니다.

### 이벤트 전달 {#event-forwarding}

데이터 수집 요청은 Adobe의 Edge Network에 직접 수집됩니다. Edge Network 요청에서 외부 RESTful 엔드포인트로의 요청을 외부 대상에 전송하도록 구성할 수 있습니다.

자세한 내용은 [이벤트 전송](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko) 설명서를 참조하세요.

#### 사용 사례

* Adobe의 서버 측 이벤트 전송을 사용하여 클라이언트 측 환경의 미가공 스트리밍 정보를 직접 기업 엔드포인트로 수집합니다.

#### 고려할 사항

* 이벤트 전달을 사용하려면 Web SDK 또는 MobileSDK를 사용하여 Edge Network로 데이터를 보내야 합니다.
* 이벤트 전송 접근 방식은 페이지에 태그를 더 추가하는 데 따른 페이지 로드 시간과 가중치를 줄여 줍니다.
* Edge 프로필이나 다른 데이터 소스를 통한 데이터 보강은 현재 지원하지 않습니다.
* 제한된 데이터 필터링 및 간단한 매핑 변환을 지원합니다.

### Real-time Customer Data Platform 대상 {#RTCDP-destinations}

프로필 속성 데이터와 대상자 멤버십 데이터를 기업 및 광고 대상에 활성화할 수 있습니다. 즉, 전송 데이터를 Experience Platform 실시간 고객 프로필로 수집해야 합니다.

자세한 내용은 [Real-time Customer Data Platform 대상](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=ko) 설명서 를 참조하십시오.

#### 사용 사례

* 내부 기업 데이터 저장소, 분석 도구, 이메일 시스템 또는 지원 시스템에 대해 대상자 멤버십 등 프로필 속성 정보를 활성화합니다.
* 외부 광고 벤더에 대해 프로필 대상자 멤버십을 활성화하여 프로필에 보이는 콘텐츠를 타겟팅하고 개인화합니다.

#### 고려할 사항

* 프로필 속성 및 대상자 멤버십을 활성화할 수 있습니다. 미가공 경험 이벤트는 현재 RTCDP 대상의 일부로 활성화할 수 없습니다.
* 세그먼트 평가의 특성과 대상이 허용하는 수집 프로토콜의 특성에 따라 스트리밍 또는 일괄 처리 방식으로 활성화가 일어납니다.

### Journey Optimizer 사용자 정의 작업 {#jo-custom-actions}

고객은 Journey Optimizer를 사용하여 여정 캔버스에서 사용자 정의 작업을 호출하여 구성해 둔 외부 API 엔드포인트에 페이로드나 메시지를 보낼 수 있습니다. JSON 포맷 페이로드로 REST API를 통해 호출할 수 있는 모든 공급자의 모든 서비스에 대해 작업을 구성할 수 있습니다. 이 페이로드에는 여정에서 구성한 이벤트 정보, 프로필 속성 및 이전 이벤트 데이터, 변환 및 데이터 보강 등이 포함될 수 있습니다.

자세한 내용은 [Journey Optimizer 사용자 정의 작업](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=ko) 설명서를 참조하세요.

#### 사용 사례

* 실시간 고객 프로필에서 가져온 추가 정보를 포함하는 Experience Platform과 Journey Optimizer에서의 활성화 이벤트.
* 고객이 여정의 특정 지점에 도달하면 외부 시스템에 알립니다.

#### 고려할 사항

* [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=ko)에서 지원하는 처리량 및 [실시간 고객 프로필](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)에서 지원하는 보강에 대한 가드레일이 적용됩니다.
* 사용자 정의 작업은 여정의 이벤트 또는 프로필 각각에 대해 하나씩 스트리밍으로 수행할 수 있습니다. 고객 여정 간 파일 또는 종합 요청 형태의 대량 작업 또는 대량 데이터 전송은 수행할 수 없습니다.
* 활성화 페이로드에 포함할 수 있는 실시간 고객 프로필 속성 및 경험 이벤트에는 스트리밍 액세스가 적용됩니다.
* 이벤트를 외부 대상으로 보내기 전에 이벤트 데이터를 필터링하고 간단한 매핑 변형을 적용할 수 있습니다.
