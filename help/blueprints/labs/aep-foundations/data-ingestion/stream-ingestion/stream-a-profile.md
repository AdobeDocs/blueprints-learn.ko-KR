---
title: 프로필 스트리밍
description: Postman, 스트리밍 끝점 및 데이터 흐름 ID를 사용하여 고객 프로필 레코드를 HTTP API를 통해 Adobe Experience Platform으로 보냅니다.
doc-type: article
solution: Experience Platform
exl-id: 937d153c-9230-4f5a-a397-6c177a3ea890
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%
---

# 프로필 스트리밍

## API 개요

원시 양식으로 Adobe Experience Platform에 데이터를 스트리밍할 때 API의 구조를 이해하는 것이 중요하므로 생성하는 데이터 흐름에 관계없이 쉽게 다시 만들 수 있습니다.  다음은 cURL을 사용하는 호출의 기본 구조에 대한 예입니다

**샘플 요청(원시 데이터)**

```curl
curl --location '' \
--header 'Content-Type: application/json' \
--header 'x-adobe-flow-id:  <dataflow-id>;' \
--header 'Authorization: Bearer XXX;' \
--data '{
    "customer_id": "202208240125",
    "firstName": "",
    "lastName": "",
    "email": "",
    "createDate": "1660096899",
    "modifyDate": "2022-08-09T22:01:40Z",
    "birth_Date": "1991-06-12",
    "mobile_phone": "888-888-8888",
    "email_optIn": "y",
    "sms_optIn": "n",
    "shipping_street_address": "1901 W Madison St",
    "shipping_city": "Chicago",
    "shipping_state": "IL",
    "shipping_zip_code": "60612",
    "billing_street_address": "1901 W Madison St",
    "billing_city": "Chicago",
    "billing_state": "IL",
    "billing_zip_code": "60612",
    "plan_id": "m1",
    "plan_name": "basic",
    "account_create_date": "Created on 2022-04-20T22:19:03Z",
    "account_end_date": "2022-01-20T13:15:32Z",
    "source": "inStore"
}'
```



위의 요청에서 알아 두어야 할 몇 가지 중요한 요소입니다.

| 주요 요소 | 필수 | 설명 |
| --------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 요청 URL(즉, 위치) | - | 스트리밍 데이터가 가리킬 HTTP API 소스 계정의 URL입니다. **항상 POST 형식입니다** |
| 헤더 &quot;Content-Type&quot; | * | 보내는 데이터가 JSON 형식이므로 항상 `application/json`(으)로 설정하십시오. |
| 헤더 &quot;x-adobe-flow-id&quot; | - | 소스 커넥터에서 만든 데이터 흐름 ID로 설정합니다. |
| 헤더 &quot;인증&quot; | * | 선택적 값이지만 보안상의 이유로 적극 권장됩니다. 이는 [Postman 설치](../../postman-setup/environment-file.md) 랩 동안 생성한 `access_token`과(와) 동일합니다 |
| 본문 내용 | - | Adobe Experience Platform으로 전송할 실제 데이터를 포함합니다 |

>[!NOTE]
>
>본문 콘텐츠는 항상 JSON 형식이어야 하며 데이터 흐름 디자인 중에 제공된 샘플 페이로드와 일치해야 합니다



## 필수 값 수집

데이터를 스트리밍하기 전에 위에 나열된 필수 값(특히, 스트리밍 끝점 URL 및 본문 콘텐츠 &#39;헤더&#39; 값)을 수집합니다.

다음 단계를 수행하십시오.

1. **스트리밍 끝점** 값을 복사하여 로컬 컴퓨터에 저장합니다(이전 섹션의 단계에서 탐색하지 않았다고 가정). 다른 곳으로 이동한 경우 소스->계정에서 찾을 수 있습니다.

   >[!NOTE]
   >
   >다른 곳으로 이동한 경우 다음을 수행하여 이 페이지에 액세스할 수 있습니다.
   >
   >- 왼쪽 레일에서 **소스** 클릭
   >- **계정** 탭에 있는지 확인하고 **스트리밍 수집 - \&lt;이니셜>**&#x200B;이라는 제목으로 만든 계정을 클릭하십시오.

   >[!NOTE]
   >
   >이 값이 표시되지 않으면 해당 행을 클릭하여 선택한 데이터 흐름 행이 없는지 확인합니다.  파란색 링크를 클릭하지 마십시오

   ![계정 세부 정보의 오른쪽에 표시되는 스트리밍 끝점 URL](assets/stream-a-profile-streaming-endpoint-url-on-the-right.png)



1. 파란색 링크를 피하여 데이터 흐름 행을 클릭하여 선택합니다. **데이터 흐름 ID**&#x200B;을(를) 복사하여 안전한 곳에 저장하십시오.

![API 사용 세부 정보 및 데이터 흐름 ID를 보여주는 데이터 흐름 세부 정보 오른쪽 레일](assets/stream-a-profile-dataflow-details-right-rail-api-usage.png)



## API 요청 업데이트

Postman 애플리케이션으로 전환하고 수집한 정보로 고객 계정 만들기 요청을 업데이트합니다.

1. Postman을 열고 **데이터 수집 랩 -> 고객 계정 만들기** API 요청으로 이동한 다음 엽니다

   ![Postman에서 열린 고객 계정 API 요청 만들기](assets/stream-a-profile-create-customer-account-api-request.png)



1. 이전에 저장한 **스트리밍 끝점** 값을 복사하여 요청의 URL에 붙여넣습니다.

   ![고객 계정 만들기 요청 URL에 붙여넣은 스트리밍 끝점 값](assets/stream-a-profile-create-customer-account-streaming-endpoint-url.png)



1. 이전에 저장한 데이터 흐름 ID 값을 **x-adobe-flow-id** 헤더 값에 복사하여 붙여 넣으십시오

   ![x-adobe-flow-id 헤더 값에 붙여넣은 데이터 흐름 ID](assets/stream-a-profile-copy-paste-x-adobe-flow-id.png)



1. 요청 본문에서 다음과 같은 속성을 업데이트합니다.

   - **이름** -> 내 이름
   - **성** -> 성
   - **전자 메일** -> 전자 메일 주소
   - **birth_Date** -> YYYY-MM-DD

   **5. 요청**&#x200B;개 저장

1. **보내기** 단추를 클릭하여 고객 계정 프로필에서 스트리밍할 요청을 실행합니다.

   ![Postman에서 보낼 준비가 된 최종 고객 계정 만들기 요청](assets/stream-a-profile-final-create-customer-account-request.png)



1. Adobe Experience Platform에서 성공적으로 수신했음을 나타내는 `200 OK` 응답을 받습니다

샘플 200 OK 응답

```none
{
    "inletId": "57e8b639020de08147888c2ce2046f2f4d36f622ee22b7313a565ab3a4ecee54",
    "xactionId": "1688068236344:7186:152",
    "flowId": "7d1d1a20-3df2-43fb-8bd8-2856bb3ea6a4",
    "receivedTimeMs": 1688068236344
}
```

>[!NOTE]
>
>응답에서 **xactionId**&#x200B;을(를) 확인합니다.  수집된 레코드가 표시되지 않는 오류가 발생하는 경우 지원 팀이 환경 문제를 디버깅하는 데 사용하는 주요 참조이므로 항상 고객 지원 티켓의 일부로 제공해야 합니다

>[!SUCCESS]
>
>축하합니다!  프로필 레코드에서 Adobe Experience Platform으로 스트리밍했습니다.
