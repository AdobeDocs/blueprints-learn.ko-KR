---
title: Developer Console 설정
description: DEP CLI에서 사용하는 Experience Platform 및 Journey Optimizer API에 대한 OAuth 서버 간 자격 증명으로 Adobe Developer Console 프로젝트를 만듭니다.
doc-type: article
solution: Experience Platform
exl-id: 8b8f2a3e-2f4a-4b0e-9c5a-6e0c2b7a1d4f
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Developer Console 설정

>[!WARNING]
>
>자신의 속도에 맞게 실습을 진행하는 경우에만 필요합니다. 라이브 교육 과정 또는 이벤트에 있는 경우 샌드박스가 이미 배포되었습니다.

DEP CLI는 Adobe Developer Console 프로젝트의 OAuth 서버 간 자격 증명을 사용하여 샌드박스를 인증합니다. 이 페이지는 해당 프로젝트를 만드는 과정을 안내합니다. 이 작업은 한 번만 수행하면 됩니다. 아래에 설명된 두 API를 모두 추가하면 AEP Foundations 및 AJO Architecture Foundations 트랙에서 동일한 자격 증명이 작동합니다.

>[!NOTE]
>
>Adobe Experience Platform에 대한 자격 증명이 포함된 Developer Console 프로젝트가 이미 있는 경우(필요한 경우 Adobe Journey Optimizer) 이 섹션을 건너뛰고 [배포 지침](deployment-instructions.md)(으)로 바로 이동합니다.

## 필요 조건

- 조직에 대한 개발자 액세스 권한이 있는 Adobe ID
- 비어 있고 유형이 `dev`인 Adobe Experience Platform 샌드박스
- 해당 샌드박스에 대해 모든 권한이 부여된 Adobe Experience Platform 역할(확실하지 않은 경우 시스템 관리자에게 문의)

## 프로젝트 만들기

1. [Adobe Developer Console](https://developer.adobe.com/console)&#x200B;(으)로 이동하여 로그인
1. 둘 이상의 조직에 액세스할 수 있는 경우 오른쪽 상단의 조직 전환기를 사용하여 올바른 조직을 선택합니다
1. **새 프로젝트 만들기** 선택
1. 나중에 알아볼 수 있도록 프로젝트 이름을 변경합니다(예: `DEP Sandbox`).

## Experience Platform API 추가

1. 프로젝트 개요에서 **API 추가**&#x200B;를 선택합니다.
1. **Adobe Experience Platform** 제품 아이콘을 선택한 다음 **Adobe Experience Platform API**&#x200B;를 선택합니다.
1. **다음** 선택
1. 인증 유형으로 **OAuth 서버 간**&#x200B;을(를) 선택하고 **다음**&#x200B;을(를) 선택합니다.
1. 자격 증명의 이름을 지정하고 **다음**&#x200B;을(를) 선택하십시오.
1. 사용 중인 샌드박스와 일치하는 제품 프로필을 선택한 다음 **구성된 API 저장**&#x200B;을 선택합니다.

## Adobe Journey Optimizer API 추가

1. 프로젝트 개요에서 **API 추가**&#x200B;를 선택합니다.
1. **Adobe Journey Optimizer** 제품 아이콘을 선택하고 관련 API를 선택하십시오
1. **OAuth 서버 간** 선택
1. 동일한 제품 프로필을 선택하고 **구성된 API 저장**&#x200B;을 선택합니다.

>[!NOTE]
>
>새 자격 증명을 만들지 않고 위에서 만든 자격 증명을 재사용합니다. CLI에는 범위가 결합된 단일 자격 증명 집합만 필요합니다.



## 값 수집

자격 증명의 **OAuth 서버 간** 개요 페이지를 엽니다. CLI 환경 파일에는 다음 네 가지 값이 필요합니다.

| **개발 콘솔 값** | **환경 파일 필드** |
| --------------------- | ------------------------------- |
| 클라이언트 ID | `API_KEY` |
| 클라이언트 암호 | `CLIENT_SECRET` |
| 조직 ID | `IMS_ORG`(`@AdobeOrg`에 종료) |
| 범위 | `SCOPES` |

>[!NOTE]
>
>자격 증명 페이지에 표시된 기본 범위를 복사합니다. 수동으로 추가할 필요가 없습니다. 위에서 두 API를 모두 추가한 경우 범위 목록에 두 API가 모두 자동으로 포함됩니다.

이 페이지를 열어 두거나 이 네 가지 값을 안전한 곳에 복사하십시오. 트랙의 설정 가이드의 다음 단계에서 CLI의 환경 파일에 붙여넣습니다.
