---
title: 작동 중인 메시지 게재
description: 기본 계획 구성원을 타겟팅하고 AEP 프로필과 관계형 스키마 이메일 채널 간의 게재 동작을 비교하는 오케스트레이션된 캠페인 구축에 대한 개요를 확인합니다.
doc-type: overview-page
solution: Experience Platform
exl-id: 84b16fff-f733-439a-9a93-726811e543ce
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%
---

# 작동 중인 메시지 게재

## 필요 조건

>[!WARNING]
>
>이 실습을 시작하기 전에 아래 실습을 완료해야 합니다.

- **데이터 저장소 — 동작 중인 관계 저장소** **—>** [프로필 대상 Dimension](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **데이터 저장소 —>** [전자 메일 채널 구성](../../data-stores/configure-email-channels/overview.md) *(이 설정 단계는 완료되는 데 3시간 이내 소요)*

이러한 실습을 완료하지 않은 경우 계속하기 전에 지금 완료하십시오.

>[!CAUTION]
>
>이 실습에는 샌드박스에서 Adobe에게 위임된 하위 도메인이 필요합니다. 자습하고 아직 없으면 [설정](../../setup.md)을 참조하세요.

## 랩 개요

이 비디오에서는 기본 계획 멤버 대상 구축 및 포크와 프로필 및 관계형 이메일 채널 간 게재 결과 비교 등 이 랩에 대해 오케스트레이션된 캠페인을 구축하는 방법을 알아봅니다.

>[!VIDEO](https://video.tv.adobe.com/v/3486541/)

## 학습 목표

- 여러 워크플로우 활동을 사용하여 오케스트레이션된 캠페인 구축
- 대상 작성 활동을 사용하여 대상 구성
- 대상을 포크하여 두 개의 분기를 만들고 이전 랩에서 만든 이메일 채널을 사용하여 메시지를 보냅니다
- 캠페인을 테스트하고 이메일 채널 간 동작의 차이점을 이해합니다

&quot;기본&quot; 계획 구성원을 타깃팅하려면 이 랩에서 캠페인을 만들고 오케스트레이션된 다양한 캠페인 설정이 이메일 채널 구성에 미치는 영향을 살펴보십시오.
