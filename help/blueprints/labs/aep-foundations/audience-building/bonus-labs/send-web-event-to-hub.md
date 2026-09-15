---
title: 허브로 웹 이벤트 보내기
description: Postman을 사용하여 웹 이벤트를 허브에 직접 보내고, 이 이벤트가 프로필에 도달하고 스트리밍 세그먼트에 적합한지 확인하는 방법을 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: a8343499-b4d5-4540-8fe1-7497bc20e437
source-git-commit: 8b3391d41cd4a3ea6cb52d5167e627b7f6bd2c6e
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%
---

# 허브로 웹 이벤트 보내기

>[!IMPORTANT]
>
>이 실습을 시작하기 전에 [Postman 설정](../../postman-setup/postman-installation.md)을 완료합니다. 관련 [외부 대상 활성화 워크플로](../use-case-1-acquisition/configure-destinations/setup-streaming-destination.md)의 [webhook.site](https://webhook.site/)에도 액세스해야 합니다.

## Postman 열기

컴퓨터에서 postman을 시작하고 다음 API 호출로 이동합니다.

1. **Postman 왼쪽 사이드바** —> `Collections`
1. **컬렉션** —> `AEP Foundations Bootcamps (labs)`
1. **폴더** —> 프로필 랩
1. **API 요청** —> `Create Web Event`

![Postman에서 웹 이벤트 API 만들기 요청을 엽니다](assets/send-web-event-to-hub-create-web-event-api-request.png)


## API 요청 수정

샘플 API 요청을 만들려면 API 요청 본문에 다음 부분을 채워야 합니다.

다음 값을 취합하여 시작합니다.



## 계정 스트리밍 끝점 찾기

1. 왼쪽 레일에서 **소스**(으)로 이동한 다음 위쪽 탐색에서 **계정**&#x200B;을 클릭합니다
1. **dep: HTTP API \[raw]**&#x200B;를 검색하고, 행을 강조 표시하고 나중에 참조할 수 있는 위치에 **스트리밍 끝점**&#x200B;의 값을 복사하고 저장합니다.

 계정 및 해당 스트리밍 끝점 복사](assets/send-order-event-to-hub-http-api-raw-streaming-endpoint.png &quot;dep: HTTP API \[raw]&quot;)

## 웹 데이터 흐름 ID 찾기

1. **HTTP API \[raw]** 계정 클릭
1. **dep: 웹(스트림)**&#x200B;이라는 데이터 흐름 행 찾기 및 선택
1. 오른쪽 레일 복사본에서 **데이터 흐름 ID** 값을 나중에 참조할 수 있는 위치에 저장합니다.

>[!NOTE]
>
>행에서 빈 공간을 클릭합니다.  파란색 링크를 클릭하지 마십시오!

![dep에 대한 데이터 흐름 ID 복사: 웹(스트림) 데이터 흐름](assets/send-web-event-to-hub-web-stream-dataflow-id.png "웹 데이터 흐름 ID")

## 최종 API 요청 만들기

이전 단계에서 저장한 값을 아래 강조 표시된 위치에 복사합니다.

- **빨강** —> `Streaming Endpoint URL`
- **녹색** —> `Dataflow ID`

완료 시 최종 API 요청은 다음과 같아야 합니다

>[!CAUTION]
>
>아직 실행하지 마십시오!

![스트리밍 끝점 및 데이터 흐름 ID가 채워진 웹 이벤트 API 만들기 요청 완료](assets/send-web-event-to-hub-final-web-api-request.png)

## API 실행

1. **저장** 단추를 클릭하여 API 호출을 저장합니다.
1. **보내기** 단추를 클릭하여 요청을 실행합니다.

호출이 성공하면 다음 응답이 발생합니다.

![웹 이벤트를 보낸 후 API 응답 성공](assets/send-web-event-to-hub-successful-api-response.png)

## 유효성 검사

1. 프로필로 이동하여 프로필에서 이벤트가 수집되었는지 확인합니다.  초 단위로 표시됩니다.
   1. 전화에서 이메일을 사용하여 프로필 조회
1. 이벤트에서 마지막으로 보낸 이후 기간에 따라 새 세그먼트에 대한 자격이 없을 수도 있습니다. 그렇지 않으면 다음 항목이나 다른 항목이 표시될 수 있습니다.
   1. 모든 이벤트 Edge(15분 이내)
      1. Edge 평가와 함께 저장된 모든 대상자는 스트리밍 데이터가 유입될 때 허브에서 평가됩니다
   2. dep: 모든 이벤트 스트리밍(시간 내)
1. 이 Hub 이벤트는 웹후크로 전송되지 않습니다.
   1. 이벤트 전달은 허브에 직접 전송된 이벤트가 아니라 Edge에 전송된 이벤트를 처리합니다. [외부 대상 활성화 워크플로](../use-case-1-acquisition/configure-destinations/setup-streaming-destination.md)를 사용하여 webhook.site에서 이벤트를 캡처합니다.
1. 최소 30분 후, 다음과 같이 데이터 세트를 확인할 수도 있습니다.
   1. 아래 테이블 이름을 샌드박스의 이름으로 변경합니다.  이를 찾으려면 데이터 집합 목록으로 이동하여 &quot;`dest`&quot;에서 필터링하고 데이터 집합을 열고 오른쪽 레일에서 테이블 이름을 복사합니다.

```sql
SELECT * FROM profile_export_for_destination_merge_policy_xxx
WHERE extSourceSystemAudit.LASTREFERENCEDDATE >= CURRENT_DATE
AND identitymap['email'][0].ID in ('depche.mode@dep.com')
ORDER BY extSourceSystemAudit.LASTREFERENCEDDATE DESC
LIMIT 10
```
