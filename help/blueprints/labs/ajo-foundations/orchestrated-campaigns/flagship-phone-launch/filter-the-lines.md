---
title: 라인 필터링
description: 분할 활동으로 옵트아웃 고객 라인을 필터링하고 차원 변경을 사용하여 워크플로우의 타겟 차원을 SMS 채널 구성과 정렬하는 방법을 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: fb556a27-5c73-4457-ae98-dba43d445c7f
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
    internal-label: Experience Platform
source-git-commit: 689f227965176096ccd1785699de65046af4f3d3
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%
---

# 라인 필터링

## 목표

다음 단계 세트에서는 라인 수준에서 옵트아웃됨으로 인해 SMS 메시지로 타깃팅할 수 없는 모든 라인을 필터링할 예정입니다.  이는 라인 수준 대상이므로 프로필 동의에 의존할 수 없습니다.



## 분할 활동 설정

1. 포크 활동의 아래쪽 전환에 있는 **+** 아이콘을 클릭하고 팝업에서 **분할** 활동을 선택합니다.

   ![아래쪽 포크 분기에 분할 활동 추가](assets/filter-the-lines-add-split-activity.png)



2. 오른쪽 레일에서 레이블을 업데이트하여 다음 내용을 표시합니다. `Filter out opt'd out lines`

   ![활동 레이블 분할을 옵트아웃 줄 필터링으로 설정](assets/filter-the-lines-set-split-label.png)



3. 오른쪽 레일에서 기본 세그먼트 **하위 집합** 섹션을 확장하고 **필터 만들기** 단추를 클릭합니다.

   ![하위 집합 섹션에 필터 단추를 만듭니다](assets/filter-the-lines-create-filter-button.png)



4. SMS 메시지에서 옵트아웃된 모든 고객 회선을 제거하도록 조건을 추가한 다음 **확인**&#x200B;을 클릭합니다.

   ![고객 회선을 제거하는 조건이 SMS에서 옵트아웃됨](assets/filter-the-lines-sms-optin-condition.png)

   >[!NOTE]
   >
   >조건을 만드는 방법을 파악해야 하지만 최종 결과는 위의 스크린샷과 일치합니다.  잡았다!



5. 작업 내용을 저장하려면 오른쪽 상단에 있는 저장 버튼을 클릭합니다.  캔버스는 현재 다음과 같습니다.

![분할 활동을 저장한 후 워크플로 캔버스](assets/filter-the-lines-canvas-after-split-save.png)



## SMS 활동 추가

1. 워크플로우 캔버스에서 추가한 분할 조건 뒤에 있는 **+** 아이콘을 클릭하고 **모바일 메시지 활동**&#x200B;을 선택합니다

   ![분할 조건 뒤에 모바일 메시지 활동 추가](assets/filter-the-lines-add-sms-activity.png)

   ![SMS 활동이 워크플로우 캔버스에 추가됨](assets/filter-the-lines-sms-activity-on-canvas.png)



2. 오른쪽 레일에서 모바일 메시지 편집 버튼을 클릭하여 SMS 메시지 구성을 시작합니다

   ![오른쪽 레일의 모바일 메시지 단추 편집](assets/filter-the-lines-edit-sms-button.png)



3. 위쪽 탐색에서 Actions 메뉴 항목을 클릭하고 Mobile message configuration 드롭다운에서 이전에 만든 채널을 선택합니다.

![SMS 구성에서 선택한 채널을 표시했습니다](assets/filter-the-lines-sms-configuration-selected.png)




## 요약

옵트아웃으로 인해 SMS 메시지로 타깃팅할 수 없는 모든 줄을 필터링했으며, 타깃팅할 수 있는 사람에 대한 SMS 활동을 추가했습니다.
