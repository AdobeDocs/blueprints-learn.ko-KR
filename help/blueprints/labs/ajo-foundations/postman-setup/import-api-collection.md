---
title: API 컬렉션 가져오기
description: 부트캠프의 Postman API 컬렉션을 가져오고 해당 환경 변수가 샌드박스에 대해 올바르게 확인되는지 확인합니다.
doc-type: article
solution: Experience Platform
exl-id: 7562c7f1-0d60-4a3a-8bce-fa42bda08962
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%
---

# API 컬렉션 가져오기

## 목표

이 단계에서는 부트캠프 전체에서 수행해야 하는 모든 다양한 요청이 포함된 API 컬렉션을 가져옵니다.  이러한 API 요청은 방금 가져온 환경 파일에 따라 다릅니다.



## 요청 컬렉션 가져오기

1. **AJO Bootcamp(Labs).postman\_collection.json** 파일 다운로드:

   파일 다운로드 — [AJO Bootcamp(Labs).postman_collection.json](assets/ajo-bootcamp-labs.postman_collection.json)

2. 이전과 같이 **가져오기** 단추를 클릭합니다.
3. **AJO Bootcamp(Labs).postman\_collection.json** 파일의 로컬 URL을 [가져오기] 양식 텍스트 상자에 붙여 넣거나 [가져오기] 대화 상자에 놓습니다.  그러면 자동 가져오기가 트리거됩니다.
4. 가져오기 프로세스가 완료되면 왼쪽 탐색 모음에서 **컬렉션**&#x200B;을 클릭하고 **AJO Bootcamp(Labs)** 폴더를 확장하면 새로 가져온 컬렉션이 표시됩니다

![postman 컬렉션 가져오기 확인](assets/import-api-collection-verify-collection-imported.png)

>[!SUCCESS]
>
>축하합니다!  부트캠프의 Postman 컬렉션을 정상적으로 가져왔습니다.



## 환경 변수 유효성 검사

가져온 컬렉션에는 부트캠프 전체에서 Labs에 필요한 모든 API 호출이 포함되어 있습니다.  각 랩은 고유한 요청 세트가 있는 특정 폴더로 구성됩니다.

각 폴더에 대한 자세한 내용은 아래에 나와 있습니다.

- **프로필 및 여정 Labs** - 웹 이벤트 및 배송 확인을 시뮬레이션하는 이벤트를 보내는 요청 집합이 포함되어 있습니다.
- **Decisioning Labs** - 일반적으로 AEP Web SDK 태그가 지정된 사이트에서 발견되는 위쪽 및 아래쪽 페이지 호출을 모방하는 방문자 3명에 대한 요청이 포함됩니다.

환경과 컬렉션이 올바르게 작동하는지 확인하려면 다음 단계를 수행하십시오.

1. 필요한 경우 왼쪽 레일에서 **컬렉션**&#x200B;을 클릭한 다음 **프로필 및 여정 Labs** 폴더를 확장하세요.
2. **웹 이벤트 만들기** 요청을 클릭하면 환경 변수가 **빨강**&#x200B;인 것을 볼 수 있습니다.

   ![환경이 선택되지 않았으므로 환경 변수가 빨간색으로 강조 표시된 Postman 요청](assets/import-api-collection-environment-variables-shown-red.png "postman 환경 변수가 빨간색인지 확인")

3. 오른쪽 상단의 **환경 드롭다운**&#x200B;을 클릭하고 **AJO Bootcamp** 환경을 선택합니다.

   ![올바른 Postman 환경 선택](assets/import-api-collection-select-postman-environment.png)

4. 적절한 환경을 선택하면 이제 EDGE\_REGION 변수가 더 연한 파란색으로 바뀝니다. 이는 이제 변수에 선택한 환경에 대한 값이 있음을 나타냅니다. DATASTREAM\_CONFIG 변수는 아직 데이터 스트림을 만들지 않았으므로 아직 해당 환경 변수에 대한 값이 없으므로 빨간색으로 유지됩니다. Edge\_REGION을 마우스로 가리키면 환경 값의 값이 표시됩니다.

![Postman EDGE_REGION 변수가 채워져서 더 이상 빨간색으로 표시되지 않습니다](assets/import-api-collection-environment-works-with-collection.png "Postman 환경이 컬렉션에서 작동하는지 확인")

## 요약

이제 환경 및 컬렉션 파일을 가져왔고 이러한 파일을 사용하는 방법을 알고 있습니다.
