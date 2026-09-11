---
hold: true
title: 오브젝트 복사 매핑
description: 제품 배열에 대한 개체 복사 매핑을 구성한 다음 기본 사본 위에 필드 수준 재정의를 추가 및 제거합니다.
doc-type: article
solution: Experience Platform
exl-id: 762d0e19-ed1c-4f4d-91ec-a962bd6277a7
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# 오브젝트 복사 매핑

이 섹션에서는 객체 복사 매핑을 추가하고 일부 재정의를 생성합니다.

## 통과 매핑

새 필드 유형을 클릭하여 **products\[\*]** 및 **products\[\*].productID**&#x200B;와(과) 함께 다음 통과 매핑을 추가하고 여기에 각 행에 새 필드를 추가합니다. 일부는 ML 권장 사항으로 인해 이미 존재할 수 있습니다.

| Source 열 | XDM 열 |
| ----------------------- | ------------------------- |
| orderStatus | eventType |
| lastOrderStatusUpdate | timestamp |
| products\[\*] | productListItems\\*] |
| products\[\*].productID | productListItems\[\*].SKU |

>[!NOTE]
>
>**products\[\*]**&#x200B;이(가) 개체 필드 간에 1-1 필드 매핑을 수행하고 있으며 명시적 필드 매핑 **products\[\*].productID**&#x200B;이(가) 기본 복사본을 재정의합니다.

>[!NOTE]
>
>**products\[\*].productID**&#x200B;은(는) **productListItems\[\*].\_id** 외에 **productListItems\[\*].SKU**&#x200B;에도 매핑되어 있습니다. 이는 XDM 스키마의 여러 출력 필드에 매핑되는 단일 입력 필드의 예입니다. 매핑을 그대로 유지합니다.

1. **productListItems\[\*].priceTotal**&#x200B;에 대한 **products\[\*].price** 매핑을 유지합니다.

## 특정 필드에 재정의 추가

1. 객체 복사 매핑 재정의 기준
   1. **products\[\*].make**&#x200B;을(를) **productListItems\[\*].\_devbc.make**&#x200B;에 매핑
   2. **products\[\*].model**&#x200B;을(를) **productListItems\[\*].\_devbc.model**&#x200B;에 매핑

## 특정 필드에 대한 재정의 삭제

1. **productListItems.currencyCode** 및 **productListItems.quantity**&#x200B;이(가) 자동으로 채워져 있는지 확인하십시오.
1. **productListItems\[\*].quantity** 및 **productListItems\[\*].currencyCode** 매핑을 제거합니다.
1. 재정의는 발생하지 않으며 통과 필드가 통과하면 객체 복사본이 적용됩니다.


## 객체 복사 매핑, 재정의 및 삭제 요약

| Source 열 | XDM 열 | 액션 |
| -------------------------- | ----------------------------------- | -------------------------------------- |
| products\[\*] | productListItems\\*] | `Add` |
| products\[\*].productID | productListItems\[\*].SKU | `Add` |
| products\[\*].productID | productListItems\[\*].\_id | `No change` |
| products\[\*].make | productListItems\[\*].\_devbc.make | `Change` |
| products\[\*].model | productListItems\[\*].\_devbc.model | `Change` |
| products\[\*].price | productListItems\[\*].priceTotal | `No change` |
| products\[\*].quantity | productListItems\[\*].quantity | `Remove` |
| products\[\*].currencyCode | productListItems\[\*].currencyCode | `Remove` |

## 매핑 확인

확인해야 하는 매핑 세트가 2개 있습니다. 총 2개를 제거한 후에 6개의 매핑이 있어야 합니다.



![개체 복사 재정의를 추가한 후 productListItems에 대한 결과 매핑](assets/object-copy-mappings-resultant-mappings-for-productlistitems.png "ProductListItems\[*]에 대한 결과 매핑은 다음과 같아야 합니다.")

![개체 복사 재정의 후 productListItems에 대한 결과 매핑의 두 번째 보기](assets/object-copy-mappings-resultant-mappings-for-productlistitems--2.png)
