---
hold: true
title: 관계 정의
description: 관계 설명자가 API를 통해 고객 스키마를 XDM 스키마 레지스트리의 조회 스키마에 연결하는 방법을 알아봅니다.
doc-type: overview-page
solution: Experience Platform
exl-id: be672c84-09ac-4941-b40e-da7bd3fd6704
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 관계 정의

## 관계 설명자

한 스키마에서 다른 스키마로의 관계를 만들려면 스키마 레지스트리에서 관계 설명자를 만들어야 합니다. 샘플 스키마 설명자 본문은 다음과 같습니다.

일대일 설명자

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:destinationSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7",
  "xdm:destinationVersion": 1
}
```

참조 ID 설명자

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/6470f71181cf87aa39c2c2c43824eaa15f523652f7f88ff7",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/plan/planID",
  "xdm:identityNamespace": "planID"
}
```

## 귀하의 목표

고객 계정 스키마에 대한 관계 ID를 만듭니다. 다음 섹션의 단계를 수행한 후 스키마는 다음과 같아야 합니다.

![관계 및 참조 ID 설명자를 표시하는 고객 계정 스키마](assets/overview-schema-with-relationship-identities.png)
