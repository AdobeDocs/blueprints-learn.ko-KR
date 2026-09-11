---
hold: true
title: 최종 매핑 세트 확인
description: 고객 계정 스키마에 대한 단순 및 계산된 필드 매핑을 예상 최종 매핑 세트와 비교합니다.
doc-type: article
solution: Experience Platform
exl-id: d1521d08-1ccb-405f-b728-a2777598cb9f
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# 최종 매핑 세트 확인

> [!NOTE]
>
>스트리밍 수집 랩에서 이동하는 경우 아래 링크를 클릭하여 해당 랩의 다음 단계로 진행하십시오.
>
>[스트리밍 수집 랩 - 최종 매핑 집합 확인](../../stream-ingestion/check-final-mapping-set.md)



## 단순 매핑

>[!NOTE]
>
>\&lt;tenant-name> 을 샌드박스의 값으로 바꿉니다.

| Source 필드 | 대상 필드 |
| ------------------------- | --------------------------------- |
| account\_create\_date | \&lt;tenant-name>.account.createDate |
| account\_end\_date | \&lt;tenant-name>.account.endDate |
| customer\_id | \&lt;tenant-name>.customerID |
| plan\_name | \&lt;tenant-name>.plan.name |
| plan\_id | \&lt;tenant-name>.plan.planID |
| billing\_city | billingAddress.city |
| billing\_zip\_code | billingAddress.postalCode |
| billing\_state | billingAddress.state |
| billing\_street\_address | billingAddress.street1 |
| email\_optIn | consents.marketing.email.val |
| mobile\_phone | mobilePhone.number |
| 이름 | person.name.firstName |
| 성 | person.name.lastName |
| 이메일 | personalEmail.address |
| createDate | repo.createDate |
| modifydate | repo.modifyDate |
| shipping\_city | shippingAddress.city |
| shipping\_zip\_code | shippingAddress.postalCode |
| shipping\_state | shippingAddress.state |
| shipping\_street\_address | shippingAddress.street1 |

> [!NOTE]
>
>계속하기 전에 최종 매핑이 아래에 표시된 것과 일치하는지 확인하십시오.



## 계산된 매핑

| 계산된 필드 | XDM 필드 |
| ------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| iif(sms\_optIn == null 또는 sms\_optIn == &quot;&quot;, &#39;n&#39;, sms\_optIn) | consents.marketing.sms.val |
| concat(date\_part(&quot;month&quot;, date(birth\_Date,&quot;M/d/yyyy&quot;)).toString(), &quot;-&quot;, date\_part(&quot;day&quot;, date(birth\_Date,&quot;M/d/yyyy&quot;)).toString() | person.birthdayAndMonth |
| date\_part(&quot;yyyy&quot;,date(birth\_Date,&quot;M/d/yyyy&quot;)) | person.birthYear |

> [!NOTE]
>
>계속하기 전에 최종 매핑이 아래에 표시된 것과 일치하는지 확인하십시오
