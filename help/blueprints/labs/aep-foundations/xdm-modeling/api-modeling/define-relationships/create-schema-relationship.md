---
hold: true
title: 스키마 관계 만들기
description: 스키마 레지스트리 API를 사용하여 고객 계정 스키마를 조회 계획 스키마에 연결하는 일대일 관계 설명자를 만듭니다.
doc-type: article
solution: Experience Platform
exl-id: c9079585-fff1-4ee1-8992-93825fcde759
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# 스키마 관계 만들기

1. `XDM Schema Lab -> Create Relationship Descriptors` 폴더에서 `Step 2 - Relationship Descriptor Customer Account To Plan` API 요청 클릭

>[!CAUTION]
>
>아직 요청을 실행하지 마십시오.

![2단계 - 계획 API 요청에 대한 관계 설명자 고객 계정](assets/create-schema-relationship-step-2-descriptor-request.png "2단계 - 계획에 대한 관계 설명자 고객 계정")



&#x200B;2. API 호출 본문에서 다음 속성을 업데이트합니다.

- `xdm:sourceSchema` 속성의 값을 [스키마 만들기](../build-schema/create-schema.md) 랩 단계에서 저장한 고객 계정 스키마의 `$id`(으)로 설정합니다.
- `xdm:sourceProperty`의 값을 고객 계정 스키마에서 `planID` 필드의 경로로 설정합니다.
- `xdm:destinationSchema` 속성의 값을 첫 번째 단계에서 저장한 `dep: Lookup Plan` 스키마의 `$id`(으)로 설정합니다.

>[!NOTE]
>
>고객 계정 스키마에서 planId 필드의 점 표기법 값을 사용하고 `.`을(를) `/`(으)로 바꿉니다.
>
>
>선행 `/` 또는 😄을(를) 잊지 마십시오.

예만

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:destinationSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7"
,
  "xdm:destinationVersion": 1
}
```

>[!NOTE]
>
>위의 테넌트 이름(\_devbc)을 고유한 이름으로 업데이트해야 합니다



&#x200B;3. `Save` 단추를 계속 사용하기 전에 요청을 저장하십시오.

&#x200B;4. `Send` 단추를 클릭하여 API를 실행하십시오.

이제 아래와 같은 `201 Created` 응답이 표시됩니다.

![계획 관계 설명자에 대한 고객 계정을 만든 후 응답을 만들었습니다](assets/create-schema-relationship-customer-account-plan-descriptor.png "고객 계정 - 계획 관계 설명자")

>[!NOTE]
>
>실시간 고객 프로필(및 모든 Experience Platform)은 XDM 개별 프로필 또는 XDM 경험 이벤트 스키마(즉, 하나의 (1) 수준 조회 관계만 만들 수 있음)에서 **one (1) 홉 조인**&#x200B;이라고 하는 기능만 지원합니다.

>[!NOTE]
>
>관계 설명자 `@type`이(가) `OneToOne` 값으로 설정되어 있습니다. XDM ERD on Paper의 고객 계정과 플랜 테이블 간의 관계는 1\:N이 아닙니까?  무슨 일입니까?
>
>
>실시간 고객 프로필은 개인의 트레이트 및 행동을 설명하기 위해 작성됩니다.  따라서 개별 사용자 렌즈에서 조회 테이블은 세분화 동안 1:1 관계로 정의된 **only** **ever**&#x200B;입니다.
>
>뇌가 아프면...
