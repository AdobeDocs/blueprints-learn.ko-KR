---
title: Experience Platform(AEP) 및 애플리케이션 아키텍처 다이어그램
description: AEP(Adobe Experience Platform)가 다른 Experience Cloud 애플리케이션 및 애플리케이션 서비스와 어떻게 관련되는지를 보여 주는 아키텍처 다이어그램을 봅니다.
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Real-Time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 9fe44d93dcc05711c77ce1325b6549bb6c27a860
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 89%

---

# Adobe Experience Platform 및 애플리케이션 아키텍처 다이어그램

이러한 아키텍처 다이어그램은 Experience Platform(AEP)가 다른 Experience Cloud 애플리케이션 및 애플리케이션 서비스와 어떻게 관련되는지를 보여 줍니다.

>[!MORELIKETHIS]
>
>[Experience Cloud 응용 프로그램 통합을 위한 통합 구성](https://experienceleague.adobe.com/docs/integrations-learn/experience-cloud/overview.html?lang=en).


## 아키텍처 다이어그램

이 아키텍처 다이어그램은 Adobe Experience Platform과 Adobe Experience Cloud 애플리케이션 및 애플리케이션 서비스 간의 관계를 보여 줍니다.

<img src="assets/aep+apps.svg" alt="Experience Platform과 애플리케이션" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## 개요 다이어그램

<img src="assets/aep+apps_overview.svg" alt="Experience Platform과 애플리케이션" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## 자세한 아키텍처 다이어그램

<img src="assets/aep+apps_detailed.svg" alt="Experience Platform과 애플리케이션" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## AEP 및 Experience Cloud 애플리케이션 통합

<table class="relative-table wrapped" style="width: 100%;">
<colgroup>
<col style="width: 16.0202%;" />
<col style="width: 29.3423%;" />
<col style="width: 33.5582%;" />
<col style="width: 21.0793%;" />
</colgroup>
<tbody>
<tr>
<th>애플리케이션</th>
<th>Experience Platform에서 애플리케이션으로 통합</th>
<th>애플리케이션에서 Experience Platform으로 통합</th>
<th>관련 블루프린트</th>
</tr>
<tr>
<td colspan="1">Ad Cloud</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform에서 정의한 대상자를 Audience Manager를 통해 Ad Cloud에 공유하여 타겟팅할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>현재 통합 없음</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=ko">익명 대상자 활성화</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ko">알려진 고객 활성화</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=ko">Experience Platform과 애플리케이션을 사용한 활성화</a></li>
</ul>
</td>
</tr>
<tr>
<td>Analytics</td>
<td>
<ul>
<li>Web/Mobile SDK를 통해 수집한 데이터를 Adobe Analytics에 전송할 수 있습니다.</li>
</ul>
</td>
<td>
<ul>
<li>Analytics에서 수집한 데이터를 Experience Platform 데이터 레이크 및 프로필 저장소로 보낼 수 있습니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ko">Analytics 데이터 커넥터</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=ko">Experience Platform 데이터 흐름</a></li>
</ul>
</td>
</tr>
<tr>
<td>Audience Manager</td>
<td>
<ul>
<li>Real-time Customer Data Platform에서 정의한 대상자를 Audience Manager에 공유하여 타사 쿠키 대상에 대해 활성화할 수 있습니다.</li>
</ul>
</td>
<td>
<ul>
<li>수집 및 평가한 데이터는 Audience Manager에서 가져온 대상자 멤버십과 함께 Experience Platform 데이터 레이크 및 프로필 저장소에 공유할 수 있습니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ko">Audience Manager 소스 커넥터</a></li>
</ul>
</td>
<td>
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=ko">익명 대상자 활성화</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ko">알려진 고객 활성화</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=ko">Experience Platform과 애플리케이션을 사용한 활성화</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Classic</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform에서 정의한 대상자를 Campaign Classic에 공유하여 캠페인을 시작할 대상자로 사용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Campaign에서 수집한 상호 작용 및 캠페인 데이터를 Experience Platform으로 보내면 Real-time Customer Data Platform을 통해 대상자를 구축하고 Customer Journey Analytics와 Experience Platform Query Service를 통해 분석할 데이터 소스로 활용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=ko">고객 여정</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Campaign Standard</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform에서 정의한 대상자를 Campaign Standard에 공유하여 캠페인을 시작할 대상자로 사용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Campaign에서 수집한 상호 작용 및 캠페인 데이터를 Experience Platform으로 보내면 Real-time Customer Data Platform을 통해 대상자를 구축하고 Customer Journey Analytics와 Experience Platform Query Service를 통해 분석할 데이터 소스로 활용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/overview.html?lang=ko">고객 여정</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Customer Journey Analytics</td>
<td colspan="1">
<ul>
<li>수집하여 Experience Platform 데이터 레이크로 가져온 데이터는 Customer Journey Analytics로 처리할 수 있습니다. </li>
<li>Real-time Customer Data Platform의 프로필 및 대상 데이터를 CJA로 수집할 수 있습니다. <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-usecases/ingest-aep-segments.html?lang=ko">RTCDP와 CJA 통합</a>.
</li>
</ul>
</ul>
</td>
<td colspan="1">
<ul>
<li>Customer Journey Analtyics에서 대상자를 작성하고 그 결과로 나온 대상자를 Real-time Customer Data Platform에 공유합니다. <a href="https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/audiences/publish.html?lang=ko">CJA 대상자 게시</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=ko">Customer Journey Analytics</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Experience Manager</td>
<td colspan="1">
<ul>
<li>서버 측에서 Experience Platform 프로필에 직접 액세스하여 Experience Manager을 통한 개인화 경험 제공의 기반으로 사용할 수 있습니다. 개인화 활동은 보통 Experience Manager에서 Target 통합을 통해 게재합니다. </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Experience Manager 사이트에서 현재 수행하는 통합, 동작 및 상호 작용은 Experience Platform 웹 및 모바일 SDK를 통해 직접 수집되지 않습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ko">알려진 고객 활성화</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Journey Optimizer</td>
<td colspan="1">
<ul>
<li>Experience Platform으로 수집한 데이터 이벤트와 프로필은 Journey Optimizer에서 여정을 시작하고 강화하는 데 사용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Journey Optimizer에서 만든 상호 작용 및 캠페인 데이터를 Experience Platform으로 수집하여 Real-time Customer Data Platform을 통해 대상자를 구축하고 Customer Journey Analytics와 Experience Platform Query Service를 통해 분석할 데이터 소스로 활용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/journey-optimizer.html?lang=ko">Journey Optimizer</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Adobe Commerce</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform에 내장된 프로필 및 대상을 Adobe Commerce의 개인화에 사용할 수 있습니다. </li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Adobe Commerce 네이티브 데이터는 Adobe Commerce 소스 커넥터를 통해 Experience Platform으로 보낼 수 있습니다. </li>
</ul>
</td>
<td colspan="1">현재 통합 없음</td>
</tr>
<tr>
<td colspan="1">Marketo</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform에서 정의한 대상자를 Marketo에 공유하여 Marketo 캠페인을 시작하고 Marketo 개체를 업데이트할 대상자로 사용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Marketo 계정, 연락처 및 기회 데이터는 Marketo에서 만든 상호 작용 및 캠페인 데이터와 함께 Experience Platform으로 수집되어 B2B-CDP를 통한 대상자 구축과 Customer Journey Analytics, Experience Platform Query Service를 통한 분석에 사용됩니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=ko">Marketo Engage 커넥터</a></li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/b2b-activation/b2bactivation.html?lang=ko">B2B 활성화 블루프린트</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Real-Time CDP</td>
<td colspan="1">
<ul>
<li>Experience Platform으로 수집한 데이터는 Real-time Customer Data Platform을 지원하는 실시간 고객 프로필을 만들기 위한 데이터 소스로 사용됩니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>대상자 및 프로필 지표는 Experience Platform 데이터 레이크로 전송되어 프로필 인사이트 보고 대시보드의 기반으로 활용됩니다.</li>
<li>데이터 레이크의 대상자 및 프로필 데이터는 Query Service 및 Customer Journey Analytics를 통해 더 많은 인사이트를 얻는 데 사용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ko">알려진 고객 활성화</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=ko">Experience Platform과 애플리케이션을 사용한 활성화</a></li>
</ul>
</td>
</tr>
<tr>
<td colspan="1">Target</td>
<td colspan="1">
<ul>
<li>Real-time Customer Data Platform에서 정의한 대상자 및 프로필 속성을 Target에 공유하여 Target에서 제공하는 개인화 및 타겟팅 경험에 사용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li>Target 경험 및 상호 작용에 대해 수집한 데이터는 Experience Platform Web/Mobile SDK를 통해 Experience Platform으로 수집할 수 있습니다. 이 데이터는 Real-time Customer Data Platform을 통해 대상자를 구축하고 Customer Journey Analytics, Experience Platform Query Service를 통해 분석하는 데 사용할 수 있습니다.</li>
</ul>
</td>
<td colspan="1">
<ul>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/known-customer-audience-activation/known.html?lang=ko">알려진 고객 활성화</a></li>
<li><a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=ko">Experience Platform과 애플리케이션을 사용한 활성화</a></li>
</ul>
</td>
</tr>
</tbody>
</table>