---
title: 데이터 흐름 만들기
description: 새 데이터 세트로 배치 소스 데이터 흐름을 구성하고 프로필 및 부분 수집을 활성화하고 샘플 고객 계정 CSV 파일을 업로드합니다.
doc-type: article
solution: Experience Platform
exl-id: 70145966-d6c0-4741-8216-903de0d61e1d
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---


# 데이터 흐름 만들기

## 소스로 이동

1. Adobe Experience Platform UI에서 다음 위치로 이동합니다.\
   **소스** -> **카탈로그** -> **로컬 시스템**
1. **로컬 파일 업로드** 카드에 대한 **데이터 추가** 단추를 클릭합니다.

![소스 카탈로그의 로컬 파일 업로드 카드에 대한 데이터 추가 단추](assets/create-dataflow-local-file-upload-add-data.png "데이터 랜딩 영역에 액세스")



## 데이터 흐름 설정

1. 데이터 흐름 세부 정보 화면에서 **새 데이터 세트**&#x200B;를 선택합니다.
1. 출력 데이터 세트의 이름을 **고객 계정 - \&lt;이니셜>**(으)로 지정합니다.
1. 드롭다운 목록에서 **dep: 고객 계정** 스키마를 선택합니다.
1. **프로필 데이터 집합** 토글 상자를 켭니다.
(이 기능을 켜지 않으면 프로필 저장소는 이 데이터 세트에 입력되는 새 데이터를 모니터링할 수 없으므로 이 데이터를 프로필로 수집하지 않습니다.)
1. **부분 수집 사용**을 켭니다.
(이 기능을 켜지 않으면 레코드 중 하나에 오류가 있는 경우 전체 수집이 실패할 수 있습니다.)
1. 데이터 흐름 이름을 **고객 계정 일괄 처리 - \&lt;이니셜>**(으)로 설정합니다.
1. 모든 경고 설정 **소스 데이터 흐름 시작/성공/실패**

   ![새 데이터 세트, 프로필 및 부분 수집 설정이 구성된 데이터 흐름 세부 정보 화면](assets/create-dataflow-new-dataset-flow-details.png "데이터 흐름 세부 정보")

   >[!NOTE]
   >
   >**부분 수집 사용**&#x200B;은(는) 전체 데이터 흐름이 실패로 선언되기 전에 실패할 수 있는 총 레코드 수의 비율로 오류 수(**INGEST** 및 **DCVS**)를 지정합니다.

   >[!CAUTION]
   >
   >계속하기 전에 프로필과 부분 수집 모두에 대해 **을(를)** 데이터 세트를 활성화했는지 확인하십시오.

1. 모든 것이 잘 보이는 경우 화면 오른쪽 상단의 **다음** 단추를 클릭하여 다음 단계로 진행합니다.



## 샘플 파일 업로드

1. 이 랩에서 사용할 샘플 파일을 [샘플 파일](../sample-files.md)에서 다운로드합니다.
1. UI에서 **Lab\_Customer\_Account.csv** 파일을 &#39;놓기 및/또는 업로드&#39;하십시오.  완료되면 화면은 아래와 같이 표시됩니다.

   ![소스 데이터 화면에서 업로드된 고객 계정 CSV 파일 미리 보기](assets/create-dataflow-uploaded-csv-preview.png "Adobe Experience Platform 내의 Azure Storage Explorer 파일에 액세스")

1. 미리 보기 창에서 다음 속성을 확인하고 다음 사항에 유의하십시오.

   - **sms\_optIn**&#x200B;은(는) 동의 필드에 누락된 값이 여러 개 있습니다( - 로 미리 보기에 표시됨).
   - **account\_create\_date**&#x200B;에 적절한 날짜 형식이 없습니다. 여기에는 하나의 문자열에 날짜 및 시간 값과 함께 문자열 값이 있습니다.
   - **account\_end\_date**&#x200B;의 날짜 형식이 잘못되었습니다.



   ![동의 값이 누락된 sms_optIn 필드를 표시하는 미리 보기](assets/create-dataflow-sms-optin-missing-values.png "sms_optin")



   ![일관되지 않은 서식을 표시하는 account_create_date 및 account_end_date 필드 값 미리 보기](assets/create-dataflow-account-create-end-date-preview.png "account_create_date &amp; account_end_date")

   >[!NOTE]
   >
   >이 실습의 후반부에 있는 매핑 단계에서 누락된 값, 날짜 및 잘못된 형식의 필드를 처리해야 합니다

1. 화면 오른쪽 위의 **다음** 단추를 클릭하여 다음 단계를 계속합니다
