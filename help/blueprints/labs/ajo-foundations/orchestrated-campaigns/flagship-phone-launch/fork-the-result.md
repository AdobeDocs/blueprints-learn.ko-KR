---
title: 결과 포크
description: 대상자를 저장하고 SMS 메시지를 보내기 위한 결과를 분기하기 위해 오케스트레이션된 캠페인에 포크 활동을 추가하는 방법을 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: 8f1d0839-e4ca-4b7c-bc97-4e271a457296
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# 결과 포크

## 목표

이 단계는 간단한 단계로, 결과를 복제하여 향후 단계에서 두 가지 다른 작업을 수행할 수 있도록 포크 활동을 추가하기만 하면 됩니다.

1. 다른 사람이 광고 또는 크로스 채널 목적으로 사용할 수 있도록 대상을 저장합니다.
1. SMS 메시지를 개별 라인으로 보냅니다.



## 포크 만들기

1. 워크플로우 캔버스에서 대상자 작성 활동 후에 **+** **아이콘**&#x200B;을 클릭하고 **활동 포크**&#x200B;를 선택합니다

   ![대상 작성 활동 뒤에 포크 활동 추가](assets/fork-the-result-add-fork-activity.png)



2. 전환을 클릭한 다음 아래에 설명된 대로 이름을 할당하여 포크에서 각 전환의 이름을 업데이트합니다.
   - **상위** —> `Save Audience`
   - **아래쪽** —> `SMS`

   ![대상 및 SMS 저장으로 이름이 변경된 포크 전환](assets/fork-the-result-rename-transitions.png)



   캔버스를 완료하면 다음과 같이 표시됩니다.

   포크 활동을 추가한 후 ![워크플로 캔버스](assets/fork-the-result-final-canvas.png)

   >[!NOTE]
   >
   >포크 활동은 기본적으로 이전 활동의 결과를 두 개의 독립적인 분기로 복제하는 것입니다



3. 워크플로 캔버스 맨 위에서 **저장**&#x200B;을 클릭합니다.

![워크플로 캔버스 도구 모음의 저장 단추](assets/fork-the-result-click-save.png)

>[!TIP]
>
>너무 어려웠어요. 😁님



## 요약

환영, 결과의 포크를 생성 (즉, 결과 복제)했습니다. 이 포크를 사용하면 분기를 지정하여 대상자 저장을 처리할 수 있지만 다른 하나는 SMS 전송에 사용할 수 있습니다.

>[!NOTE]
>
>특히 대상자 저장 활동에서 활동을 허용하지 않으므로 대상자를 저장하려는 경우 포크 를 사용해야 합니다.
