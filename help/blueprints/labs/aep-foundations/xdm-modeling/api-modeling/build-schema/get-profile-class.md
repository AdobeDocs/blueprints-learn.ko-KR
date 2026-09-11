---
hold: true
title: 프로필 클래스 가져오기
description: 사용자 지정 스키마에서 사용하기 위해 XDM 개인 프로필 클래스의 $id를 검색하고 저장하려면 전역 스키마 레지스트리 API를 호출하십시오.
doc-type: article
solution: Experience Platform
exl-id: d87c21a2-dad4-4666-b917-cdf8e16058d4
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# 프로필 클래스 가져오기

## 3단계 실행 - 프로필 클래스 가져오기

1. `XDM API Lab -> Create Schema` 폴더에서 `Step 3 - Get Profile Class` 요청을 클릭합니다.
1. `Send` 단추를 클릭하여 실행

![3단계 - 프로필 클래스 API 요청 가져오기](assets/get-profile-class-step-3-api-request.jpeg "3단계 - 프로필 클래스 API 요청 가져오기")

>[!NOTE]
>
>GET 요청에서 `global` 경로: .../schemregistry/**global**/classes를 확인합니다. `global`을(를) 사용하면 Adobe 표준 XDM 개체만 반환하려는 스키마 레지스트리에 표시됩니다.


## 클래스 $id를 찾아 저장합니다.

API 요청을 실행한 후 다음 단계를 수행하여 XDM 개별 프로필 클래스에 대한 `$id`을(를) 찾아 저장합니다.

1. 응답에서 `XDM Individual Profile` 클래스 검색
1. `XDM Individual Profile` 클래스에 대한 `$id`을(를) 복사하고 나중에 참조할 수 있는 위치에 저장합니다.

![API 응답에 있는 XDM 개별 프로필 클래스](assets/get-profile-class-xdm-individual-profile-class.png "XDM 개별 프로필 클래스")

>[!WARNING]
>
>`$id`을(를) 어딘가에 저장할 때까지 계속하지 마십시오.  고객 계정 스키마를 만들려면 나중에 필요합니다
