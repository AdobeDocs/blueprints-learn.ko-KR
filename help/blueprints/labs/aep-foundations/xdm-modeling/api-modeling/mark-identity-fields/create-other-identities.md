---
title: 다른 ID 만들기
description: 스키마 레지스트리 API를 사용하여 고객 계정 스키마에 대한 비기본 이메일 주소 ID 설명자를 만듭니다.
doc-type: article
solution: Experience Platform
exl-id: 22c40299-fb93-4d41-a23b-f8629df3e7b9
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 다른 ID 만들기

1. `XDM Schema Lab -> Create Identity Descriptors` 폴더에서 `Step 2 - Create Email Address Identity for Customer Account Schema` API 호출 클릭

   >[!CAUTION]
   >
   >아직 요청을 실행하지 마십시오.

   ![2단계 - 고객 계정 스키마 Postman 요청에 대한 전자 메일 주소 ID 만들기](assets/create-other-identities-step-2-postman-request.jpeg "2단계 - 전자 메일 주소 ID 설명자 만들기")



1. [스키마 만들기](../build-schema/create-schema.md) 랩 단계에서 저장한 `$id`을(를) 사용하여 요청 본문의 `xdm:sourceSchema` 값을 업데이트합니다.

1. 요청 본문의 `xdm:isPrimary` 값을 `false`(으)로 업데이트

   예만

   ```json
   {
     "@type": "xdm:descriptorIdentity",
     "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
     "xdm:sourceVersion": 1,
     "xdm:sourceProperty": "/personalEmail/address",
     "xdm:namespace": "Email",
     "xdm:property": "xdm:code",
     "xdm:isPrimary": false
   }
   ```

   >[!NOTE]
   >
   >위의 테넌트 이름(\_devbc)을 고유한 이름으로 업데이트해야 합니다



1. `Save` 단추를 계속 사용하기 전에 요청을 저장하십시오.

1. `Send` 단추를 클릭하여 API를 실행하십시오. 이제 아래와 같은 `201 Created` 응답이 표시됩니다.

![201 전자 메일 주소 ID 설명자를 만든 후 응답을 만들었습니다](assets/create-other-identities-201-created-response.png "전자 메일 주소에 대한 ID 설명자 성공")
