---
hold: true
title: 소스 설정
description: 데이터 랜딩 영역에 이전 주문 JSON 파일을 업로드하고 주문 스키마를 타겟팅하는 새 데이터 흐름을 구성합니다.
doc-type: article
solution: Experience Platform
exl-id: 046d50ad-687e-4cdb-a8b1-3c55ab39b68e
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# 소스 설정

## 샘플 파일 업로드

랩 중에 사용할 수 있도록 샘플 데이터 파일을 Azure 저장소 탐색기를 통해 데이터 랜딩 영역에 업로드해야 합니다.  이렇게 하려면 다음을 수행합니다.

1. [샘플 파일](../../../sample-files.md) 다운로드
1. 위에서 저장한 데이터 랜딩 영역으로 **Lab\_Historical\_Orders.json** 파일을 &#39;놓기 및/또는 업로드하십시오.



업로드할 때 화면은 아래 스크린샷과 같아야 합니다.

![데이터 랜딩 영역에 Lab_Historical_Orders.json 파일 업로드](assets/setup-source-lab-historical-orders-json-uploaded-to-dlz.png "DLZ에 Lab_Historical_Orders.json 업로드")

## 소스로 이동

1. Adobe Experience Platform으로 이동하여 다음 위치로 이동: **소스** -> **카탈로그** -> **클라우드 저장소**
1. 데이터 랜딩 영역에 대해 **설정** / **데이터 추가**&#x200B;를 클릭합니다.

![소스 > 카탈로그 > 클라우드 저장소로 이동하여 데이터 랜딩 영역 설정](assets/setup-source-navigate-to-data-landing-zone-source.png "소스 - 데이터 랜딩 영역")

>[!NOTE]
>
>이전 일괄 처리 수집 랩에서 연결을 이미 설정한 경우 **데이터 추가**&#x200B;가 기본 작업으로 표시됩니다



## 파일 미리 보기

1. **Lab\_Historical\_Orders.json** 파일을 선택하고 내용을 미리 봅니다.
1. 화면 오른쪽 상단의 **다음**&#x200B;을 클릭하여 다음 단계를 계속합니다

![Lab_Historical_Orders.json 파일 내용 선택 및 미리 보기](assets/setup-source-select-and-preview-lab-historical-orders.png "Lab_Historical_Orders.json 파일 선택 및 미리 보기")

## 데이터 흐름 설정

1. 데이터 흐름 세부 정보 화면에서 **새 데이터 세트**&#x200B;를 선택합니다.
1. 출력 데이터 세트의 이름을 **Orders - YourNameHere**(으)로 지정합니다.
1. 스키마 이름 **dep: Orders** 선택
1. **프로필 데이터 집합** 토글 상자 켜기
(이 기능을 켜지 않으면 프로필 저장소는 이 데이터 세트에 입력되는 새 데이터를 모니터링할 수 없으므로 이 데이터를 프로필로 수집하지 않습니다.)
1. **부분 수집 사용**
(이 기능을 켜지 않으면 레코드 중 하나에 오류가 있으면 수집이 실패할 수 있습니다.)
1. 데이터 흐름 이름을 **주문 - 다시 채우기 - YourNameHere**(으)로 설정합니다.
1. 모든 경고 설정 **소스 데이터 흐름 시작/성공/실패**

![Orders 데이터 집합에 대해 구성된 데이터 흐름 세부 정보 화면](assets/setup-source-dataflow-details-for-orders.png "Orders에 대한 데이터 흐름 세부 정보")

>[!CAUTION]
>
>프로필 및 부분 수집 모두에 대해 데이터 세트를 **활성화**&#x200B;했는지 확인하십시오.

화면 오른쪽 상단의 **다음**&#x200B;을 클릭하여 다음 단계를 계속합니다
