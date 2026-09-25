---
title: B2B 대상 및 프로필 활성화
description: 채널 및 대상 전반에서 활성화를 위해 Real-Time Customer Data Platform B2B edition을 사용하여 계정 기반 및 사용자 기반 대상자를 제공합니다.
solution: Real-Time Customer Data Platform
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 5%
---

# B2B 대상 및 프로필 활성화

**Real-Time Customer Data Platform B2B edition**&#x200B;을(를) 사용하여 계정, 기회 및 개인 데이터를 통합 B2B 프로필로 모은 다음 LinkedIn, Marketo Engage 및 클라우드 저장소와 같은 대상 전반에서 사용자 대상과 계정 대상을 모두 활성화합니다. 이 블루프린트는 B2B 스키마를 디자인하고, 다중 엔티티 대상을 빌드하고, 여러 채널 및 대상을 활성화하기 위해 내보내고, **Journey Optimizer B2B Edition** 및 **Customer Journey Analytics B2B edition**&#x200B;과 같은 응용 프로그램에서 오케스트레이션 및 분석을 위해 내보내는 방법을 설명합니다.

## 사용 사례

- 계정, 기회 및 리드를 포함한 B2B 데이터를 기반으로 채널 간 타기팅 및 개인화를 위한 사람 대상을 만듭니다.
- **세그먼트** 접근 방식을 사용하여 계정 및 영업 기회 수준 특성과 사용자 수준 동작을 결합하는 다중 엔터티 대상을 만듭니다(예: &quot;지난 3일 동안 가격 책정 페이지를 방문했으며 업계 Y의 계정에 대해 단계 X에서 영업 기회의 의사 결정자인 사람&quot;).
- 타깃팅, 개인화, 판매 지원 및 분석을 위해 Experience Platform 및 클라우드 스토리지 대상(예: Marketo Engage, LinkedIn Matched Audiences, Google Customer Match, DV360, The Trade Desk, Amazon Ads, Bombora 및 Demandbase)에 대해 사람 및 계정 대상을 활성화합니다.

## 애플리케이션

- Real-Time Customer Data Platform B2B edition
- (선택 사항) **Customer Journey Analytics B2B edition**
- (선택 사항) **Journey Optimizer B2B Edition**

## 통합 패턴

이 블루프린트에 대한 일반적인 B2B 통합 패턴은 다음과 같습니다.

- **B2B 참여 및 CRM 소스 → RTCDP B2B → 대상**

  Marketo Engage, Salesforce 및 Microsoft Dynamics과 같은 B2B 참여 및 CRM 시스템은 표준 B2B 스키마를 사용하여 리드/연락처, 계정 및 기회를 **Real-Time CDP B2B edition**&#x200B;로 보냅니다. 여기에서 사용자와 계정의 대상은 다음을 포함한 대상으로 활성화됩니다.

  - Marketo Engage
  - LinkedIn/LinkedIn 일치하는 대상
  - Google Customer Match &amp; DV360
  - 트레이드 데스크
  - Amazon 광고
  - Trade Desk CRM, Criteo, Bing 및 기타 광고 플랫폼
  - 다운스트림용 Amazon S3, ADLS 및 Snowflake과 같은 클라우드 스토리지 대상

- **B2B 의도 및 이벤트 소스 → RTCDP B2B → 대상 →**

  B2B 의도 및 이벤트 소스(예: Bombora 의도, Demandbase 의도, PathFactory 및 RainFocus 스트림 의도 및 참여 이벤트)를 RTCDP B2B에 저장 이러한 이벤트는 표준 B2B 스키마에 매핑되며, 광고 및 마케팅 대상에 활성화할 수 있는 사람 및 계정 대상을 빌드하는 데 사용됩니다.

다양한 B2B 데이터 소스를 사용하여 표준 **B2B 스키마 및 관계**&#x200B;를 사용하여 계정, 리드, 기회 및 개인 데이터를 Real-Time Customer Data Platform의 B2B edition에 매핑할 수 있습니다.

## 아키텍처

![B2B 대상 및 프로필 활성화 블루프린트에 대한 참조 아키텍처](assets/b2b-audience-profile-activation.png){width="1000" zoomable="yes"}

## 가드레일

B2B 대상 및 프로필을 디자인할 때 다음 보호 기능 및 자격 요건 설명서를 참조하십시오.

- [Real-Time Customer Data Platform B2B edition 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Real-Time CDP B2B edition에 대한 세그멘테이션 사용 사례](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/segmentation/b2b)
- [프로필 및 세그먼테이션 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)
- [스트리밍 세분화 자격 기준 업데이트](https://experienceleague.adobe.com/ko/docs/experience-platform/segmentation/eligibility-criteria-update)

### 다중 인스턴스 및 IMS 조직 지원

다음은 매핑 Experience Platform 및 Marketo Engage 인스턴스의 지원되는 패턴을 간략하게 설명합니다.

#### Experience Platform에 데이터 소스로서의 Marketo

- 여러 Marketo Engage 인스턴스에서 하나의 Experience Platform 인스턴스로 지원됩니다.
- 다중 Experience Platform 인스턴스에 대한 단일 Marketo Engage 인스턴스는 지원되지 않습니다.
- 단일 Experience Platform 인스턴스와 다중 샌드박스에 대한 단일 Marketo Engage 인스턴스가 지원됩니다.

#### Experience Platform의 대상으로서의 Marketo

- 많은 Marketo Engage 인스턴스에 대한 Experience Platform이 지원됩니다.
- 많은 Experience Platform 인스턴스에서 하나의 Marketo Engage 인스턴스로 지원됩니다.

#### Experience Platform 프로필 및 세그멘테이션 보호

Experience Platform 프로필 및 세그멘테이션 보호 기능을 보려면 [프로필 및 세그멘테이션 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/profile/guardrails)을 참조하세요.

계정, 리드 또는 기회와 같은 B2B 엔터티를 포함하는 세그먼트는 다중 엔터티 관계에 의존하며 **batch**&#x200B;에서 평가됩니다. 반대로 B2B 엔터티를 통합하지 않는 사람 및 이벤트로 제한된 대상에 대해서는 **스트리밍 세분화**&#x200B;이 지원됩니다. 실시간에 가까운 B2B 활성화 시나리오의 경우 일괄 평가된 B2B 대상을 지원되는 스트리밍 또는 에지 대상에 대한 입력으로 사용하는 것이 좋습니다.

#### Experience Platform - Marketo Engage Source 커넥터

- [여기](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo) 설명서를 참조하세요.

#### Experience Platform - Marketo 대상 커넥터

- [여기](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/catalog/adobe/marketo-engage-connection) 설명서를 참조하세요.

#### 대상 가드 레일

- 각 대상에 대한 특정 지침은 대상 설명서를 참조하십시오. [대상 보호](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/guardrails).
- Facebook, Google Customer Match &amp; DV360, Microsoft Bing, The Trade Desk, Amazon Ads, Bombora, Demandbase 등과 같은 광고 대상의 경우 스키마 및 ID 전략에서 선택한 식별자(이메일, 모바일 광고 ID, 주소 필드, 계정 ID)가 해당 대상에 대해 지원되는 ID 및 매핑 기능과 일치하는지 확인하십시오.

## 구현 단계

Real-Time Customer Data Platform의 B2B edition을 구현하고 구성하는 방법에 대한 지침은 Real-Time CDP B2B edition 설명서([Real-Time Customer Data Platform의 B2B edition](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview))를 참조하십시오.

두 가지 구현 패턴은 일반적입니다.

- Marketo Engage(및 연결된 CRM)의 B2B 데이터 및 프로필을 RTCDP B2B edition으로 수집합니다.
- 관련 소스 커넥터를 사용하여 CRM 또는 기타 B2B 시스템에서 RTCDP B2B edition으로 직접 B2B 데이터를 수집합니다.

RTCDP B2B 아키텍처 업그레이드의 일부로, 이전에 사용된 일부 패턴은 이제 B2B 엔티티에 대해 더 이상 사용되지 않습니다. 자세한 내용은 자세한 설명서 [여기](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)를 참조하세요.

## 구현 시 고려 사항

블루프린트의 주요 고려 사항 및 구성에 대한 지침입니다.

- **Marketo과 CRM 통합**

  - 구현에서 Marketo Engage을 소스로 사용하고 Marketo Engage이 CRM에 연결되어 있는 경우 Marketo에 동기화되는 CRM 데이터(예: 리드/연락처, 계정, 기회)는 Marketo 소스 커넥터를 통해 RTCDP B2B edition으로 흐릅니다.
  - Marketo을 통해 전달되지 않는 추가 CRM 테이블 또는 특성(예: 사용자 지정 개체 또는 추가 필드)이 있는 경우, CRM 소스 커넥터를 사용하여 CRM 소스를 직접 Experience Platform에 연결하고 해당 테이블을 표준 B2B 스키마 및 관계에 매핑합니다.
  - CRM + Marketo 수집을 함께 디자인하여 RTCDP B2B에 있는 B2B 엔티티가 중복되거나 충돌하는 것을 방지하고 모든 B2B 엔티티가 표준 스키마를 준수하는지 확인합니다.

## 관련 설명서

- [Real-Time Customer Data Platform의 B2B edition](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview)
- [Real-Time Customer Data Platform B2B edition 시작하기](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial?lang=en)
- [Real-Time Customer Data Platform B2B edition 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [Real-Time Customer Data Platform B2B edition의 스키마](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/schemas/b2b)
- [Real-Time CDP B2B edition으로 아키텍처 업그레이드](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)
- [Adobe Experience Platform](https://experienceleague.adobe.com/ko/docs/experience-platform)
- [Marketo Engage](https://experienceleague.adobe.com/ko/docs/marketo/using/home)
- [Adobe Experience Platform - Marketo Source 커넥터](https://experienceleague.adobe.com/ko/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo)
- [Adobe Experience Platform - Marketo 대상 커넥터](https://experienceleague.adobe.com/ko/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-platform-segment-to-a-marketo-static-list)
- [대상 가드 레일](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/guardrails)
