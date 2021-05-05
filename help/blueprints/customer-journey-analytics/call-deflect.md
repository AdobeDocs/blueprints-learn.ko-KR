---
title: 호출 처짐 분석 블루프린트
description: 고객이 콜센터에 연락하기 전에 어떤 행동을 보이는지 분석합니다.
solution: Experience Platform, Customer Journey Analytics
kt: 7209
exl-id: 13593c1c-4c58-4b8a-aa6c-7530fd679a14
translation-type: tm+mt
source-git-commit: 9fe9d67c5f97b633e45155bd54e2006f1b797332
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 93%

---

# 통화 감소 여정 분석 블루프린트

고객이 콜센터에 연락하기 전에 어떤 행동을 보이는지 데스크탑과 모바일 채널에 걸쳐 분석합니다. 고객이 고객 지원 센터에 연락하기 전 달성하려 하는 행동, 보는 콘텐츠 및 검색하는 단어를 이해하여 고객 여정을 개선할 방안을 찾아봅니다. 고객이 문의할 필요 없이 문제를 해결할 수 있도록 개선할 여지가 있는 콘텐츠와 셀프 서비스 도구를 확인합니다.

## 사용 사례

* 고객이 지원 센터에 연락하기 전의 행동 분석
* 셀프 서비스 기능 개선 방안 확인

## 애플리케이션

* Adobe Experience Platform
* Customer Journey Analytics

## 통합 패턴

* Adobe Experience Platform → Customer Journey Analytics

## 아키텍처

<img src="assets/CJA.svg" alt="Customer Journey Analytics 블루프린트를 위한 참조 아키텍처" style="border:1px solid #4a4a4a" />

## 구현 단계

1. [데이터](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) 를 인제스트할 구성 요소를 만듭니다.
1. [데이터](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) 를 인제스트할 데이터세트를 만듭니다.
1. [데이터를 Experience Platform으로 수집합니다.
](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion)
데이터를 Customer Journey Analytics로 수집하려면 먼저 Platform으로 수집해야 합니다.
1. 크로스채널 이벤트 데이터 세트를 분석합니다.
통합 분석하는 데이터 세트는 공통 네임스페이스 ID를 가지거나 Customer Journey Analytics의 필드 기반 결합 기능을 통해 재입력되어야 합니다.  

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

* 시계열 데이터를 하나로 처리하려면 모든 기록에 대해 동일한 ID 네임스페이스를 설정해야 합니다. 콜센터 데이터와 익명 디바이스 데이터를 연결하려면 디지털 ID에 문의 연락 ID를 연결해야 합니다. 이 연결에는 몇 가지 메커니즘을 사용할 수 있습니다.
   * 문의 번호를 해당 방문자 고유 번호로 설정하고 룩업 테이블을 통해 관계를 추적 관찰합니다.
   * 사용자가 지원 요청에 앞서 인증하도록 하고 이 인증을 문의 매체(전화번호 또는 이메일)를 통해 확인되는 ID와 연결합니다.
   * 온보딩 파트너를 활용하여 지원 요청에 연결된 알려진 ID로 온라인 디바이스 ID를 입력합니다.
* 종류가 다른 데이터 세트를 통합 처리하려면 전체 데이터 세트에 걸쳐 동일한 기본 인물/항목 일반 키가 있어야 합니다.
* 보조 키 기반 통합은 현재 지원하지 않습니다.
* 필드 기반 ID 결합 처리는 다음에 오는 임시 ID 기록(예: 인증 ID)을 기반으로 행 단위로 ID를 재입력합니다. 이 과정을 통해 종류가 다른 기록을 단일 ID로 처리하여 디바이스 또는 쿠키 수준이 아닌 인물 수준에서 분석할 수 있습니다.
* 결합은 1주일에 한 번 수행하며, 결합을 완료하면 다시 시작합니다.

## FAQ

* Customer Journey Analytics 데이터 모델은 하위 데이터에 어떤 영향을 주나요?

   같은 XDM 필드의 개체 및 속성은 Customer Journey Analytics에서 단일 차원으로 병합됩니다. 다양한 데이터 세트의 여러 속성을 같은 CJA 차원으로 병합하려면 데이터 세트에서 같은 XDM 필드 또는 스키마를 참조해야 합니다.

## 관련 설명서

* [Customer Journey Analytics 제품 소개](https://helpx.adobe.com/kr/legal/product-descriptions/customer-journey-analytics.html)
* [Customer Journey Analytics 설명서](https://experienceleague.adobe.com/docs/customer-journey-analytics.html?lang=ko)
* [Customer Journey Analytics 튜토리얼](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/overview.html?lang=ko)
