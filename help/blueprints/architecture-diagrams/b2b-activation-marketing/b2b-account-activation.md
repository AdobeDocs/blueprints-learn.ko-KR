---
title: Advertising 및 파일 대상에 대한 B2B 계정 활성화
description: 계정 기반 참여를 사용하여 계정 대상을 만들고 광고 대상 및 클라우드 스토리지에 활성화합니다.
solution: Real-Time Customer Data Platform
exl-id: 578c0019-6133-4508-ae9d-8a8a463376f0
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 1%
---

# 광고 대상 및 파일 대상에 대한 B2B 계정 활성화

계정 기반 참여를 통해 B2B 마케터는 **Real-Time Customer Data Platform B2B edition**&#x200B;에서 계정 대상(회사 목록)을 만들고 이러한 계정 대상을 LinkedIn 일치 대상, Bombora 및 Demandbase와 같은 광고 대상 및 클라우드 저장소 대상으로 활성화할 수 있습니다. 이러한 계정 대상은 타깃팅, 판매 지원 및 다운스트림 분석에 사용될 수 있습니다.

## 사용 사례

마케터는 계정 기반 서비스를 사용하여 세 가지 주요 사용 사례를 잠금 해제할 수 있습니다.

- **구매 그룹 차이를 메웁니다.** 마케터는 CMO 또는 CIO 역할에 대한 연락처가 없는 계정에 광고를 낼 수 있습니다. 먼저 &quot;CMO&quot; 또는 &quot;CIO&quot;라는 제목과의 접촉 없이 계정 대상을 구성한 다음, LinkedIn Matched Audiences 또는 기타 지원되는 광고 대상에서 대상을 활성화할 수 있습니다. 그런 다음 대상 내에서 &quot;CMO&quot; 또는 &quot;CIO&quot; 직함을 가진 대상자와 특정 사람을 대상으로 캠페인을 시작하여 이러한 새로운 담당자에게 연락하고 오퍼링의 이점을 강조할 수 있습니다.
- **기존 고객인 회사의 다른 부서에 상향 판매 또는 교차 판매:** 마케터는 3개월에서 9개월 전에 제품 X를 구매했지만 아직 제품 Y를 소유하지 않은 계정 대상을 구축할 수 있습니다. 그런 다음 이 계정 대상을 활성화하여 LinkedIn Matched Audiences, 다른 광고 플랫폼 또는 판매 및 마케팅 전달을 위한 클라우드 스토리지 내보내기를 통해 해당 타겟 대상에 대한 제품 Y의 이점을 강조할 수 있습니다.
- **경쟁 제품을 사용하는 대상 회사:** 마케터는 해당 계정에 연락처가 없어도 경쟁사 제품을 대체하기 위해 계정을 마케팅할 수 있습니다. 경쟁업체 제품의 소유권이나 사용을 보여 주는 파트너 또는 의도 데이터를 기반으로 계정 대상을 만든 다음, LinkedIn Matched Audiences 또는 기타 지원되는 광고 대상을 통해 활성화하여 확장을 위해 타겟 계정의 소스 연락처를 만들 수 있습니다.

## 애플리케이션

- Real-Time Customer Data Platform B2B edition
- (선택 사항) Customer Journey Analytics B2B edition

## 통합 패턴

이 블루프린트의 일반적인 통합 패턴은 다음과 같습니다.

- **B2B 참여 및 CRM 소스 → RTCDP B2B edition → 계정 대상자 → 대상**

  Marketo Engage, Salesforce 및 Microsoft Dynamics과 같은 CRM 시스템 및 B2B 참여는 표준 스키마 및 관계를 사용하여 **Real-Time CDP B2B edition**&#x200B;로 잠재 고객/연락처, 계정 및 기회를 보냅니다. 계정 대상은 이 통합 B2B 데이터 모델 위에 구축되고 광고 및 파일 대상에 활성화됩니다.

- **B2B 의도 및 이벤트 소스 → RTCDP B2B edition → 계정 대상자 → 대상**

  Bombora Intent 및 Demandbase Intent와 같은 B2B 의도 및 이벤트 소스는 의도 및 참여 이벤트를 Experience Platform으로 보냅니다. 이러한 데이터 세트는 표준 B2B 스키마에 매핑되므로 마케터는 계정 대상(예: 경쟁업체 주제에서 급증하는 계정)을 빌드하고 광고 및 클라우드 스토리지 대상에 활성화할 수 있습니다. 그런 다음 지원되는 Bombora 및 Demandbase와 같은 광고 파트너에 대해 계정 대상을 활성화할 수 있습니다.

## 아키텍처

![B2B 계정 활성화 블루프린트에 대한 참조 아키텍처](assets/b2b-account-activation.png){width="1000" zoomable="yes"}

## 계정 대상자 대상

- **일치하는 대상**
- **봄보라**
- **Demandbase**
- **클라우드 저장소 대상**
  - Azure Data Lake Storage Gen2
  - 데이터 랜딩 영역
  - SFTP
  - Azure Blob
  - AWS

계정 대상을 지원하는 최신 대상 목록은 대상 설명서 를 참조하십시오.

## 가드레일

계정 대상을 디자인하고 활성화할 때 다음 가드레일을 참조하십시오.

- [Real-Time Customer Data Platform B2B edition 보호 기능](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-guardrails?lang=en)
- [계정 대상자](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en)
- [계정 대상자 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)
- [프로필 및 세그먼테이션 보호](https://experienceleague.adobe.com/en/docs/experience-platform/profile/guardrails)
- [스트리밍 세분화 자격 기준 업데이트](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/eligibility-criteria-update)

## Real-Time Customer Data Platform B2B edition, 계정 대상자 만들기 및 활성화를 위한 구현 단계

- Real-Time Customer Data Platform B2B edition의 구현 단계는 [Real-Time Customer Data Platform B2B edition 시작하기](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-tutorial?lang=en) 설명서를 참조하십시오.
- 계정 대상자 만들기 단계는 [계정 대상자](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en) 설명서를 참조하십시오.
- 계정 대상자 활성화 단계는 [계정 대상자 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en) 설명서를 참조하십시오.

  - [LinkedIn 일치하는 대상](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en#required-mappings)에 대한 매핑이 필요합니다.

## 구현 시 고려 사항

LinkedIn 일치하는 대상에는 최소 대상 크기 요구 사항(예: 일치하는 구성원 300명)이 있습니다. LinkedIn Matched Audiences에 활성화된 계정 대상자가 이 요구 사항을 충족하지 않는 경우 캠페인을 시작하기 전에 대상 정의를 확장하여 일치 가능한 대상 크기를 늘려야 할 수 있습니다.

## 관련 설명서

- [B2B 대상 및 프로필 활성화 블루프린트](b2b-audience-profile-activation.md) - 사람 수준 및 계정 수준 B2B 활성화를 모두 다루는 상위 블루프린트입니다.
- [Real-Time Customer Data Platform의 B2B edition](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-overview?lang=en)
- [계정 대상자 만들기 및 활성화 - 튜토리얼 비디오](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/audiences/create-audiences-with-b2b-data?lang=en)
- [계정 대상자 만들기](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/account-audiences?lang=en)
- [계정 대상자 활성화](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-account-audiences?lang=en)
- [Adobe Experience Platform - LinkedIn 대상 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/social/linkedin?lang=en)
- [Real-Time CDP B2B edition의 스키마](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/schemas/b2b)
- [Real-Time CDP B2B edition으로 아키텍처 업그레이드](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdpb2b-intro/b2b-architecture-upgrade)
- [대상 가드 레일](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/guardrails)
