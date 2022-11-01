---
title: 데이터 액세스 및 내보내기 블루프린트
description: 이 블루프린트는 Adobe Experience Platform 및 애플리케이션에서 데이터를 액세스 및 내보낼 수 있는 모든 방법을 제공하고 개괄적으로 설명합니다.
product: adobe experience platform
solution: Experience Platform, Journey Optimizer, Real-time Customer Data Platform, Tags
source-git-commit: 67e66068bb8a2106dd8aa9784b5a39377225c045
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 4%

---

# 데이터 액세스 및 내보내기 블루프린트

데이터 액세스 및 내보내기 블루프린트는 Adobe Experience Platform 및 애플리케이션에서 데이터를 액세스하거나 내보낼 수 있는 모든 방법을 간략하게 설명합니다.

블루프린트는 Experience Platform 및 응용 프로그램에서 데이터 액세스를 위해 두 가지 카테고리로 분류됩니다. 먼저 Experience Platform 및 응용 프로그램에서 데이터를 가져오는 방법 이는 데이터 전송의 푸시 유형 메서드로 간주됩니다. 두 번째, Experience Platform 및 애플리케이션에서의 데이터 액세스 방법 이는 데이터 액세스의 가져오기 유형 메서드로 간주됩니다.

데이터 액세스 접근 방식

* [실시간 고객 프로필 액세스 API](#rtcp-profile-access-api)
* [데이터 액세스 API](#data-access-api)
* [쿼리 서비스](#query-service)

데이터 내보내기 방법

* [클라이언트측 태그](#client-side-tags-extensions)
* [이벤트 전달](#event-forwarding)
* [Real-time Customer Data Platform 대상](#RTCDP-destinations)
* [Journey Optimizer 사용자 지정 작업](#jo-custom-actions)

## 데이터 액세스 및 내보내기 개요 아키텍처

<img src="../experience-platform/assets/aep_data_flow.svg" alt="데이터 준비 및 수집 블루프린트의 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a" />

## 데이터 액세스 방법

### 실시간 고객 프로필 액세스 API {#rtcp-profile-access-api}

고객은 실시간 고객 프로필 액세스 API를 사용하여 모든 프로필 ID, 대상 멤버십, 속성 및 경험 이벤트를 포함한 실시간 고객 프로필 저장소에서 단일 통합 프로필에 액세스할 수 있습니다.

자세한 내용은 [실시간 고객 프로필 액세스 API](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=en) 설명서 를 참조하십시오.

#### 사용 사례

* 단일 프로필을 조회하여 채팅 및 콜 센터를 통한 지원 상호 작용 또는 판매 시점에 영업 상호 작용과 같은 에이전트 고객 상호 작용에 컨텍스트를 추가합니다.
* 웹 개인화 시스템 또는 오퍼 결정 시스템과 같이 외부 시스템에서 수행한 개인화 설명에 추가된 컨텍스트를 허용합니다.

#### 고려 사항

* 실시간 고객 프로필 [가드 레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) 적용합니다.
* 한 번에 단일 프로필 조회를 위해 설계되었습니다. 분석 또는 데이터 과학을 사용하기 위해 전체 프로필 모집단의 벌크 프로필 액세스 또는 다운로드에 사용되지 않습니다.
* 프로필 조회 응답 시간은 프로필 보호 기능에 반영됩니다. 지연 시간이 짧은 요구 사항 - 예를 들어 동일한 페이지 개인화 요구 사항에 대해서는 지연 시간이 짧은 프로필 액세스를 위해 Edge Profile 또는 Customer Personalization 대상을 활용해야 합니다. [설명서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/custom-personalization.html?lang=en).

### 데이터 액세스 API {#data-access-api}

데이터 액세스 API를 사용하는 고객은 Experience Platform 데이터 레이크에 저장된 원시 데이터 세트 파일에 직접 액세스할 수 있습니다.

* 데이터 액세스 API 사용에 대한 자세한 내용은 [설명서](https://experienceleague.adobe.com/docs/experience-platform/data-access/home.html?lang=en).

#### 사용 사례

* 엔터프라이즈 환경에서 스토리지 및 평가를 위해 Experience Platform에서 원시 및 처리된 데이터 파일을 가져옵니다.

#### 고려 사항

* 데이터는 일괄적으로 비동기식으로 액세스하므로 데이터 액세스 는 태그의 재사용, 이벤트 전달 또는 RTCDP 대상과 같은 스트리밍 데이터 송신 접근 방식에 비해 기본적으로 지연됩니다.
* Experience Platform으로 처리할 때 데이터 파일은 일괄로 파일 컬렉션으로 저장되고 압축된 후 parquet 형식으로 저장됩니다. 따라서 파일을 다른 환경에 액세스하고 다운로드할 때는 전체 데이터 세트에 비해 배치 및 파일이 체계적으로 액세스해야 하며, 데이터의 모든 작업은 parquet 형식으로 압축되는 파일을 고려해야 합니다.

### 쿼리 서비스 {#query-service}

Experience Platform Query Service 고객은 Experience Platform 내에서 데이터 세트를 쿼리하고 쿼리 결과를 유지할 수 있습니다. SQL 클라이언트를 사용하여 SQL 클라이언트가 지원할 수 있는 원하는 저장소 대상에서 쿼리 응답을 쿼리하고 유지할 수 있습니다. Query Service UI를 사용하여 SQL 결과를 Experience Platform의 대상 데이터 세트에 저장하거나 결과를 로컬 시스템에 저장할 수 있습니다.

* Experience Platform 쿼리 서비스에서 SQL 결과를 지속하기 위한 SQL 클라이언트와의 연결에 대한 자세한 내용은 다음을 참조하십시오 [설명서](https://experienceleague.adobe.com/docs/experience-platform/query/clients/overview.html?lang=en).

#### 사용 사례

* Experience Platform 데이터 세트에서 원시 데이터를 쿼리하고 쿼리 결과를 유지합니다.
* 프로필 스냅샷 데이터 세트를 쿼리하여 실시간 고객 프로필에 대한 통찰력을 추출합니다. [사용자 가이드](https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html?lang=en#profile-attribute-datasets).
* 쿼리 결과를 별도의 데이터 세트에 저장하여 액세스하거나 나중에 RTCDP 및 실시간 고객 프로필에 액세스하는 다른 Experience Cloud 애플리케이션을 통해 가져올 수 있습니다.

#### 고려 사항

* 데이터는 배치 비동기적으로 쿼리되므로 데이터에 대한 액세스는 태그의 무효화, 이벤트 전달 또는 RTCDP 대상과 같은 스트리밍 데이터 송신 접근 방식에 비해 기본적으로 지연됩니다.
* Experience Platform 데이터 레이크에서 사용할 수 있는 데이터만 쿼리 서비스를 사용하여 쿼리할 수 있습니다. ID 그래프인 실시간 고객 프로필 저장소는 쿼리 서비스를 사용하여 Customer Journey Analytics을 직접 쿼리할 수 없습니다. 데이터 세트를 데이터 레이크로 내보내는 경우에만 프로필 스냅샷 데이터 세트의 예와 같이 이러한 데이터 세트를 쿼리할 수 있습니다.
* 쿼리 결과 수 및 쿼리 시간 초과에 대한 보호 기능이 [쿼리 서비스 보호 기능](https://experienceleague.adobe.com/docs/experience-platform/query/guardrails.html?lang=en) 설명서.

## 데이터 내보내기 방법

### 클라이언트 측 태그 확장 {#client-side-tags-extensions}

확장은 Adobe의 태그 솔루션을 사용하여 배포할 수 있습니다. 확장이 배포되면 클라이언트 브라우저 또는 애플리케이션에 직접 데이터 요청을 배포하고 요청을 호출하여 원하는 대상에 데이터 및 요청을 보낼 수 있습니다.

자세한 내용은 [태그 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en) 설명서 를 참조하십시오.

#### 사용 사례

* 태깅을 사용하여 클라이언트 측 환경에서 직접 원시 스트리밍 정보를 수집합니다.

#### 고려 사항

* Experience Platform 실시간 고객 프로필 및 대상 멤버십과 같은 서버 측 정보에 직접 액세스할 수 없습니다.
* 페이지에 추가 데이터 수집 태그를 추가하면 페이지 로드 시간이 늘어날 수 있습니다.
* 특정 기준이 충족되는 경우에만 데이터를 요청하도록 규칙을 설정하는 기능.
* 데이터는 클라이언트로부터 직접 수집되므로 데이터를 수집하기 전에 수행할 수 있는 변환 및 데이터 보강 유형을 제한합니다.

### 이벤트 전달 {#event-forwarding}

데이터 수집 요청은 Adobe 에지 네트워크에 직접 수집됩니다. Edge 네트워크 요청에서 외부 RESTful 엔드포인트에 대한 이 요청을 외부 대상에 전달하도록 구성할 수 있습니다.

다음을 참조하십시오 [이벤트 전달](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=en) 설명서 를 참조하십시오.

#### 사용 사례

* Adobe의 서버측 이벤트 전달을 사용하여 클라이언트 측 환경에서 엔터프라이즈 엔드포인트로 직접 원시 스트리밍 정보를 수집합니다.

#### 고려 사항

* 이벤트 전달을 사용하려면 WebSDK 또는 MobileSDK를 사용하여 Edge 네트워크로 데이터를 전송해야 합니다.
* 이벤트 전달 접근 방식은 페이지에 추가 태그가 추가되어 페이지 로드 시간과 가중치를 줄입니다.
* 에지 프로필이나 다른 데이터 소스의 데이터 보강은 현재 지원되지 않습니다.
* 제한된 데이터 필터링 및 간단한 매핑 변환이 지원됩니다.

### Real-time Customer Data Platform 대상 {#RTCDP-destinations}

프로필 속성 데이터 및 대상 멤버십 데이터를 엔터프라이즈 및 광고 대상에 활성화할 수 있습니다. 즉, 가져온 데이터를 Experience Platform 실시간 고객 프로필에 수집해야 합니다.

자세한 내용은 [Real-time Customer Data Platform 대상](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en) 설명서 를 참조하십시오.

#### 사용 사례

* 엔터프라이즈 데이터 저장소, 분석 도구, 이메일 시스템 또는 지원 시스템에 대한 대상 멤버십을 비롯한 프로필 속성 정보를 활성화합니다.
* 외부 광고 벤더에 프로필 대상 멤버십을 활성화하여 프로필을 타겟팅하고 개인화합니다.

#### 고려 사항

* 프로필 속성 및 대상 멤버십을 활성화할 수 있습니다. 원시 경험 이벤트는 현재 RTCDP 대상의 일부로 활성화할 수 없습니다.
* 활동은 세그먼트 값의 특성과 대상이 수락하는 수집 프로토콜의 특성에 따라 스트리밍이나 배치에서 발생합니다.

### Journey Optimizer 사용자 지정 작업 {#jo-custom-actions}

Journey Optimizer 고객은 여정 캔버스에서 사용자 지정 작업을 호출하여 구성된 외부 API 엔드포인트에 페이로드나 메시지를 보낼 수 있습니다. JSON 형식 페이로드를 사용하여 REST API를 통해 호출할 수 있는 모든 공급자의 어떤 서비스로든 작업을 구성할 수 있습니다. 이 페이로드에는 여정에 구성된 이벤트 정보, 프로필 속성 및 이전 이벤트 데이터, 변환 및 데이터 보강 등이 포함될 수 있습니다.

자세한 내용은 [Journey Optimizer 사용자 지정 작업](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=en) 설명서 를 참조하십시오.

#### 사용 사례

* 실시간 고객 프로필의 추가 정보를 포함하는 Experience Platform 및 Journey Optimizer의 활성화 이벤트입니다.
* 고객이 여정의 특정 지점에 도달하면 외부 시스템에 알립니다.

#### 고려 사항

* 지원되는 처리량에 대한 보호 기능 [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en) 및 [실시간 고객 프로필](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) 적용합니다.
* 사용자 지정 작업은 여정의 각 이벤트 또는 프로필에 대해 하나씩 스트리밍으로 수행할 수 있습니다. 파일 형태로 대량 작업 또는 벌크 데이터 송신 또는 고객 여정 간에 집계된 요청을 수행할 수 없습니다.
* 활성화 페이로드에 포함할 수 있는 실시간 고객 프로필 속성 및 경험 이벤트에 대한 스트리밍 액세스.
* 이벤트 데이터를 필터링하고, 이벤트를 외부 대상으로 보내기 전에 적용된 간단한 매핑 변형을 수행할 수 있습니다.










