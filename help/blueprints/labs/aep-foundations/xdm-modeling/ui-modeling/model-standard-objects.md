---
hold: true
title: 모델 표준 개체
description: UI에서 개별 프로필 스키마를 만들고 인구 통계학적 세부 정보, 동의 및 환경 설정과 같은 표준 필드 그룹을 추가하고 트리밍합니다.
doc-type: article
solution: Experience Platform
exl-id: ea516c0b-3644-483c-a167-0264cc795449
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---


# 모델 표준 개체

## 스키마로 이동

1. 왼쪽 레일에서 **스키마** 탭을 클릭합니다

![왼쪽 레일 탐색의 스키마 탭](assets/model-standard-objects-schemas-tab-left-rail.png "왼쪽 레일을 사용하여 스키마로 이동")



1. 상단 탐색에는 기존 스키마를 찾아볼 수 있는 옵션과 현재 XDM 레지스트리에 있는 필드 그룹 및 데이터 유형을 볼 수 있는 옵션이 표시됩니다.

![스키마, 필드 그룹 및 데이터 형식을 검색할 수 있는 위쪽 탐색 옵션](assets/model-standard-objects-browse-schemas-top-nav.png "스키마 위쪽 탐색 옵션")

>[!NOTE]
>
>샌드박스에 미리 생성된 스키마가 이미 있습니다. 여기에는 이 부트캠프의 일부로 미리 만들어진 스키마(`dep` 접두사가 추가됨)와 Adobe Real-Time CDP 및 Adobe Journey Optimizer 모두에 대해 시스템에서 생성한 스키마가 포함됩니다.


## 개별 프로필 스키마 만들기

1. **스키마 만들기**&#x200B;를 클릭하여 시작

![스키마 만들기 단추](assets/model-standard-objects-create-schema-button.png "스키마 만들기")



1. **수동** 선택

![수동 스키마 만들기 옵션 선택](assets/model-standard-objects-select-manual-option.png "수동 선택")



1. **개별 프로필** 선택

![개별 프로필 클래스 선택](assets/model-standard-objects-select-individual-profile-class.png "개별 프로필 클래스 선택")


## 스키마 이름 지정

XDM 개별 프로필 클래스 기반 스키마를 사용하면 프로필에 결합할 개인에 대한 속성을 수집할 수 있습니다. 클래스 자체에는 *modifiedByBatchID*, *PersonID* 등과 같이 편집할 수 없는 필드가 포함되어 있습니다.

1. 스키마에 이름과 설명을 지정합니다.
   - **스키마 표시 이름** —> *고객 계정 - \[이니셜]*
   - **설명** —> 이 스키마는 개인의 ID, 플랜 정보, 인구 통계학적 세부 정보 및 연락처 세부 정보를 수집합니다.
1. 오른쪽 상단의 **완료** 단추를 사용하여 스키마를 저장합니다.

![스키마 이름 지정, 설명 추가, 저장](assets/model-standard-objects-name-schema-and-save.png "스키마 이름 지정, 설명 추가, 저장")

## 인구 통계 세부 정보 필드 그룹 추가

스키마에 추가하고 맞춤화할 수 있도록 Adobe Experience Platform에는 표준 XDM으로 존재하는 필드 그룹이 많습니다.

1. 필드 그룹 섹션의 왼쪽 레일에서 **+(추가)**&#x200B;을(를) 클릭합니다.

![왼쪽 레일에 필드 그룹 추가 단추](assets/model-standard-objects-add-field-group-button.png "필드 그룹 추가")



1. **인구 통계 세부 정보**&#x200B;를 검색하거나 목록을 검색하여 찾으십시오.

- 필드 그룹을 찾으면 필드 그룹의 오른쪽에 있는 돋보기를 클릭하여 해당 구조를 확인합니다.  이 방법은 스키마를 실제로 추가하지 않고 추가하려는 항목을 미리 보는 데 유용합니다.
- 검토를 마치면 미리보기를 닫습니다.



![돋보기를 클릭하여 필드 그룹의 구조를 미리 봅니다](assets/model-standard-objects-click-magnify-glass-to-preview-field-group-structure.png "돋보기를 클릭하여 필드 그룹의 구조를 미리 봅니다")

![인구 통계 세부 정보 필드 그룹 구조 미리 보기](assets/model-standard-objects-demographic-details-structure-preview.png)



&#x200B;3. 필드 그룹 옆의 확인란을 **확인**&#x200B;한 다음 **필드 그룹 추가** 단추를 클릭합니다.

![인구 통계학적 세부 정보 필드 그룹을 선택하여 스키마에 추가](assets/model-standard-objects-select-demographic-details-field-group.png "인구 통계학적 세부 정보 필드 그룹을 선택하여 스키마에 추가")


## 다른 표준 필드 그룹 추가

스키마에 추가 표준 필드 그룹을 추가해야 합니다. 이전 단계를 반복하여 스키마에 두 개의 추가 필드 그룹을 추가합니다.

- 개인 연락처 세부 정보
- 동의 및 환경 설정 세부 정보

완료되면 스키마가 완료 시 아래 이미지와 같아야 합니다. **저장** 단추를 클릭하고 작업을 저장하십시오!

![인구 통계학적 세부 정보, 개인 연락처 세부 정보, 동의 및 환경 설정 세부 정보 필드 그룹을 추가한 후의 스키마](assets/model-standard-objects-final-schema-after-adding-field-groups.png "저장한 후의 최종 스키마 ")

>[!NOTE]
>
>선택하고 추가한 필드 그룹이 이제 스키마에 나타나고 왼쪽 레일에 표시됩니다. 추가한 각 필드 그룹의 모든 필드가 반드시 필요한 것은 아닙니다.  다음 단계에서는 관련 없는 필드를 제거합니다.

>[!WARNING]
>
>계속하기 전에 스키마를 저장하십시오!


## 표준 필드 그룹 사용자 정의

### 인구 통계 세부 정보 필드 그룹

인구 통계 세부 정보 필드 그룹은 많은 필드를 가져오지만, LID 방법론의 스키마 디자인을 기반으로 다음 필드만 있으면 됩니다.

- person.name.firstName
- person.name.lastName
- person.birthdayAndMonth
- person.birthYear

Adobe 표준 필드 그룹에서 필드를 제거하려면 **관련 필드 관리** 옵션을 사용할 수 있습니다. 관련 필드 관리를 사용하면 스키마에서 표준 필드를 제거할 수 있으므로 필요한 필드만 남습니다.

1. 스키마에서 **person** 개체 선택
1. 오른쪽 레일에서 **관련 필드 관리**&#x200B;를 클릭합니다.

![인구 통계 세부 정보 필드 그룹의 사용자 개체에 대한 관련 필드 관리 옵션](assets/model-standard-objects-manage-related-fields-person-object.png "인구 통계 세부 정보 필드 그룹의 일부로 사용자 개체에 대한 관련 필드 관리")



1. 사용자 왼쪽에 있는 V자형 화살표를 클릭하여 사용자 객체를 확장하고 이름 객체 왼쪽에 있는 V자형 화살표를 클릭하여 전체 이름 객체를 확장합니다. 다음 필드만 유지:

- person.name.firstName
- person.name.lastName
- person.birthdayAndMonth
- person.birthYear

완료되면 오른쪽 상단의 **확인** 단추를 클릭합니다.

![선택한 인구 통계 세부 정보 사용자 필드를 표시하는 관련 필드 관리 대화 상자](assets/model-standard-objects-demographic-details-person-fields-dialog.png "인구 통계 세부 정보 사용자 개체의 관련 필드 관리")

>[!NOTE]
>
>**인구 통계학적 세부 정보**&#x200B;의 맨 위 확인란을 클릭하여 모든 하위 개체를 자동으로 선택 취소한 다음 필요한 개체만 다시 선택할 수 있습니다.



1. 완료되면 아래와 같이 스키마에 개인 오브젝트가 표시됩니다. 모든 항목이 정상인 경우 **저장** 단추를 클릭하여 스키마를 저장합니다.

![필수 필드만 있는 최종 인구 통계 세부 정보 사용자 개체](assets/model-standard-objects-final-demographic-details-person-object.png "필수 필드만 있는 최종 인구 통계 세부 정보 필드 그룹")

### 동의 및 환경 설정 필드 그룹

이전과 동일한 단계를 수행하지만 이번에는 동의 및 환경 설정 필드 그룹에 대해 수행합니다.

1. 왼쪽 레일에서 **동의 및 환경 설정** 필드 그룹 이름을 클릭하여 스키마에서 해당 필드를 강조 표시합니다.
1. **동의** 개체를 선택한 다음 **관련 필드 관리** 프로세스를 사용하여 동의 개체에서 필요하지 않은 필드를 제거합니다. 다음 필드만 유지:

- consents.marketing.email.val
- consents.marketing.sms.val

>[!NOTE]
>
>스키마 작업 영역의 오른쪽 위 모서리에 있는 **필드에 대한 표시 이름 표시**&#x200B;에 대한 토글이 해제되어 있는지 확인하십시오
>
>![필드 표시 이름 표시 토글 해제](assets/model-standard-objects-show-display-names-toggle-off.png)



완료되면 이제 최종 스키마가 다음과 같이 표시됩니다.  계속하기 전에 **저장**&#x200B;을 클릭하세요.

![동의 및 환경 설정 필드 그룹의 관련 필드 관리 후 스키마](assets/model-standard-objects-final-consent-and-preferences-fields.png "동의 및 환경 설정 필드 그룹의 관련 필드 관리")

>[!TIP]
>
>이제 스키마에 표준 구성 요소를 추가했습니다. 좋습니다! 계속해서 스키마에 대한 일부 사용자 지정 속성을 빌드합니다.
