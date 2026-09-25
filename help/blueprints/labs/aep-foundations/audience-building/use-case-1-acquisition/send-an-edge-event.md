---
title: Edge 이벤트 보내기
description: Postman을 통해 인증되지 않은 웹 이벤트를 Edge으로 보내고, 이벤트 전달, 프로필 수집, 대상 자격 조건 및 대상 활성화를 통해 추적합니다.
doc-type: article
solution: Experience Platform
exl-id: 465d09da-e30f-404c-8778-5df06e5a199f
source-git-commit: 96308d5726def849ef22540a5d13618017c40cc3
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%
---

# Edge 이벤트 보내기

모든 것이 구성되었으므로 이벤트를 Edge에 보내어 모든 것이 작동하는지 확인하십시오. 이렇게 하려면 Postman을 사용하여 웹 이벤트를 만든 데이터 스트림으로 보냅니다. 웹에서 Edge으로 들어오는 페이지 보기를 시뮬레이션하도록 **OAuth 토큰 없이** 이벤트를 보냅니다.  이 실습을 수행하려면 컴퓨터에서 Postman이 열려 있어야 합니다.

>[!NOTE]
>
>인증된 토큰을 전달하지 않으므로 속성을 다시 가져올 수 없습니다.

## 랩 기대

1. Edge을 히트할 경험 이벤트
1. 이벤트 전달 서비스를 사용하기 위한 데이터 스트림 구성
1. 이벤트를 웹후크로 보내기 위한 이벤트 전달
1. AEP 서비스를 사용하기 위한 데이터 스트림 구성
   1. 실행할 Edge 대상
   2. 허브에 이벤트 보내기
1. Edge 대상을 포함하는 Postman 응답(하지만 속성은 없음)
1. 이벤트를 받고 이벤트 프로필 조각을 추가할 프로필 스토어
1. 관계를 추가할 ID 저장소
1. 데이터를 받고 데이터 레이크에 저장할 데이터 세트
1. 허브에서 프로필에 결과를 평가하고 저장하는 스트리밍 대상
1. 스트리밍 대상 &quot;항목&quot;을 다시 Edge으로 전송하기 위한 사용자 지정 Personalization 대상
1. Webhook으로 스트리밍 대상 &quot;항목&quot;을 전송하기 위한 HTTP API 대상
1. 스트리밍 대상 &quot;종료&quot;를 Webhook에 전송하기 위한 HTTP API 대상입니다.
1. 결국 사용자 지정 Personalization 대상을 통해 스트리밍 대상 &quot;종료&quot;를 Edge으로 전송합니다



## 호출로 이동

1. **Postman 왼쪽 사이드바** -> 컬렉션
1. **컬렉션** -> AEP Foundations 부트캠프(Labs)
1. **폴더** -> 프로필 랩
1. **API 요청** -> 웹 이벤트 Edge 만들기(인증 없음)

![Postman에서 웹 이벤트 만들기 Edge(인증 없음) 요청을 엽니다](assets/send-an-edge-event-navigate-to-the-postman-call.png)

## API 요청 수정

이 작업을 이미 수행한 경우 API 실행으로 건너뛸 수 있습니다.

API 요청을 실행하려면 먼저 요청에 몇 가지 추가 정보를 추가해야 합니다. 다음 값을 취합하여 시작합니다.

## 데이터 스트림 ID 수집

1. 왼쪽 레일에서 **데이터스트림**(데이터 수집 제목 아래)을 클릭합니다.
1. 데이터 스트림을 선택하고 **데이터 스트림 ID** 값을 복사합니다.

![데이터 스트림 ID 값 복사](assets/send-an-edge-event-gather-datastream-id.png)

## Postman 쿼리 매개 변수 업데이트

1. 요청 자체에서 **매개 변수**&#x200B;을 클릭합니다.
1. 이전 단계의 데이터 스트림 ID로 **Value**&#x200B;을(를) 업데이트합니다.
1. 업데이트를 저장하려면 **저장** 단추를 클릭하십시오.
1. 이메일을 이메일로 변경

![Params 값을 데이터 스트림 ID로 업데이트하고 [저장]을 클릭합니다](assets/send-an-edge-event-update-datastreamid.png)

![요청 본문의 전자 메일 값을 자신의 전자 메일로 변경](assets/send-an-edge-event-change-email-to-your-email.png)

## API 실행

**보내기** 단추를 클릭하여 요청을 실행합니다.

![Edge Network에서 성공한 200 OK 응답이 반환됨](assets/send-an-edge-event-successful-response-from-edge.png)



응답에서 다시 돌아올 것을 보아야 하는 것은 다음과 같은 핵심적인 것입니다.

- 200 OK 응답은 Edge Network이 데이터를 성공적으로 보내고 수락했음을 의미합니다
- 페이로드 응답에는 다음 내용도 표시되어야 합니다.
  - 설정한 사용자 지정 Personalization 대상의 destinationId
  - 해당 대상의 별칭 이름(사용자 이름은 customPersonalization)
  - 프로필에서 자격이 부여된 모든 세그먼트가 에지에 있음

>[!NOTE]
>
>스트리밍 및 배치 세그먼트는 먼저 허브에서 평가될 때까지 표시되지 않습니다

>[!NOTE]
>
>전달자 토큰을 사용하여 server.adobedc.net으로 전송하는 경우 사용자 지정 Personalization 대상에 구성한 속성도 표시됩니다

## 발생할 수 있는 오류

다음은 발생할 수 있는 오류의 예입니다. 즉, Edge 네트워크로 전송되는 데이터를 평가할 때 Edge Segmentation 평가를 아직 사용할 수 없습니다.

```none
"errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/EXEG-0203-502",
            "status": 502,
            "title": "The service call has failed.",
            "detail": "An error occurred while calling the 'com.adobe.experience_platform.edge_segmentation' service for this request. Try again.",
            "report": {
                "eventIndex": 0
            }
        }
    ]
```

## 이벤트 전달 유효성 확인

webhook.site에는 Postman 요청을 통해 보낸 것과 동일한 페이로드 본문이 즉시 표시됩니다.

![이벤트 전달 후 webhook.site에 페이로드가 표시됨](assets/send-an-edge-event-payload-appears-on-webhook-site.png)

>[!NOTE]
>
>Edge 설정에서 사용한 데이터 스트림을 설정할 때 페이로드가 요청한 지역 조회 정보를 추가했음을 확인합니다

## 프로필 조회

Adobe Experience Platform에서 방금 Edge Network으로 보낸 이벤트에서 방금 전송한 프로필을 찾습니다.  프로파일 -> 찾아보기로 이동하여 다음 정보를 사용하여 조회를 수행합니다.

- 병합 정책 -> 기본 시간 기반
- ID 네임스페이스 -> 이메일
- ID 값 -> edge-email\@dep.com



1. **보기**&#x200B;를 클릭하여 프로필 조회
1. 프로필을 열려면 **프로필 ID**&#x200B;를 클릭하십시오.

   ![프로필을 검색하고 프로필 ID를 클릭하여 열기](assets/send-an-edge-event-lookup-profile.png)



1. 위쪽 탐색에서 **이벤트**&#x200B;를 클릭하면 방금 보낸 이벤트를 볼 수 있습니다

   ![프로필의 이벤트 탭에서 이벤트를 봅니다](assets/send-an-edge-event-view-the-profile-event.png)



1. 위쪽 탐색에서 Audience Membership 탭을 검토하여 프로필이 Audiences에 적합한지 확인합니다.  다음이 표시됩니다.

- 모든 이벤트 Edge(최근 15분 이내)
- 모든 이벤트 스트리밍(지난 1시간 이내)
- 사용 사례 #1에서 다음 대상도 표시되어야 합니다.
  - iPhone 14 페이지를 방문했지만 소유/주문하지 않음
  - iPhone 14 페이지 방문

![방문한 iPhone 14 페이지 대상에 적합한 프로필](assets/send-an-edge-event-visited-iphone-14-page.png)

## 스트리밍 대상 활성화의 유효성 검사

구성한 스트리밍 대상이 세그먼트를 활성화했는지 확인하려면 웹후크를 확인하십시오.  \~5분 내에 표시됩니다.

![Webhook에서 활성화된 스트리밍 대상 세그먼트의 유효성을 검사합니다](assets/send-an-edge-event-validate-streaming-destination-activation.png)

>[!NOTE]
>
>스트리밍 대상은 두 ID가 아직 연결되지 않은 경우 다른 세그먼트 자격 페이로드를 전송할 수 있습니다.

ECID와 이메일이 아직 연결되지 않은 경우, 몇 분 후 identityMap을 제외한 다른 페이로드가 동일한 값으로 나타날 수 있습니다(이메일 및 ecid)

시간이 지남에 따라 &quot;종료됨&quot; 상태에 대해 웹후크에 더 많은 페이로드를 수신하기 시작해야 합니다.

![스트리밍 대상에 대해 &quot;종료됨&quot; 상태를 표시하는 Webhook 페이로드](assets/send-an-edge-event-webhook-exited-status-payload.png)

## 모든 검사를 해석하는 방법

1. Postman에서 200개의 응답 확인(적절한 형식의 페이로드)
1. 웹후크에 이벤트가 있는지 확인합니다(이벤트 전달이 올바르게 구성됨).
1. 프로필에 이벤트가 있는지 확인합니다(허브에 올바르게 구성된 AEP 서비스, 이벤트를 수신하고 처리함).
1. 프로필에 두 개의 ID(ID 그래프가 허브에 연결됨)가 있는지 확인
1. 프로필이 대상(올바르게 정의된 대상)에 적합한지 확인
1. 웹후크가 스트리밍 대상을 받았는지 확인(올바르게 구성된 HTTP API 대상)
1. Postman 응답에 세그먼트가 포함되어 있는지 확인 (올바르게 구성된 사용자 지정 Personalization 대상)
1. 데이터 레이크에 전송 로그가 있는지 확인합니다(올바르게 구성되고 보낸 대상 자격 및 스트리밍 대상). 아래를 참조하십시오.

## 대상의 데이터 레이크 &quot;로그&quot;

최소 60분 후에는 데이터 세트에 사용자가 전송한 이벤트가 있는지 확인할 수도 있습니다. 이렇게 하려면 쿼리 서비스를 사용하여 다음 쿼리를 수행합니다.

아래 테이블 이름을 샌드박스의 이름으로 변경합니다. 이를 찾으려면 데이터 집합 목록으로 이동하여 &quot;`dest`&quot;에서 필터링하고 데이터 집합을 열고 오른쪽 레일에서 테이블 이름을 복사합니다.

```sql
SELECT * FROM profile_export_for_destination_merge_policy_xxx
WHERE extSourceSystemAudit.LASTREFERENCEDDATE >= CURRENT_DATE
AND identitymap['email'][0].ID in ('edge-email@dep.com')
ORDER BY extSourceSystemAudit.LASTREFERENCEDDATE DESC
LIMIT 10
```
