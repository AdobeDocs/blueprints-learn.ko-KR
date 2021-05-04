---
title: 크로스 채널 여정 분석
description: 고객 여정 전반에 걸친 고객 상호 작용을 분석하여 인사이트를 얻습니다.
solution: Experience Platform, Customer Journey Analytics, Data Collection
kt: 7208
exl-id: b042909c-d323-40d5-8b35-f3e5e3e26694
translation-type: tm+mt
source-git-commit: 58368eb06b9bbd6c332424bdcfa2789dde7d4c2f
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 98%

---

# 크로스 채널 여정 분석 블루프린트

다양한 웹, 모바일 및 오프라인 속성에서 수집한 데이터를 통합하여 전 채널에 걸친 고객 행동을 통합된 단일 관점으로 분석합니다.

## 사용 사례

* 데스크탑과 모바일에 걸친 고객 상호 작용을 분석하여 고객 행동을 이해하고 디지털 고객 경험을 최적화하기 위한 인사이트를 얻습니다.
* 고객 여정을 더 잘 이해하고 최적화하기 위해 고객 지원 상호 작용과 매장 내 구매 등 디지털 및 오프라인 채널을 포함한 전 채널에 걸쳐 고객 상호 작용을 분석합니다.  

## 애플리케이션

* Adobe Experience Platform
* Customer Journey Analytics
* Adobe Analytics(선택 사항)

## 통합 패턴

* Adobe Experience Platform → Customer Journey Analytics
* Adobe Analytics → Adobe Experience Platform → Customer Journey Analytics

## 아키텍처

<img src="assets/CJA.svg" alt="Customer Journey Analytics 블루프린트를 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 구현 단계

1. 데이터 세트 및 스키마를 구성합니다.
1. 데이터를 Platform으로 수집합니다.
데이터를 Customer Journey Analytics로 처리하려면 먼저 Platform으로 수집해야 합니다.
1. 크로스채널 이벤트 데이터 세트를 통합 분석하여 공통 네임스페이스 ID를 가지거나 Customer Journey Analytics의 필드 기반 결합 기능을 통해 재입력되도록 합니다.  

   >[!NOTE]
   >
   >Customer Journey Analytics는 현재 데이터 결합에 Experience Platform 프로필 또는 ID 서비스를 사용하지 않습니다.

1. 데이터에 사용자 정의 준비 또는 필드 기반 ID 결합을 수행하여 시계열 데이터 세트에 걸쳐 일반 키가 Customer Journey Analytics로 수집되도록 합니다.
1. 룩업 데이터에 기본 ID를 설정하여 이벤트 데이터 내 필드에 들어갈 수 있도록 합니다. 라이센스 부여 시 행으로 취급됩니다.
1. 이벤트 데이터의 기본 ID와 동일한 기본 ID를 프로필 데이터에 설정합니다.
1. Experience Platform에서 Customer Journey Analytics로 데이터를 수집하기 위한 데이터 연결을 구성합니다. 데이터가 데이터 레이크에 도착하면 90분 내에 Customer Journey Analytics로 처리됩니다.
1. 연결에 대해 데이터 보기를 구성하여 보기에 들어갈 특정 차원 및 지표를 선택합니다. 기여도 분석 및 할당 속성도 데이터 보기에서 구성합니다. 이 설정은 보고 시에 계산됩니다.
1. 프로젝트를 만들어 Analysis Workspace 내 대시보드와 보고를 구성합니다.

## 구현 시 고려 사항

### ID 결합 시 주의 사항

* 시계열 데이터를 하나로 처리하려면 모든 기록에 대해 동일한 ID 네임스페이스를 설정해야 합니다.
* 종류가 다른 데이터 세트를 통합 처리하려면 전체 데이터 세트에 걸쳐 동일한 기본 인물/항목 일반 키가 있어야 합니다.
* 보조 키 기반 통합은 현재 지원하지 않습니다.
* 필드 기반 ID 결합 처리는 다음에 오는 임시 ID 기록(예: 인증 ID)을 기반으로 행 단위로 ID를 재입력합니다. 이를 통해 종류가 다른 기록을 단일 ID로 처리하여 디바이스 또는 쿠키 수준이 아닌 인물 수준에서 분석할 수 있습니다.
* 결합은 1주일에 한 번 수행하며, 결합을 완료하면 다시 시작합니다.

## FAQ

* Customer Journey Analytics 데이터 모델은 하위 데이터에 어떤 영향을 주나요?

   같은 XDM 필드의 개체 및 속성은 Customer Journey Analytics에서 단일 차원으로 병합됩니다. 다양한 데이터 세트의 여러 속성을 같은 Customer Journey Analytics 차원으로 병합하려면 데이터 세트에서 같은 XDM 필드 또는 스키마를 참조해야 합니다.

## 관련 설명서

* [Customer Journey Analytics 제품 소개](https://helpx.adobe.com/kr/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics 설명서](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=ko)
* [Customer Journey Analytics 튜토리얼](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html?lang=ko)
