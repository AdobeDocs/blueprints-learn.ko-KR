---
title: 고객 활동 허브 블루프린트
description: 직원이 관여하는 지원 및 영업의 맥락을 제공하는 [!UICONTROL Real-time Customer Profile] 확인 블루프린트입니다.
solution: Data Collection
kt: 7195
exl-id: 3616cbf1-2e59-4e68-a1ff-1d2e3b344a1c
source-git-commit: 5110ee2a7a079945475055cbcfdabf7cdcaa0ab5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 고객 활동 허브 블루프린트

고객 활동 허브 블루프린트에서는 외부 애플리케이션에서 Adobe Experience Platform의 [!UICONTROL 실시간 고객 프로필]에 액세스하는 방법을 보여 줍니다.

외부 애플리케이션에서는 API GET 요청을 통해 프로필에 액세스할 수 있습니다. 이렇게 하면 해당 프로필 내에 저장된 속성, 이벤트, 세그먼트 멤버십 및 모델 기반 특성을 해당 Adobe 외부 애플리케이션에서 사용할 수 있습니다.

이를 통해 고객의 콜센터 문의에 대해 풍부한 맥락을 표면화할 수 있습니다. 예를 들면 지원 담당자가 고객의 생애 가치, 이탈 경향 또는 어떤 마케팅 캠페인에 노출되었는지 등을 확인할 수 있습니다. 영업 담당자도 고객에 대해 맥락 또는 인사이트를 얻어 활용할 수 있습니다.

>[!NOTE]
>
>프로필 확인 API에서 현재 제공하는 대기 시간은 약 500ms이므로, 이 방법은 해당 프로필을 동일 페이지 웹 또는 모바일 개인화 등의 실시간 의사결정 엔진과 통합하기에는 적합하지 않습니다.

## 사용 사례

* 지원 및 영업 경험 등 직원이 관여하는 상호 작용에 대해 보다 자세한 고객의 맥락을 제공합니다. Experience Platform에서 프로필 확인 기능을 사용하면 담당자가 소비자에 대해 실시간 고객 프로필에 저장된 최근 구매, 캠페인 상호 작용, 성향, 대상자 멤버십 및 기타 속성과 인사이트 등 더 많은 맥락을 확인할 수 있습니다.

## 아키텍처

<img src="assets/customer_activity_hub.svg" alt="고객 활동 허브 블루프린트를 위한 참조 아키텍처" style="width:90%; border:1px solid #4a4a4a"  class="modal-image" />

## 가드레일

* [[!UICONTROL Real-time Customer Profile] 데이터에 적용되는 가드레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)

## 구현 단계

1. 수집할 데이터를 위한 [스키마를 만듭니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=ko)
1. 수집할 데이터를 위한 [데이터 세트를 만듭니다.](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=ko)
1. 수집한 데이터를 통합 프로필로 결합할 수 있도록 스키마에 [올바른 ID와 ID 네임스페이스를 구성합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html?lang=ko).
1. [프로필에 대해 스키마와 데이터 세트를 활성화합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html?lang=ko).
1. 데이터를 Experience Platform으로 [수집합니다.](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion&amp;lang=ko)
1. [병합 정책을 설정합니다](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html?lang=ko).
1. [항목 API를 사용하여 프로필 속성을 확인합니다](https://experienceleague.adobe.com/docs/experience-platform/profile/api/entities.html?lang=ko). 기록 항목 또는 경험 이벤트 항목에서 가져올 수 있습니다.

## 관련 설명서

* [Adobe Experience Platform Activation 제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions/adobe-experience-platform0.html)
* [[!UICONTROL Real-time Customer Profile] 설명서](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=ko)
* [프로필 가드레일](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* [프로필 확인 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)
