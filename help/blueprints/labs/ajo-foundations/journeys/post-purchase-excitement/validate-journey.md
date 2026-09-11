---
hold: true
title: 여정 확인
description: 시작 및 종료 카운트, 이메일 게재 보고 및 단계 이벤트에 대한 서비스 데이터를 쿼리하여 여정 실행을 확인합니다.
doc-type: article
solution: Experience Platform
exl-id: 2e6e73e5-6bd8-4dde-ba06-29b67f927131
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---


# 여정 확인

## 학습 목표

여정이 예상대로 트리거되고 실행되었는지 확인합니다.  보고서에 예상대로 업데이트된 지표가 표시되는지 확인하십시오.

## 여정 확인 중

1. Order Shipped 여정으로 이동하여 닫았다면 엽니다.
2. 입력된 프로필이 2개 이상 있습니다.

![여정에 대해 표시된 프로필 입력 개수](assets/validate-journey-profile-entered-count.png)

3. 오른쪽 상단의 **보고서 보기** -> **최근 24시간**&#x200B;을 클릭합니다.
4. 기본적으로 왼쪽 레일의 **여정** 탭에 있습니다.
   - 일부 시작 및 종료가 표시됩니다(횟수는 전송된 이벤트 수, 테스트, 오류 등에 따라 달라집니다).

![시작 및 종료를 표시하는 여정 탭 보고](assets/validate-journey-journey-tab-enters-exits.png)

모든 항목이 정리된 경우 (아래로 스크롤하여 확인):

**여정 통계**

입력된 프로필 3개(Henry, You and the Testing we did)

원하는 경우 상단의 토글을 클릭하여 **테스트 이벤트를 제외**&#x200B;할 수 있으며, 이 수치는 변경됩니다

종료된 프로필 3개(Henry, 귀하와 당사가 수행한 테스트)

**실행된 액션 및 오류**

6가지 작업(이메일 3개, GetShippingDetails 3개)

**작업 오류 이유**

0 오류(잘만 함)

**이벤트**

3개 이벤트(orderShipped)

3개의 외부 이벤트

5. 왼쪽 레일에서 **전자 메일** 탭을 클릭합니다.
   - **이메일 - 전송 성능**
     - **배달됨** 및 **전송됨**&#x200B;에 대한 일부 값이 표시됩니다(개수는 보낸 이벤트 수, 오류 등에 따라 다릅니다).
     - 이전에 문제가 발생하지 않은 한 오류가 없기를 바랍니다.
   - **전자 메일 - 통계**
     - 이메일 - 타겟팅, 전송, 게재됨 3개

![전송 성능 및 통계를 표시하는 전자 메일 탭](assets/validate-journey-email-tab-sending-performance.png)

6. **전자 메일 받은 편지함**&#x200B;에서 전자 메일을 받았는지 확인하세요(아래와 비슷함).
   - *,*&#x200B;주문하신 제품은 ETA: *10/17/2026* 추적 번호: *051009364*

> [!NOTE]
>
>AJO 캠페인 [ajo-campaigns@email.dep-labs.com](mailto:ajo-campaigns@email.dep-labs.com)의 스팸 폴더를 확인하세요.

>[!NOTE]
>
>**이름이 누락된 이유는 무엇입니까?**
>
>이메일 주소에 대한 이벤트 컨텍스트를 살펴보기 위해 이메일 노드를 변경했습니다.  하지만 개인화의 이름은 \{\{profile.person.name.firstName\}\}에서 가져옵니다.
>
>이메일에 대한 프로필을 조회할 때 이름이 있습니까?



7. *30~60분 후*&#x200B;에는 다음과 같이 데이터 레이크에서 데이터 집합을 확인할 수도 있습니다. **쿼리** -> **쿼리 만들기** -> **SQL 복사/붙여넣기** -> **실행**

>[!NOTE]
>
>주문 배송 이벤트는에서 스트리밍되므로 프로필을 빠르게 업데이트하는 동안 데이터 레이크가 업데이트되기까지 시간이 소요됩니다.

```sql
SELECT * FROM dep_orders
WHERE timestamp >= CURRENT_DATE
LIMIT 10
```

![dep_orders 데이터 세트에 대한 쿼리 서비스 결과](assets/validate-journey-query-service-dataset-results.png)

## 보너스(단계 이벤트 확인)

>[!NOTE]
>
>단계 여정은 프로필이 여정을 시작할 때마다 이벤트의 모든 단계를 기록합니다. 참고: 이러한 이벤트를 데이터 세트에 기록하는 데 몇 분이 걸릴 수 있습니다.



1. 쿼리 서비스에서 이 SQL을 실행하여 단계 이벤트 데이터 세트가 캡처하고 있는 항목을 볼 수 있습니다. 아래 SQL을 복사하여 쿼리에 붙여넣습니다.

```sql
select timestamp,
  identityMap,
  _experience.journeyOrchestration.stepevents.journeyVersionName,
  _experience.journeyOrchestration.stepevents.NodeName,
  _experience.journeyOrchestration.stepevents.*
  from journey_step_events
limit 50
```

결과에 100개가 넘는 열이 있으며 단계 이벤트가 기록하는 내용을 알 수 있습니다.

>[!NOTE]
>
>각 필드의 의미에 대해 궁금한 점은 AJO 스키마 사전을 확인하고 드롭다운을 여정 단계 이벤트 스키마로 변경하십시오. [https://experienceleague.adobe.com/tools/ajo-schemas/schema-dictionary.html?lang=en](https://experienceleague.adobe.com/tools/ajo-schemas/schema-dictionary.html?lang=en)



## 요약

여정 인스턴스가 여정 보고 또는 로그에 나타나고 구성된 작업이 실행됩니다
