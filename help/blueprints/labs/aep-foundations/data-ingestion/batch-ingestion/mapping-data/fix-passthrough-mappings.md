---
title: 통과 매핑 수정
description: 유효성 검사 전에 중복 또는 일치하지 않는 대상 필드 할당과 같은 잘못된 AI/ML 통과 매핑을 식별하고 수정합니다.
doc-type: article
solution: Experience Platform
exl-id: b06cc091-661e-4ff4-b6e5-f16bc5128b6b
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# 통과 매핑 수정

## 특정 매핑 삭제

소스 데이터 중 일부는 계산된 필드를 사용하여 처리해야 합니다.  이러한 문제를 해결하려면 매핑에서 삭제한 다음 매핑의 유효성을 다시 검사하십시오.

1. 매핑에서 다음 소스 데이터를 삭제합니다.
   - birth\_date
   - 소스
   - sms\_optIn
1. 유효성 검사 버튼을 클릭하여 매핑 유효성 재검사

![필드를 삭제한 후 매핑을 다시 확인하는 데 사용되는 유효성 검사 단추](assets/fix-passthrough-mappings-re-validate-mappings-using-validate-button.png "유효성 검사 단추를 사용하여 매핑을 다시 확인")

>[!NOTE]
>
>유효성 검사를 클릭한 후에도 오류가 있을 수 있습니다



## 잘못된 매핑 예

AI/ML 권장 사항은 도움이 되지만 때로는 틀립니다.  권장 사항을 검사하면 수정해야 하는 이러한 유형의 오류를 발견할 수 있습니다

>[!NOTE]
>
>다음은 자체 샌드박스에서 볼 수 있는 잘못된 매핑의 몇 가지 예입니다. 다른 오류도 표시될 수 있습니다.

## 중복 매핑

이 시나리오에서는 AI/ML 추천자가 두 개의 다른 소스 필드를 동일한 대상 필드 **person.name.lastName**&#x200B;에 매핑했음을 알 수 있습니다.



![같은 대상 필드 person.name.lastName에 매핑된 두 개의 다른 원본 필드](assets/fix-passthrough-mappings-person-lastname-mapped-twice.png "person.name.lastName이 이 매핑에서 두 번 매핑됩니다")

![plan_name 필드와 관련된 통과 매핑 예제를 복제합니다](assets/fix-passthrough-mappings-plan-name-duplicate-mapping.png)



## 잘못된 매핑

이 매핑은 올바르게 보이지만 더 자세히 검사하면 **email**&#x200B;이(가) **emailFormat**&#x200B;과(와) 다릅니다.

![emailFormat 대신 전자 메일이 잘못 매핑된 매핑](assets/fix-passthrough-mappings-email-mapped-incorrectly.png "전자 메일이 올바르게 매핑된 것처럼 보이지만 요구 사항에 따라 올바르지 않습니다.")

**email\_optIn**&#x200B;이(가) 잘못된 동의 개체에 잘못 매핑되는 경우입니다.

![잘못된 동의 개체에 잘못 매핑된 email_optIn](assets/fix-passthrough-mappings-email-optin-wrong-consent-object.png "email_optIn이 올바르게 매핑된 것 같지만 요구 사항에 따라 올바르지 않습니다.")



## 통과 매핑 고정

잘못된 대상 필드를 잘못 가리키는 통과 매핑을 수정하려면 다음 단계를 수행하십시오.

### 예

1. 잘못된 매핑으로 시작하고 대상 필드 상자를 클릭합니다. 예를 들어 아래 매핑에서 **person.name.lastName** 필드가 올바르게 매핑되지 않고 **planName**&#x200B;에 매핑됩니다.
1. 오른쪽에 열리는 대상 스키마 패널에서 적절한 대상 필드를 선택하고 **\_devbc.plan.name**&#x200B;을(를) 선택합니다
1. 이제 대상 필드 상자에서 대상 필드를 업데이트해야 합니다.
1. 이러한 오류를 수정한 후에는 **유효성 검사** 단추를 눌러 이러한 오류를 줄이고 새 오류를 도입하지 않도록 해야 합니다.



![각 매핑 오류를 해결하기 위해 매핑 목록을 통해 작업](assets/fix-passthrough-mappings-work-through-mapping-errors.png "매핑을 통해 작업하고 매핑 오류를 수정")



![통과 매핑을 수정할 올바른 필드를 선택하기 위한 대상 스키마 패널](assets/fix-passthrough-mappings-choose-correct-target-field.png "올바른 대상 필드를 선택하고 통과 요구 사항과 일치하는지 확인")

>[!WARNING]
>
>매핑 오류를 모두 해결할 때까지 다음 단계를 계속 진행하지 마십시오
