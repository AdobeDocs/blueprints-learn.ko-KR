---
hold: true
title: 계획 스키마 ID 가져오기
description: 테넌트 스키마 레지스트리 API를 쿼리하여 관계 설명자에 사용할 계획 조회 스키마의 $id를 찾아 저장합니다.
doc-type: article
solution: Experience Platform
exl-id: f66e0483-b5b3-4493-b752-c4e00211a8bd
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# 계획 스키마 ID 가져오기

## 모든 테넌트 스키마 나열

1. `XDM Schema Lab -> Create Relationship Descriptors` 폴더에서 `Step 1 - Get Lookup Schemas` API 요청 클릭
1. `Send` 단추를 클릭하여 API를 실행하십시오.

![1단계 - 조회 스키마 API 요청 가져오기](assets/get-plan-schema-id-step-1-get-lookup-schemas.jpeg "1단계 - 조회 스키마 가져오기")

>[!NOTE]
>
>이 GET 호출은 스키마 레지스트리의 &quot;테넌트&quot; 부분 내에 있는 모든 스키마(즉, 사용자 지정 생성 스키마)를 가져옵니다. **계획** 스키마만 검색하면 고객 계정 스키마와 연결할 수 있습니다.



## 계획 스키마 식별

1. 호출 응답에서 `dep: Plan [Lookup] ` 스키마 검색
1. 나중에 참조할 수 있도록 스키마의 `$id`을(를) 복사하고 어딘가에 저장하십시오.

![dep: API 응답에 있는 플랜 조회 스키마 $id](assets/get-plan-schema-id-dep-lookup-plan-schema-sid.png "dep: 조회 계획 스키마 $id")

>[!NOTE]
>
>이 스키마는 이미 샌드박스에 미리 배포되어 있어야 합니다.

>[!WARNING]
>
>스키마 `$id`을(를) 어딘가에 저장할 때까지 계속하지 마십시오.  관계 설명자를 만들려면 나중에 필요합니다.
