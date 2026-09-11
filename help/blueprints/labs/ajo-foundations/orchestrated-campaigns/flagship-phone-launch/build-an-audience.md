---
hold: true
title: 대상자 작성
description: 오케스트레이션된 캠페인에서 대상 작성 활동을 사용하여 관계형 스키마 조건을 사용하여 특정 전화기로 활성 고객 라인을 타깃팅하는 방법에 대해 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: 697d3edb-2b63-4038-a934-3587495e17f7
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# 대상자 작성

## 목표

다음 몇 단계에서는 캠페인에 타깃팅할 대상을 만듭니다. 이 대상은 출시되는 플래그십 휴대폰과 일치하는 메이크를 가진 모든 활성 회선 보유자입니다.  목표는 휴대폰을 업그레이드하도록 힌트를 주는 SMS 메시지로 타깃팅하려는 그룹입니다.



## 대상 작성 활동 추가

1. 캔버스에서 **+ 기호**&#x200B;을(를) 클릭한 다음 **대상자 작성** 활동을 선택하여 워크플로우에 추가합니다

![워크플로 캔버스에 대상 만들기 활동 추가](assets/build-an-audience-add-activity.png)



&#x200B;2. 오른쪽 레일에 빌드 대상 속성이 표시됩니다. 레이블을 업데이트하여 다음을 지정하십시오. `Active Lines with Apple`

![대상 레이블을 Apple의 활성 줄로 설정](assets/build-an-audience-set-label.png)


## 타겟팅 차원 선택

다음 단계는 **타겟팅 차원**(즉, 쿼리할 테이블)을 선택하는 것입니다. 다음 단계를 수행합니다.

1. 타깃팅 차원 상자에서 **검색 아이콘**&#x200B;을 클릭합니다

![타깃팅 차원 상자의 검색 아이콘](assets/build-an-audience-search-targeting-dimension.png)

&#x200B;2. 팝업에서 이름이 **dep-rel: Customer Line**&#x200B;인 테이블을 검색하여 선택한 다음 **확인** 단추를 클릭합니다.

![dep-rel: Customer Line 테이블을 선택하고 확인을 클릭합니다](assets/build-an-audience-select-customer-line-table.png)

>[!NOTE]
>
>만든 각 대상의 **타깃팅 차원**&#x200B;을(를) 항상 기억하십시오. 다음 단계에서 그 중요성에 대해 알아봅니다.

>[!NOTE]
>
>Adobe에서 만든 스키마를 선택하면 스키마가 -> *(caas)*(으)로 시작하는 것을 확인합니다. 이는 관계형 저장소 내의 테이블에 적용되는 네임스페이스일 뿐이며 Campaign as a Service 의 약자입니다.



## 대상자 만들기

타겟팅 차원(쿼리할 관계형 스키마)을 선택했으므로 이제 정의 생성을 시작할 수 있습니다.

1. 오른쪽 레일에서 **대상 만들기** 단추를 클릭합니다.

![오른쪽 레일에서 대상 만들기 단추](assets/build-an-audience-click-create-audience.png)

&#x200B;2. **조건 추가** 단추를 클릭합니다.

![대상 정의에 대한 조건 추가 단추](assets/build-an-audience-click-add-condition.png)



## 조건 만들기

스키마에 있는 속성을 사용하여 대상자 논리를 작성할 시간입니다. 목표는 활성 상태이고 Apple을 사용하는 모든 고객 라인을 찾는 것입니다.

### 조건 #1 만들기

1. 다음 정보를 사용하여 조건을 설정합니다.
   - **특성**: `Active Line`
   - **값**: `true`

![조건 1이 true와 같은 활성 줄로 설정됨](assets/build-an-audience-condition-active-line-true.png)

&#x200B;2. **새로 고침** 아이콘을 클릭하여 조건에 대한 적격 수를 확인합니다.

![새로 고침 아이콘으로 조건 1](assets/build-an-audience-condition-1-refresh-count.png)에 대해 241개의 올바른 수를 표시합니다.

>[!TIP]
>
>조건을 올바르게 빌드하면 241의 결과가 표시됩니다



### 조건 #2 만들기

1. **조건 추가** 단추를 클릭하고 **>** 아이콘을 클릭하여 **dep-rel:** **제품 \[조회]** 스키마를 선택합니다

![dep-rel: > 아이콘을 클릭하여 제품 [조회] 스키마를 선택합니다](assets/build-an-audience-select-product-lookup-schema.png)


&#x200B;2. 이름이 **만들기**&#x200B;인 필드를 찾은 다음 세 점을 클릭하고 **값 분포**&#x200B;를 선택합니다.

![만들기 필드에 대한 값 배포 옵션](assets/build-an-audience-make-distribution-of-values.png)



&#x200B;3. 다양한 값을 확인합니다. `Apple`만 필요하며 100개의 다른 철자가 없습니다. **Apple 필드**&#x200B;를 클릭하여 선택한 다음 오른쪽 상단의 **특성 및 값 선택 단추**&#x200B;를 클릭합니다.

![특성 및 값 선택 단추로 선택한 Apple 값](assets/build-an-audience-select-apple-attribute-value.png)

>[!NOTE]
>
>이는 데이터 설계자가 열거형으로 스키마를 디자인해야 하는 주요 예입니다.  이렇게 하면 마케터가 값을 수동으로 선택/입력할 필요가 없습니다.  데이터 설계자를 부끄럽게 생각합니다!



&#x200B;4. 아래 표시된 조건과 함께 `Make` 필드가 자동으로 추가됩니다.
   - **연산자:** `Equal to`
   - **값:** `Apple`
   - **대/소문자 구분:** `Enabled`

&#x200B;5. **계산 아이콘**&#x200B;을 클릭하면 85가 표시됩니다.

![조건 2 계산된 개수 85](assets/build-an-audience-condition-2-final-count.png)

>[!NOTE]
>
>그룹에서 AND 연산자를 사용할 때 주의하십시오. 표시된 것처럼 단일 그룹이든 여러 그룹이든 AND는 오케스트레이션된 캠페인에 알려주기 때문에 중요합니다. 두 조건은 모두 true여야 합니다.



## 카운트 확인

1. 대상 크기를 정확히 예측하려면 대상 프로필 제목 아래의 오른쪽 레일에 있는 **계산 아이콘**&#x200B;을 클릭하십시오. **65**&#x200B;이(가) **최종 개수**(으)로 표시됩니다.

![65의 최종 대상 크기를 표시하는 계산 아이콘](assets/build-an-audience-calculate-final-audience-size.png)

>[!NOTE]
>
>각 개별 조건이 어떻게 다른 숫자(조건 #1 —> 241 및 조건 #2 —> 85)를 반환했지만 최종 대상자 크기는 두 조건 중 더 작았는지 확인합니다.  이는 해당 AND 연산자 때문입니다.



&#x200B;2. **65**&#x200B;의 최종 수가 표시되면 화면 오른쪽 상단의 **확인** 단추를 클릭한 다음 오른쪽 상단의 **저장** 단추를 클릭하여 작업을 저장합니다.



## 과제

`Make`이(가) `apple`(소문자)와 같도록 마지막 조건을 입력한 후 `Case sensitive`에 대한 구성 옵션을 그대로 두고 `on`을(를) 전환했다고 가정합니다.  그러면 조건 레코드 수가 0이 됩니다.  그래서 당신은 241개의 활성 라인과 0의 메이크가 사과인 곳을 갖게 될 것이다.



**이 경우 최종 대상자 크기는 얼마입니까?**

![레코드 수가 0인 마지막 조건 &quot;마지막 조건이 0임&quot;](assets/build-an-audience-challenge-zero-count-condition.png "마지막 조건이 0")임

## 답변

0이야. 왜 그런지 알아?

![최종 개수가 0인 이유에 대한 설명](assets/build-an-audience-answer-zero-count-explanation.png)



## 요약

첫 번째 대상을 성공적으로 만들었으므로 이제 대상 작성 활동 내에서 카운트를 개발하고 확인하는 것이 얼마나 쉬운지 확인할 수 있습니다.

![다시 요약 후 대상자 작성 활동을 완료했습니다](assets/build-an-audience-recap-completed-audience.png)
