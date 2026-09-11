---
title: 액세스 토큰
description: Postman에서 OAuth 서버 간 액세스 토큰을 생성하고 AEP API 호출 인증에 필요한 헤더를 이해합니다.
doc-type: article
solution: Experience Platform
exl-id: e38a1bd4-5a09-40c6-8303-c3770801c864
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# 액세스 토큰

## API 보안 개요



Adobe 제품에 대한 보안 API 연결을 설정하려면 Adobe에서 OAuth 서버 간 자격 증명 생성을 제공합니다. 이렇게 하려면 먼저 Adobe Developer Console 내에서 개발자 프로젝트를 만들어야 합니다. Developer Console에 액세스하려면 Adobe Admin Console 내의 개발자 권한을 할당받아야 합니다. 이러한 권한이 있으면 다양한 Adobe 제품 관련 API를 사용하여 개발자 프로젝트를 만들 수 있습니다. 여기서 OAuth 서버 간 자격 증명이 실행됩니다. 액세스 토큰을 생성하려면 Adobe의 Identity Management 서비스(IMS)에 특정 클레임 세트를 전달해야 합니다. OAuth 서버 간 자격 증명의 경우 예제 호출은 다음과 같습니다.

```curl
curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3?client_id={CLIENT_ID}' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'client_secret={CLIENT_SECRET}&grant_type=client_credentials&scope={SCOPE}'
```

>[!NOTE]
>
>OAuth 서버 간 자격 증명 [여기](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/#generate-access-tokens)를 사용하여 개발자 프로젝트를 만드는 e2e 프로세스에 대해 자세히 알아볼 수 있습니다. 부트캠프의 경우 프로세스 😄의 이 단계를 &quot;손 흔들어&quot;겠습니다.



## Adobe Experience Platform + Adobe IMS

모든 Adobe 서비스에 대한 모든 요청에는 개발자 프로젝트 생성 중에 생성된 클라이언트 암호와 함께 인증 헤더에 액세스 토큰이 포함되어야 합니다. 또한 Experience Platform 및 관련 애플리케이션에는 각 요청에 두 개의 다른 헤더 매개 변수가 있어야 합니다.

- `x-gw-ims-org-id` - 이 매개 변수는 요청이 속한 `IMS Org`을(를) 지정하고 요청 처리가 적절한 SaaS 환경으로 확인되도록 합니다.
- `x-sandbox-name` - 이 매개 변수는 Experience Platform 내에서 요청을 처리할 샌드박스를 지정합니다.

Adobe이 API를 보호하는 방법과 API 사용에 필요한 사항을 이해했으므로 지금 사용하십시오.

>[!CAUTION]
>
>`x-sandbox-name` 매개 변수를 지정하지 않으면 예상대로 요청이 실패하지 않습니다. 대신 처리에 대한 요청의 기본값이 Experience Platform 환경에서 자동으로 프로비저닝되는 `default` 샌드박스로 설정됩니다

>[!NOTE]
>
>이 부트캠프의 일부로 개발자 프로젝트를 만들고 `access_token`을(를) 요청하는 데 필요한 모든 값이 포함된 Postman 환경 파일을 제공했습니다. 이 내용은 실습의 이전 단계에서 업로드한 것입니다

## Postman으로 인증

1. Postman을 시작하고 `IMS Authenticate` 디렉터리로 이동한 다음 해당 디렉터리를 클릭하여 요청을 엽니다.
1. 다음은 Postman의 오른쪽 위 모서리에 환경 드롭다운이 표시됩니다. 드롭다운에서 `AEP Bootcamp` 환경 선택
1. 이제 &quot;Send&quot; 버튼을 클릭하여 호출을 실행합니다.

![액세스 토큰을 생성하기 위해 IMS 인증 호출을 보낸 후 Postman 요청](assets/access-token-execute-ims-authenticate-request.png)

성공적인 응답은 다음과 같아야 합니다.

```none
200 OK Successful Authentication
```

성공한 응답

```json
{
    "token_type": "bearer",
    "access_token": "<value>",
    "expires_in": 86399979
}
```

`token_type` - 항상 형식 전달자가 됩니다.

`access_token` - 권한 부여를 증명하며 모든 API 호출의 권한 부여 헤더에 필요합니다.

액세스 토큰이 만료될 때까지 `expires_in` - 밀리초(오늘 만료 기간 24시간)

>[!TIP]
>
>축하합니다! 인증되었으며 액세스\_token이 이제 환경 파일에 저장됩니다.



## 일반적인 오류

### 잘못된 토큰

이 문제는 환경 파일의 `private_key`이(가) 잘못되었거나 더 이상 유효하지 않을 때 발생합니다. 이 경우 줄 바꿈을 포함하여 전체 키를 복사했는지 확인합니다

예:

```none
-----BEGIN PRIVATE KEY----- 
some uber long varchar set is here
-----END PRIVATE KEY----- 
```

```none
400 invalid_token
```

>[!NOTE]
>
>JWT 기반 인증을 사용할 때만 적용 가능

### 잘못된 IMS\_ORG

이 오류는 드롭다운에서 postman 환경을 설정하는 것을 잊어버렸을 때 발생합니다

선택한 Postman 환경이 없을 때 ![활성 환경에서 IMS_ORG를 찾을 수 없음 오류](assets/access-token-forgot-to-select-postman-environment.png)

>[!NOTE]
>
>API 호출을 실행할 때 Postman 환경을 설정하는 것을 잊지 마십시오
>
>![Postman 환경 드롭다운에서 AEP Bootcamp 환경 선택](assets/access-token-set-postman-environment.png)
