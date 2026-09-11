---
title: API 컬렉션
description: AEP Foundations Labs 전체에서 사용된 요청이 포함된 부트캠프의 Postman API 컬렉션을 다운로드하여 가져옵니다.
doc-type: article
solution: Experience Platform
exl-id: 18d820c5-56ad-46b8-a9cf-f725555d2db3
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# API 컬렉션

## Postman API 컬렉션 파일

파일 다운로드 — [AEP Foundations Bootcamp(Labs).postman_collection.json](assets/aep-foundations-bootcamp-labs.postman_collection.json)



## API 컬렉션 가져오기

1. 파일을 클릭하여 브라우저에서 `Postman API Collection File`을(를) 엽니다.
1. 클립보드에 파일의 URL 복사
1. 로컬 컴퓨터에서 Postman을 시작하고 작업 공간에서 `Import` 단추를 클릭합니다.
1. `Postman API Collection File`의 URL을 오버레이의 가져오기 양식 텍스트 상자에 붙여 넣습니다.  자동 가져오기가 트리거됩니다.

![Postman 작업 영역에서 가져오기 단추를 클릭하여 API 컬렉션을 가져옵니다](assets/api-collection-click-import-button.png "가져오기 단추")



![API 컬렉션 파일 URL을 Postman 가져오기 양식 텍스트 상자에 붙여 넣기](assets/api-collection-import-modal-paste-url.png "가져오기 단추 양식 텍스트 상자")

이제 컬렉션이 왼쪽 사이드바의 `Collections` 탭 아래에 채워집니다. 이름은 `AEP Foundations Bootcamp`입니다.



![AEP Foundations Bootcamp 컬렉션이 Postman 컬렉션 사이드바 탭에 채워짐](assets/api-collection-imported-collection-in-sidebar.png)

## AEP Foundations Bootcamp 컬렉션 개요

가져온 API 컬렉션에는 부트캠프 전체에서 Labs에 필요한 모든 API 호출이 포함되어 있습니다.  각 랩은 자체 API 세트와 함께 특정 폴더로 구성됩니다.  이번 주 실습을 진행하면서 이 점을 꼭 숙지하시기 바랍니다.

각 폴더에 대한 자세한 내용은 아래에서 확인할 수 있습니다.

- **IMS 인증** - Adobe Experience Platform API로 작업할 때 필요한 액세스\_토큰을 생성하기 위한 단일 요청이 포함되어 있습니다.
- **XDM 스키마 랩** - 실시간 고객 프로필에 대한 스키마를 빌드하고 구성하는 데 필요한 XDM 구성 요소를 만들기 위한 요청 집합이 포함되어 있습니다.
- **데이터 수집 랩** - Experience Platform으로 데이터를 스트리밍하기 위한 요청 집합을 포함합니다.
- **프로필 랩** - Real-Time Customer Profile의 트레이트 및 동작을 보기 위한 요청 집합을 포함합니다.

>[!TIP]
>
>축하합니다!  부트캠프의 Postman 컬렉션을 정상적으로 가져왔습니다.
