---
title: Edge 대상 만들기
description: 각 항목이 실시간 수신 이벤트에 응답하는 방식을 비교하는 것과 동일한 일괄 처리와 함께 Edge 평가 대상을 빌드하고 게시합니다.
doc-type: article
solution: Experience Platform
exl-id: 79265a8f-81dd-41a3-89c5-c6646e435328
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Edge 대상 만들기

이 대상은 페이로드(예: 페이지 보기)가 클라이언트(예: 웹 SDK)에서 Edge으로 전송될 때 자격을 부여하는 데 사용됩니다.

>[!NOTE]
>
>Personalization에서 전환하여 사용할 수 있도록 일반적으로 Edge에서 대상을 평가합니다. Edge에서 Personalization을 수행하지 않는다면 대상자가 허브에서 스트리밍으로 평가하도록 할 수 있습니다.

## 대상자 만들기

1. 왼쪽 레일에서 대상 을 클릭합니다.
1. 그런 다음 화면의 오른쪽 상단에 있는 대상 만들기 를 클릭합니다
1. 그런 다음 규칙 작성 을 클릭합니다.



![대상 만들기 단추 및 규칙 빌드 옵션이 강조 표시된 대상 페이지](assets/create-edge-audience-create-audience-step-1.png)



새 대상을 만들기 위해 ![빌드 규칙 캔버스 열림](assets/create-edge-audience-create-audience-step-2.png)



## 대상을 규칙으로 변환

1. **대상**(으)로 이동하여 **Experience Platform** 폴더를 클릭합니다.
1. 이름이 **dep: 모든 이벤트 스트리밍(시간 내)**&#x200B;인 대상을 캔버스로 드래그하여 놓습니다.

   ![dep: 모든 이벤트 스트리밍(시간 내) 대상을 규칙 빌더 캔버스로 드래그하는 중](assets/create-edge-audience-drag-audience-to-canvas.png)



1. 아래 표시된 **아이콘**&#x200B;을 클릭하여 대상을 캔버스에서 규칙 집합으로 변환한 다음 **변환**&#x200B;을 클릭합니다

![대상자를 규칙 집합으로 변환하는 데 사용되는 캔버스의 변환 아이콘](assets/create-edge-audience-convert-to-rules-icon.png)

## 이벤트 규칙 업데이트

이벤트 규칙을 다음과 같이 변경합니다(이벤트를 확장하여 확인해야 할 수 있음).

1. 마지막
1. 15
1. 분

![지난 15분 동안 트리거하도록 구성된 이벤트 규칙](assets/create-edge-audience-update-event-rules.png)

## 세그먼트 게시

1. 세그먼트 이름을 **모든 이벤트 Edge(15분 이내)로 업데이트**
1. 평가 방법을 Edge으로 업데이트
1. 세그먼트 게시

![게시하기 전에 Edge 평가 방법을 보여 주는 세그먼트 세부 정보](assets/create-edge-audience-publish-segment.png)

## 일괄 처리 평가 세그먼트 만들기

방금 만든 모서리 세그먼트에 대해 수행한 것과 동일한 단계를 반복하되, 대신 다음 정보를 사용합니다.

>[!NOTE]
>
>이벤트가 Edge에 전달되더라도 일괄 평가로 저장된 모든 대상은 스트리밍 방식으로 평가되지 않는다는 것을 알 수 있도록 일괄 처리 대상을 만들 것입니다.

이벤트 규칙:

- 마지막
- 1
- 일



세그먼트 세부 사항:

- 이름 -> **모든 이벤트 일괄 처리(1일 이내)**
- 평가 방법 -> 일괄 처리
