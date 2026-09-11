---
hold: true
title: 스트리밍 대상 설정
description: Webhook 끝점, 거버넌스 정책, 대상 및 필드 매핑을 사용하여 HTTP API 스트리밍 대상을 구성하여 세그먼트 활성화를 테스트합니다.
doc-type: article
solution: Experience Platform
exl-id: c52d301f-b308-40fc-a59c-ace1c96ccd13
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# 스트리밍 대상 설정

>[!NOTE]
>
>스트리밍 대상을 이미 구성한 경우 다음 단계로 건너뜁니다.

## Webhook URL 가져오기

>[!NOTE]
>
>우리는 데이터를 보낼 목적지에 도착했는지 확인할 수 있도록 여기에 웹후크를 사용할 것입니다. 실제 시나리오에서는 대신 해당 대상에 로그인하고 해당 도구를 사용하여 무엇이 도착했는지 확인합니다.

1. 브라우저의 새 탭에서 다음 링크를 엽니다. -> [https://webhook.site](https://webhook.site/)
1. 표시되는 고유 URL을 복사하여 안전한 곳에 저장하십시오.

![Webhook.site는 고유 URL을 복사합니다](assets/setup-streaming-destination-webhooksite-copy-your-unique-url.png "Webhook.site는 고유 URL을 복사합니다")


## HTTP API 대상 구성

>[!NOTE]
>
>이 데이터를 타사(예: Facebook)에 전송하는 프록시로 스트리밍 대상을 사용하고 있습니다. 실제 시나리오에서는 HTTP API 대상 대신 Facebook 대상을 사용하여 데이터를 Facebook으로 보냅니다.

Experience Platform UI에서 다음을 수행하여 대상 카탈로그로 이동합니다

1. 왼쪽 레일에서 **대상** 클릭
1. 상단 레일에서 **카탈로그** 클릭
1. 검색 상자에 **http**&#x200B;을(를) 입력하십시오.
1. HTTP API 대상을 구성하려면 **설정** 단추를 클릭하십시오.

![HTTP API 대상으로 이동하여 설치를 시작합니다](assets/setup-streaming-destination-navigate-to-http-api-destination.png "HTTP API 대상으로 이동하여 설치를 시작합니다")

>[!NOTE]
>
>실습용 HTTP API 스트리밍 대상을 사용하여 실제 스트리밍 커넥터의 작동 방식을 보여 줍니다.

## 구성

1. 연결 유형 **없음**
1. **대상에 연결**&#x200B;을 클릭합니다.

![대상에 연결](assets/setup-streaming-destination-connect-to-destination.png "대상에 연결")

>[!NOTE]
>
>일반적으로 이 단계에서는 모든 인증 자격 증명을 추가하지만 이 웹후크에는 필요하지 않습니다.



&#x200B;3. 다음과 같이 대상의 구성 세부 정보를 입력합니다.

- **이름** -> `Streaming DEP Webhook - [Your Initials]`
- **설명** -> `[your webhook endpoint you copied above]`
- **끝점** -> ` [your webhook endpoint you copied above]`
- **쿼리 매개 변수** -> `leave blank`
- **머리글** -> `leave blank`
- 세그먼트 이름 포함 -> 켜기/끄기
- 세그먼트 타임스탬프 포함 -> 켜기/끄기

완료되면 구성이 아래에 표시되는 항목과 일치하는지 확인합니다.  제대로 표시되었으면 오른쪽 상단의 **다음** 단추를 클릭하여 다음 단계를 계속합니다

![이름, 설명, 끝점 및 전환을 포함한 대상 필드 구성](assets/setup-streaming-destination-configure-destination-fields.png)

>[!CAUTION]
>
>저장한 후에는 UI에서 끝점, 헤더 및 쿼리 매개 변수를 변경할 수 없습니다

## 거버넌스 정의

1. 마케팅 작업에서 **사이트 간 타깃팅**&#x200B;을(를) 선택합니다.
1. 완료되면 **다음** 단추를 클릭하여 다음 단계로 진행합니다.

![대상의 거버넌스 화면](assets/setup-streaming-destination-governance-screen-for-destinations.png "대상의 거버넌스 화면")

>[!NOTE]
>
>Experience League의 거버넌스 정책에 대해 자세히 알아볼 수 있습니다
>
>[https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=ko#core-actions](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=ko#core-actions)

## 대상자 선택

1. 모든 대상 선택
1. 완료되면 **다음** 단추를 클릭하여 다음 단계로 진행합니다.

![모든 대상 선택](assets/setup-streaming-destination-select-all-audiences.png)

## 매핑 추가

>[!NOTE]
>
>여기에서는 프로필에서 필드를 추가합니다. 해당 필드에 데이터가 없으면 대상에 아무 것도 전달되지 않을 수 있습니다. 프로필 및 이벤트 간 시간에 따른 여러 업데이트로 인해 대상이 여러 번 트리거되고 여러 페이로드가 전송될 수 있습니다.

1. 스키마에 필드를 추가하려면 **새 필드 추가**&#x200B;를 클릭하십시오.
1. 스키마 필드 입력 상자에 **model**&#x200B;을(를) 입력하고 표시되는 필드 목록에서 **\_dep.activeProducts\[0].model** 필드를 선택합니다
1. 필드 이름에서 **\[0]**&#x200B;을(를) **\[\*]**(으)로 변경합니다.  이제 마지막 필드가 **\_dep.activeProducts\[\*].model**(으)로 표시됩니다.
1. 완료되면 **다음** 단추를 클릭하여 다음 단계로 진행합니다.



![모델 필드 선택](assets/setup-streaming-destination-select-model-field.png "모델 필드 선택")



![최종 모델 필드](assets/setup-streaming-destination-final-model-field.png "최종 모델 필드")

>[!NOTE]
>
>이는 경험 이벤트가 아닌 프로필에 필드를 매핑하는 것입니다. 대상 자격에 따라 프로필을 대상으로 보내는 경우에도 발생하는 상황을 염두에 두어야 합니다.
>
>1. 이벤트 발생
>2. 대상자가 규칙에 따라 프로필을 정규화합니다.
>3. 자격 증명이 프로필에 저장됩니다.
>4. 프로필이 자격이 있다는 알림이 대상에 전송됩니다.
>5. 대상에서 프로필을 보냅니다. 즉, 대상이 프로필을 보내면 대상 평가를 트리거한 이벤트에 대한 인식이 더 이상 없습니다.

## 검토 단계

최종 대상의 유효성을 검사한 다음 **마침** 단추를 클릭하십시오.

![대상 검토 화면](assets/setup-streaming-destination-destination-review-screen.png "대상 검토 화면")

>[!NOTE]
>
>이제 대상이 구성되며 평가 속도에 따라 추가된 모든 세그먼트의 세그먼트 자격을 기다립니다.
>
>- Edge
>- 스트림
>- 일괄 처리

>[!NOTE]
>
>처음 대상을 설정할 때는 다음 사항을 기억해야 합니다.
>
>- 채우기(기존 적격 프로필)가 활성화를 시작하는 데 최대 2시간이 소요됩니다
>- 새로 추가된 대상이 활성화를 시작하는 데 최대 20분이 소요됩니다
