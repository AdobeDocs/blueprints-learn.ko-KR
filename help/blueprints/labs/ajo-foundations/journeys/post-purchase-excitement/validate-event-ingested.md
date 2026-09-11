---
hold: true
title: 수집된 이벤트 유효성 확인
description: 배송된 주문 이벤트가 프로필에 수집된 후 예상 대상에 적합한지 확인합니다.
doc-type: article
solution: Experience Platform
exl-id: c04397dd-8b5c-48a8-82b5-78188b8374f1
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# 수집된 이벤트 유효성 확인

## 학습 목표

이벤트가 Adobe Experience Platform에 성공적으로 수집되었는지 확인합니다.

## 프로필의 이벤트 유효성 검사

1. **프로필**(으)로 이동하고 프로필을 조회하여 프로필에 이벤트가 수집되었는지 확인합니다.  초 단위로 표시됩니다.
   - **ID 네임스페이스** -> `email`
   - **ID 값** -> `henry.creel@emailsim.io`
2. **이벤트** 탭을 클릭합니다. `orders.shipped` 이벤트를 찾습니다.

프로필의 이벤트 탭에 표시되는 ![orders.shipped 이벤트](assets/validate-event-ingested-orders-shipped-event.png)

>[!WARNING]
>
>**message.feedback** 이벤트가 표시되었습니다.  이는 여정에서 가져온 것이며 일반적으로 실패 또는 제외를 나타냅니다.  해당 항목을 클릭하고 `reason`을(를) 봅니다.
>
>프로덕션에서 를 실행할 수 있는 몇 가지 예는 다음과 같습니다.
>
>- EmailNoAddressFoundInProfile(전자 메일이 없는 프로필로 전자 메일을 전송하려고 했습니다.)
>- EmailNoConsent(동의가 아니요로 설정된 프로필로 이메일을 전송하려고 했습니다.)



3. 프로필이 **대상**&#x200B;에 대해 유효한지 확인합니다(몇 분 정도 소요될 수 있음).
   - 모든 이벤트 Edge(15분 이내)
   - 모든 이벤트 스트리밍(15분 이내)

![모든 이벤트 Edge 및 모든 이벤트 스트리밍 대상에 적합한 프로필](assets/validate-event-ingested-profile-qualified-audiences.png)



## 자신의 이메일로 시도

이제 프로필이 로그인되었는지 확인했으므로 이메일을 사용하여 일부 주문 배송 이벤트를 보냅니다.

1. Postman으로 돌아가서 **배송 주문 이벤트**&#x200B;를 찾습니다.
2. **본문**&#x200B;을 클릭하고 **전자 메일 주소**&#x200B;을(를) 내 주소로 변경합니다.

![Postman 요청 본문에서 변경된 전자 메일 주소](assets/validate-event-ingested-change-email-in-postman-body.png)

3. **저장**&#x200B;하고 **보내기**&#x200B;를 누르십시오.
4. 1-3단계로 돌아가서 이메일 주소를 사용하여 확인합니다.

## 요약

이벤트는 프로필 스토어에 표시되며 프로필은 이제 이벤트를 찾고 있던 Audiences의 일부입니다.
