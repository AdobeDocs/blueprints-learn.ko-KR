---
title: 다중 샌드박스 이벤트 전달 데이터 수집
description: Experience Platform Web 및 Mobile SDK로 수집한 데이터를 구성하여 단일 이벤트를 수집하고 여러 Experience Platform 샌드박스로 전달하는 방법을 알아봅니다.
solution: Data Collection
kt: 7202
exl-id: ecc94fc8-9fad-4b88-a153-3d0fc00d8d58
source-git-commit: 72eb4e2ff276279a2fc88ead0b17d77cc8e99b97
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 55%

---

# 다중 샌드박스 이벤트 전달 데이터 수집

이 블루프린트는 데이터가 [!DNL Experience Platform] 웹 및 모바일 SDK는 단일 이벤트를 수집하고 여러 AEP 샌드박스로 전달하도록 구성할 수 있습니다. 이 블루프린트는 이 목표를 달성하기 위해 [!UICONTROL 이벤트 전달]을 사용하는 다중 샌드박스 데이터 수집에만 적용됩니다.

[!UICONTROL 이벤트 전달] 기능을 사용하면 이벤트를 복제하는 것 외에도 기존에 수집한 데이터 중 다른 샌드박스의 요구 사항을 충족하는 데이터를 추가하거나 필터링하거나 조정할 수 있습니다.

[!UICONTROL 이벤트 전달] 기능은 사용자의 조건에 맞는 데이터를 구분하기 위해 [!UICONTROL 데이터 요소], [!UICONTROL 규칙] 및 [!UICONTROL 확장]을 포함하는 별도의 속성을 사용합니다. [!UICONTROL 이벤트 전달] 속성을 이용하면 이벤트가 들어올 때 전달 전에 필요에 따라 데이터를 수집하고 관리할 수 있습니다.

대상 샌드박스에 Adobe [!UICONTROL Cloud Connector] 확장에서 사용할 HTTP 스트리밍 엔드포인트가 구성되어 있어야 합니다.

## 사용 사례

* 전역 데이터 보고 - 여러 샌드박스를 사용하여 운영 환경을 분리하고 있으며 여러 샌드박스에 걸친 보고를 위해 데이터 수집을 단일 샌드박스로 통합해야 하는 경우. [!UICONTROL 이벤트 전달]을 통해 Experience Edge 이벤트를 보고 샌드박스로 라우팅하면 각 샌드박스 운영 환경에서 실시간으로 수집한 데이터를 그대로 보고 샌드박스로 보낼 수 있습니다.

* 각 샌드박스 운영 환경에 대한 다양한 데이터 규칙을 기반으로 샌드박스 간 데이터 수집을 관리합니다.

## 애플리케이션

* [!DNL Experience Platform] 데이터 수집
* [!UICONTROL 이벤트 전달]
* AEP [!UICONTROL 확장]
* [!UICONTROL Cloud Connector 확장]

## 고려 사항

여러 샌드박스에 데이터를 보내기 위한 방법으로 [!UICONTROL 이벤트 전달]을 사용하려면 솔루션 아키텍처와 관해 고려해야 할 사항이 있습니다.

### HIPAA 데이터 불가

[!UICONTROL 이벤트 전달] 는 HIPAA 준비로 간주되지 않으며 HIPAA 데이터가 수집되는 HIPAA 사용 사례에서 사용되어서는 안 됩니다.

하지만, 다음과 같은 용도로 사용되는 인프라 [!UICONTROL 이벤트 전달] 는 HIPAA 준비 상태로 간주되며 전적으로 고객의 재량에 따릅니다. [!UICONTROL 이벤트 전달] 태그 속성이 [!UICONTROL 이벤트 전달] 시스템에 있는 동안에 수집한 데이터 페이로드 전체는 처리를 위해 [!UICONTROL 이벤트 전달] 시스템으로 보내집니다. 이 프로세스는 다음을 수행합니다. [!UICONTROL 이벤트 전달] HIPAA 사용 사례에 대해 설명합니다. 전체 페이로드가 [!UICONTROL 이벤트 전달] 시스템, 이 프로세스에는 모든 HIPAA 값이 포함됩니다. 비록 [!UICONTROL 이벤트 전달] 규칙은 해당 데이터를 대상으로 보내기 전에 필터링하며 HIPAA 데이터는 여전히 비 HIPAA 준비 인프라에 제공됩니다. 그러나 페이로드 데이터는 저장되지 않으며 단순한 패스스루입니다.

### 서로 다른 데이터스트림과 스트리밍 엔드포인트

데이터가 의 데이터스트림을 통해 [!DNL Platform Edge Network], 사용 시 [!UICONTROL 이벤트 전달] 다른 AEP 샌드박스에서 요구 사항은 원래 컬렉션을 만드는 데이터스트림과 동일한 데이터스트림 또는 스트리밍 끝점을 사용하지 않는 것입니다. 이 경우 AEP 인스턴스가 손상될 수 있고, DoS 상황이 발생할 가능성이 있습니다.

### 예상 트래픽량

각 사용 사례를 검토할 때는 트래픽량을 알아야 합니다. 트래픽이 많으면 스로틀링 상황이 발생할 수 있고, 이 경우 고객에게 알림이 가기 때문에 미리 확인해 두는 것이 중요합니다.

## 아키텍처

![다중 샌드박스 [!UICONTROL 이벤트 전달]](assets/multi-sandbox-data-collection.png)

1. 이벤트 데이터를 수집하여 로 보내기 [!DNL Platform Edge Network] 을(를) 사용하려면 이 필수입니다. [!UICONTROL 이벤트 전달]. 클라이언트측 또는 의 Adobe 태그를 사용할 수 있습니다 [!DNL Platform Edge Network Server API] 서버 간 데이터 수집에 사용됩니다.

   다음 [!DNL Platform Edge Network API] 은 서버 간 컬렉션 기능을 제공할 수 있습니다. 그러나 이를 구현하려면 다른 프로그래밍 모델이 필요합니다. [Edge Network Server API 개요](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ko)를 참조하세요.

1. 수집된 페이로드는 태그 구현에서 [!DNL Platform Edge Network] (으)로 [!UICONTROL 이벤트 전달] 자체적으로 처리 및 처리되는 서비스 [!UICONTROL 데이터 요소], [!UICONTROL 규칙], 및 [!UICONTROL 작업]. 차이점에 대한 자세한 내용은 다음을 참조하십시오. [태그 및 [!UICONTROL 이벤트 전달]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko#differences-from-tags).

1. An [!UICONTROL 이벤트 전달] 속성은에서 수집된 이벤트 데이터를 받는 데에도 필요합니다. [!DNL Platform Edge Network]: 해당 이벤트 데이터가 [!DNL Platform Edge Network] 를 배포된 Tags 구현 또는 서버 간 컬렉션으로 만듭니다.

   작성자는 이벤트 데이터를 두 번째 샌드박스로 전달하기 전에 보강할 때 사용할 데이터 요소와 규칙, 작업을 정의합니다. 사용자 정의 코드 [!DNL JavaScript] 데이터 요소를 사용하여 데이터의 구조를 샌드박스 수집용으로 설정하는 과정을 지원하는 것도 고려해 볼 수 있습니다. 이 데이터 요소를 Platform 데이터 준비 기능과 결합하면 여러 방식 중 원하는 것으로 데이터 구조를 관리할 수 있습니다.

1. 현재는 [!UICONTROL 이벤트 전달] 속성 내에서 [!UICONTROL Cloud Connector 확장]을 사용해야 합니다. 규칙이 이벤트 데이터를 처리하거나 보강하면 [!UICONTROL 클라우드 커넥터] 페이로드를 두 번째 샌드박스로 전송하여 POST에 대해 구성된 가져오기 호출 내에서 사용됩니다.

1. 두 번째 샌드박스에는 데이터 수집을 위한 스트리밍 엔드포인트가 필요합니다. 다음을 고려할 수도 있습니다. [!UICONTROL 데이터 준비] 의 수집 및 매핑에 도움이 되는 AEP의 기능 [!UICONTROL 이벤트 전달] XDM에 대한 페이로드입니다. AEP 설명서의 [UI를 사용한 HTTP API 스트리밍 연결](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/streaming/http.html?lang=ko) 만들기 문서를 참고하세요.
