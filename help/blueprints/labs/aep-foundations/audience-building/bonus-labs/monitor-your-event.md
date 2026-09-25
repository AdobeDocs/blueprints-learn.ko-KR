---
title: 이벤트 모니터링
description: Adobe Experience Platform Assurance을 사용하여 디버그 세션을 만들고, Postman을 통해 유효성이 확인된 이벤트를 보내고, Edge 이벤트 처리 로그를 검사합니다.
doc-type: article
solution: Experience Platform
exl-id: 94b200c0-6714-4996-a266-119cc8f7f4e2
source-git-commit: 96308d5726def849ef22540a5d13618017c40cc3
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%
---

# 이벤트 모니터링

## Assurance으로 이동

[Adobe Experience Platform Assurance](https://experienceleague.adobe.com/ko/docs/experience-platform/assurance/home)은(는) Adobe Experience Platform Edge에 대한 데이터 수집 방법을 검사, 증명, 시뮬레이션 및 확인하는 데 도움이 되는 Adobe Experience Cloud의 제품입니다.

1. Adobe Experience Platform -> Assurance -> 세션 만들기로 이동

   ![Adobe Experience Platform Assurance으로 이동하여 세션 만들기](assets/monitor-your-event-navigate-to-assurance-create-session.png)



2. **시작** 단추 클릭

![시작 단추를 클릭하여 Assurance 세션 구성을 시작합니다](assets/monitor-your-event-click-start-button.png)



## 세션 구성

1. 이름 —> \[Sandbox] Edge 세션
1. URL —> https\://www\.adobe.com
   - 이 URL은 고객의 실제 사이트로 대체됩니다.
1. Next 단추를 클릭합니다.

   ![세션 이름과 URL을 입력한 후 [다음]을 클릭합니다](assets/monitor-your-event-click-next-button.png)

1. 나중에 참조할 수 있는 위치에 링크를 복사합니다.

1. **완료** 단추를 클릭합니다.

   ![Assurance 세션 링크를 복사하고 완료](assets/monitor-your-event-copy-link.png)를 클릭합니다.



1. **설정**(으)로 이동

   ![Assurance 세션의 설정 탭으로 이동](assets/monitor-your-event-navigate-to-settings.png "설정 클릭")



1. **+** 단추를 클릭한 다음 **완료**&#x200B;를 클릭하여 **이벤트 트랜잭션** 및 **Edge Delivery**&#x200B;을(를) 사용하도록 설정합니다.

![이벤트 트랜잭션 및 Edge Delivery을 사용하도록 설정한 다음 완료](assets/monitor-your-event-enable-event-transactions-and-edge-delivery.png)를 클릭합니다.


## Postman 열기

Postman -> 웹 이벤트 만들기 Edge(인증 없음) -> 헤더로 이동

1. Assurance에서 복사한 링크를 사용하여 **x-adobe-aep-validation-token**&#x200B;을 헤더에 추가합니다. Assurance에서 복사한 링크에서 = 뒤에 있는 **ID** 값을 가져옵니다. 예: [https://www.adobe.com/?adb\_validation\_sessionid=](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0) [`efa4a9ed-02d8-4647-80fa-f01a5be273d0`](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0)
1. 전체 URL이 아닌 [`efa4a9ed-02d8-4647-80fa-f01a5be273d0`](https://www.adobe.com/?adb_validation_sessionid=efa4a9ed-02d8-4647-80fa-f01a5be273d0) 값만 사용합니다.

   ![Postman에서 Assurance 세션 ID를 사용하여 x-adobe-aep-validation-token 헤더를 추가합니다](assets/monitor-your-event-populate-the-x-adobe-aep-validation-token.png)



1. Postman에서 **웹 이벤트 만들기 Edge(인증 없음)** 요청을 저장하고 실행합니다.



## Assurance 로그 보기

Assurance으로 돌아가면 많은 이벤트가 표시됩니다. 데이터 스트림 ID를 검색에 추가하여 관련 이벤트 유형으로만 필터링합니다

![데이터 스트림 ID를 검색하여 Assurance 이벤트를 필터링합니다](assets/monitor-your-event-filter-using-search.png)



이벤트를 선택하고 오른쪽 레일에서 필요한 경우 메시지를 엽니다.

![이벤트를 선택하고 오른쪽 레일에서 메시지를 확장합니다](assets/monitor-your-event-expand-messages.png)

찾을 이벤트 유형:

- hitReceived (Edge에서 받은 페이로드를 표시함)
- evaluatingRule(SSF를 설정하는 경우 평가되는 규칙이 표시됨)
- firedDestinations(전송된 대상)
- segmentsDiscovered(에지 세그먼트에 적합한지 확인)
- com.adobe.experience\_platform.edge\_segmentation/response (어떤 세그먼트로 응답했습니까)

![각 이벤트 유형을 선택하여 Assurance에서 어떻게 해석하는지 확인](assets/monitor-your-event-select-each-event.png)

이를 살펴보고 각 단계가 Assurance에 의해 어떻게 해석되는지 확인하십시오.
