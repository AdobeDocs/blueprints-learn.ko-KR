---
hold: true
title: 환경 파일 가져오기
description: Postman 환경 파일을 가져오고 부트캠프 전체에서 API 호출에 필요한 EDGE_REGION과 같은 전역 변수를 설정합니다.
doc-type: article
solution: Experience Platform
exl-id: a5d45656-e3f5-4207-823c-ad33d4ef26a4
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# 환경 파일 가져오기

## 목표

이 페이지에서는 Postman 환경 파일을 가져옵니다.  이 파일에는 부트캠프 전체에서 다른 Labs를 수행하는 동안 수행되는 다양한 API 호출 내에서 사용할 수 있는 여러 전역 변수가 포함되어 있습니다.

## 환경 파일 가져오기

1. **AJO Bootcamp.postman\_environment.json** 파일 다운로드:

파일 다운로드 — [AJO Bootcamp.postman_environment.json](assets/ajo-bootcamp.postman_environment.json)

&#x200B;2. 로컬 컴퓨터에서 Postman을 실행합니다.
&#x200B;3. 필요한 경우 이러한 Labs에 사용하는 Workspace(Workspace을 사용하는 경우)로 전환하고 **가져오기** 단추를 클릭합니다.

![Postman 가져오기 시작](assets/import-environment-file-click-import-button.png)

&#x200B;4. **AJO Bootcamp.postman\_environment.json** 파일의 로컬 URL을 [가져오기] 양식 텍스트 상자에 붙여 넣거나 [가져오기] 대화 상자에 놓습니다.  자동 가져오기가 트리거됩니다.

![파일 URL을 붙여넣는 옵션을 보여 주는 Postman 가져오기 대화 상자](assets/import-environment-file-import-button-overlay.png "URL을 통한 Postman 가져오기")

![드래그 앤 드롭을 통해 드롭된 파일을 수락하는 Postman 가져오기 대화 상자](assets/import-environment-file-drag-and-drop-import.png "드래그 앤 드롭을 통한 Postman 가져오기")

&#x200B;5. 가져온 후에는 왼쪽 사이드바에서 **환경** 탭을 클릭하여 환경이 있는지 확인하십시오. 이제 AJO Bootcamp 환경을 사용할 수 있습니다.

![환경 가져오기 유효성 검사](assets/import-environment-file-validate-environment-imported.png)

## 환경 변수 설정

Postman은 테스트하고 API와 상호 작용하도록 설계되었습니다. 하지만 브라우저나 서버측 실시간 데이터 수집 호출의 AEP Web SDK 히트를 시뮬레이션하는 데 사용하고 있습니다. 이러한 호출은 여전히 가장 엄격한 의미의 API 호출이지만 헤더에 인증 토큰과 같은 것이 필요한 일반적인 API 호출은 아닙니다. 이러한 Labs의 환경 변수는 주로 URL 경로의 변수에 사용됩니다(하나는 헤더에 사용됨).

1. 필요한 경우 Postman의 왼쪽 사이드바에서 **환경** 탭을 클릭합니다
2. **AJO Bootcamp** 환경 파일을 클릭합니다. 채워야 할 값이 표시됩니다.

![비어 있는 값을 입력해야 하는 Postman 환경 변수](assets/import-environment-file-values-need-filling-in.png "환경에서 postman 변수 확인")

&#x200B;3. 지금은 DATASTREAM\_CONFIG 값을 건너뜁니다. 이후 실습에서 데이터 스트림 구성을 만듭니다.
&#x200B;4. 아래 표를 조회 항목으로 사용하여 이 부트캠프의 실제 위치와 가장 가까운 지역 코드로 **EDGE\_REGION** 필드를 업데이트합니다.

| **지역** | **지역 코드** |
| ---------- | --------------- |
| 미국 서부 | or2 |
| 미국 동부 | va6 |
| 유럽 | irl1 |
| 오스트레일리아 | aus3 |
| 일본 | jpn3 |
| 아시아 | spg3 |

완료되면 환경 파일은 다음과 유사해야 합니다.



![Postman 지역 변수 확인](assets/import-environment-file-region-variable-set.png)

&#x200B;5. 이제 환경 변수를 저장해야 하지만, Postman UI에는 저장 버튼이 없습니다. 저장할 때 Windows 또는 Mac 단축키를 사용합니다(예: Windows의 경우 ctrl+s). Postman UI의 오른쪽 하단에 **변경 내용 저장됨** 메시지가 표시되면 변경 내용이 저장된 것을 알 수 있습니다.

![변경 내용 저장 확인](assets/import-environment-file-changes-saved-confirmation.png)

>[!TIP]
>
>축하합니다! Postman 환경 파일을 완료했습니다
