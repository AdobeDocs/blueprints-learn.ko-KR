---
title: Adobe Real-Time CDP 활성화
description: Adobe Real-Time CDP에서 광고, 소셜, 클라우드 스토리지 및 엔터프라이즈 대상으로 대상 및 프로필 데이터를 활성화하기 위한 아키텍처 참조.
solution: Real-Time Customer Data Platform, Experience Platform
source-git-commit: ce7331f279a6e59db95ca3b763148440598cde84
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%
---
# Adobe Real-Time CDP 활성화

이 아키텍처는 Adobe [!DNL Real-Time Customer Data Platform]&#x200B;([!DNL Real-Time CDP])이(가) 스트리밍 및 일괄 데이터 흐름을 통해 광고, 소셜, 클라우드 스토리지 및 엔터프라이즈 대상으로 대상과 프로필 데이터를 활성화하는 방법을 보여 줍니다.

## 대상자 및 프로필 활성화

아키텍처는 [!DNL Real-Time CDP]개의 대상 및 프로필에서 대상 애플리케이션으로의 공유 활성화 경로를 보여 줍니다. 여기에는 광고 및 소셜 플랫폼을 위한 대상 활성화와 스토리지, 분석 및 다운스트림 애플리케이션 워크플로우에 사용되는 엔터프라이즈 대상이 포함됩니다.

![Adobe Real-Time CDP 대상 및 프로필 활성화 아키텍처](assets/real_time_cdp_activation.png){width="1000" zoomable="yes"}

## 지원되는 사용 사례 패턴

위의 아키텍처는 다음과 같은 사용 사례 패턴을 지원합니다.

- [대상에 대한 대상 활성화](/help/blueprints/use-case-patterns/audience-building-activation/audience-activation-to-destinations.md) — 평가된 대상을 광고, 소셜, 클라우드 스토리지, CRM 및 기타 엔터프라이즈 대상으로 활성화합니다.
- [익명 방문자 웹 개인화](/help/blueprints/use-case-patterns/personalization/anonymous-visitor-web-personalization.md) - 디지털 채널에서 대상 활성화 및 프로필 기반 개인화를 지원합니다.

## 기본 데이터 흐름 및 통합 지점

- 여러 원본의 고객 데이터를 [!DNL Real-Time CDP]&#x200B;(으)로 수집합니다.
- [!DNL Real-Time Customer Profile]에서 ID 및 프로필 특성을 통합합니다.
- 프로필을 대상자로 평가하여 활성화합니다.
- 광고, 소셜, 클라우드 스토리지 및 엔터프라이즈 대상에 대한 대상자 및 프로필 변경 사항을 스트리밍 또는 일괄 처리합니다.
- 다운스트림 마케팅, 판매, 지원, 분석 및 개인화 워크플로우에서 활성화된 프로필 및 대상 데이터를 사용합니다.

## 추가 읽기

- [Adobe Real-Time CDP 대상](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/home)
- [대상에 대상 활성화](https://experienceleague.adobe.com/ko/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations)
- [Adobe Real-Time CDP 보호 기능](https://experienceleague.adobe.com/ko/docs/experience-platform/rtcdp/guardrails/overview)
