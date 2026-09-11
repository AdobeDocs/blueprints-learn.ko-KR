---
title: 빌드 사용 사례
description: 컨테이너 변수를 사용하여 1주일 내에 동일한 주문에 대해 주문된 이벤트와 주문이 취소된 이벤트를 일치시키는 배치 대상을 작성합니다.
doc-type: article
solution: Experience Platform
exl-id: 4b72b76f-de64-4712-85a6-ec7890b23b97
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# 빌드 사용 사례 #3

## 대상자 만들기

1. 새 대상 만들기
1. 캔버스에 주문 이벤트 추가
1. 주문된 이벤트 오른쪽에 주문 취소됨 이벤트 추가
1. 일주일 이내로 시간 변경

>[!NOTE]
>
>**이벤트 유형 필드**
>
>다음을 사용할 수 있습니다.
>
>- Event Type=order.placed 로 필터링된 모든 이벤트
>- 이벤트 유형=order.canceled로 필터링된 모든 이벤트

![이벤트 기간을 일주일 이내로 변경](assets/build-use-case-3-change-time-to-within-a-week.png)



![주문 및 주문 취소 이벤트가 일주일 이내에 발생하도록 구성되었습니다.](assets/build-use-case-3-change-time-to-within-a-week--2.png)

>[!NOTE]
>
>**시간**
>
>대상 엔진은 타임스탬프만 사용하여 이벤트의 순서를 해석합니다. 따라서 이벤트에 날짜/시간 필드가 여러 개 있는 경우 타임스탬프 필드가 사용되는 필드임을 기억하십시오.



## 취소된 이벤트 구성

주문 ID를 검색하고 필드를 주문 취소됨 이벤트로 드래그합니다.

![주문 ID를 검색하고 필드를 주문 취소 이벤트로 끌어서 놓습니다](assets/build-use-case-3-search-order-id-drag-onto-order-cancelled-event.png)

>[!NOTE]
>
>주문된 주문이 취소된 주문과 동일한지 확인하기 위해 주문 ID에 대한 필터를 추가하고 있습니다



검색 내용을 지우고 **변수 찾아보기** 아래의 **배치됨**&#x200B;을 클릭합니다.

![변수 찾아보기 아래에 있는 항목을 클릭합니다](assets/build-use-case-3-click-into-placed-under-browse-variables.png)



주문 ID로 드릴다운한 다음 드래그하여 비교 피연산자를 추가합니다

![주문 ID로 드릴다운한 다음 드래그하여 비교 피연산자를 추가하십시오.](assets/build-use-case-3-drill-down-to-order-id-add-compare-operand.png)

>[!WARNING]
>
>**변수 내에서 검색을 사용하지 않음**
>
>변수의 컨텍스트를 유지하지 않습니다



최종 결과는 아래에서 보았던 대로여야 합니다.

![주문 ID 비교 피연산자가 추가된 최종 대상 구성](assets/build-use-case-3-final-audience-configuration-result.png)

>[!NOTE]
>
>**컨테이너**
>
>이는 변수 컨테이너를 사용하여 주문 취소됨이 주문된 주문과 동일한지 확인하는 것입니다
>
>이전에는 Container를 사용하여 배열에서 요소를 분리했습니다. 여기에서는 컨테이너를 사용하여 다른 이벤트 내의 필터 기준에서 특정 이벤트를 참조합니다.
>
>주문 취소됨 이벤트는 자체 주문 ID가 주문 ID와 동일하도록 합니다.
>
>다른 방법으로는 어떻게 사용할 수 있습니까?
>
>- 페이지 보기에 대한 제품 SKU의 비교는 구매한 제품 SKU입니다.
>- 납품처 도시를 비교하는 것은 청구처 도시와 다릅니다.
>- 이벤트가 다른 스키마에서 발생할 수 있더라도 동일한 데이터 유형의 두 필드 비교가 가능해야 합니다
>
>https\://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-blogs/how-exactly-do-containers-work-in-aep-segmentation-a-deeper-look/ba-p/458780

>[!NOTE]
>
>**컨테이너 이름**
>
>컨테이너는 해당 컨텍스트에서 변수 이름을 상속합니다.
>
>예: Any Event 카드를 사용하는 경우 컨테이너 이름은 Any1이 됩니다.



## 대상자 저장

1. 설명을 입력합니다. 평가 방법을 배치로 설정합니다.
1. 대상을 &quot;*주내에 주문 및 주문 취소됨*&quot;으로 저장

>[!TIP]
>
>**선택적 Challenge Lab**
>
>일찍 끝났나요? 이거...
>
>장바구니 포기를 위한 새 캠페인을 시작하려고 합니다.  장바구니 포기에 대한 대상을 만들되, 한 시간 동안 사용자를 타겟팅하지 않도록 하십시오.
>
>
>
>아직 시간 있어? 이거...
>
>이 회사는 합병하여 다음 두 개의 새 사업부를 인수했습니다.
>
>- ISP
>- 케이블
>
>이러한 스키마를 포함하도록 스키마를 수정하려면 어떻게 해야 합니까?
