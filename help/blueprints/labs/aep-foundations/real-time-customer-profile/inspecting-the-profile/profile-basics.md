---
hold: true
title: 프로필 기본 사항
description: 프로필 결합 스키마를 탐색하고 UI에서 프로필을 조회하고 해당 속성, ID 맵 및 ID 그래프 관계를 검사합니다.
doc-type: article
solution: Experience Platform
exl-id: 5be38b40-47ef-42ce-8829-39fa09394716
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---


# 프로필 기본 사항

## 프로필 유니온 스키마

실시간 고객 프로필 보기는 프로필에 대해 정의하고 활성화한 스키마를 사용하여 작성됩니다. Adobe이 프로필의 유니온 스키마라고 하는 것입니다.

다음을 수행하여 프로필의 유니온 스키마를 볼 수 있습니다.

1. 왼쪽 레일에서 **프로필** 클릭
1. 위쪽 탐색에서 **유니온 스키마**&#x200B;를 클릭합니다.

![프로필 상단 탐색 아래의 유니온 스키마 보기](assets/profile-basics-profile-union-view.png "프로필 유니온 보기")

>[!NOTE]
>
>프로필은 모든 XDM 클래스에 대한 유니온 보기를 만듭니다. 이 보기를 활용하여 어떤 스키마가 어떤 클래스에 기여했는지, 각 클래스 내의 ID 및 모든 관계를 확인할 수 있습니다.

XDM 개별 프로필 클래스에 대한 유니온 스키마를 검토하고 테넌트 네임스페이스를 확장합니다. **LID 방법론** 및 **XDM 모델링 Labs**&#x200B;에서 정의한 다양한 스키마에서 가져온 많은 항목이 여기에 표시됩니다.

![테넌트 네임스페이스 필드를 표시하도록 확장된 XDM 개별 프로필 클래스의 유니온 스키마 보기](assets/profile-basics-union-schema-tenant-namespace-objects.png "테넌트 개체의 프로필 유니온 스키마 보기 ")

**account** 개체를 클릭하고 화면의 오른쪽 레일에 표시되는 내용을 확인합니다. 이제 오브젝트, 해당 형성에 기여한 스키마 및 데이터 세트, 기타 관련 정보에 대한 세부 정보를 볼 수 있습니다.

![기여 스키마 및 데이터 세트를 표시하는 계정 개체에 대한 올바른 레일 세부 정보](assets/profile-basics-union-schema-account-object-details.png "프로필 통합 스키마 계정 개체 세부 정보")

>[!NOTE]
>
>유니온 스키마는 프로필 내에 특정 요소가 존재하는 이유와 그 출처를 이해하는 데 유용한 도구입니다.
>
>유니온 스키마는 관찰 가능하다는 점을 기억하십시오. 즉, 프로필은 실제 실시간 고객 프로필을 볼 때 데이터가 포함된 필드만 표시합니다


## 프로필 조회

1. 왼쪽 레일에서 **프로필**&#x200B;을 클릭한 다음 위쪽 탐색에서 **찾아보기**&#x200B;를 선택합니다.
1. **전자 메일**&#x200B;의 ID 네임스페이스 선택
1. **depeche.mode\@dep.com**&#x200B;의 ID 값을 입력하십시오.
1. **보기** 단추를 클릭하여 프로필을 조회합니다.
1. 프로필의 세부 정보를 보려면 프로필에 대한 **링크**&#x200B;를 클릭하십시오.

![이메일 네임스페이스와 depeche.mode@dep.com이 입력된 프로필 뷰어 찾아보기 탭](assets/profile-basics-profile-viewer-browse-tab.png "프로필 뷰어(찾아보기)")



이제 이걸 봐야해!

![전자 메일로 조회 후 장치 모드 프로필 세부 정보 페이지](assets/profile-basics-depeche-mode-profile-details.png "장치 모드 프로필 세부 정보 페이지")

위쪽 탐색에서 각 탭을 보면 디페시 모드(Depeche Mode)라는 프로필을 탐색할 수 있습니다. 사용할 탭은 다음과 같습니다.

- 세부 사항 - 지정된 프로필에 대해 다양한 측면을 보여 주는 사용자 지정된 카드를 표시합니다.
- 속성 - 유니온 스키마에서 나오는 지정된 프로필의 연관된 모든 속성을 표시합니다.
- 이벤트 - 유니온 스키마에서 오는 해당 프로필에 대한 관련 이벤트를 모두 표시합니다.
- 대상자 멤버십 - 프로필이 현재 멤버인 대상자를 표시합니다.

## 속성 보기

**특성** 탭으로 이동하여 **JSON 보기**&#x200B;를 클릭합니다.

![특성 탭에 JSON으로 표시되는 장치 모드 프로필 특성](assets/profile-basics-depeche-mode-attributes-json.png "장치 모드 특성")

고객 계정 스키마에 추가한 필드 그룹에서 가져온 필드가 표시되는 방식을 확인합니다.

- 제목이 **entity**&#x200B;인 상위 노드 찾기
- 하위 개체 **billingAddress**&#x200B;을(를) 확인합니다(개인 연락처 정보 필드 그룹에서 가져옴)

```json
"billingAddress": {
  "postalCode": "11355",
  "city": "New York City",
  "state": "NY",
  "street1": "108 Ruskin Terrace"
}
```

프로필 통합 스키마의 기능과 비교하여 관측 가능한 의미: 😄을(를) 파악해야 합니다.

```json
"billingAddress": {
    "_repo": {
        "createDate": "datetime",
        "modifyDate": "datetime",
    },
    "_schema": {
        "description": "string",
        "elevation": "double",
        "latitude": "double",
        "longitude": "double"
    },
    "_id": "string",
    "city": "string",
    "country": "string",
    "countryCode": "string",
    "createdByBatchID": "string",
    "dmaID": "integer",
    "label": "string",
    "lastVerifiedDate": "date",
    "modifiedByBatchID": "string",
    "msaID": "string",
    "postOfficeBox": "string",
    "postalCode": "string",
    "primary": "boolean"
    "region": "string",
    "repositoryCreatedBy": "string",
    "repositoryLastModifiedBy": "string",
    "state": "string",
    "stateProvince": "string",
    "status": "string",
    "statusReason": "string"
    "street1": "string",
    "street2": "string",
    "street3": "string",
    "street4": "string"
}
```

>[!NOTE]
>
>관찰 가능한 스키마는 말 그대로 데이터가 있는 필드만 표시하고 데이터가 없는 필드는 숨기는 것을 의미합니다.  기존의 관계형 데이터베이스와 매우 다릅니다!



다음 번에 **동의** 개체(동의 및 환경 설정 세부 정보 필드 그룹에서 가져옴)를 찾습니다

```json
"consents":{
   "marketing":{
      "sms":{
         "val":"y"
      },
      "email":{
         "val":"y"
      }
   }
}
```



테넌트 네임스페이스 **\_devbc**(으)로 스크롤하여 **plan** 개체를 찾습니다(이 개체는 &#39;dep: 계획 세부 정보&#39;라는 사용자 지정 생성 필드 그룹에서 가져옴).

```json
"plan": {
    "planID": "m3",
    "type": "mobile",
    "name": "pro"
}
```



업셀 사용 사례에 대해 정의한 **집계** 개체를 확인합니다. 이러한 필드는 테넌트 네임스페이스 \_devbc 아래에 있습니다. 다른 스키마(dep: 고객 집계) 및 사용자 정의 필드 그룹(dep: 집계)에서 가져왔습니다

```json
"aggregates":{
   "rollingSixMonthAvgMonthlyDataUsage":30,
   "rollingSixMonthTotalDataUsage":200
}
```

## ID 맵 보기

또한 프로필의 연결된 ID가 **identityMap.**&#x200B;이라는 맵 기반 개체 내에 저장되어 있을 때 해당 ID를 볼 수 있습니다. JSON 문서 아래쪽에서 **identityMap**&#x200B;을(를) 찾습니다.

이것은 identityMap 필드를 사용했는지 또는 ID 설명자를 사용하여 필드를 표시했는지에 관계없이 전달된 모든 ID를 나타냅니다.

```json
"identityMap": {
  "ecid": [{
          "id": "34537751351243145301122536487445728054"
      },
      {
          "id": "66385443304271800137026604878870723316"
      },
      {
          "id": "34537751351243145301122536483456723542"
      }
  ],
  "email": [{
          "id": "dave.gahan@dep.com"
      },
      {
          "id": "depeche.mode@dep.com"
      }
  ],
  "customerid": [{
      "id": "266242885"
  }],
  "gaid": [{
          "id": "266242-9013"
      },
      {
          "id": "266242-9012"
      }
  ]
}
```

>[!NOTE]
>
>identityMap에는 &quot;기본 ID&quot; 개념에 대한 참조가 없습니다. 이유는 두 가지입니다.
>
>1. 프로필 속성에 표시되는 identityMap은 Identity 서비스의 그래프를 사용하는 각 프로필에 대해 작성됩니다\*
>2. ID 그래프는 ID 간의 관계만 고려합니다. 각 ID는 동일하게 처리됩니다. A는 B와 관련이 있으며 기본 ID, 개인 ID 등을 통해 수행되었는지는 중요하지 않습니다.
>
>*\* ID 그래프를 사용하지 않으면 identityMap은 조회에서 요청한 ID로만 구성됩니다*

>[!NOTE]
>
>고객 계정 스키마를 빌드했을 때 ID(즉, personalEmail.address)로 표시된 이메일 필드는 하나만 있었습니다. identityMap에 두 개의 이메일 주소가 있는 것을 보셨습니까?
>
>무슨 일입니까?
>
>- Identity Graph는 데이터가 해당 서비스에 유입될 때 새로운 관계와 해당 관계 내의 값을 지속적으로 기록합니다
>- 프로필의 동작은 데이터가 해당 서비스에 수집될 때 기존 필드 값을 새 값으로 덮어쓰는 것입니다
>- ID 설명자가 있는 필드에 플래그를 지정할 때 해당 필드는 여전히 프로필용 필드입니다



## ID 그래프

위쪽 탐색의 **세부 정보** 탭으로 돌아가서 **연결된 ID** 카드 하단에 있는 **ID 그래프 보기** 링크를 클릭합니다

![세부 정보 탭의 연결된 ID 카드 하단에 있는 ID 그래프 링크 보기](assets/profile-basics-view-identity-graph-link.png "ID 그래프 보기")

이제 이 화면이 표시됩니다.

![Depeche 모드 프로필에 대한 ID 그래프 시각화 도우미, 세부 정보 및 선택한 ID 패널](assets/profile-basics-identity-graph-view-of-depeche-mode.png "Depeche 모드 프로필의 ID 그래프 보기")

위의 보기는 디바이스 모드 프로필의 ID 그래프이며 3개의 주요 영역으로 분류됩니다.

**ID 그래프 시각화 도우미** - 프로필 ID 클러스터 내의 ID 및 연결된 관계를 표시합니다.

**ID 그래프 세부 정보** - ID 그래프 시각화 도우미에 표시되는 모든 관계를 만든 전체 ID 그래프 네임스페이스, 값 및 데이터 소스에 대한 특정 세부 정보를 제공합니다.

**선택한 ID 세부 정보** - 선택한 ID에 대한 자세한 정보를 해당 ID가 관계에서 처리된 마지막 5개의 일괄 처리와 함께 표시합니다.

>[!NOTE]
>
>ID 그래프 뷰어에는 모든 ID 간의 관계와 ID 관계가 마지막으로 조회된 시간과 데이터 세트의 정보가 모두 표시됩니다



customerID ID를 대신 사용하여 디바이스 모드의 ID 그래프를 봅니다.  다음 작업을 수행합니다.

1. **customerID**&#x200B;을(를) 복사하여 어딘가에 저장합니다.
1. ID 네임스페이스 상자의 네임스페이스 값을 **customerID**(으)로 변경합니다.
1. 이전 단계에서 저장한 **customerID** 값에 붙여넣습니다.
1. 새 ID 값을 사용하여 이 ID가 포함된 ID 그래프를 보려면 **보기** 단추를 클릭하십시오.

![전자 메일 대신 customerID로 검색한 후 동일한 그래프를 표시하는 ID 그래프 보기](assets/profile-basics-identity-graph-view-via-customerid.png "customerID를 통한 ID 그래프 보기")

>[!NOTE]
>
>정확히 동일한 ID 그래프가 어떻게 표시되는지 확인하십시오. 이 그래프에서 사용하는 모든 ID는 항상 동일한 결과를 가져옵니다.



## ID 변경

이제 프로필 뷰어로 돌아가 customerID를 사용하여 차원 모드를 조회합니다.

1. ID 네임스페이스를 **customerID**(으)로 변경
1. 마지막 섹션에서 저장한 customerID 값을 사용하여 ID 값을 업데이트합니다
1. **보기** 단추 클릭

![depeche 모드를 조회하기 위해 customerID 네임스페이스와 값이 입력된 프로필 뷰어](assets/profile-basics-lookup-depeche-mode-using-customerid.png "customerID를 사용하여 depeche 모드 조회")



이전에 본 프로필과 동일한 프로필이 표시됩니다!

![이전 전자 메일 조회와 일치하는 customerID별로 조회 후 장치 모드 프로필 세부 정보 페이지](assets/profile-basics-depeche-mode-profile-details-via-customerid.png "장치 모드 프로필 세부 정보 페이지")

>[!NOTE]
>
>ID 그래프를 사용하면 다양한 프로필 조각을 어셈블할 때 사용하는 ID가 동일한 프로필에서 결과를 얻을 수 있습니다
