---
hold: true
title: 확인 및 유효성 검사
description: UI에서 스트리밍된 데이터 세트를 미리 보고 SQL 쿼리를 실행하여 수집된 레코드 및 중첩된 스키마 필드를 확인합니다.
doc-type: article
solution: Experience Platform
exl-id: fbdb0b6b-08b6-49b8-b6ab-d59d5941c678
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# 확인 및 유효성 검사

## 데이터 세트 미리 보기

1. **데이터 세트** 클릭
1. 만든 데이터 세트 이름을 **찾기**&#x200B;하고 **클릭**&#x200B;합니다.

![데이터 세트 창에서 만든 데이터 세트에 액세스](assets/verification-and-validation-access-the-dataset-in-the-datasets-pane.png "데이터 세트 창에서 데이터 세트에 액세스")



1. 오른쪽 상단 모서리에서 **데이터 세트 미리 보기**&#x200B;를 클릭합니다.

![데이터 집합 화면의 오른쪽 상단 모서리에 있는 데이터 집합 미리 보기 단추](assets/verification-and-validation-preview-dataset-button.png "데이터 집합 미리 보기는 오른쪽 상단 모서리에 있습니다. ")



1. 스키마 계층 구조를 보여 주는 왼쪽 창을 클릭하여 수집한 동일한 레코드를 **확인** 및 **확인**&#x200B;합니다.

![스키마 계층 구조 창을 사용하여 수집된 레코드를 확인 및 확인](assets/verification-and-validation-verify-and-validate-the-dataset.png "데이터 집합 확인 및 확인")

>[!NOTE]
>
>**데이터 집합 미리 보기**&#x200B;에는 데이터 집합의 처음 몇 행만 표시됩니다. 배열 개체를 볼 수 없습니다.



## 쿼리 데이터 세트

1. 미리 보기 **닫기**
1. 데이터 집합 화면에서 **테이블 이름**&#x200B;의 복사 아이콘을 클릭합니다. 아래 예제 화면에서 테이블 이름은 `customer_account_sm`입니다.

![쿼리에 사용할 수 있도록 데이터 집합 화면에서 테이블 이름 복사](assets/verification-and-validation-copy-the-table-name.png "테이블 이름 복사")



1. **쿼리** 섹션으로 이동

1. **쿼리 만들기**&#x200B;를 클릭합니다

![쿼리 섹션에서 쿼리 편집기에 액세스](assets/verification-and-validation-access-the-query-editor.png "쿼리 편집기에 액세스")



1. **향상된 쿼리 편집기**&#x200B;에 대한 토글을 전환합니다.

![향상된 쿼리 편집기 토글을 사용하는 쿼리 편집기 인터페이스](assets/verification-and-validation-enhanced-query-editor-toggle.png "쿼리 편집기 인터페이스")



1. 복사한 후 **편집기**&#x200B;에 다음 SQL 쿼리를 붙여 넣습니다. `<table_name>`을(를) 2단계에서 얻은 값으로 바꾸십시오.

```sql
SELECT * FROM <table_name>
```



1. **재생** 단추를 누릅니다.

1. 결과를 **미리 보기**&#x200B;합니다.

1. 또한 다음 SQL 쿼리를 실행하여 데이터와 함께 XDM 스키마를 검색합니다.

```sql
SELECT to_json(shippingAddress) FROM <table_name>
```



1. `postalCode` **노드**&#x200B;의 데이터에 액세스하려면 다음을 입력할 수 있습니다.

```sql
SELECT shippingAddress.postalCode FROM <table_name>
```

>[!TIP]
>
>축하합니다!  실시간 고객 프로필의 샘플 세트를 정상적으로 수집 및 생성했습니다
