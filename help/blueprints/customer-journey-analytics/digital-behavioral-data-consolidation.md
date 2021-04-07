---
title: 디지털 행동 데이터 통합 청사진
description: 고객 여정에서 고객과의 인터랙션을 분석하고 인사이트를 추출할 수 있습니다.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
exl-id: b042909c-d323-40d5-8b35-f3e5e3e26694
translation-type: tm+mt
source-git-commit: 844fff1cefe367575beb5c03aa0f0d026eb9f39b
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# 디지털 행동 데이터 통합 청사진

다양한 웹, 모바일 및 오프라인 속성의 데이터를 통합하여 다양한 채널에서 고객 행동을 한 번에 파악할 수 있습니다.

## 사용 사례

* 데스크탑 및 모바일에서 고객과의 인터랙션을 분석하여 고객 행동을 파악하고 인사이트를 추출하여 디지털 고객 경험을 최적화할 수 있습니다.
* 고객 여정을 더 잘 이해하고 최적화하기 위해 고객 상호 작용 및 매장 내 구매와 같은 디지털 및 오프라인 채널을 비롯한 모든 채널에서 고객 상호 작용을 분석합니다. 

## 애플리케이션

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics(선택 사항)

## 통합 패턴

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics

## 아키텍처

<img src="assets/CJA.svg" alt="Customer Journey Analytics 청사진을 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 가드레일

Customer Journey Analytics에 데이터 통합:

* 호수 데이터 수집:API ~ 7GB/시간, 소스 커넥터 ~ 200GB/시간, ~ 15분, 호수로 스트리밍되는 Adobe Analytics 소스 커넥터는 ~ 45분.
* 데이터가 데이터 호수에 게시된 후 Customer Journey Analytics으로 처리하는 데 최대 90분이 걸릴 수 있습니다.

## 구현 단계

1. 데이터 집합 및 스키마를 구성합니다.
1. 데이터를 플랫폼에 인제스트
Customer Journey Analytics으로 처리하기 전에 데이터를 플랫폼에 수집해야 합니다.
1. 결합에서 분석할 크로스 채널 이벤트 데이터 세트를 분석하여 공통 네임스페이스 ID가 있는지 또는 Customer Journey Analytics의 필드 기반 스티칭 기능을 통해 다시 입력하는지 확인합니다. 

   >[!NOTE]
   >
   >Customer Journey Analytics은 현재 스티칭에 Experience Platform 프로필 또는 ID 서비스를 사용하지 않습니다.

1. 데이터를 기반으로 하는 필드 기반 ID를 사용자 요구에 맞게 준비하고 사용할 수 있도록 데이터 세트에 대해 Customer Journey Analytics으로 인제스트할 공통 키를 보장합니다.
1. 이벤트 데이터의 필드에 참여할 수 있는 기본 ID를 조회 데이터에 제공합니다. 라이센스에서 행으로 카운트됩니다.
1. 이벤트 데이터의 기본 ID와 프로필 데이터에 대해 동일한 기본 ID를 설정합니다.
1. Experience Platform에서 Customer Journey Analytics으로 데이터를 인제스트하는 데이터 연결을 구성합니다. 데이터가 데이터 호수에 도달하면 90분 이내에 Customer Journey Analytics으로 전달됩니다.
1. 보기에 포함할 특정 차원 및 지표를 선택할 수 있도록 연결에서 데이터 보기를 구성합니다. 속성 및 할당 설정은 데이터 보기에서도 구성됩니다. 이러한 설정은 보고서 시간에 계산됩니다.
1. Analysis Workspace 내에서 대시보드 및 보고서를 구성하는 프로젝트를 만듭니다.

## 구현 고려 사항

### ID 연결 고려 사항

* 분리할 시계열 데이터는 모든 레코드에 동일한 ID 네임스페이스가 있어야 합니다.
* 서로 다른 데이터 세트를 통합하는 결합 프로세스에는 데이터 세트에서 공통적인 기본 개인/엔티티 키가 필요합니다.
* 보조 키 기반 조합은 현재 지원되지 않습니다.
* 필드 기반 ID 연결 프로세스를 사용하면 인증 ID와 같은 후속 임시 ID 레코드를 기준으로 행에서 ID를 다시 입력할 수 있습니다. 따라서 장치 또는 쿠키 수준이 아니라 개인 수준에서 분석을 위해 개별 레코드를 단일 ID로 해결할 수 있습니다.
* 스티칭은 한 주에 한 번, 스티치를 한 후에 다시 재생합니다.

## FAQ

* Customer Journey Analytics의 데이터 모델의 다운스트림에 미치는 영향은 무엇입니까?

   동일한 XDM 필드의 개체 및 속성은 Customer Journey Analytics에서 하나의 차원으로 병합됩니다. 받는 사람  여러 데이터 집합의 여러 특성을 동일한 Customer Journey Analytics 차원으로 병합하면 데이터 집합은 동일한 XDM 필드 또는 스키마를 참조해야 합니다.

## 관련 설명서

* [Customer Journey Analytics 제품 설명](https://helpx.adobe.com/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics 설명서](https://experienceleague.adobe.com/docs/customer-journey-analytics.html)
* [Customer Journey Analytics 자습서](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html)
