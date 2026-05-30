---
title: 이벤트 전달
description: Edge Network을 통해 수집된 실시간 이벤트 데이터를 분석, 저장 또는 광고를 위한 Adobe이 아닌 대상으로 전달하는 방법을 알아봅니다.
solution: Experience Platform
exl-id: 24964d27-db56-4fa4-a79f-1b6750564b34
source-git-commit: 349d26f612d4002d1de3d27c7f893bd63ac467a3
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# 이벤트 전달

이 안내서에서는 [!DNL Adobe Experience Platform] Edge Network에서 서버측 처리를 사용하여 타사 분석 플랫폼, 클라우드 저장소 끝점, 광고 네트워크 또는 사용자 지정 웹후크와 같은 Adobe이 아닌 대상에 실시간 이벤트 데이터를 배포하는 이벤트 전달 사용 사례 패턴에 대해 설명합니다. 이 솔루션은 이러한 패턴의 기능, 지원하는 비즈니스 목표, 사용 가능한 전술적 사용 사례 및 관련된 Adobe 애플리케이션을 이해해야 하는 솔루션 설계자, 마케팅 기술자 및 구현 엔지니어를 위해 설계되었습니다.

## 사용 사례 패턴

이 섹션에서는 이벤트 전달을 구현하는 데 사용되는 패턴 및 실행 계획에 대해 설명합니다.

**이벤트 전달** - Edge Network을 통해 수집된 실시간 이벤트 데이터를 분석, 저장 또는 광고를 위한 Adobe 이외의 대상으로 전달합니다.

**실행 계획:** 데이터스트림 구성 > 이벤트 규칙 정의 > 대상 매핑 > 전달 실행 > 모니터링

## 사용 사례 개요

[!DNL Adobe Experience Platform] Web SDK, Mobile SDK 또는 Server API를 통해 동작 데이터를 수집하는 조직은 종종 [!DNL Google Analytics] 또는 [!DNL Snowflake]과(와) 같은 분석 플랫폼, 전환 추적을 위한 광고 네트워크, 장기 저장을 위한 데이터 웨어하우스 또는 사용자 지정 내부 서비스 등 Adobe이 아닌 시스템과 동일한 이벤트 스트림을 공유해야 합니다. 일반적으로 이러한 클라이언트측 태그의 증가는 페이지 가중치를 높이고, 지연을 초래하며, 개인 정보 및 거버넌스 위험을 만듭니다.

이벤트 전달은 Edge Network에서 서버측을 운영하여 이 문제를 해결합니다. 방문자 상호 작용이 웹 SDK 또는 서버 API를 통해 이벤트를 트리거하면 해당 이벤트는 데이터 스트림을 통해 Edge Network으로 라우팅됩니다. 전용 이벤트 전달 속성에 구성된 이벤트 전달 규칙은 들어오는 이벤트 데이터를 평가하여 하나 이상의 구성된 대상에 선택적으로 전달합니다. 이 서버측 접근 방식은 클라이언트측 태그 증가를 줄이고, 페이지 성능을 개선하며, 데이터 거버넌스를 중앙 집중화하고, 조직이 Adobe 에코시스템에서 나가는 데이터를 정확하게 제어할 수 있도록 합니다.

이 패턴의 대상 대상에는 데이터 수집을 위해 [!DNL Adobe Experience Platform] Web SDK 또는 서버 API를 이미 배포했거나 배포할 계획이며 클라이언트측 JavaScript 태그를 추가하지 않고 이벤트 데이터를 Adobe이 아닌 끝점에 배포하여 해당 투자를 연장하려는 조직이 포함됩니다.

## 주요 비즈니스 목표

이 사용 사례 패턴에서는 다음 비즈니스 목표가 지원됩니다.

### 데이터 품질 및 거버넌스 향상

정확하고 완벽하며 규정을 준수하는 데이터를 보장하여 정확한 타겟팅, 줄어든 낭비 및 안정적인 분석을 수행할 수 있습니다. 이벤트 전달은 서버측에서 데이터 배포를 중앙 집중화하여 조직에서 외부 시스템과 공유하는 데이터에 대한 단일 제어 지점을 제공하여 데이터 유출 위험을 줄이고 데이터가 [!DNL Adobe] Edge Network에서 나가기 전에 거버넌스 정책을 적용하도록 합니다.

**KPI:** 효율성, 비용 절감

자세한 내용은 [데이터 품질 및 거버넌스 개선](../../business-objectives/cost-efficiency/improve-data-quality-governance.md)을 참조하세요.

### 마케팅 기술 통합 및 현대화

확장성이 뛰어난 통합 플랫폼으로 마이그레이션하여 툴 조각화 및 기술적 부담 감소 이벤트 전달을 통해 조직은 여러 클라이언트측 공급업체 태그를 단일 서버측 데이터 배포 메커니즘으로 대체할 수 있으므로 페이지 로드 오버헤드가 줄어들고 기술 스택이 단순화됩니다.

**KPI:** 비용 절감, 효율성, 출시 속도

자세한 내용은 [마케팅 기술 통합 및 현대화](../../business-objectives/cost-efficiency/consolidate-modernize-marketing-technology.md)를 참조하십시오.

## 예시 전술 사용 사례

다음은 이러한 사용 사례 패턴이 적용되는 일반적인 전술적 시나리오입니다.

- **타사 분석 데이터 보강** — 페이지 보기, 클릭 및 전환 이벤트를 클라이언트측 태그를 추가하지 않고 실시간으로 [!DNL Google Analytics], [!DNL Snowflake] 또는 다른 분석 플랫폼으로 전달합니다
- **Advertising 전환 추적** — 서버 측 전환 측정 및 최적화를 위해 구매 및 리드 생성 이벤트를 [!DNL Meta] 전환 API, [!DNL Google Ads], [!DNL TikTok] 또는 [!DNL Snap]&#x200B;(으)로 보냅니다.
- **Data Warehouse 스트리밍** — 장기 저장 및 오프라인 분석을 위해 원시 이벤트 데이터를 클라우드 데이터 웨어하우스([!DNL Google BigQuery], [!DNL Amazon S3], [!DNL Azure Event Hubs])로 라우팅합니다.
- **사용자 지정 웹후크 통합** - 필터링되거나 변환된 이벤트 데이터를 HTTP 끝점을 통해 내부 마이크로서비스, CRM 시스템 또는 파트너 플랫폼으로 전달합니다.
- **태그 감소 및 페이지 성능 개선** — 여러 클라이언트측 공급업체 JavaScript 태그를 단일 웹 SDK 구현 및 서버측 이벤트 전달 규칙으로 대체하여 페이지 가중치를 줄이고 Core Web Vitals을 개선합니다.
- **개인 정보 보호 준수 데이터 공유** — 이벤트 데이터를 서드파티와 공유하기 전에 데이터 필터링 및 필드 수준 교정 규칙을 서버측에서 적용하여, 외부 시스템에 도달하기 전에 PII가 제거되거나 해시되도록 합니다
- **다중 클라우드 이벤트 배포** — 동일한 이벤트 스트림을 단일 서버측 규칙 집합에서 여러 대상(예: 분석, 광고 및 데이터 웨어하우스)으로 동시에 전달합니다.
- **실시간 사기 신호 전달** - 실시간 위험 점수 및 알림을 위해 가치가 높은 트랜잭션 이벤트를 사기 탐지 시스템으로 전달합니다.

## 주요 성과 지표

다음 KPI는 이 사용 사례 패턴의 성공을 측정하는 데 도움이 됩니다.

- **페이지 로드 시간 감소** — 클라이언트측 태그를 서버측 이벤트 전달로 마이그레이션한 후 페이지 로드 속도와 Core Web Vitals이 개선되었습니다.
- **데이터 배달 성공률** — 오류나 시간 초과 없이 대상 끝점에 성공적으로 전달된 이벤트의 비율
- **태그 수 감소** — 서버측 해당 태그를 구현한 후 제거된 클라이언트측 공급업체 태그의 수
- **데이터 새로 고침/지연** — 클라이언트의 이벤트 발생과 대상 끝점의 이벤트 도착 사이의 시간(대상: 초~초)
- **거버넌스 준수율** — 서버측 필터링 규칙을 통과하는 아웃바운드 데이터 공유의 백분율로, PII 또는 제한된 데이터가 승인되지 않은 대상에 도달하지 않도록 합니다.
- **운영 효율성** — 개발자가 클라이언트측 태그 배포 관리 및 태그 충돌 문제 해결에 소요하는 시간 감소

## 애플리케이션

이 사용 사례 패턴에는 다음 응용 프로그램이 사용됩니다.

- **[!DNL Adobe Experience Platform] (Edge Network)** - 구성된 데이터스트림을 통해 Web SDK, Mobile SDK 또는 Server API에서 실시간 이벤트 데이터를 수신하고 라우팅합니다.
- **[!DNL Adobe Experience Platform] (이벤트 전달)** — 이벤트 데이터를 평가, 필터링, 변환 및 외부 대상으로 전달하기 위한 서버측 규칙 엔진을 제공합니다.
- **[!DNL Adobe Experience Platform] (태그/데이터 수집)** — 이벤트 전달 속성 라이프사이클, 확장, 규칙 및 게시 워크플로우를 관리합니다.

## 관련 설명서

다음 리소스는 이 안내서에서 다루는 항목에 대한 추가 세부 정보를 제공합니다.

**이벤트 전달**

- [이벤트 전달 개요](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview)
- [이벤트 전달 시작](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started)
- [이벤트 전달 모니터링](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/monitoring)
- [이벤트 전달 비밀](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/secrets)

**이벤트 전달 확장**

- [서버측 확장 카탈로그](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/overview)
- [Adobe Cloud Connector 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/cloud-connector/overview)
- [Meta 전환 API 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/meta/overview)
- [Google Cloud Platform 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-cloud-platform/overview)
- [AWS 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/aws/overview)
- [Snowflake 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/snowflake/overview)
- [Google Ads Enhanced Conversions 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/google-ads-enhanced-conversions/overview)
- [Mailchimp 확장](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/server/mailchimp/overview)

**데이터 수집 및 Edge Network**

- [데이터스트림 구성](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)
- [데이터스트림 개요](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)
- [웹 SDK 개요](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home)
- [Edge Network 서버 API 개요](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview)
- [태그 개요](https://experienceleague.adobe.com/en/docs/experience-platform/tags/home)
