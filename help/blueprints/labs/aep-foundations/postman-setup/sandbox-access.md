---
hold: true
title: 샌드박스 액세스
description: Labs를 시작하기 전에 Postman 환경이 할당된 Experience Platform 샌드박스를 성공적으로 검색할 수 있는지 확인합니다.
doc-type: article
solution: Experience Platform
exl-id: c841e497-a695-4d3f-85e6-d653478cad1e
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# 샌드박스 액세스

계속하기 전에 액세스가 합법적인지 다시 한 번 확인하십시오. 다음 단계를 수행하십시오.

1. 제목이 `Check Sandbox Access`인 폴더를 열고 제목이 `Retrieve Your Sandbox`인 호출을 클릭합니다.
1. Postman의 오른쪽 위 모서리에 환경 드롭다운 상자가 표시됩니다.  `AEP Bootcamp` 환경을 선택하십시오.
1. `Send` 단추를 클릭하여 호출 실행

![보내기 전에 샌드박스 호출 검색에 대한 Postman 요청 창](assets/sandbox-access-check-sandbox-request.png "샌드박스 API 호출 검색")



성공적인 응답은 다음과 같습니다.

할당된 샌드박스의 성공적인 검색을 확인하는 ![200 OK 응답](assets/sandbox-access-successful-response.png "200 OK 샌드박스 요청 성공")

>[!NOTE]
>
>**name** 값은 postman 환경의 sandbox\_name 변수와 일치해야 합니다.

>[!TIP]
>
>축하합니다!  Experience Platform API 사용을 시작할 준비가 되었습니다.
