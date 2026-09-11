---
hold: true
title: 데이터 흐름 확인 및 예약
description: 전체 주문 매핑 세트를 확인하고 출력을 미리 본 다음 데이터 흐름이 15분마다 실행되도록 예약합니다.
doc-type: article
solution: Experience Platform
exl-id: b7f0c43b-092c-45ba-b95b-27cb4a49d110
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 7%

---


# 데이터 흐름 확인 및 예약

## 매핑 세트 다시 확인

| # | Source 열 | XDM 열 |
| -- | ------------------------------------------- | -------------------------------------------------------- |
| 1 | orderStatus | eventType |
| 2 | lastOrderStatusUpdate | timestamp |
| 3 | orderID | order.orderId |
| 4 | orderDate | order.orderDate |
| 5 | orderTotal | order.priceTotal |
| 6 | paymentType | order.payment.paymentType |
| 7 | 결제 금액 | order.payment.paymentAmount |
| 8 | paymentCurrencyCode | order.payment.currencyCode |
| 9 | paymentTransactionId | order.payment.transactionID |
| 10 | plan.ID | order.\_devbc.plan.planID |
| 11 | customerID | \_devbc.customerID |
| 12 | personalEmail | \_devbc.personalEmail |
| 13 | storeID | store.storeID |
| 14 | shippingStreetAddress | shipping.address.street1 |
| 15 | shippingCity | shipping.address.city |
| 16 | shippingState | shipping.address.state |
| 17 | shippingZip | shipping.address.postalCode |
| 18 | shippingMethod | shipping.shippingMethod |
| 19 | shippingMount | shipping.shippingAmount |
| 20 | shippingDestination | shipping.shippingDestination |
| 21 | billingStreetAddress | billing.address.street1 |
| 22 | billingCity | billing.address.city |
| 23 | billingState | billing.address.state |
| 24 | billingZip | billing.address.postalCode |
| 25 | products\[\*] | productListItems\\*] |
| 26 | products\[\*].productID | - productListItems\[\*].\_id - productListItems\[\*].SKU |
| 27 | products\[\*].make | productListItems\[\*].\_devbc.make |
| 28 | products\[\*].model | productListItems\[\*].\_devbc.model |
| 29 | products\[\*].price | productListItems\[\*].priceTotal |
| 30 | concat(orderID, &quot;-&quot;, lastOrderStatusUpdate) | \_id |
| 31 | &quot;inStore&quot; | order.\_devbc.acqSource |



## 매핑 출력 미리 보기

1. 매핑 출력을 미리 봅니다. 모든 속성을 스크롤하여 오른쪽의 속성 옆에 빨간색 느낌표가 없도록 합니다.

![매핑된 특성에 오류가 없는 매핑 화면 미리 보기](assets/verify-and-schedule-dataflow-preview-mapping-screen.png "매핑 화면 미리 보기는 다음과 같습니다.")

1. 미리 보기의 왼쪽 탐색에서 **productListItems** 개체 배열을 선택합니다. 오른쪽은 해당 오브젝트 배열의 속성만 표시하도록 업데이트됩니다.

>[!NOTE]
>
>**productListItems.currencyCode** 및 **productListItems.quantity**&#x200B;은(는) 매핑을 제거한 후에도 자동으로 채워집니다. 이 문제는 상위 개체로 **productListItems**&#x200B;이(가) 매핑되었기 때문에 발생합니다.

![중복 재정의를 제거한 후 productListItems에 대한 매핑 화면을 완료했습니다](assets/verify-and-schedule-dataflow-completed-mapping-screenshot.png "완료된 매핑은 다음 스크린샷과 유사합니다")

## 실행 예약

1. 빈도를 분으로 설정하고 간격을 15로 설정하여 **15분마다**&#x200B;을(를) 실행하도록 일정을 설정합니다. 플로우를 검토하고 마침을 클릭합니다.

>[!CAUTION]
>
>일정이 15분으로 설정되어 있는지 확인합니다. **한 번 실행**(으)로 실행을 예약하면 나중에 매핑을 변경하더라도 다시 실행할 수 없습니다.

1. 데이터 흐름 실행은 즉시 시작되지 않으며 몇 분 정도 소요됩니다. 따라서 마지막 데이터 흐름 실행 상태가 &quot;*실행 없음*&quot;으로 설정됩니다.

1. 몇 분 후에 데이터 흐름이 성공합니다. **마지막 데이터 흐름 실행 상태** 및 **마지막 데이터 흐름 실행 날짜**&#x200B;를 확인합니다.

1. 데이터 흐름 이름을 클릭하여 데이터 흐름 실행 목록을 가져옵니다. 10개의 레코드를 수집해야 합니다.

1. 오류 진단 세부 정보를 보려면 데이터 흐름 실행 시작 시간을 클릭하십시오.

1. 왼쪽 탐색 막대에서 플랫폼의 데이터 세트로 이동하여 **주문 - YourNameHere**&#x200B;을 클릭합니다.

1. **데이터 집합 미리 보기를 클릭합니다.**
