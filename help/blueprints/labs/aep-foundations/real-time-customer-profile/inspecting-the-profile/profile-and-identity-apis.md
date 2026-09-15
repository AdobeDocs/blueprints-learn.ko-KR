---
title: 프로필 및 ID API
description: Postman의 Profile Entity API 및 Identity Service Cluster API를 사용하여 프로필 속성, 이벤트 및 연결된 ID를 조회합니다.
doc-type: article
solution: Experience Platform
exl-id: 1db55c5b-fdf8-4c63-b435-477626bb0450
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%
---

# 프로필 및 ID API

>[!IMPORTANT]
>
>프로필 및 ID API 연습을 시작하기 전에 [Postman 설정](../../setup.md)을 완료하십시오.

## 프로필 엔티티 API

프로필 API를 활용하는 방법을 파악하는 것은 실시간 고객 프로필 작업에 있어 매우 중요합니다. 또한 콜센터에서 키오스크에 이르기까지 가능한 다양한 시스템 통합에 노출되면서 빠른 분류 및 디버그 기능의 잠금을 해제합니다.

가장 중요한 API 중 하나는 프로필 엔티티 API입니다. 이 API를 사용하면 UI에서 확인한 것처럼 개별 프로필을 조회할 수 있습니다. 프로필은 매개 변수를 사용하여 프로필의 속성 또는 이벤트를 볼지 여부를 나타냅니다.

다음은 프로필 엔티티 API의 GET 메서드에 대한 전체 사양입니다


## API 개요

다음은 프로필 엔티티 API를 호출하는 데 필요한 최소 정보입니다.

`GET https://platform.adobe.io/data/core/ups/access/entities`

### 필수 쿼리 매개 변수

모든 요청과 함께 이 매개 변수를 보냅니다. 해당 값은 프로필의 속성을 조회하는지 아니면 이벤트를 조회하는지에 따라 다릅니다.

| 매개 변수 | 유형 | 설명 | 예 |
| ------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| `schema.name` | 문자열 | 조회 중인 엔티티의 XDM 스키마 클래스 이름입니다. | `_xdm.context.profile` |
| `schema.name` | 문자열 | 대신 이 값을 사용하여 프로필의 이벤트를 조회합니다. 이벤트를 프로필로 범위를 지정하려면 `relatedSchema.name=_xdm.context.profile`과(와) 연결합니다. | `_xdm.context.experienceevent` |

### 조회할 엔티티 식별

대부분의 요청은 `entityId` 및 `entityIdNS`을(를) 사용하여 이미 해당 XID를 알고 있어야 하는 것이 아니라 이메일 주소, CRM ID 또는 충성도 ID와 같은 알려진 ID 값으로 엔티티를 식별합니다. XID는 ID를 나타내기 위해 ID 서비스에서 내부적으로 생성하고 할당하는 base64 인코딩 식별자입니다. 네임스페이스와 ID 값을 하나의 압축 토큰으로 통합합니다(자세한 내용은 [기본 XID](https://experienceleague.adobe.com/docs/experience-platform/identity/api/list-native-id.html?lang=ko) 참조).

| 매개 변수 | 유형 | 설명 | 예 |
| ------------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `entityId` | 문자열 | 조회할 식별자 값입니다. 엔티티의 XID를 이미 알고 있는 경우 여기서 직접 사용하고 `entityIdNS`을(를) 생략합니다. | `depeche.mode@dep.com` |
| `entityIdNS` | 문자열 | `entityId`이(가) 속한 ID 네임스페이스 코드(예: `email`, `crmid`, `ECID`). `entityId`이(가) 아직 XID가 아닐 때 필요합니다. | `email` |

>[!NOTE]
>
>이 실습의 Postman 요청은 XID가 아닌 이메일 주소(`entityIdNS=email`, `entityId=depeche.mode@dep.com`)로 Depeche 모드 프로필을 조회합니다.

### 필수 헤더

모든 요청에는 다음 헤더도 필요합니다.

| 머리글 | 유형 | 설명 | 예 |
| ----------------- | ------ | ---------------------------------------------- | --------------------- |
| `x-gw-ims-org-id` | 문자열 | IMS 조직 ID. | `<your IMS org>` |
| `x-api-key` | 문자열 | 등록된 프로젝트/자격 증명의 API 키. | `<your API key>` |
| `Authorization` | 문자열 | 요청에 대한 전달자 토큰. | `Bearer <your token>` |

>[!NOTE]
>
>추가 ID 조회 옵션, 이벤트 필터링(`startTime`, `endTime`, `property`, `orderby`, `limit`), 필드 선택 및 병합 정책 재정의를 포함하여 쿼리 매개 변수의 전체 목록을 보려면 [프로필 엔터티 API 참조](https://developer.adobe.com/experience-platform-apis/references/profile#tag/Entities)를 참조하십시오.

>[!WARNING]
>
>모든 API 요청은 샌드박스별로 다르므로 API를 사용할 때는 호출된 각 요청의 헤더 매개 변수가 적절한 샌드박스로 올바르게 설정되었는지 확인하는 것이 중요합니다.`x-sandbox-name`
>
>이 실습의 경우 환경 파일에 이미 `x-sandbox-name`이(가) 설정되어 있습니다.

## 엔티티 조회(속성)

엔티티 조회 API에 대한 느낌을 얻으려면 이전 랩의 차원 모드 프로필을 사용합니다.

1. **Postman**&#x200B;을(를) 열고 **프로필 랩** 폴더로 이동
1. **엔터티 조회(특성)** 요청을 클릭하여 엽니다.
1. **보내기** 단추를 클릭하여 호출 실행

   ![보내기 전에 엔터티 조회(특성) 호출에 대한 Postman 요청 창](assets/profile-and-identity-apis-entity-lookup-attributes-request.png "프로필 엔터티 조회(특성) API")

   요청이 성공하면 `200 OK`(으)로 응답해야 하며 딥시트 모드 프로필에 대한 모든 특성이 포함된 결과가 표시됩니다.

   ![장치 모드 프로필에 대한 모든 특성을 포함하는 OK 응답](assets/profile-and-identity-apis-successful-attributes-api-response.png "성공한 프로필 엔터티(특성) API 응답")

   >[!NOTE]
   >
   >기본적으로 프로필 엔티티 요청에 병합 정책이 지정되지 않으면 샌드박스의 기본 병합 정책을 사용합니다

   Entity API를 사용하여 쿼리 매개 변수를 사용하여 응답에 반환되는 사항을 변경합니다.

1. 엔터티 조회(특성) 요청에서 요청에 대한 **매개 변수** 옵션을 클릭합니다
1. **필드**(이)라는 **키** 옆의 확인란을 선택하세요.
1. **보내기** 단추를 클릭하여 요청 실행

![응답을 필터링하기 위해 필드 매개 변수가 활성화된 엔터티 조회(특성) 요청](assets/profile-and-identity-apis-entity-lookup-attributes-with-filter-enabled.png)

>[!NOTE]
>
>`mergePolicyId`을(를) 지정하는 매개 변수도 있습니다. 이에 대한 값을 찾으려면 다른 API를 사용하거나 UI를 사용하여 ID를 조회합니다.

성공적인 요청은 `200 OK`(으)로 응답해야 하며 방금 활성화한 매개 변수 필터에 지정된 필드인 이름, 성 및 활성 제품 배열만 표시됩니다.

![이름, 성 및 활성 제품 필드만 표시하는 필터링된 200 OK 응답](assets/profile-and-identity-apis-successful-filtered-attributes-response.png "필터가 활성화된 성공적인 프로필 엔터티 조회(특성) API 응답")

>[!SUCCESS]
>
>축하합니다!  프로필 엔티티 API를 사용하여 프로필의 속성을 조회했습니다

## 엔티티 조회(이벤트)

프로필의 이벤트를 조회하려면 동일한 프로필 엔티티 API를 사용합니다.  유일한 차이점은 응답에 사용할 클래스 유형을 변경할 프로필 서비스에 알려 주어야 한다는 것입니다.

1. **엔터티 조회(이벤트)** 요청을 클릭하여 엽니다.
1. **보내기** 단추를 클릭하여 호출 실행

보내기 전에 엔터티 조회(이벤트) 호출에 대한 ![Postman 요청 창](assets/profile-and-identity-apis-entity-lookup-events-request.png)

성공적인 요청은 `200 OK`(으)로 응답해야 하며, 디바이스 모드 프로필에 대한 모든 이벤트가 포함된 결과가 표시됩니다.



![자격 증명 모드 프로필에 대한 모든 이벤트를 포함하는 OK 응답](assets/profile-and-identity-apis-successful-events-api-response.png "성공한 프로필 엔터티 조회(이벤트) API 응답")

프로필 속성을 조회할 때 엔티티 API에는 응답으로 반환되는 것을 변경하는 훨씬 더 많은 쿼리 매개 변수가 있습니다.

매개 변수 섹션에서 활성화하고 요청을 실행하여 몇 가지 매개 변수를 시도하십시오. 작동 방식을 확인하십시오.

![매개 변수 섹션에서 추가 쿼리 매개 변수가 활성화된 엔터티 조회(이벤트) 요청](assets/profile-and-identity-apis-entity-lookup-events-query-params.png "경험 이벤트에 대한 프로필 엔터티 조회")

**샘플 쿼리 매개 변수 정의**

| 키 | 값 | 설명 |
| ------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------- |
| mergePolicyId | \&lt;blank> | 조회에 사용되는 병합 정책을 전환합니다. 비워 두면 샌드박스의 기본 병합 정책을 사용합니다 |
| 필드 | eventType,timestamp,identityMap | 값이 있는지 여부에 관계없이 각 이벤트의 이러한 필드만 표시합니다. |
| 속성 | eventType=&quot;order.placed&quot; | 지정된 유형의 이벤트만 필터링합니다 |
| orderby | +타임스탬프 | 오름차순으로 이벤트 정렬 |
| 제한 | 5 | 응답에서 5개의 이벤트만 표시 |

>[!NOTE]
>
>모든 쿼리 매개 변수 옵션에 대해 자세히 알아보세요. -> [https://developer.adobe.com/experience-platform-apis/references/profile/#tag/Entities/operation/retrieveEntity](https://developer.adobe.com/experience-platform-apis/references/profile/#tag/Entities/operation/retrieveEntity)



## ID 서비스 클러스터 API

어떤 시점에서 ID 그래프 내의 특정 프로필의 ID 클러스터에 속하는 ID에 대한 질문이 있을 수 있습니다.  이 API를 사용하면 단일 ID 네임스페이스/값을 전달하고 해당 프로필에 대한 전체 ID 클러스터를 받을 수 있습니다.

직접 사용해 보십시오.

1. 열려면 **연결된 ID 목록** 요청을 클릭하십시오.
1. **보내기** 단추를 클릭하여 호출 실행

>[!NOTE]
>
>요청의 매개 변수는 ID 네임스페이스와 ID(즉, 값)입니다



![보내기 전에 연결된 ID 목록 호출에 대한 Postman 요청 창](assets/profile-and-identity-apis-list-linked-identities-request.png "연결된 ID 목록 API")

성공적인 응답은 아래 스크린샷과 같아야 합니다



![자격 증명 모드 프로필의 모든 ID를 표시하는 연결된 ID 응답 목록 만들기](assets/profile-and-identity-apis-successful-list-linked-identities-response.png)

>[!NOTE]
>
>응답에 프로필 디바이스 모드의 모든 ID가 포함되어 있음을 알 수 있습니다
