---
hold: true
title: 스키마 보기
description: 스키마 UI 및 스키마 가져오기 API를 모두 통해 계획 스키마에 대한 고객 계정 스키마의 조회 관계를 확인합니다.
doc-type: article
solution: Experience Platform
exl-id: dae48ef4-f762-4173-8564-c1ad40c0109b
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 스키마 보기

## UI를 통해 보기

1. 브라우저를 열고 `Schema -> Browse` 섹션으로 다시 이동합니다.
1. 스키마 `Sample Customer Schema - <your sandbox number>` 검색
1. `dep: Plan [Lookup]`에 대한 관계가 정의되어 있습니다.

![dep: 계획 조회 관계를 표시하는 Experience Platform UI의 샘플 고객 스키마](assets/view-schema-relationship-to-plan-lookup-schema.png)


## API를 통해 보기

1. `Step 4 - Get Customer Account Schema and its descriptors` API를 클릭하여 선택합니다.

![4단계 - 고객 계정 스키마 및 해당 설명자 API 호출 가져오기](assets/view-schema-step-4-get-schema-and-descriptors.png "4단계 - 고객 계정 스키마 및 해당 설명자 가져오기")



&#x200B;2. 요청의 URL에서 `<replace me>`을(를) 아래와 같이 이전 섹션 [스키마 만들기](../build-schema/create-schema.md)에서 저장한 `$meta:altId`(으)로 바꿉니다

URL에 meta:altId이 추가된 ![4단계 요청](assets/view-schema-final-step-4-request.png "마지막 4단계 요청")



&#x200B;3. `Save` 단추를 사용하여 요청 저장

&#x200B;4. `Send` 단추를 클릭하여 요청을 실행합니다.

이제 `200 OK` 응답이 표시되고 XDM JSON 구조의 렌즈를 통해 ID를 보기 위해 만든 스키마 끝으로 이동할 수 있습니다.



![고객 계정 스키마 JSON에 표시되는 관계 설명자](assets/view-schema-relationship-descriptor.png "관계 설명자")



![고객 계정 스키마 JSON에 표시되는 참조 ID 설명자](assets/view-schema-reference-identity-descriptor.png "참조 ID 설명자")
