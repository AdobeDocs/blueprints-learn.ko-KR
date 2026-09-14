---
title: 기본 ID 만들기
description: 스키마 레지스트리 API를 사용하여 고객 계정 스키마에 대한 기본 customerID ID 설명자를 만듭니다.
doc-type: article
solution: Experience Platform
exl-id: db690081-e857-4875-8bb9-7ac197d73cab
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%
---

# 기본 ID 만들기

1. `XDM Schema Lab -> Create Identity Descriptors` 폴더에서 `Step 1 - Create Primary Identity for Customer Account Schema` API 요청 클릭

   ![1단계 - 고객 계정 스키마 Postman 요청에 대한 기본 Id 만들기](assets/create-primary-identity-step-1-postman-request.jpeg "1단계 - 고객 계정 스키마에 대한 기본 Id 만들기")

   >[!CAUTION]
   >
   >아직 요청을 실행하지 않음



1. [스키마 만들기](../build-schema/create-schema.md) 랩 단계에서 저장한 `$id`을(를) 사용하여 요청 본문의 `xdm:sourceSchema` 값을 업데이트합니다.

1. 요청 본문의 `xdm:isPrimary` 값을 `true`(으)로 업데이트

   예만

   ```json
   {
     "@type": "xdm:descriptorIdentity",
     "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
     "xdm:sourceVersion": 1,
     "xdm:sourceProperty": "/_devbc/customerID",
     "xdm:namespace": "customerID",
     "xdm:property": "xdm:code",
     "xdm:isPrimary": true
   }
   ```

   >[!NOTE]
   >
   >위의 테넌트 이름(\_devbc)을 고유한 이름으로 업데이트해야 합니다



1. `Save` 단추를 계속 사용하기 전에 요청을 저장하십시오.

1. `Send` 단추를 클릭하여 API를 실행하십시오. 이제 아래와 같이 `201 Created` 응답이 표시됩니다.

![201 기본 ID 설명자를 만든 후 응답을 만들었습니다](assets/create-primary-identity-201-created-response.png "기본 ID 설명자를 만들었습니다")

>[!SUCCESS]
>
>축하합니다!  스키마에 기본 ID 설명자를 만들었습니다.
