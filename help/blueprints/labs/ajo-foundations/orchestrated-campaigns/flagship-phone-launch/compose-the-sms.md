---
hold: true
title: SMS 구성
description: 관계형 스토어의 전화 및 모델 특성을 사용하여 오케스트레이션된 캠페인에서 SMS 메시지를 구성하고 개인화하는 방법에 대해 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: 3deb822b-8374-4537-a260-f4f6f4d67569
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# SMS 구성

## 목표

다음 몇 단계에서는 매우 간단한 SMS 메시지를 작성합니다.  극히 기본적인 수준에서 일부 콘텐츠를 쉽게 추가하고 관계형 저장소의 데이터를 기반으로 메시지를 개인화하는 방법에 대해 알아봅니다.



## 컨텐츠로 이동

**콘텐츠 편집** 단추를 클릭하거나 직접 **콘텐츠** 탭으로 이동합니다.

![콘텐츠 편집 단추 및 콘텐츠 탭 탐색 &quot;콘텐츠 편집&quot;](assets/compose-the-sms-navigate-to-content-tab.png "콘텐츠 편집")



## 메시지 만들기

1. **Personalization** 단추를 클릭하여 메시지를 만듭니다.

SMS 메시지를 만드는 ![Personalization 단추](assets/compose-the-sms-click-personalization-button.png)

>[!NOTE]
>
>&quot;자동 선택&quot; 옵션은 AI를 사용하여 메시지를 작성하는 데 도움을 줍니다. 원하신다면 확인해 보세요. 하지만 이 실험실에서는 다루지 않을 겁니다.



2. 아래 텍스트를 복사하여 SMS 메시지 본문에 붙여넣습니다.

```none
Hi from Connection 5G! Your phone_make phone_model is eligible for a free upgrade to one of the new iPhone 17 models. Shop online or come into a store today to take advantage of this offer.
```

>[!NOTE]
>
>메시지 편집기에서 자동 줄 바꿈을 **켜짐**(으)로 설정하십시오.  창의 오른쪽 아래에 있습니다.



3. 왼쪽 레일에서 **대상 특성** 옵션을 사용하여 아래 **phone\_make** 및 **phone\_model**(이)라는 메시지의 두 필드를 업데이트합니다.  완료되면 메시지가 스크린샷과 일치해야 합니다.

![휴대폰 제조사 및 모델이 개인화된 최종 SMS 메시지](assets/compose-the-sms-final-message-text.png)

>[!NOTE]
>
>왜 이러는 거야?  고객들의 전화 번호 및 모델과 함께 메시지를 개인화하려고 하며, 이 정보는 관계 상점의 고객 라인 테이블 내에 있습니다.  이 비디오에서는 오케스트레이션된 캠페인의 데이터를 사용하여 메시지를 개인화하는 방법을 보여 줍니다.



4. 편집기에서 **유효성 검사**&#x200B;를 클릭하고 유효성 검사 오류가 없는지 확인한 다음 **저장** 단추를 클릭하십시오

![메시지 편집기의 유효성 검사 및 저장 단추](assets/compose-the-sms-validate-and-save.png)



5. 워크플로우 캔버스로 돌아가려면 **뒤로 화살표(\&lt;-)**&#x200B;를 클릭하십시오.

![뒤로 화살표를 클릭하여 워크플로 캔버스로 돌아가기](assets/compose-the-sms-return-to-canvas.png)



## 요약

방금 메시지를 만들었는데 이제 메시지 편집기의 작동 방식에 대해 좀 더 잘 알고 있기를 바랍니다.  관계형 스토어의 데이터를 사용하여 개인화할 수 있지만 실시간 고객 프로필의 데이터도 사용하여 개인화할 수 있습니다.

>[!NOTE]
>
>실시간 고객 프로필 속성을 사용하여 오케스트레이션된 캠페인에서 메시지를 개인화하는 경우 속성이 최대 24시간 경과될 수 있도록 데이터 레이크의 프로필 스냅샷 데이터 세트에서 가져오고 있다는 것만 기억하십시오. 프로필 스냅숏은 일별 일괄 처리 세분화 작업 후 하루에 한 번만 업데이트됩니다.
