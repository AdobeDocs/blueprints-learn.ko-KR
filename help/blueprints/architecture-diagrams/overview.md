---
title: 아키텍처 다이어그램
description: 플랫폼 아키텍처, 대상 활성화, B2B 마케팅, 고객 통찰력 및 고객 여정을 다루는 Adobe Experience Platform 및 애플리케이션에 대한 시각적 아키텍처 및 데이터 흐름 참조 다이어그램입니다.
solution: Experience Platform
doc-type: overview-page
source-git-commit: 79738031788419872e32b8f754febacbfd18cc06
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%
---
# 아키텍처 다이어그램

아키텍처 다이어그램은 시스템 통합 지점, 데이터 및 콘텐츠 흐름, 작업 순서 등 Adobe Experience Platform과 애플리케이션이 어떻게 서로 연결되는지를 보여 주는 시각적, 기술적 참조입니다. [사용 사례 패턴](/help/blueprints/use-case-patterns/overview.md)의 단계별 지침으로 이동하기 전에 솔루션 디자인을 이해할 수 있습니다.

다이어그램은 다음 카테고리로 구성됩니다. 해당 범주의 랜딩 페이지 또는 리드 다이어그램으로 이동할 카드를 선택하십시오. 왼쪽 탐색을 사용하여 범주 내의 모든 다이어그램을 탐색할 수 있습니다.

<table style="table-layout:fixed; width:100%;">
<tr>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="architecture-overviews/overview.md">
      <img alt="아키텍처 개요" src="architecture-overviews/assets/aep_apps_overview.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="architecture-overviews/overview.md">
        <strong>아키텍처 개요</strong>
      </a>
      <p>Experience Cloud 애플리케이션, Experience Platform 및 배포 SDK를 함께 사용하는 방법과 보호 기능 및 지연 시간</p>
    </div>
  </td>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="audience-profile-activation/overview.md">
      <img alt="대상자 및 프로필 활성화" src="audience-profile-activation/assets/real_time_cdp_activation.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="audience-profile-activation/overview.md">
        <strong>대상자 및 프로필 활성화</strong>
      </a>
      <p>Adobe Real-Time CDP에서 대상과 프로필을 빌드하고 대상 및 애플리케이션에 활성화하는 방법입니다.</p>
    </div>
  </td>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="b2b-activation-marketing/overview.md">
      <img alt="B2B 활성화 및 마케팅" src="b2b-activation-marketing/assets/b2b-audience-profile-activation.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="b2b-activation-marketing/overview.md">
        <strong>B2B 활성화 및 마케팅</strong>
      </a>
      <p>채널 및 대상 전반에서 Real-Time Customer Data Platform B2B edition을 사용하여 계정 기반 및 사용자 기반 대상 활성화.</p>
    </div>
  </td>
</tr>
<tr>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="customer-insights/overview.md">
      <img alt="고객 인사이트" src="customer-insights/assets/cja.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="customer-insights/overview.md">
        <strong>고객 인사이트</strong>
      </a>
      <p>Customer Journey Analytics이 크로스 채널 행동 데이터를 통합 및 분석하고 Real-Time CDP 및 Journey Optimizer과 통합하는 방법입니다.</p>
    </div>
  </td>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;">
    <a href="customer-journeys/journey-optimizer/journey-optimizer-overview.md">
      <img alt="고객 여정" src="customer-journeys/journey-optimizer/images/ajo-architecture.png" style="display:block; width:100%; height:160px; object-fit:contain; background-color:#ffffff; border:1px solid #d3d3d3; padding:10px; box-sizing:border-box;" />
    </a>
    <div style="min-height:100px;">
      <a href="customer-journeys/journey-optimizer/journey-optimizer-overview.md">
        <strong>고객 여정</strong>
      </a>
      <p>Journey Optimizer을 통한 이벤트 기반 여정 오케스트레이션, Edge와 Hub에서의 의사 결정, Adobe Campaign을 통한 일괄 오케스트레이션.</p>
    </div>
  </td>
  <td style="width:33%; vertical-align:top; padding:10px; box-sizing:border-box;"></td>
</tr>
</table>

## 관련 콘텐츠

* [사용 사례 패턴](/help/blueprints/use-case-patterns/overview.md) - 이러한 아키텍처를 기반으로 하는 반복 가능한 구현 접근 방식
* [주요 비즈니스 목표](/help/blueprints/business-objectives/overview.md) - 이러한 아키텍처를 통해 달성할 수 있는 비즈니스 성과
* [업계 사용 사례](/help/blueprints/industry-use-cases/use-case-catalog.md) — 이러한 패턴의 수직적 응용 프로그램
