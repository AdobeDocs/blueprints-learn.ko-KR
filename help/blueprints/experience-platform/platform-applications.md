---
title: Adobe Experience Platform과 애플리케이션 아키텍처 다이어그램
description: 이 아키텍처 다이어그램은 Adobe Experience Platform과 다른 Adobe Experience Cloud 애플리케이션 및 애플리케이션 서비스 간의 관계를 보여 줍니다.
solution: Experience Platform, Campaign, Analytics, Target, Customer Journey Analytics, Journey Orchestration, Offer Decisioning, Real-time Customer Data Platform
kt: 7199
thumbnail: null
exl-id: 9b12cd7a-5e5f-443a-91a1-44273cdabc2d
source-git-commit: 6c4b72159d4ba2a171215678e4e4842956d82745
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 11%

---

# Adobe Experience Platform과 애플리케이션

## Adobe Experience Platform과 애플리케이션 아키텍처 다이어그램

이 아키텍처 다이어그램은 Adobe Experience Platform과 Adobe Experience Cloud 애플리케이션 및 애플리케이션 서비스 간의 관계를 보여 줍니다.

<img src="assets/aep+apps_vertical.svg" alt="Experience Platform과 애플리케이션" style="border:1px solid #4a4a4a; width:80%;" />

>[!VIDEO](https://video.tv.adobe.com/v/32456/?quality=12&learn=on)

## Adobe Experience Platform과 애플리케이션 상세 아키텍처 다이어그램

<img src="assets/aep+apps_horizontal.svg" alt="Experience Platform과 애플리케이션" style="border:1px solid #4a4a4a; width:80%;" />

## Adobe Experience Platform 및 Experience Cloud 애플리케이션 통합

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
      <th>응용 프로그램에 Experience Platform</th>
      <th>Experience Platform에 애플리케이션</th>
      <th>관련 블루프린트</th>
    </tr>
    <tr>
      <td colspan="1">Ad Cloud</td>
      <td colspan="1">
        <ul>
          <li>실시간 고객 데이터 플랫폼에 정의된 대상은 Audience Manager을 통해 타깃팅하기 위해 Ad Cloud에 공유할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">현재 통합 없음</td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/anonymous.html?lang=en">익명 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">온라인/오프라인 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform 및 애플리케이션을 사용한 활성화</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Analytics</td>
      <td>현재 통합 없음</td>
      <td>
        <ul>
          <li>Analytics에서 수집한 데이터를 Experience Platform 데이터 레이크 및 프로필 저장소로 보낼 수 있습니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en">Analytics 데이터 커넥터</a>
          </li>
        </ul>
      </td>
      <td>
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-data-flow.html?lang=en">Experience Platform 데이터 흐름</a>
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
          <li>실시간 고객 데이터 플랫폼에 정의된 대상은 타사 쿠키 대상에 대한 활성화를 위해 Audience Manager에 공유할 수 있습니다.</li>
        </ul>
      </td>
      <td>
        <ul>
          <li>수집 및 평가된 대상 멤버십은 Experience Platform 데이터 레이크 및 프로필 스토어에 공유할 수 있습니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/audience-manager.html?lang=en">Audience Manager 소스 커넥터</a>
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
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform 및 애플리케이션을 사용한 활성화</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Campaign Classic</td>
      <td colspan="1">
        <ul>
          <li>실시간 고객 데이터 플랫폼에서 정의한 대상자는 캠페인을 시작할 대상으로 Campaign Classic에 공유될 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Campaign에서 수집한 상호 작용 및 캠페인 데이터는 Customer Journey Analytics 및 Experience Platform 쿼리 서비스 및 데이터 과학 작업 공간을 통해 실시간 고객 데이터 플랫폼을 통해 고객 구축 및 분석에 추가로 사용할 수 있도록 데이터 소스로 Experience Platform에 수집할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/batch-messaging.html?lang=en">일괄 메시징</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Campaign Standard</td>
      <td colspan="1">
        <ul>
          <li>실시간 고객 데이터 플랫폼에서 정의한 대상자는 캠페인을 시작할 대상으로 Campaign Standard에 공유될 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Campaign에서 수집한 상호 작용 및 캠페인 데이터는 Customer Journey Analytics 및 Experience Platform 쿼리 서비스 및 데이터 과학 작업 공간을 통해 실시간 고객 데이터 플랫폼을 통해 고객 구축 및 분석에 추가로 사용할 수 있도록 데이터 소스로 Experience Platform에 수집할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/batch-messaging.html?lang=en">일괄 메시징</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Customer Journey Analytics</td>
      <td colspan="1">
        <ul>
          <li>Experience Platform 데이터 레이크에 수집 및 수집된 데이터는 Customer Journey Analytics으로 처리할 수 있습니다.  </li>
        </ul>
      </td>
      <td colspan="1">현재 통합을 사용할 수 없습니다. Customer Journey Analytics의 Experience Platform에 대상 결과를 공유하는 기능이 로드맵에 있습니다.</td>
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
          <li>Experience Platform 프로필은 서버 측에 직접 액세스하여 Experience Manager을 통해 개인화된 경험을 제공할 수 있습니다. 개인화 활동은 가장 일반적으로 Target 통합을 통해 Experience Manager을 통해 전달됩니다.  </li>
        </ul>
      </td>
      <td colspan="1">Experience Manager 사이트에서 수행된 현재 통합, 동작 및 상호 작용은 Experience Platform 웹 및 모바일 SDK를 통해 직접 수집되지 않습니다.</td>
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
          <li>Journey Optimizer에서 Journey Optimizer을 시작하고 실행하는 데 여정에서 Experience Platform에 수집된 데이터 이벤트 및 프로필을 사용할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Journey Optimizer에서 만든 상호 작용 및 캠페인 데이터는 Customer Journey Analytics, Experience Platform 쿼리 서비스 및 데이터 과학 작업 공간을 통해 실시간 고객 데이터 플랫폼을 통해 대상 구축에 추가로 사용하기 위해 Experience Platform에 수집됩니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/multi-channel-message-orchestration/triggered-messaging.html?lang=en">트리거된 메시징</a>
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
          <li>실시간 고객 데이터 플랫폼에서 정의한 대상자는 Marketo 캠페인을 시작하고 Marketo 개체를 업데이트하는 대상으로 Marketo에 공유할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Marketo에서 만든 상호 작용 및 캠페인 데이터와 함께 Marketo 계정, 연락처 및 기회 데이터는 Customer Journey Analytics, Experience Platform 쿼리 서비스 및 데이터 과학 작업 공간을 통해 B2B-CDP를 통해 대상 빌드에 추가로 사용하기 위해 Experience Platform으로 수집됩니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=en">Marketo Engage 커넥터</a>
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
      <td colspan="1">실시간 CDP</td>
      <td colspan="1">
        <ul>
          <li>Experience Platform에 수집하여 수집된 데이터는 실시간 고객 데이터 플랫폼을 지원하는 실시간 고객 프로필을 어셈블하기 위한 데이터 소스입니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>대상 및 프로필 지표는 프로필 인사이트 보고 대시보드를 작동시키기 위해 Experience Platform 데이터 레이크로 전송됩니다.</li>
          <li>Data Lake의 대상 및 프로필 데이터는 Query Service, Data Science Workspace 및 Customer Journey Analytics을 통해 더 자세한 통찰력을 위해 사용할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">온라인/오프라인 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform 및 애플리케이션을 사용한 활성화</a>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td colspan="1">Target</td>
      <td colspan="1">
        <ul>
          <li>실시간 고객 데이터 플랫폼에 정의된 대상은 Target이 제공하는 개인화 및 타깃팅 경험에 공유되고 Target에 사용할 수 있습니다.  </li>
          <li>실시간 세그먼트 멤버십 및 프로필 속성 액세스를 위해 Experience Edge와 Target을 직접 통합할 수 있습니다.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>Target 경험 및 상호 작용에 대해 수집된 데이터는 Experience Platform 웹 SDK를 통해 Experience Platform에 수집할 수 있습니다. 이 데이터는 실시간 고객 데이터 플랫폼을 통해 대상 빌드에 사용되고 Customer Journey Analytics을 통해 분석하는 데 사용할 수 있습니다.  Experience Platform 쿼리 서비스 및 데이터 과학 작업 공간.</li>
        </ul>
      </td>
      <td colspan="1">
        <ul>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/online-offline.html?lang=en">온라인/오프라인 대상자 활성화</a>
          </li>
          <li>
            <a href="https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/platform-and-applications.html?lang=en">Experience Platform 및 애플리케이션을 사용한 활성화</a>
          </li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
