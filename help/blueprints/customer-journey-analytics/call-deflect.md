---
title: 호출 처짐 분석 시나리오
description: 콜센터에 연락하기 전에 고객 행동을 분석합니다.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
translation-type: tm+mt
source-git-commit: e1a9881996a181310bdc32cb083e4c5654139bf0
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---


# 통화 감소 여정 분석 시나리오

콜센터에 연락하기 전에 데스크탑 및 모바일에서 고객의 행동을 분석합니다. 고객이 고객 지원에 연락하기 전에 완료하려는 작업, 고객이 보는 컨텐츠 및 검색어를 파악하여 고객 여정을 향상시킬 수 있는 기회를 식별합니다. 고객이 전화를 하지 않고도 문제를 해결할 수 있도록 개선할 수 있는 컨텐츠 및 셀프 서비스 툴을 확인할 수 있습니다.

## 사용 사례

* 고객이 지원에 문의하기 전에 고객 행동 분석
* 셀프 서비스 기능 향상 기회 발견

## 애플리케이션

* Adobe Experience Platform
* Customer Journey Analytics

## 통합 패턴

* Adobe Experience Platform → Customer Journey Analytics

## 아키텍처

<img src="assets/CJA.svg" alt="Customer Journey Analytics 청사진을 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

Customer Journey Analytics에 데이터 통합:

* 호수 데이터 수집:API ~ 7GB/시간, 소스 커넥터 ~ 200GB/시간, ~ 15분, Analytics 소스 커넥터는 호수에서 최대 45분 정도 스트리밍됩니다.
* 데이터가 데이터 호수에 게시된 후 Customer Journey Analytics으로 처리하는 데 최대 90분이 걸릴 수 있습니다.

## 구현 단계

1. 데이터 집합 및 스키마를 구성합니다.
1. 데이터를 플랫폼에 인제스트
Customer Journey Analytics에 수집하기 전에 데이터를 플랫폼에 수집해야 합니다.
1. 크로스채널 이벤트 데이터 세트를 분석합니다.
조합으로 분석된 데이터 집합은 공용 네임스페이스 ID가 있어야 하며 Customer Journey Analytics의 필드 기반 스티칭 기능을 통해 다시 입력해야 합니다. 

   >[!NOTE]
   >
   >Customer Journey Analytics은 현재 스티칭에 Experience Platform 프로필 또는 ID 서비스를 사용하지 않습니다.

1. 데이터를 기반으로 하는 필드 기반 ID 스티칭의 사용자 지정 데이터 준비 또는 사용을 수행하여 Customer Journey Analytics으로 인제스트할 시간 시리즈 데이터 세트에 대한 공통 키를 확인합니다.
1. 이벤트 데이터의 필드에 연결할 수 있는 조회 데이터에 대한 기본 ID를 제공합니다. 라이센스에서 행으로 카운트됩니다.
1. 프로필 데이터에 이벤트 데이터의 기본 ID와 동일한 기본 ID를 설정합니다.
1. Experience Platform에서 Customer Journey Analytics으로 데이터를 인제스트하는 데이터 연결을 구성합니다. 데이터가 데이터 호수에 도달하면 90분 이내에 Customer Journey Analytics으로 전달됩니다.
1. 보기에 포함할 특정 차원 및 지표를 선택할 수 있도록 연결에서 데이터 보기를 구성합니다. 속성 및 할당 설정은 데이터 보기에서도 구성됩니다. 이러한 설정은 보고서 시간에 계산됩니다.
1. Analysis Workspace 내에서 대시보드 및 보고서를 구성하는 프로젝트를 만듭니다.

## 구현 고려 사항

### ID 연결 고려 사항

* 분리할 시계열 데이터는 모든 레코드에 동일한 id 네임스페이스가 있어야 합니다. 콜 센터 데이터를 익명 장치 데이터에 연결하려면 디지털 ID를 호출 ID에 연결해야 합니다. 이러한 단점은 몇 가지 가능한 메커니즘을 통해 발생할 수 있습니다.
   * 해당 시간의 해당 방문자에 대한 고유 전화 번호인 전화 걸기와 관계를 추적하는 조회 테이블.
   * 지원을 요청하기 전에 사용자가 인증을 받아야 하며 이 인증을 콜 에이전트가 결정하는 식별자(예: 전화 번호 또는 이메일)에 연결합니다.
   * 온보딩 파트너를 사용하여 지원 요청에 연결된 알려진 식별자가 있는 온라인 장치 식별자를 입력합니다.
* 서로 다른 데이터 세트를 통합하는 결합 프로세스에는 데이터 세트에서 공통적인 기본 개인/엔티티 키가 필요합니다.
* 보조 키 기반 조합은 현재 지원되지 않습니다.
* 필드 기반 ID 연결 프로세스를 사용하면 인증 ID와 같은 후속 임시 ID 레코드를 기준으로 행에서 ID를 다시 입력할 수 있습니다. 이 프로세스를 통해 장치 또는 쿠키 수준이 아니라 개인 수준에서 분석을 위해 서로 다른 레코드를 단일 ID로 해결할 수 있습니다.
* 스티칭은 한 주에 한 번, 스티치를 한 후에 다시 재생합니다.

## FAQ

* Customer Journey Analytics의 데이터 모델의 다운스트림에 미치는 영향은 무엇입니까?

   동일한 XDM 필드의 개체 및 속성은 Customer Journey Analytics에서 하나의 차원으로 병합됩니다. 여러 데이터 집합의 여러 특성을 동일한 CJA 차원으로 병합하려면 데이터 집합은 동일한 XDM 필드 또는 스키마를 참조해야 합니다.

## 관련 설명서

* [Customer Journey Analytics 제품 설명](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics 설명서](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Customer Journey Analytics 자습서](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
