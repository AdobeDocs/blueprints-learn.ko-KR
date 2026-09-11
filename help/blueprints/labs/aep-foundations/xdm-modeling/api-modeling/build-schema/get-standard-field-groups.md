---
title: 표준 필드 그룹 가져오기
description: 글로벌 스키마 레지스트리 API를 쿼리하여 고객 프로필 스키마를 구축하는 데 필요한 표준 XDM 필드 그룹의 $id를 찾아 저장합니다.
doc-type: article
solution: Experience Platform
exl-id: 62017ece-eef2-4785-afed-5c690c00ed02
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# 표준 필드 그룹 가져오기

>[!NOTE]
>
>**&quot;필드 그룹&quot;**&#x200B;은(는) 이전에 **&quot;Mixin&quot;**&#x200B;이라고 불렀으므로 API 요청 및 안내서 전체에서 이 용어를 서로 교환하여 사용할 수 있습니다.



## XDM 표준 필드 그룹 요청

1. `XDM Schema Lab -> Create Schema` 폴더에서 `Step 1 - Get XDM Standard Field Groups` API 호출 클릭
1. `Send` 단추를 클릭하여 호출 실행



**요청**

![1단계 - XDM 표준 필드 그룹 API 요청 가져오기](assets/get-standard-field-groups-step-1-request.jpeg "1단계 - 요청")

>[!NOTE]
>
>아래 요청 URL에서 `global` 값을 사용하십시오.
>
>https\://platform.adobe.io/data/foundation/schemaregistry/**global**/mixins
>
>`global`은(는) XDM 표준 구성 요소(이 경우 필드 그룹/mixin)만 요청하는 데 사용됩니다. Experience Platform XDM 레지스트리에는 Adobe과 테넌트(즉, 사용자 지정)의 두 가지 유형의 소유자가 있습니다.
>
>- Adobe에서 만든 개체는 모든 XDM 목록 또는 조회 요청에서 항상 `global`이라는 단어를 사용합니다
>- 테넌트가 만든 개체(즉, 사용자 지정)는 XDM 목록 또는 조회 호출에서 항상 `tenant` 단어를 사용합니다.



**응답**

![XDM 표준 필드 그룹을 나열하는 API 응답](assets/get-standard-field-groups-step-1-response.png "1단계 응답")


## 필수 XDM 표준 필드 그룹 식별

스키마는 항상 하나 이상의 필드 그룹과 클래스로 구성됩니다.  연결 5G 개인 프로필 스키마의 경우 스키마에 필요한 표준 XDM 필드 그룹을 찾습니다.

- 인구 통계 세부 정보
- 개인 연락처 세부 정보
- 동의 및 환경 설정 세부 정보



1. 호출 응답에서 `Demographic Details` 필드 그룹을 검색합니다.
1. 필드 그룹의 `$id`을(를) 복사하고 나중에 참조할 수 있도록 어딘가에 저장하십시오.
1. 위에 나열된 다른 두 필드 그룹에 대해 1~2단계를 반복합니다

![API 응답에 있는 인구 통계 세부 정보 필드 그룹](assets/get-standard-field-groups-demographic-details-field-group.png)

>[!WARNING]
>
>세 개의 `$ids`을(를) 모두 어딘가에 저장할 때까지 계속하지 마십시오.  나중에 고객 계정 스키마를 만드는 데 필요합니다
