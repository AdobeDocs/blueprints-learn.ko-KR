---
hold: true
title: 디버깅 오류
description: 미리보기 오류 진단을 사용하여 실패한 데이터 흐름을 조사하고 INGEST 형식 오류를 MAPPER 전환 경고와 구별합니다.
doc-type: article
solution: Experience Platform
exl-id: beee191b-a860-494c-873f-ab2e407ffbf5
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# 디버깅 오류

## 오류 진단 미리 보기

몇 분 후에 **Status**&#x200B;에 오류가 표시됩니다. 실패 세부 정보를 드릴다운하여 실패의 원인을 확인합니다.

1. **데이터 흐름 실행 시작** 날짜를 클릭합니다.
1. 실패한 각 행에 대한 특정 세부 정보를 보려면 **오류 진단 미리 보기**&#x200B;를 클릭하십시오.

![실패를 표시하는 데이터 흐름 실행 상태](assets/debugging-errors-dataflow-run-failure.png "데이터 흐름 실행 실패")

![데이터 흐름 실행 세부 정보 화면에서 오류 진단 링크 미리 보기](assets/debugging-errors-preview-error-diagnostics-link.png "오류 진단 미리 보기")



이제 표시되는 화면에는 전체 오류 메시지와 함께 오류 코드의 의미와 실패한 행에 대한 여러 가지 세부 사항이 표시됩니다.

![오류 코드, 메시지 및 실패한 행을 표시하는 오류 진단 세부 정보 화면](assets/debugging-errors-error-diagnostics-detail-screen.png "오류 진단 미리 보기")

>[!NOTE]
>
>오른쪽으로 스크롤하여 이 오류 코드와 연관된 소스 데이터를 확인합니다



## 오류 유형 이해

### 수집-XXXX-XXX 오류

이 오류는 **person.birthDayAndMonth**&#x200B;이(가) 두 자리 월과 두 자리 일 형식으로 예상되기 때문에 발생합니다(예: 4월 27일의 형식은 04-27이어야 함).

```none
The value (9-27) does not conform to the specified
regex pattern: [0-1][0-9]-[0-9][0-9] in field: 
person.birthDayAndMonth of type: String
```

>[!CAUTION]
>
>person.birthDayAndMonth는 필수 필드가 아니지만 정규 표현식에 대한 부적합은 시스템에서 &quot;데이터 손상 문제&quot;로 처리되며 심각한 오류입니다.



### MAPPER-XXXX-XXX 오류

이 오류는 **createDate**&#x200B;의 원본 필드에 `Created on 2022-04-22T19:34:17Z`의 문자열 값이 있기 때문에 발생합니다. 시작 부분의 텍스트 때문에 이 값을 자동으로 날짜로 변환할 수 없습니다. `Created on`. 데이터를 정리하려면 계산된 필드를 사용해야 합니다.

```none
Error transforming data for destination path 
_dep.account.createDate. Details: Unable to convert 
Created on 2023-09-24T10:19:58Z to schema type DATE_TIME
```

&#x200B;> [!NOTE]
>
>이 오류는 매핑 중에 경고만 발생하므로 심각한 오류는 아닙니다. 이로 인해 데이터 흐름 실행이 실패하지 않으므로 이 랩에서는 이 오류를 수정하지 않습니다.
