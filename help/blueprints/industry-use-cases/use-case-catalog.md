---
title: 사용 사례 카탈로그
description: 수직, 성숙 수준 또는 구현 패턴별로 업계 사용 사례를 탐색하여 Adobe Experience Platform 여정에 적합한 시작점을 찾습니다.
doc-type: overview-page
exl-id: 7a3c2f1e-9b4d-4e6a-8f5c-2d1b3a4e7c9f
source-git-commit: 8ad59ff130dae13553f10049eb685cf557a73ead
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 6%

---

# 사용 사례 카탈로그

[!DNL Adobe Experience Platform] 및 응용 프로그램에 대한 업계 사용 사례를 살펴봅니다. 업종별로 탐색하여 귀사의 수직적 사용 사례를 확인하거나, 성숙도 수준별로 탐색하여 조직에 적합한 시작점을 찾거나, 구현 패턴별로 탐색하여 요구 사항에 맞는 기술 접근 방식을 이해합니다.

각 사용 사례는 사용 사례를 구현하는 데 필요한 기능 체인, 의사 결정 지점 및 구성 단계를 설명하는 사용 사례 패턴을 통해 자세한 구현 안내로 연결됩니다.

## 업종별 찾아보기

>[!BEGINTABS]

>[!TAB 소매]

소매 조직은 [!DNL Adobe Experience Platform]을(를) 사용하여 온라인 상점, 실제 위치 및 고객 충성도 프로그램의 고객 데이터를 각 쇼핑객의 단일 보기로 통합합니다.

| | 사용 사례 | 설명 | 완성도 | 패턴 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="개인화된 제품 추천" width="40"> | [개인 맞춤화된 제품 추천](retail/retail-overview.md#personalized-product-recommendations) | 검색 및 구매 내역을 기반으로 개인화된 제품 표시 | [!BADGE 표시]{type=Informative} | [동작 권장 사항](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="포기한 장바구니" width="40"> | [포기한 장바구니 전자 메일 복구](retail/retail-overview.md#abandoned-cart-email-recovery) | 포기한 장바구니에 대해 개인화된 미리 알림 보내기 | [!BADGE 기본]{type=Neutral} | [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="재고 긴급도" width="40"> | [인벤토리 기반 긴급도 캠페인](retail/retail-overview.md#inventory-based-urgency-campaigns) | 제품 재고가 낮을 때 실시간 경고 트리거 | [!BADGE 기본]{type=Neutral} | [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="크로스셀 업셀" width="40"> | [교차 판매 및 상향 판매 권장 사항](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | 체크아웃 시 및 이메일에서 관련 크로스셀 및 업셀 제품 표시 | [!BADGE 고급]{type=Caution} | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="시작 시리즈" width="40"> | [새 고객 환영 시리즈](retail/retail-overview.md#new-customer-welcome-series) | 개인화된 추천을 통해 다중 이메일 환영 시리즈 자동화 | [!BADGE 표시]{type=Informative} | [여러 단계로 조정된 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="가격 하락" width="40"> | [가격 하락 경고](retail/retail-overview.md#price-drop-alerts) | 위시리스트 또는 조회한 항목의 가격이 하락하면 고객에게 알림 | [!BADGE 기본]{type=Neutral} | [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="보충" width="40"> | [보충 알림](retail/retail-overview.md#replenishment-reminders) | 정기적으로 구매하는 소모성 제품에 대한 자동 미리 알림 보내기 | [!BADGE 표시]{type=Informative} | [여러 단계로 조정된 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="범주 페이지" width="40"> | [개인 설정된 범주 페이지](retail/retail-overview.md#personalized-category-pages) | 각 고객의 기본 설정을 기반으로 하여 동적으로 카테고리 페이지 재정렬 | [!BADGE 표시]{type=Informative} | [동작 권장 사항](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="구매 후" width="40"> | [구매 후 후속 캠페인](retail/retail-overview.md#post-purchase-follow-up-campaigns) | 관리 팁 보내기, 검토 요청 및 관련 제품 제안 | [!BADGE 표시]{type=Informative} | [여러 단계로 조정된 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [VIP Customer Exclusive Offers](retail/retail-overview.md#vip-customer-exclusive-offers) | 독점 제공 및 고부가가치 고객에 대한 조기 액세스 제공 | [!BADGE 고급]{type=Caution} | [Decisioning을 사용한 크로스 채널 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |
| | [재고 부족 알림](retail/retail-overview.md#out-of-stock-notifications) | 품절된 제품을 사용할 수 있게 되면 고객에게 알림 | [!BADGE 기본]{type=Neutral} | [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [소셜 증명 Personalization](retail/retail-overview.md#social-proof-personalization) | 고객 프로필을 기반으로 개인화된 리뷰 및 등급 표시 | [!BADGE 표시]{type=Informative} | [알려진 방문자 웹/앱 Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB 금융 서비스]

금융 서비스 사용 사례가 곧 제공될 예정입니다. [현재 금융 서비스 사용 사례 보기](financial-services/financial-services-overview.md).

>[!TAB 의료 서비스]

의료 이용 사례가 곧 제공될 예정입니다. [현재 의료 서비스 사용 사례 보기](healthcare/healthcare-overview.md).

>[!TAB 자동차]

자동차 사용 사례가 곧 출시될 예정입니다. [현재 자동차 사용 사례 보기](automotive/automotive-overview.md).

>[!TAB 여행 및 접대]

여행 및 접대 사용 사례가 곧 제공될 예정입니다. [현재 여행 및 접대 사용 사례 보기](travel-hospitality/travel-hospitality-overview.md).

>[!TAB 통신]

통신 사용 사례가 곧 제공될 예정입니다. [현재 통신 사용 사례 보기](telecommunications/telecommunications-overview.md).

>[!TAB 미디어 및 엔터테인먼트]

미디어 및 엔터테인먼트 사용 사례가 곧 제공될 예정입니다. [현재 미디어 및 엔터테인먼트 사용 사례 보기](media-entertainment/media-entertainment-overview.md).

>[!TAB 보험]

보험 이용 사례가 곧 나올 예정입니다. [현재 보험 사용 사례 보기](insurance/insurance-overview.md).

>[!TAB B2B]

B2B 사용 사례가 곧 제공될 예정입니다. [현재 B2B 사용 사례 보기](b2b/b2b-overview.md).

>[!ENDTABS]

## 완성도 수준별 찾아보기

>[!BEGINTABS]

>[!TAB 기본]

단일 채널 제공을 통한 기본적이고 검증된 패턴 [!DNL Experience Platform] 여정을 시작하는 조직에 이상적인 시작점입니다.

| | 사용 사례 | 업계 | 비즈니스에 대한 영향 | 패턴 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="포기한 장바구니" width="40"> | [포기한 장바구니 전자 메일 복구](retail/retail-overview.md#abandoned-cart-email-recovery) | 리테일 | 25-35% 장바구니 복구율 | [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="재고 긴급도" width="40"> | [인벤토리 기반 긴급도 캠페인](retail/retail-overview.md#inventory-based-urgency-campaigns) | 리테일 | 전환 30-40% 증가 | [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="가격 하락" width="40"> | [가격 하락 경고](retail/retail-overview.md#price-drop-alerts) | 리테일 | 20-30% 전환율 | [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |
| | [재고 부족 알림](retail/retail-overview.md#out-of-stock-notifications) | 리테일 | 40-50% 전환율 | [이벤트 트리거된 메시징](/help/blueprints/use-case-patterns/campaign-management-orchestration/event-triggered-messaging.md) |

>[!TAB 표시]

AI 기반 개인화 및 오케스트레이션된 여정을 통해 기본 기능을 기반으로 하는 다중 채널 및 다중 단계 패턴입니다.

| | 사용 사례 | 업계 | 비즈니스에 대한 영향 | 패턴 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="제품 추천" width="40"> | [개인 맞춤화된 제품 추천](retail/retail-overview.md#personalized-product-recommendations) | 리테일 | CTR에서 20-30% 증가, 15-25% 전환 리프트 | [동작 권장 사항](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="범주 페이지" width="40"> | [개인 설정된 범주 페이지](retail/retail-overview.md#personalized-category-pages) | 리테일 | 참여 25-35% 증가 | [동작 권장 사항](/help/blueprints/use-case-patterns/personalization/behavioral-recommendation.md) |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="시작 시리즈" width="40"> | [새 고객 환영 시리즈](retail/retail-overview.md#new-customer-welcome-series) | 리테일 | 40-50%의 참여율 | [여러 단계로 조정된 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="보충" width="40"> | [보충 알림](retail/retail-overview.md#replenishment-reminders) | 리테일 | 30-40% 반복 구매율 | [여러 단계로 조정된 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="구매 후" width="40"> | [구매 후 후속 캠페인](retail/retail-overview.md#post-purchase-follow-up-campaigns) | 리테일 | 15-20% 검토율, 10-15% 반복 구매 | [여러 단계로 조정된 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/multi-step-orchestrated-journey.md) |
| | [소셜 증명 Personalization](retail/retail-overview.md#social-proof-personalization) | 리테일 | 전환율 10-15% 증가 | [알려진 방문자 웹/앱 Personalization](/help/blueprints/use-case-patterns/personalization/known-visitor-web-app-personalization.md) |

>[!TAB 고급]

가장 정교한 고객 경험을 위한 실시간 의사 결정 및 AI 기반 오퍼 선택을 통한 크로스 채널 오케스트레이션.

| | 사용 사례 | 업계 | 비즈니스에 대한 영향 | 패턴 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="크로스셀 업셀" width="40"> | [교차 판매 및 상향 판매 권장 사항](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | 리테일 | AOV에서 25-75달러 증가, 10-15% 매출 향상 | [Offer Decisioning](/help/blueprints/use-case-patterns/personalization/offer-decisioning.md) |
| | [VIP Customer Exclusive Offers](retail/retail-overview.md#vip-customer-exclusive-offers) | 리테일 | VIP의 50-70% 참여 비율 | [Decisioning을 사용한 크로스 채널 여정](/help/blueprints/use-case-patterns/campaign-management-orchestration/cross-channel-journey-with-decisioning.md) |

>[!ENDTABS]

## 구현 패턴별 찾아보기

>[!BEGINTABS]

>[!TAB 캠페인 관리 및 오케스트레이션]

### 이벤트 트리거된 메시징

적시에 단일 채널 메시지로 실시간 행동 이벤트에 응답합니다.

| | 사용 사례 | 업계 | 완성도 | 비즈니스에 대한 영향 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-abandoned-cart.png" alt="포기한 장바구니" width="40"> | [포기한 장바구니 전자 메일 복구](retail/retail-overview.md#abandoned-cart-email-recovery) | 리테일 | [!BADGE 기본]{type=Neutral} | 25-35% 장바구니 복구율 |
| <img src="assets/use-case-icons/icon-inventory-urgency.png" alt="재고 긴급도" width="40"> | [인벤토리 기반 긴급도 캠페인](retail/retail-overview.md#inventory-based-urgency-campaigns) | 리테일 | [!BADGE 기본]{type=Neutral} | 전환 30-40% 증가 |
| <img src="assets/use-case-icons/icon-price-drop.png" alt="가격 하락" width="40"> | [가격 하락 경고](retail/retail-overview.md#price-drop-alerts) | 리테일 | [!BADGE 기본]{type=Neutral} | 20-30% 전환율 |
| | [재고 부족 알림](retail/retail-overview.md#out-of-stock-notifications) | 리테일 | [!BADGE 기본]{type=Neutral} | 40-50% 전환율 |

### 여러 단계로 조정된 여정

고객의 참여도와 행동에 따라 적응하는 멀티 터치 시퀀스를 안내합니다.

| | 사용 사례 | 업계 | 완성도 | 비즈니스에 대한 영향 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-welcome-series.png" alt="시작 시리즈" width="40"> | [새 고객 환영 시리즈](retail/retail-overview.md#new-customer-welcome-series) | 리테일 | [!BADGE 표시]{type=Informative} | 40-50%의 참여율 |
| <img src="assets/use-case-icons/icon-replenishment.png" alt="보충" width="40"> | [보충 알림](retail/retail-overview.md#replenishment-reminders) | 리테일 | [!BADGE 표시]{type=Informative} | 30-40% 반복 구매율 |
| <img src="assets/use-case-icons/icon-post-purchase.png" alt="구매 후" width="40"> | [구매 후 후속 캠페인](retail/retail-overview.md#post-purchase-follow-up-campaigns) | 리테일 | [!BADGE 표시]{type=Informative} | 15-20% 검토율, 10-15% 반복 구매 |

### Decisioning을 사용한 크로스 채널 여정

모든 터치포인트에서 실시간 오퍼 결정을 통해 크로스 채널 경험을 조정합니다.

| | 사용 사례 | 업계 | 완성도 | 비즈니스에 대한 영향 |
| --- | --- | --- | --- | --- |
| | [VIP Customer Exclusive Offers](retail/retail-overview.md#vip-customer-exclusive-offers) | 리테일 | [!BADGE 고급]{type=Caution} | VIP의 50-70% 참여 비율 |

>[!TAB Personalization]

### 행동 추천

AI 기반 모델을 사용하여 행동 신호를 기반으로 개인화된 콘텐츠와 제품을 표시할 수 있습니다.

| | 사용 사례 | 업계 | 완성도 | 비즈니스에 대한 영향 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-product-recommendations.png" alt="제품 추천" width="40"> | [개인 맞춤화된 제품 추천](retail/retail-overview.md#personalized-product-recommendations) | 리테일 | [!BADGE 표시]{type=Informative} | CTR에서 20-30% 증가, 15-25% 전환 리프트 |
| <img src="assets/use-case-icons/icon-category-pages.png" alt="범주 페이지" width="40"> | [개인 설정된 범주 페이지](retail/retail-overview.md#personalized-category-pages) | 리테일 | [!BADGE 표시]{type=Informative} | 참여 25-35% 증가 |

### Offer Decisioning

중앙 집중식 의사 결정 논리를 사용하여 각 고객 및 컨텍스트에 가장 적합한 오퍼를 평가하고 선택합니다.

| | 사용 사례 | 업계 | 완성도 | 비즈니스에 대한 영향 |
| --- | --- | --- | --- | --- |
| <img src="assets/use-case-icons/icon-cross-sell-upsell.png" alt="크로스셀 업셀" width="40"> | [교차 판매 및 상향 판매 권장 사항](retail/retail-overview.md#cross-sell-and-upsell-recommendations) | 리테일 | [!BADGE 고급]{type=Caution} | AOV에서 25-75달러 증가, 10-15% 매출 향상 |

### 알려진 방문자 웹/앱 Personalization

프로필, 환경 설정 및 검색 컨텍스트를 기반으로 식별된 방문자에 대한 웹 및 앱 컨텐츠를 개인화합니다.

| | 사용 사례 | 업계 | 완성도 | 비즈니스에 대한 영향 |
| --- | --- | --- | --- | --- |
| | [소셜 증명 Personalization](retail/retail-overview.md#social-proof-personalization) | 리테일 | [!BADGE 표시]{type=Informative} | 전환율 10-15% 증가 |

>[!ENDTABS]
