---
hold: true
title: 데이터 레이크에서 이벤트 유효성 검사
description: 데이터 레이크를 쿼리하여 스트리밍된 웹 이벤트가 올바른 데이터 세트에 작성되었는지 확인하는 방법에 대해 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: 14445089-aa3c-4cce-9d33-80032b6f9868
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---


# 데이터 레이크에서 이벤트 유효성 검사

## 학습 목표

웹 이벤트가 Experience Platform 데이터 레이크에 기록되었는지 확인합니다.

## 이벤트 유효성 검사

&#x200B;> [!NOTE]
>
>결국 데이터가 데이터 레이크에 표시됩니다.  **최대 60분**&#x200B;이 소요될 수 있습니다.  프로필에 대해 데이터 세트가 활성화되어 있으므로 이벤트는 프로필 조각을 생성합니다.
>
>웹 데이터 세트를 찾아 쿼리할 수 있습니다.

1. **쿼리** 및 **쿼리 만들기**(으)로 이동

![쿼리 섹션에서 쿼리 화면 만들기](assets/validate-event-on-data-lake-create-query.png)

&#x200B;2. 이 SQL을 복사하여 쿼리에 붙여넣기

```sql
SELECT identityMap['email'][0].id, * FROM dep_web
where identityMap['email'][0].id = 'henry.creel@emailsim.io'
```

&#x200B;3. **실행** 쿼리

&#x200B;> [!NOTE]
>
>**저장**: 데이터가 데이터 레이크에 표시됩니다.  **최대 60분**&#x200B;이 소요될 수 있습니다.
>
>표시될 때까지 기다릴 필요가 없습니다. 이 단계로 돌아가서 나중에 확인해 보십시오.



![데이터 레이크에서 스트리밍된 웹 이벤트를 표시하는 쿼리 결과](assets/validate-event-on-data-lake-query-results.png)

## 요약

이벤트 레코드가 적절한 데이터 세트에 표시됩니다.
