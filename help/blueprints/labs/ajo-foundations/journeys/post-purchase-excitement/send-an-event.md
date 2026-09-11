---
hold: true
title: 이벤트 보내기
description: Postman을 사용하여 시뮬레이트된 주문 배송 이벤트를 Edge으로 보내지 않고 허브로 바로 스트리밍하여 여정을 트리거할 수 있습니다.
doc-type: article
solution: Experience Platform
exl-id: a0f75f5a-e3b3-42a2-8547-f075a7661a22
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# 이벤트 보내기

## 학습 목표

Postman을 사용하여 여정을 트리거하기 위해 시뮬레이션된 주문 출하 이벤트 보내기

## Hub와 Edge으로 스트리밍

이전에는 이벤트를 Edge에 보냈습니다.  이벤트에서 스트리밍하되, Edge으로 전송할 필요는 없는 백엔드 시스템이 있을 수 있는 사용 사례가 있습니다.  이 실습에서는 **Order Shipped 이벤트를 Hub로 스트리밍**(예: 서버 간 스트리밍, 예: Commerce Server에서 AEP으로 주문 배송 알림)하여 이를 수행하는 방법을 보여 줍니다.

## 유효성 검사 이벤트가 프로필에 없음

1. **프로필**(으)로 이동하여 프로필을 조회합니다.
   - **ID 네임스페이스** -> `email`
   - **ID 값** -> `henry.creel@emailsim.io`
1. **이벤트** 탭을 클릭합니다.
   - **아니요** `orders.shipped` 이벤트가 있어야 합니다.

## API 요청 수정

API 요청을 만들려면 API 요청 본문에 다음 부분을 채워야 합니다.

다음 값을 취합하여 시작합니다.

### 계정 스트리밍 끝점 찾기

1. 왼쪽 레일에서 **소스**(으)로 이동한 다음 위쪽 탐색에서 **계정**&#x200B;을 클릭합니다
1. **dep: HTTP API \[raw]**&#x200B;를 검색하고, 행을 강조 표시하고 나중에 참조할 수 있는 위치에 **스트리밍 끝점**&#x200B;의 값을 복사하고 저장합니다.

![dep: 스트리밍 끝점 값으로 강조 표시된 HTTP API [raw] 계정 행](assets/send-an-event-streaming-endpoint-account-row.png "dep: HTTP API \[raw]")


### 데이터 흐름 ID 찾기

1. **dep: HTTP API \[raw]** 클릭
1. **dep: 주문(스트림)**&#x200B;에 대한 레코드를 찾고 데이터 흐름 링크를 클릭합니다.
1. 오른쪽 레일 복사본에서 **데이터 흐름 ID** 값을 나중에 참조할 수 있는 위치에 저장합니다.

> [!WARNING]
>
>행에서 빈 공간을 클릭합니다.  파란색 링크를 클릭하지 마십시오!

![오른쪽 레일에 표시된 데이터 흐름 ID 값](assets/send-an-event-dataflow-id-in-right-rail.png "웹 데이터 흐름 및 데이터 세트 ID")



### Postman 열기

컴퓨터에서 Postman을 시작하고 다음 API 호출로 이동합니다.

- **Postman 왼쪽 사이드바** —> `Collections`
- **컬렉션** —> `AJO Bootcamp (Labs)`
- **폴더** —> `Profile & Journey Labs`
- **API 요청** —> `Ship Order Event`

![Postman 컬렉션에 있는 배달 주문 이벤트 요청](assets/send-an-event-open-ship-order-event-postman.png)



### 최종 API 요청 만들기

1. 이전 단계에서 저장한 값을 아래 강조 표시된 위치에 복사합니다.
1. **머리글**&#x200B;을 클릭하고 다음 값에 붙여넣습니다(후행 공백 제거).
   - **빨강** —> `Streaming Endpoint URL`
   - **녹색** —> `Dataflow ID`
     - 값은 GUID처럼 보입니다(http로 시작하지 않음).

> [!CAUTION]
>
>아직 실행하지 마십시오!

![Postman 헤더에 붙여넣은 스트리밍 끝점 URL 및 데이터 흐름 ID](assets/send-an-event-paste-headers-in-postman.png)

## API 실행

1. **저장** 단추를 클릭하여 API 호출을 저장합니다.
1. **보내기** 단추를 클릭하여 요청을 실행합니다.

호출이 성공하면 다음 응답이 발생합니다.

![웹 이벤트를 보낸 후 성공한 응답](assets/send-an-event-successful-web-event-send.png)

## 요약

출하 주문 이벤트가 플랫폼으로 성공적으로 전송됨
