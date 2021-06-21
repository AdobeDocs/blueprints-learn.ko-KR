---
title: Adobe Experience Platform과 애플리케이션 아키텍처 다이어그램
description: 이 아키텍처 다이어그램은 Adobe Experience Platform과 다른 Adobe Experience Cloud 애플리케이션 및 애플리케이션 서비스 간의 관계를 보여 줍니다.
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Offer Decisioning, Real-time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 584007cc71e00729732c67a97546e2c21aed3f87
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 97%

---

# Adobe Experience Platform과 애플리케이션

## Adobe Experience Platform과 애플리케이션 아키텍처 다이어그램

이 아키텍처 다이어그램은 Adobe Experience Platform과 Adobe Experience Cloud 애플리케이션 및 애플리케이션 서비스 간의 관계를 보여 줍니다.

<img src="assets/aep+apps_vertical.svg" alt="Experience Platform과 애플리케이션" style="border:1px solid #4a4a4a; width:80%;" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## Adobe Experience Platform과 애플리케이션 상세 아키텍처 다이어그램

<img src="assets/aep+apps_horizontal.svg" alt="Experience Platform과 애플리케이션" style="border:1px solid #4a4a4a; width:80%;" />

## Adobe Experience Platform과 Experience Cloud 애플리케이션 통합

<table class="relative-table wrapped" style="width: 100%;" >
   <colgroup>
    <col style="width: 16.0202%;"/>
    <col style="width: 29.3423%;"/>
    <col style="width: 33.5582%;"/>
    <col style="width: 21.0793%;"/>
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
      <td colspan="1">현재 통합 없음</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=ko">익명 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=ko">온라인/오프라인 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=ko">Experience Platform과 애플리케이션을 사용한 활성화</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Analytics</td>
      <td>현재 통합 없음</td>
      <td>
        <ul>
          <li>Analytics에서 수집한 데이터를 Experience Platform 데이터 레이크 및 프로필 저장소로 보낼 수 있습니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=ko">Analytics 데이터 커넥터</a>
          </li>
        </ul>
      </td>
      <td>
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=ko">Experience Platform 데이터 흐름</a>
          </li>
        </ul>
        <p>
          <br/>
        </p>
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
          <li>수집 및 평가한 대상자 멤버십을 Experience Platform 데이터 레이크 및 프로필 저장소에 공유할 수 있습니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=ko">Audience Manager 소스 커넥터</a>
          </li>
        </ul>
      </td>
      <td>
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">익명 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">온라인/오프라인 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform과 애플리케이션을 사용한 활성화</a>
          </li>
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
          <li>Campaign에서 수집한 상호 작용 및 캠페인 데이터를 Experience Platform으로 보내면 Real-time Customer Data Platform을 통해 대상자를 구축하고 Customer Journey Analytics와 Experience Platform Query Service 및 Data Science Workspace를 통해 분석할 데이터 소스로 활용할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/batch-messaging.html?lang=en">일괄 메시지 처리</a>
          </li>
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
          <li>Campaign에서 수집한 상호 작용 및 캠페인 데이터를 Experience Platform으로 보내면 Real-time Customer Data Platform을 통해 대상자를 구축하고 Customer Journey Analytics와 Experience Platform Query Service 및 Data Science Workspace를 통해 분석할 데이터 소스로 활용할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/batch-messaging.html?lang=en">일괄 메시지 처리</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Customer Journey Analytics</td>
      <td colspan="1">
        <ul>
          <li>수집하여 Experience Platform 데이터 레이크로 가져온 데이터는 Customer Journey Analytics로 처리할 수 있습니다. </li>
        </ul>
      </td>
      <td colspan="1">현재 사용할 수 있는 통합이 없습니다. Customer Journey Analytics에서 Experience Platform으로 대상자 결과를 공유하는 방법이 로드맵에 있습니다.</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journey-analytics/overview.html?lang=en">Customer Journey Analytics</a>
          </li>
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
      <td colspan="1">Experience Manager 사이트에서 현재 수행하는 통합, 동작 및 상호 작용은 Experience Platform 웹 및 모바일 SDK를 통해 직접 수집되지 않습니다.</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">온라인/오프라인 대상자 활성화</a>
          </li>
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
          <li>Journey Optimizer에서 만든 상호 작용 및 캠페인 데이터를 Experience Platform으로 수집하여 Real-time Customer Data Platform을 통해 대상자를 구축하고 Customer Journey Analytics와 Experience Platform Query Service 및 Data Science Workspace를 통해 분석할 데이터 소스로 활용할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/customer-journeys/triggered-messaging.html?lang=en">트리거 메시지</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Magento</td>
      <td colspan="1">현재 통합 없음</td>
      <td colspan="1">현재 통합 없음</td>
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
          <li>Marketo 계정, 연락처 및 기회 데이터는 Marketo에서 만든 상호 작용 및 캠페인 데이터와 함께 Experience Platform으로 수집되어 B2B-CDP를 통한 대상자 구축과 Customer Journey Analytics, Experience Platform Query Service 및 Data Science Workspace를 통한 분석에 사용됩니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=ko">Marketo Engage 커넥터</a>
          </li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>B2B 활성화 - 개발 중</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Real-time CDP</td>
      <td colspan="1">
        <ul>
          <li>Experience Platform으로 수집한 데이터는 Real-time Customer Data Platform을 지원하는 실시간 고객 프로필을 만들기 위한 데이터 소스로 사용됩니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>대상자 및 프로필 지표는 Experience Platform 데이터 레이크로 전송되어 프로필 인사이트 보고 대시보드의 기반으로 활용됩니다.</li>
          <li>데이터 레이크의 대상자 및 프로필 데이터는 Query Service, Data Science Workspace 및 Customer Journey Analytics를 통해 더 많은 인사이트를 얻는 데 사용할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">온라인/오프라인 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform과 애플리케이션을 사용한 활성화</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Target</td>
      <td colspan="1">
        <ul>
          <li>Real-time Customer Data Platform에 정의된 대상자를 Target에 공유하여 Target에서 제공하는 개인화 및 타겟팅 경험에 사용할 수 있습니다. </li>
          <li>Experience Edge와 Target을 직접 통합하여 실시간 세그먼트 멤버십 및 프로필 속성에 액세스하는 방법이 로드맵에 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Target 경험 및 상호 작용에 대해 수집한 데이터는 Experience Platform 웹 SDK를 통해 Experience Platform으로 수집할 수 있습니다. 이 데이터는 Real-time Customer Data Platform을 통해 대상자를 구축하고 Customer Journey Analytics, Experience Platform Query Service 및 Data Science Workspace를 통해 분석하는 데 사용할 수 있습니다. </li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">온라인/오프라인 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform과 애플리케이션을 사용한 활성화</a>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
