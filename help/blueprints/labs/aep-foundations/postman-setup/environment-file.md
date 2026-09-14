---
title: 환경 파일
description: Postman 환경 파일을 가져오고 부트캠프의 API 호출에 필요한 개발자 프로젝트 및 샌드박스 변수를 채웁니다.
doc-type: article
solution: Experience Platform
exl-id: 1461fac5-0714-44d4-b5c8-949df6bcff83
source-git-commit: df6c1852a6e0357dc9f166c88e77dcf9d334f955
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%
---

# 환경 파일

## Postman 환경 파일

파일 다운로드 — [AEP Bootcamp.postman_environment.json](assets/aep-bootcamp.postman_environment.json)



## 환경 파일 가져오기

1. 파일을 클릭하여 브라우저에서 `Environment File`을(를) 엽니다.
1. 클립보드에 파일의 URL 복사
1. 로컬 컴퓨터에서 Postman을 시작하고 작업 공간에서 `Import` 단추를 클릭합니다.
1. `Environment File`의 URL을 오버레이의 가져오기 양식 텍스트 상자에 붙여 넣습니다.  이 작업은 자동 가져오기를 트리거합니다.

![환경 파일을 가져오려면 Postman 작업 영역에서 가져오기 단추를 클릭합니다](assets/environment-file-click-import-button.png "가져오기 단추")



![환경 파일 URL을 Postman 가져오기 양식 텍스트 상자에 붙여 넣기](assets/environment-file-import-modal-paste-url.png "가져오기 단추 오버레이")



가져온 후에는 왼쪽 사이드바에서 `Environments` 탭을 클릭하여 환경 파일이 있는지 확인하십시오.  아래와 비슷한 것을 볼 수 있습니다.

![가져오기 후 Postman 환경 탭에 나열된 AEP Bootcamp 환경](assets/environment-file-aep-bootcamp-environment-listed.png "AEP Bootcamp 환경")



## 환경 변수

API를 호출하기 전에 방금 가져온 환경 파일에서 몇 가지 변수를 업데이트해야 합니다.  이러한 변수는 API 호출에서 참조되므로 올바르게 입력되었는지 확인하십시오.  변수는 두 개의 그룹으로 나뉩니다.

- **개발자 프로젝트 값** -> Adobe Developer Console에서 만든 개발자 프로젝트에서 생성된 기본 변수입니다
- **기타 값** -> 다양한 Experience Platform API를 사용하기 위해 사용자가 일반적으로 만드는 사용자 지정 생성 변수입니다

>[!NOTE]
>
>이 값은 [Developer Console 설치](../sandbox-setup/developer-console-setup.md#collect-your-values)에서 만든 OAuth 서버 간 자격 증명에서 가져옵니다.



### 개발자 프로젝트 값 업데이트

1. Postman 왼쪽 사이드바에서 `Environments` 탭을 클릭합니다.
1. `AEP Bootcamp` 환경 파일을 클릭합니다.
1. 아래 나열된 변수에 대해 `current values`을(를) 업데이트합니다.
   - CLIENT\_SECRET
   - CLIENT\_ID(API 키라고도 함)
   - 기술\_계정\_ID
   - IMS\_ORG

완료되면 환경 파일은 다음 이미지와 유사해야 합니다.

![CLIENT_SECRET, CLIENT_ID, TECHNICAL_ACCOUNT_ID 및 IMS_ORG 값을 업데이트한 후 환경 파일](assets/environment-file-with-developer-project-values.png "개발자 프로젝트 값이 있는 환경 파일")

### 다른 값 업데이트

업데이트해야 하는 다른 값은 `SANDBOX_NAME` 변수와 `TENANT_NAME` 변수뿐입니다.

- `SANDBOX_NAME` - Adobe Experience Platform에 실행할 샌드박스를 알려줍니다.
- `TENANT_NAME` - 특정 XDM 호출에서 테넌트 이름을 미리 채우는 데 사용됨

>[!NOTE]
>
>sandbox-assignment.pdf가 있는 라이브 교육 이벤트가 아닌 이러한 Labs를 독립적으로 진행하는 경우 Adobe Experience Platform UI URL에서 샌드박스에 로그인한 동안 두 값을 모두 찾습니다. 예:
>
>`https://experience.adobe.com/#/@dep/sname:prod/platform/home`
>
>- `SANDBOX_NAME`은(는) `sname:` 뒤의 값입니다. 이 예제에서는 `prod`
>- `TENANT_NAME`은(는) 밑줄이 붙은 `@` 기호 뒤의 값입니다. 이 예제에서는 `_dep`

1. 아래 나열된 변수에 대해 `current values`을(를) 업데이트합니다.
   - 샌드박스\_NAME
   - 테넌트\_NAME
1. 환경 작업 영역의 오른쪽 상단에 있는 `Save` 단추를 클릭하여 업데이트를 저장합니다.

작업을 마치면 환경 파일은 다음과 같이 표시됩니다.

![SANDBOX_NAME 및 TENANT_NAME 값을 업데이트한 후 환경 파일](assets/environment-file-with-sandbox-name-and-tenant-name.png "SANDBOX_NAME이 있는 환경 파일")

>[!SUCCESS]
>
>축하합니다! Postman 환경 구성을 완료했습니다
