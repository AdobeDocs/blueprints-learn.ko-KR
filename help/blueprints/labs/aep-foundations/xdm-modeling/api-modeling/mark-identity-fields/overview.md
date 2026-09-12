---
title: ID 필드 표시
description: ID 설명자가 XDM 스키마 레지스트리 API를 사용하여 스키마 필드를 기본 또는 비기본 ID로 표시하는 방법에 대해 알아봅니다.
doc-type: overview-page
solution: Experience Platform
exl-id: f6498584-0f4d-4baf-86b5-b00cc78e2ba7
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# ID 필드 표시

## ID 설명자

필드를 ID로 표시하려면 스키마 레지스트리에서 ID 설명자를 생성해야 합니다. 샘플 스키마 설명자 본문은 다음과 같습니다.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/devbc/schemas/8415ac18dd8943e35d12caf0c24b57b4a5a9ab7fd637245e",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/_devbc/customerID",
  "xdm:namespace": "customerID",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": true
}
```

- **@type** -> 항상 `xdm:descriptorIdentity`(으)로 설정됨
- 필드가 있는 스키마의 **xdm\:sourceSchema** -> `$id`
- **xdm\:sourceVersion** -> 항상 1
- 스키마 내 필드의 **xdm\:sourceProperty** -> 경로
- **xdm\:namespace** -> 필드를 저장해야 하는 ID 네임스페이스 코드
- **xdm\:property** -> 항상 `xdm:code`
- **xdm\:isPrimary** -> 기본 ID가 `true`인 경우, 그 외 `false`인 경우


## 귀하의 목표

고객 계정 스키마에 대한 기본 ID와 비기본 ID를 모두 만듭니다. 다음 섹션의 단계를 수행한 후 스키마는 다음과 같아야 합니다.

![기본 및 비기본 ID 설명자를 만든 후 고객 계정 스키마](assets/overview-schema-with-primary-and-non-primary-identities.png)
