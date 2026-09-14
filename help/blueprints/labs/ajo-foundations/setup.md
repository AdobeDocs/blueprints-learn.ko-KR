---
title: 설정
description: AJO Foundations 랩을 시작하기 전에 필요한 샌드박스 배포 및 Postman 구성 단계를 완료합니다.
doc-type: article

solution: Experience Platform
exl-id: 7c1a9e3d-5b8f-4a2e-9c6d-3f7b0e4a8c2d
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 1%
---

# 설정

AJO Foundations Labs를 시작하기 전에 아래 설정 단계를 완료하십시오. 어떤 단계가 필요한지는 이 부트캠프를 어떻게 수강하느냐에 따라 다릅니다.

## 샌드박스 설정

>[!NOTE]
>
>라이브 교육 과정 또는 이벤트에 있는 경우 샌드박스가 이미 배포된 상태입니다. 이 섹션을 건너뛰고 바로 아래 Postman 설정으로 이동합니다.

랩 자산이 배포된 작업 샌드박스가 없는 경우 다음 단계를 완료하십시오.

- [Developer Console 설정](sandbox-setup/developer-console-setup.md)
- [배포 지침](sandbox-setup/deployment-instructions.md)

## Postman 설정

샌드박스가 프로비저닝된 방식에 관계없이 이 과정의 랩에 Postman이 필요합니다. 계속하기 전에 다음을 완료하십시오.

- [Postman 설치](postman-setup/postman-installation.md)
- [환경 파일 가져오기](postman-setup/import-environment-file.md)
- [API 컬렉션 가져오기](postman-setup/import-api-collection.md)

## 채널 사전 요구 사항

이 부트캠프의 후반부에 있는 두 개의 랩은 자습형 학습자만 준비해야 하는 외부 계정에 따라 다릅니다. 라이브 교육 과정이나 이벤트에 있는 경우 이미 프로비저닝되어 있습니다.

### 위임된 하위 도메인

[이메일 채널 구성](data-stores/configure-email-channels/overview.md) 랩 및 이에 따라 달라지는 모든 항목([작업 중 메시지 게재](orchestrated-campaigns/message-delivery-in-action/overview.md), [구매 후 흥분](journeys/post-purchase-excitement/overview.md) 및 [AJO 브랜드](content-authoring-with-ai/overview.md))에는 이메일을 보내기 위해 Adobe에 위임된 하위 도메인이 필요합니다. 도메인이 없는 경우 도메인 등록자(예: Namechap)에 등록합니다. 그런 다음 하위 도메인(예: `email.yourdomain.com`)을 Adobe에 위임하려면 Adobe의 [하위 도메인 위임 지침](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/configuration/delegate-subdomains/delegate-subdomain)을 따르십시오.

>[!NOTE]
>
>하위 도메인 위임은 전파하는 데 시간이 걸릴 수 있습니다. 이메일 채널 구성 랩에 도달하기 전에 이 위임을 시작하십시오.

### SMS 자격 증명

[플래그십 휴대폰 시작](orchestrated-campaigns/flagship-phone-launch/overview.md) 랩에서 Twilio를 통해 SMS 채널을 구성합니다. 메시지는 전송되지 않지만 구성을 완료하려면 작업 자격 증명이 필요합니다. 가장 간단한 옵션은 무료 [Twilio 체험판 계정](https://www.twilio.com/try-twilio)입니다. 계정 SID와 인증 토큰을 등록 및 찾는 방법은 Twilio의 [시작 안내서](https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account)를 참조하십시오.
