---
title: 스키마 보기
description: UI 및 API를 통해 스키마의 ID 설명자를 보고, 해결된 스키마 응답과 해결되지 않은 스키마 응답에 대해 Accept 헤더 옵션을 비교합니다.
doc-type: article
solution: Experience Platform
exl-id: 44eedb82-259f-4f7f-84fe-acc2b42376eb
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# 스키마 보기

## UI를 통해 보기

1. 브라우저를 열고 `Schema -> Browse` 섹션으로 다시 이동합니다.
1. **고객 계정** 스키마 검색
1. ID가 스키마에 추가됩니다

![스키마에 추가된 ID를 표시하는 스키마 찾아보기 보기](assets/view-schema-schema-ui-with-identities.png "ID가 있는 스키마 UI 보기")


## API를 통해 보기

1. `Step 3 - Get Customer Account Schema and its descriptors` API를 클릭하여 선택합니다.

   ![3단계 - 설명자가 있는 고객 계정 스키마 가져오기 API 요청](assets/view-schema-step-3-get-customer-account-schema-w-descriptors.png "3단계 - 설명자가 있는 고객 계정 스키마 가져오기")



1. 요청의 URL에서 `<replace me>`을(를) 아래와 같이 이전 섹션(스키마 만들기)에서 호출 끝까지 저장한 `$meta:altId`(으)로 바꿉니다

   ![altId가 URL에 추가된 최종 5단계 요청](assets/view-schema-final-step-5-request.png "최종 5단계 요청")



1. 요청한 편집 내용을 저장합니다.

1. `Send` 단추를 클릭하여 요청을 실행합니다.

이제 `200 OK` 응답이 표시되고 XDM JSON 구조의 렌즈를 통해 만든 스키마를 찾아볼 수 있습니다

![스키마의 XDM JSON 구조를 보여 주는 API 응답의 본문](assets/view-schema-body-of-the-api-response.png "API 응답의 본문")



만든 ID 설명자를 보려면 API 응답에서 아래쪽으로 이동합니다

![API 응답에 표시된 ID 설명자](assets/view-schema-descriptors-displayed-in-api-response.png "API 응답에 표시된 설명자")


## Accept 헤더

요청에 사용된 **Accept** 헤더를 참고하십시오. 이 헤더는 API 응답의 관련 설명자와 함께 확인되지 않은 스키마 `$refs`을(를) 반환하도록 XDM 스키마 레지스트리에 지시합니다(즉, 최소한의 정보 표시).  Adobe은 스키마에 대한 다양한 세부 정보를 얻는 데 사용할 수 있는 다른 **Accept** 헤더를 제공합니다.

![3단계 고객 계정 스키마 가져오기 요청의 Accept 헤더 필드](assets/view-schema-accept-header.png "3단계 - 고객 계정 스키마 가져오기 Accept 헤더")

>[!NOTE]
>
>여기에서 다양한 Accept 헤더에 대해 자세히 읽어볼 수 있습니다. -> [Experience League 스키마 API 끝점](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=ko#lookup)



이 작업을 보려면 **Accept** 헤더를 변경하여 모든 `$ref` 및 `allOf`이(가) 완전히 해결됨(즉, 분해됨) 및 연결된 설명자에 응답하도록 스키마 레지스트리를 지정하십시오

1. `Accept` 헤더 값을 다음과 같이 업데이트하십시오.
   `application/vnd.adobe.xed-full-desc+json; version=1`
1. `Save` 단추를 사용하여 요청을 저장합니다.
1. `Send` 단추를 사용하여 요청 실행

다음과 같은 응답이 표시됩니다.

![모든 해결된 속성을 표시하는 전체 분해 스키마 응답](assets/view-schema-fully-exploded-schema-showing-all-properties.png "모든 속성을 표시하는 전체 분해 스키마")

>[!NOTE]
>
>스키마의 모든 속성이 이제 응답에 완전히 표시되는 방식을 확인합니다. 반면 이전 호출에서는 스키마의 `$ref` 값(즉, 참조 중인 필드 그룹)만 표시되고 각 개별 필드/속성으로 완전히 해결된 것은 없습니다.

>[!NOTE]
>
>API로 작업할 때 스키마의 `$id`을(를) 가져오거나 스키마 구성을 확인하는 경우 완전히 해결된 응답이 항상 필요한 것은 아니므로 이 점을 이해하는 것이 중요합니다
