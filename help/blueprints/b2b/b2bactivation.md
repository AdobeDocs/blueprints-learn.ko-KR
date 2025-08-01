---
title: B2B 대상자 및 프로필 활성화 블루프린트
description: Real-time Customer Data Platform을 통해 계정 기반 대상자 및 프로필 중심적 고객 경험을 제공합니다.
solution: Real-Time Customer Data Platform
kt: 9311
exl-id: 5215d077-b0a9-4417-ae9b-f4961d4a73fa
source-git-commit: 0509c5a8ce92c25040262130a5f583cdd7f08e59
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 52%

---

# B2B 대상자 및 프로필 활성화 블루프린트

개별 고객과 연결된 계정, 기회 및 리드 정보를 사용하여 실행 가능한 B2B 프로필을 만들어 여러 채널에서의 개인화 및 타겟팅을 개선합니다.

## 사용 사례

* 계정, 기회 및 리드를 포함한 B2B 데이터에 대해 채널 간에 타겟팅 및 개인화를 위한 대상자 그룹을 만듭니다.
* 타겟팅 및 개인화를 위해 모든 Experience Platform 대상에 대상자를 활성화합니다.
* 계정 대상(예: 회사 목록)을 만들고 타기팅 및 판매 전달을 위해 클라우드 스토리지 대상에 회사 목록을 입력 또는 내보내기로 허용하는 LinkedIn과 같은 대상을 통해 해당 회사를 타기팅합니다.

## 애플리케이션

* Real-time Customer Data Platform B2B 에디션

## 통합 패턴

* B2B 데이터 소스(Marketo, Salesforce 등) -> Real-time Customer Data Platform B2B edition -> 대상
* 다양한 B2B 데이터 소스를 사용하여 계정, 리드, 기회 및 사용자 데이터를 Real-time Customer Data Platform의 B2B edition에 매핑할 수 있습니다.

## 아키텍처

![B2B 활성화 블루프린트에 대한 참조 아키텍처](assets/b2b-activation.png)

## 가드레일

* Marketo Engage 관련 가드 레일 및 구현 단계는 Marketo Engage이 소스 및/또는 대상으로 사용되는 경우에만 관련이 있습니다.

* 데이터 모델, 크기 및 세분화에 대한 자세한 내용과 보호 기능은 [배포 보호 문서](../experience-platform/guardrails.md)를 참조하세요.


### 다중 인스턴스 및 IMS 조직 지원:

다음은 매핑 Experience Platform 및 Marketo Engage 인스턴스의 지원되는 패턴을 간략하게 설명합니다.

#### Marketo을 Experience Platform의 데이터 소스로 사용:

* 단일 Experience Platform 인스턴스에 대한 다중 Marketo Engage 인스턴스가 지원됩니다.
* 다중 Experience Platform 인스턴스에 대한 단일 Marketo Engage 인스턴스는 지원되지 않습니다.
* 단일 Experience Platform 인스턴스와 다중 샌드박스에 대한 단일 Marketo Engage 인스턴스가 지원됩니다.

#### Marketo을 Experience Platform 대상으로 사용:

* 다중 Marketo Engage 인스턴스에 대한 Experience Platform이 지원됩니다
* 단일 Marketo Engage 인스턴스에 대한 다중 Experience Platform 인스턴스가 지원됩니다

#### Experience Platform 프로필 및 세분화 가드 레일:

* Experience Platform에 대한 프로필 및 세분화 가드레일 살펴보기 - [프로필 및 세분화 가드레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* 계정, 리드, 기회를 포함하는 B2B 세그먼트는 다중 엔터티 관계를 사용하므로 세그먼트 평가가 일괄 처리됩니다. 스트리밍 세분화는 사용자 및 이벤트로 제한된 세그먼트에 대해 지원됩니다.
* 일괄 처리 b2b 세그먼트를 스트리밍 또는 에지 세그먼트에 대한 입력으로 포함하여 스트리밍 b2b 세그먼트 사용 사례를 지원합니다. 배치 세그먼트 멤버십은 최신 일일 배치 세분화 평가 결과를 기반으로 합니다.

#### Experience Platform - Marketo Engage 소스 커넥터:

* 데이터 양에 따라 기록 채우기를 완료하는 데 최대 7일이 걸릴 수 있습니다.
* Marketo에서 진행 중인 데이터 업데이트 및 변경 사항은 스트리밍 API를 통해 Experience Platform으로 전송되며, API는 프로필에 최대 10분 동안 대기할 수 있으며 볼륨에 따라 데이터 레이크에 최대 60분 정도 걸릴 수 있습니다.

#### Experience Platform - Marketo 대상 커넥터:

* Real-time Customer Data Platform에서 Marketo Engage으로 세그먼트를 공유하는 스트리밍 방식은 세그먼트 평가 후 최대 15분 정도 소요될 수 있습니다. 처음 활성화하기 전에 세그먼트에 이미 있던 프로필 채우기는 최대 24시간이 걸릴 수 있습니다.
* 일괄 처리 세분화는 Experience Platform 세분화 일정을 기반으로 하루에 한 번 공유됩니다. 다중 엔티티 관계를 사용하는 B2B 세그먼트(예: 계정 및 영업 기회 객체의 데이터를 사용하는 세그먼트)는 항상 배치 모드에서 실행됩니다.

#### Marketo Engage 가드 레일:

* Marketo Engage의 연락처 및 리드에 맞추기 위해 Real-time Customer Data Platform 대상자는 Marketo Engage에서 직접 연락처와 리드를 수집하고 정의해야 합니다.
* RTCDP Marketo 대상은 세그먼트에 있지만 Marketo에 없는 고객을 위해 Marketo에서 새로운 잠재 고객을 선택적으로 만들 수 있습니다.

#### 대상 가드 레일

* 대상에 대한 특정 지침은 대상 설명서를 참조하십시오. [대상 가드 레일](https://experienceleague.adobe.com/docs/experience-platform/destinations/guardrails.html?lang=ko)


## 구현 단계

Real-time Customer Data Platform의 B2B 버전을 구현하고 구성하는 방법에 대한 지침은 Real-time Customer Data Platform 설명서의 B2B 버전을 참조하십시오. [Real-time Customer Data Platform의 B2B 에디션](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=ko)

두 가지의 가능한 구현 패턴이 있습니다. Marketo Engage에서 B2B 데이터 및 프로필을 수집하는 기능 또는 다른 CRM 데이터 소스에서 B2B 데이터를 수집하는 기능 모두가 있습니다.

## 구현 시 고려 사항

블루프린트의 주요 고려 사항 및 구성에 대한 지침입니다.

* Marketo 포함 및 제외 CRM 통합:
구현에서 Marketo Engage을 소스로 사용하고 Marketo Engage이 CRM에 연결되어 있는 경우 CRM 데이터는 자동으로 동일한 연결을 통해 흐르기 때문에 Marketo을 통해 전달되지 않는 추가 CRM 데이터 개체가 없는 경우 CRM을 플랫폼에 직접 연결할 필요가 없습니다. 추가 테이블을 수집해야 하는 경우 Experience Platform 소스 커넥터를 사용합니다. 구현에서 Marketo Engage을 소스로 사용하지 않는 경우 CRM 소스 Experience Platform 커넥터를 사용하여 CRM 소스를 플랫폼에 직접 연결합니다.
* 활성화를 위해 대상을 Marketo Engage으로 푸시하는 Platform용 Marketo Engage 대상 커넥터는 일치하는 이메일 주소와 ECID를 기반으로 대상 구성원을 공유합니다. 연락처가 아직 없는 경우 새 잠재 고객을 만들 수 있는 옵션이 있습니다. 새 잠재 고객을 만들 때 Real-time Customer Data Platform의 최대 50개 프로필 속성(비어레이 또는 맵 속성)을 Marketo의 개인 필드에 매핑할 수 있습니다.

## 관련 설명서

* [Real-time Customer Data Platform의 B2B 에디션](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=ko)
* [Real-time Customer Data Platform B2B edition 시작하기](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial)
* [실시간 고객 데이터 플랫폼 B2B edition의 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=ko)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=ko)
* [Adobe Experience Platform - Marketo 소스 커넥터](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=ko)
* [Adobe Experience Platform - Marketo 대상 커넥터](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=ko)
