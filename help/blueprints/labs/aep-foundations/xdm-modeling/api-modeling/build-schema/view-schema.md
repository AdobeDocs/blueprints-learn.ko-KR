---
title: 스키마 보기
description: Experience Platform UI와 스키마 API 가져오기 호출을 통해 새로 생성된 고객 스키마를 봅니다.
doc-type: article
solution: Experience Platform
exl-id: 29302546-46dc-4c97-8fd8-deab6977635c
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# 스키마 보기

## UI를 통해 보기

1. 브라우저를 열고 `Schema -> Browse` 섹션으로 다시 이동합니다.

   >[!NOTE]
   >
   >방금 UI를 만들었으며 스키마 레지스트리를 다시 쿼리해야 하므로 UI를 새로 고쳐 표시합니다

2. 스키마 `Sample Customer Schema - <your sandbox number>` 검색

3. 필수 클래스와 관련 필드 그룹이 스키마에 추가됩니다

![클래스 및 필드 그룹과 함께 Experience Platform UI에 표시되는 샘플 고객 스키마](assets/view-schema-ui-view-of-sample-customer-schema.png "샘플 고객 스키마의 UI 보기")


## API를 통해 보기

1. `Step 5 - Get Customer Account Schema` API를 클릭하여 선택합니다.
1. 요청의 URL에서 `<replace me>`을(를) 아래와 같이 이전 섹션(스키마 만들기)에서 호출 끝까지 저장한 `$meta:altId`(으)로 바꿉니다
1. 요청에 대한 편집 내용을 저장합니다.
1. `Send` 단추를 클릭하여 요청을 실행합니다.

![5단계 - 고객 계정 스키마 API 호출 가져오기](assets/view-schema-step-5-get-customer-account-schema.jpeg "5단계 - 고객 계정 스키마 가져오기")



`$meta:altId`을(를) 추가한 후의 최종 요청 예

![메타가 추가된 5단계 요청:altId이 URL에 추가됨](assets/view-schema-final-step-5-request.png "마지막 5단계 요청")



`200 OK` 응답을 받은 경우 XDM JSON 구조의 렌즈를 통해 만든 스키마를 검색할 수 있어야 합니다

전체 샘플 고객 계정 스키마 JSON을 보여 주는 ![200 OK 응답](assets/view-schema-sample-customer-account-schema.png "샘플 고객 계정 스키마")
