---
title: 매핑 구성
description: 일괄 처리 수집 랩에서 매핑 세트를 가져오고 스트리밍 소스의 날짜 형식과 일치하도록 계산된 날짜 필드를 업데이트합니다.
doc-type: article
solution: Experience Platform
exl-id: c05792af-5eab-4e62-a26e-a54478a988a8
source-git-commit: 0b33b2740ee7f5af73d64f217b4475650c1d28a0
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# 매핑 구성

>[!NOTE]
>
>일괄 처리 수집 랩을 성공적으로 완료한 경우에만 이 섹션을 따르십시오.  그렇지 않으면 일괄 처리 수집 랩에 있는 [데이터 매핑](../batch-ingestion/mapping-data/overview.md) 단계를 따르십시오.

## 매핑 세트 가져오기

일괄 처리 수집 실습을 완료한 경우 😄🎉에서 만든 매핑 세트를 다시 사용할 수 있습니다.

다음 단계를 수행하십시오.

1. 매핑 화면에서 **매핑 가져오기** 단추를 클릭합니다.

   ![매핑 화면의 매핑 가져오기 단추](assets/configure-mapping-import-mapping-button.png)



1. [일괄 처리 수집] 섹션에서 생성한 데이터 흐름을 선택하고 선택합니다.  이름은 **고객 계정 일괄 처리 v2 - \&lt;이니셜>.**&#x200B;과 같이 지정해야 합니다.

![매핑 집합을 가져올 일괄 처리 수집 데이터 흐름 선택](assets/configure-mapping-choose-batch-ingestion-dataflow.png)



가져오기를 수행하면 오류가 표시됩니다.  이는 샘플 파일의 birth\_Date 필드에 사용되는 날짜 형식이 변경되었기 때문입니다.

- 사용된 배치 샘플 파일 -> mm/dd/yyyy
- 사용된 스트림 샘플 파일 -> yyyy-mm-dd

**날짜** 함수를 사용하는 계산된 필드를 업데이트하여 사용된 날짜 형식의 변경 사항을 고려해야 합니다.

![일괄 처리 수집 매핑 집합을 가져온 후 표시되는 매핑 오류](assets/configure-mapping-mapping-after-the-import.png)



## 계산된 필드 업데이트

각 계산된 필드 옆에 있는 화살표 아이콘을 클릭하여 각 계산된 필드를 업데이트한 다음 매핑의 유효성을 검사합니다

![계산된 필드의 수식을 편집하기 위해 클릭하는 화살표 아이콘](assets/configure-mapping-arrow-to-edit-calculated-field-formula.png)

| 대상 필드 | 새 계산된 필드 |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| person.birthYear | date\_part(&quot;yyyy&quot;,date(birth\_Date,&quot;yyyy-M-d&quot;)) |
| person.birthdayAndMonth | concat(date\_part(&quot;mm&quot;, date(birth\_Date, &quot;yyyy-M-d&quot;)).toString(), &quot;-&quot;, date\_part(&quot;dd&quot;, date(birth\_Date, &quot;yyyy-M-d&quot;)).toString() |
