---
title: 다중 샌드박스 이벤트 전달 데이터 수집
description: Experience Platform 웹 및 Mobile SDK로 수집된 데이터를 단일 이벤트를 수집하도록 구성하고 여러 Experience Platform 샌드박스로 전달하는 방법에 대해 알아봅니다.
solution: Data Collection
kt: 7202
source-git-commit: e9a9abeaa722bb2f9a232f4e861b1b5eae86edd1
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 20%

---


# 다중 샌드박스 이벤트 전달 데이터 수집

이 블루프린트는 Experience Platform 웹 및 Mobile SDK로 수집된 데이터를 단일 이벤트를 수집하고 여러 AEP 샌드박스로 전달하도록 구성하는 방법을 보여 줍니다. 이 블루프린트는 을 사용하는 다중 샌드박스 데이터 수집에만 적용됩니다. [!UICONTROL 이벤트 전달] 이 목표를 달성하기 위해.

를 사용하여 이벤트를 복제하는 것 외에도 [!UICONTROL 이벤트 전달] 다른 샌드박스에 대한 요구 사항을 충족하는 수집된 원본 데이터를 추가, 필터링 또는 조작할 수 있습니다.

[!UICONTROL 이벤트 전달] 는 를 포함하는 별도의 속성을 사용합니다. [!UICONTROL 데이터 요소], [!UICONTROL 규칙], 및 [!UICONTROL 확장] 데이터 요구 사항에 필요합니다. 수신 이벤트를 사용하면 [!UICONTROL 이벤트 전달] 속성은 데이터를 수집하고 전달하기 전에 필요에 따라 관리할 수 있습니다.

대상 샌드박스에 Adobe에서 사용하는 구성된 HTTP 스트리밍 끝점이 필요합니다 [!UICONTROL 클라우드 커넥터] 확장명.

## 사용 사례

* 글로벌 데이터 보고 - 여러 샌드박스를 사용하여 운영 환경을 격리하고 크로스 샌드박스 보고를 위해 데이터 수집을 하나의 샌드박스로 통합해야 하는 경우. 다음을 통해 경험 에지 이벤트 라우팅 [!UICONTROL 이벤트 전달] 보고 샌드박스에 사용하면 각 샌드박스 운영 환경에서 데이터가 실시간으로 수집되는 대로 보고 샌드박스로 전송할 수 있습니다.

* 각 샌드박스 운영 환경에 대한 다양한 데이터 규칙을 기반으로 샌드박스 간 데이터 수집을 관리합니다.

## 애플리케이션

* [!DNL Experience Platform] 데이터 수집
* [!UICONTROL 이벤트 전달]
* AEP [!UICONTROL 확장]
* [!UICONTROL Cloud Connector 확장]

## 고려할 사항

포함 [!UICONTROL 이벤트 전달] 여러 샌드박스에 데이터를 전송하는 접근 방식으로, 솔루션 아키텍처와 함께 고려해야 할 사항이 있습니다.

### HIPAA 데이터 불가

[!UICONTROL 이벤트 전달에서는 HIPAA을 바로 사용할 수 없기 때문에 HIPAA 데이터를 수집하는 HIPAA 사용 사례에서는 사용하지 마세요.] 하지만, 다음과 같은 용도로 사용되는 인프라 [!UICONTROL 이벤트 전달] 는 HIPAA 준비 상태로 간주되며 전적으로 고객의 재량에 따릅니다. 다음 기간 동안 [!UICONTROL 이벤트 전달] 태그 속성이에 있음 [!UICONTROL 이벤트 전달] 시스템에서 수집된 전체 데이터 페이로드는 [!UICONTROL 이벤트 전달] 시스템 을 참조하십시오. 다음을 만드는 것은 이 프로세스입니다 [!UICONTROL 이벤트 전달] HIPAA 사용 사례에 대해 설명합니다. 전체 페이로드가 [!UICONTROL 이벤트 전달] 시스템, 여기에는 모든 HIPAA 값이 포함됩니다. 비록 [!UICONTROL 이벤트 전달] 규칙은 해당 데이터를 대상으로 보내기 전에 필터링하며 HIPAA 데이터는 여전히 비 HIPAA 준비 인프라에 제공됩니다. 하지만 페이로드 데이터는 저장되지 않고 그냥 지나갑니다.

### 다양한 데이터스트림 및 스트리밍 끝점

데이터가 의 데이터스트림을 통해 [!UICONTROL 플랫폼 에지 네트워크], 사용 시 [!UICONTROL 이벤트 전달] 다른 AEP 샌드박스에서 요구 사항은 원래 컬렉션을 만드는 데이터스트림과 동일한 데이터스트림 또는 스트리밍 끝점을 사용하지 않는 것입니다. 이 경우 AEP 인스턴스가 손상될 수 있고, DoS 상황이 발생할 가능성이 있습니다.

### 예상 트래픽 볼륨

각 사용 사례를 검토할 때는 트래픽량을 알아야 합니다. 볼륨이 높으면 조절 상황이 발생할 수 있고 이 경우 고객에게 알림이 전송되므로 이 작업이 중요합니다.

## 아키텍처

![다중 샌드박스 [!UICONTROL 이벤트 전달]](assets/multi-sandbox-data-collection.png)

1. 이벤트 데이터를 수집하여 로 보내기 [!UICONTROL 플랫폼 에지 네트워크] 을(를) 사용하려면 이 필수입니다. [!UICONTROL 이벤트 전달]. Adobe 고객은 클라이언트측 또는 [!UICONTROL 플랫폼 에지 네트워크 서버 API] 서버 간 데이터 수집에 사용됩니다. 다음 [!UICONTROL Platform Edge Network API] 은 서버 간 컬렉션 기능을 제공할 수 있습니다. 그러나 이를 구현하기 위해서는 다른 프로그래밍 모델이 필요합니다. 을(를) 참조하십시오 [Edge Network Server API 개요](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ko).

1. 수집된 페이로드는 태그 구현에서 [!UICONTROL 플랫폼 에지 네트워크] (으)로 [!UICONTROL 이벤트 전달] 자체적으로 처리 및 처리되는 서비스 [!UICONTROL 데이터 요소], [!UICONTROL 규칙] 및 [!UICONTROL 작업]. [[!UICONTROL 태그와 이벤트 전달에서 자세한 차이를 확인할 수 있습니다]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko#differences-from-tags).

1. An [!UICONTROL 이벤트 전달] 속성은에서 수집된 이벤트 데이터를 받는 데에도 필요합니다. [!UICONTROL 플랫폼 에지 네트워크]. 배포된 태그 구현 또는 서버 간 컬렉션에 의해 해당 이벤트 데이터가 Platform Edge Network로 전송되었는지 여부입니다. 작성자는 이벤트 데이터를 두 번째 샌드박스로 전달하기 전에 보강할 때 사용할 데이터 요소와 규칙, 작업을 정의합니다. 사용자 지정 코드 사용을 고려해 보십시오 [!DNL JavaScript] 샌드박스 수집을 위한 데이터를 구조화하는 데 도움이 되는 데이터 요소입니다. Platform 데이터 준비 기능과 함께 데이터 구조를 관리하는 몇 가지 옵션이 있습니다.

1. 현재 Adobe 사용 [!UICONTROL Cloud Connector 확장] 은(는) 다음 내에 필요합니다. [!UICONTROL 이벤트 전달] 속성. 규칙이 이벤트 데이터를 처리하거나 보강하면 페이로드를 두 번째 샌드박스로 전송하는 POST에 대해 구성된 가져오기 호출 내에서 Cloud Connector가 사용됩니다

1. 두 번째 샌드박스의 데이터 수집을 위한 스트리밍 끝점이 필요합니다. 또한 AEP의 데이터 준비 기능을 고려하여 의 수집 및 매핑을 수행할 수 있습니다. [!UICONTROL 이벤트 전달] XDM에 대한 페이로드입니다. AEP 설명서의 [UI를 사용한 HTTP API 스트리밍 연결](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=ko) 만들기 문서를 참조하십시오.
