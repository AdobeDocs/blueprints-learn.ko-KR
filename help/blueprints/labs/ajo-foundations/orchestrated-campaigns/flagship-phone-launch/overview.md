---
title: 플래그십 폰 출시
description: 플래그십 폰 출시 후 SMS 업그레이드 오퍼를 통해 계정 소유자와 개별 회선을 타깃팅하는 오케스트레이션된 캠페인 구축에 대한 개요를 살펴보십시오.
doc-type: overview-page
solution: Experience Platform
exl-id: 04c509f1-aa10-4d29-aa59-5e627b79e498
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%
---

# 플래그십 폰 출시

## 필요 조건

>[!WARNING]
>
>이 실습을 시작하기 전에 아래 실습을 완료해야 합니다.

- **Postman 설치** **—>** [Postman 설치](../../postman-setup/postman-installation.md)
- **데이터 저장소 — 동작 중인 관계 저장소** **—>** [프로필 대상 Dimension](../../data-stores/relational-store-in-action/profile-target-dimension.md)
- **데이터 저장소 — 전자 메일 채널 구성 —>** [관계형 구성](../../data-stores/configure-email-channels/configure-for-relational.md)
  *(이 설정 단계를 완료하는 데 최대 3시간 소요)*

이러한 실습을 완료하지 않은 경우 계속하기 전에 지금 완료하십시오.

>[!CAUTION]
>
>이 실습에서는 SMS 채널 구성 단계를 완료하려면 샌드박스에 SMS 자격 증명이 있어야 합니다. 실제 메시지는 전송되지 않지만 Twilio 자격 증명이 있어야 합니다. 자습하고 아직 프로비전하지 않은 경우 [설정](../../setup.md)을(를) 참조하십시오.

## 랩 개요

이 비디오에서는 캠페인 타기팅 계정 보유자와 개별 라인을 구축하기 전에 플래그십 폰 출시 사용 사례가 어떻게 오케스트레이션된 캠페인에 매핑되는지 알아보고 중요한 사고 질문과 아키텍처를 요약합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3486217/)

## 학습 목표

- 다양한 워크플로우 활동을 사용하여 오케스트레이션된 캠페인 구축
- 대상 작성 활동을 사용하여 대상 구성
- SMS 채널 설정 방법 이해
- 대상자 포털에 대상자 저장
- 이메일 및 SMS 메시지로 고객 계정과 개별 라인을 모두 타겟팅합니다



## 사용 사례 설명

제조업체의 최신 플래그십 디바이스를 출시한 직후 이전 모델을 보유한 계정 소유자와 라인 사용자에게 최신 모바일 기술로 업그레이드하도록 권유하는 타기팅된 메시지를 보냅니다.

**키 설명선:**

- 모든 고객 라인의 대상자를 대상자 포털에 저장
- 메시지를 통해 개별 라인 및 계정 소유자를 타겟팅합니다(SMS 사용).

>[!NOTE]
>
>이 시나리오는 **통신 계약 업그레이드 캠페인**&#x200B;을 시뮬레이트합니다. 보조(종속) 회선이 타깃팅된 업그레이드 메시지를 받습니다.
