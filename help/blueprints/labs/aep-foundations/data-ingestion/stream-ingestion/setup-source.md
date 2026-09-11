---
title: 소스 설정
description: HTTP API 스트리밍 계정을 만들고 데이터 흐름을 구성하여 고객 계정 JSON 데이터를 프로필 사용 데이터 세트로 스트리밍합니다.
doc-type: article
solution: Experience Platform
exl-id: a5c02337-8af3-45dc-82a0-fa9731892fe4
source-git-commit: 3039df0c022176e9dada9c5a300f2df14429033d
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---


# 소스 설정

## 스트리밍 소스로 이동

1. Adobe Experience Platform UI로 이동하여 **소스**(으)로 이동
1. 위쪽 탐색에서 **Catalog** 클릭
1. 소스 목록에서 **스트리밍**&#x200B;을 선택합니다(모든 소스 라디오 단추가 선택되어 있는지 확인).
1. HTTP API에 대해 **설정** / **데이터 추가**&#x200B;를 클릭합니다.

![새 HTTP API 원본 계정을 만드는 단계 순서](assets/setup-source-sequence-of-steps-to-create-a-http-api-account.png)



## HTTP API 계정 만들기

먼저 새 계정을 만들어야 합니다. 이 계정에는 인증 처리 방법과 관련하여 스트리밍되는 데이터가 XDM과 호환되는 경우(즉, 기본 XDM 스키마의 구조와 이미 일치하는 경우)에 대한 세부 정보가 들어 있습니다

다음 작업을 수행합니다.

1. **새 계정**&#x200B;을(를) 선택하고 다음 세부 정보를 추가하십시오.
   - 계정 이름 -> `Streaming Ingestion - <Your Initials>`
1. **인증 사용**&#x200B;에 대한 토글을 사용하지 않도록 설정
1. **XDM 호환**&#x200B;에 대한 확인란을 선택하지 않은 상태로 둡니다.
1. 계속하려면 **소스에 연결** 단추를 클릭하십시오.

>[!CAUTION]
>
>**인증 사용**&#x200B;을 켜거나 **XDM 호환**&#x200B;에 대한 확인란을 선택하지 마십시오. 이게 실험실을 망가뜨리는 거야

화면은 다음과 같아야 합니다.

![새 HTTP API 계정의 소스에 연결을 클릭한 후 화면](assets/setup-source-connect-to-source-screen.png)



이제 &quot;연결됨&quot; 메시지가 표시된 녹색 확인란이 표시됩니다. 데이터 흐름을 계속 설정하려면 오른쪽 상단의 **다음** 단추를 클릭하십시오.

![HTTP API 계정을 설정한 후 연결된 메시지가 있는 녹색 확인란](assets/setup-source-green-checkbox-with-connected-message.png "연결된 녹색 확인란이 표시됨")



## 샘플 데이터 업로드

>[!NOTE]
>
>아직 다운로드하지 않았다면 [샘플 파일](../sample-files.md)을 다운로드하십시오



1. 화면의 Source 데이터 스키마 섹션에서 이전 랩에서 다운로드한 로컬 파일 시스템에서 JSON 파일 **Lab\_Single\_Customer\_sample.json**&#x200B;을(를) 업로드합니다.
1. 파일이 업로드되면 다음과 같이 미리보기가 표시됩니다. 계속하려면 오른쪽 상단의 **다음** 단추를 클릭하십시오. birth_Date 필드가 이전에 배치 수집 랩에서 보았던 MM/DD/YYYY 형식과 YYYY-MM-DD 형식이 어떻게 다른지 관찰합니다.

![파이프라인 디자인 및 유효성 검사를 위해 업로드된 Lab_Single_Customer_sample.json 레코드의 미리 보기](assets/setup-source-sample-customer-record-for-pipeline-design-and-validation.png)

>[!NOTE]
>
>JSON 샘플 파일에는 파이프라인의 디자인 및 유효성 검사를 위한 단일 레코드가 포함되어 있습니다. 스크롤하려면 XDM 노드를 클릭하여 노드가 스크롤되도록 해야 합니다.



## 데이터 흐름 세부 정보 구성

이 화면에서는 사용자가 설정한 HTTP API 계정을 활용하는 특정 데이터 흐름을 만듭니다.  계정당 많은 데이터 흐름이 있을 수 있습니다.  이 시나리오에서는 고객 계정 데이터 스트리밍을 위한 데이터 흐름을 만들어야 합니다. 데이터 흐름을 사용하려면 소스 계정, 연결된 스키마가 있는 데이터 세트 및 구성 세부 정보 간의 연결이 필요합니다.

다음 단계를 수행하십시오.

1. 새 데이터 집합을 만들고 이름을 -> `Customer Account Stream - <Your Initials>`(으)로 지정합니다.
1. **스키마**&#x200B;을(를) ->`dep: Customer Account`(으)로 선택
1. **프로필 데이터 세트** 전환이 **활성화됨**&#x200B;인지 확인하십시오.  그렇지 않으면 **사용**&#x200B;하세요.
1. 다음과 같이 **데이터 흐름 이름**&#x200B;을(를) 업데이트합니다.
   - `Customer Account Stream - <Your Initials>`
1. 계속하려면 **다음** 단추를 클릭하십시오.

![고객 계정 스트리밍 데이터 세트에 대한 데이터 흐름 세부 정보 구성](assets/setup-source-configuring-a-dataflow.png)

>[!NOTE]
>
>프로필에 대해 데이터 세트를 활성화하지 않으면 데이터가 데이터 레이크로만 스트리밍됩니다. 프로필 또는 ID 그래프에 스트리밍 이벤트가 표시되지 않습니다.
