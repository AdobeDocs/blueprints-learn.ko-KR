---
hold: true
title: Edge 활성화
description: Edge, 스트리밍 및 일괄 처리 활성화 속도가 어떻게 다른지 알아보고, 에지 세그먼트를 만들고 이벤트 전달을 구성하기 위한 랩 단계를 미리 봅니다.
doc-type: overview-page
solution: Experience Platform
exl-id: 9ecadff9-3838-4cd4-93b1-7c23a232f84c
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Edge 활성화

## 활성화 속도 요약

Adobe은 다양한 요구 사항을 해결하기 위해 세 가지 활성화 속도를 제공합니다.

1. Edge
1. 스트리밍
1. 일괄 처리

이벤트 전달, Edge 대상 및 Edge Personalization과 함께 Adobe Edge를 사용하여 를 활성화하는 방법에 대해 알아봅니다. 그런 다음 허브에서 Edge 및 외부 대상으로 스트리밍 대상을 사용하는 방법을 보여 줍니다.

>[!NOTE]
>
>이 실습에서는 일괄 처리 활성화를 다루지 않습니다. 배치 활성화 는 서로 다른 간격으로 예약할 수 있으며, 타이밍은 랩 환경에서 적어도 3~24시간을 가질 필요 없이 표시하기 어렵게 합니다.



## 실험실에서 다룰 내용

- Edge 세그먼트 만들기
- 이벤트 전달 구성
- Edge 이벤트에서 보내기
- 이 트리거는
  - 우량으로 선별할 Edge 세그먼트
  - Edge에서 Webhook으로 보낼 이벤트 전달
