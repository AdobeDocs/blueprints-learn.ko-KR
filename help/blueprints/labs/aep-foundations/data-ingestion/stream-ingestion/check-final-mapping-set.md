---
title: 최종 매핑 세트 확인
description: 스트리밍 수집 매핑을 예상 최종 통과 및 계산된 필드 매핑 세트와 비교합니다.
doc-type: article
solution: Experience Platform
exl-id: 8802aaca-f566-4972-8bd6-41aca9fae9bf
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# 최종 매핑 세트 확인

## 통과 매핑

>[!NOTE]
>
>계속하기 전에 최종 매핑이 아래에 표시된 것과 일치하는지 확인하십시오.

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



## 계산된 매핑

>[!NOTE]
>
>날짜 형식이 지정되었기 때문에 `birth_Date`에 대한 매핑이 일괄 처리 수집 랩 매핑과 다릅니다.  일괄 처리에서 슬래시 `/`을(를) 사용하는 반면 스트리밍에서는 대시 `-`을(를) 사용합니다.

| 계산된 필드 | XDM 필드 |
| ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| iif(sms\_optIn == null 또는 sms\_optIn == &quot;&quot;, &#39;n&#39;, sms\_optIn) | consents.marketing.sms.val |
| concat(date\_part(&quot;mm&quot;, date(birth\_Date, &quot;yyyy-M-d&quot;)).toString(), &quot;-&quot;, date\_part(&quot;dd&quot;, date(birth\_Date, &quot;yyyy-M-d&quot;)).toString() | person.birthdayAndMonth |
| date\_part(&quot;yyyy&quot;,date(birth\_Date,&quot;yyyy-M-d&quot;)) | person.birthYear |

>[!NOTE]
>
>계속하기 전에 최종 매핑이 아래에 표시된 것과 일치하는지 확인하십시오



## 데이터 흐름 완료

완료되면 **다음** 단추를 클릭한 다음 완료 단추를 클릭하여 데이터 흐름을 새 매핑 논리로 업데이트합니다.

![완료를 클릭하여 저장하기 전에 데이터 흐름 세부 정보 검토](assets/check-final-mapping-set-review-and-finish-dataflow.png)



이제 해당 계정을 사용하여 연결된 모든 데이터 흐름과 함께 만든 HTTP API 계정을 표시하는 화면이 표시됩니다. 만든 데이터 흐름도 표시되어야 합니다.
