---
hold: true
title: Postman 설치
description: 나중에 Postman에서 API를 호출하기 전에 Labs를 설치하고 컬렉션, 환경 및 작업 영역 인터페이스에 대해 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: c277edb5-f758-4955-bcd7-b15a9b9ab949
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Postman 설치

## 목표

이 실습이 끝나면 향후 실습에서 필요한 후속 api 호출을 수행할 수 있도록 Postman을 설치하고 기본 작업 공간 및 환경을 구성할 수 있습니다.

&#x200B;> [!IMPORTANT]
>
>이 과정의 다양한 랩에 Postman이 필요합니다.  이미 Postman을 설치했더라도 이 실습을 완료하여 환경 파일 및 API 컬렉션이 설치되어 있고 제대로 설정되었는지 확인해야 합니다.



## Postman 설치

Postman 웹 사이트로 이동하여 Postman 앱을 다운로드하거나 웹 버전 —> [https://www.postman.com/download/](https://www.postman.com/download/)을 활용하십시오.

![Postman 웹 사이트의 Postman 다운로드 페이지](assets/postman-installation-postman-download.png)

## Postman 작업 공간 만들기(선택 사항)

*Postman을 처음 사용*&#x200B;하는 경우 처음 설치하는 것이므로 새 작업 영역을 만들 필요가 없습니다. 첫 번째 실행 시 로그인하지 않고 계속 진행하도록 선택하면 작업 영역이 필요하지 않은 경량 클라이언트를 사용합니다.

*이미 Postman에 익숙하고*&#x200B;이 설치되어 있다면 이미 로그인되어 있고 여러 작업 영역이 있을 수 있습니다. 이 경우 *이 부트캠프*&#x200B;에 대한 새 작업 영역을 만드는 것이 좋습니다. 지침은 [Postman 웹 사이트에서 찾을 수 있습니다.](https://learning.postman.com/docs/collaborating-in-postman/using-workspaces/create-workspaces/)

## Postman 인터페이스

Postman을 열고 애플리케이션의 몇 가지 영역을 빠르게 숙지합니다. Experience Platform 작업을 위해서는 애플리케이션의 몇 가지 주요 영역에만 집중하면 됩니다.

![사이드바, 헤더 및 기본 작업 영역에 레이블이 지정된 Postman 인터페이스 개요](assets/postman-installation-interface-overview.png "Postman 인터페이스")

## 사이드바

사이드바는 다양한 Postman 요소를 빠르게 탐색할 수 있는 곳입니다. Labs 중에는 아래 두 항목만 사용합니다.

**컬렉션** - 외부 위치에서 가져오거나 직접 만들 수 있는 저장된 요청 그룹입니다.

**환경** - Postman 요청에서 참조할 수 있는 변수 세트입니다. Experience Platform에서 Postman 환경은 IMS 조직 내의 Adobe 샌드박스와 동의어로 간주할 수 있습니다. Postman에서 환경의 함수를 사용합니다.



## 머리글

작업 공간 - 작업을 다양한 그룹(예: 프로젝트, 팀 등)으로 구성할 수 있습니다.



## 주 작업 영역

주요 작업 영역은 Postman에서 작업할 때 대부분의 작업을 수행하는 곳입니다. 모든 API 요청은 기본 작업 영역 내의 특정 탭에 표시됩니다.

**오른쪽 사이드바** - 선택한 현재 탭에 따라 도구에 대한 추가 액세스를 제공합니다. 몇 가지 기능을 예로 들자면 요청, 주석 및 코드 조각에 대한 설명서가 있습니다.

**환경 선택기** - API를 사용하여 작업할 때 다른 환경 간을 빠르게 전환하여 사전 구성된 변수에 액세스할 수 있습니다. Experience Platform을 사용하여 작업할 때 할당된 IMS 조직 내에서 특정 AEP 샌드박스로 작업할 때 이를 활용합니다.



## 바닥글

Postman 애플리케이션의 맨 아래쪽에는 수행한 호출에 대한 로그, 찾기 및 바꾸기에 대한 빠른 액세스 및 기타 다양한 기능을 빠르게 확인할 수 있는 함수 집합이 있습니다.



## 요약

이제 Postman이 설치되고 UI의 기본 사항을 이해해야 합니다
