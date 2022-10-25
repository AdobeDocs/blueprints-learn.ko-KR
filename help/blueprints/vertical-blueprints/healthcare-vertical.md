---
title: 의료
description: Real-Time CDP, Customer Journey Analytics 및 Adobe Journey Optimizer과 같은 플랫폼 기반 애플리케이션에 대한 Adobe Experience Platform 추가 기능인 Healthcare Shield에 대해 알아보십시오. 추가 기능을 사용하면 이러한 애플리케이션이 HIPAA 및 PHI 요구 사항에 부합할 수 있습니다.
solution: Experience Platform
source-git-commit: a7dd0634533110859500e2dab63779014f8cf9b9
workflow-type: tm+mt
source-wordcount: '2367'
ht-degree: 1%

---

# 의료 보호

Healthcare Shield는 Real-time Customer Data Platform, Customer Journey Analytics 및 Adobe Journey Optimizer과 같은 Adobe Experience Platform 기반 애플리케이션에 대한 Adobe Experience Platform 추가 기능입니다. PHI(Protected Health Information)의 처리 및 사용에 관한 요구 사항을 충족하도록 HIPAA 애플리케이션을 구축했습니다.

## Healthcare Shield에 대한 FAQ

다음 FAQ는 Healthcare Shield에 대한 일반적인 질문에 대한 답변을 제공합니다.

### HIPAA란 무엇입니까?

HIPAA는 건강 보험 휴대와 책임 법안 입니다. 그것은 비즈니스를 위한 중요한 보호를 설정하는 미국의 규정입니다. 이러한 보호 기능은 HIPAA 적용 개체 또는 비즈니스 동료(예: Adobe 고객)가 비즈니스 관련(Adobe 등 기술 파트너)에 생성, 수신, 유지 관리 또는 전송할 때 PHI(보호된 상태 정보)의 사용 및 공개를 제한합니다.

Adobe은 특정 HIPAA-Ready Adobe 솔루션 및 HIPAA 보안, 개인 정보 보호 및 Breaking Notification 규칙을 준수하기 위한 비즈니스 파트너로서 HIPAA를 사용하고 있습니다.

### BAA(Business Associate Agreement)란 무엇이며 중요한 이유는 무엇입니까?

Covered Entity 또는 Business Associate(Adobe 고객)가 Business Associate의 서비스를 사용하여 PHI(Protected Healthcare Data) 또는 ePHI(Electronic Version of PHI)인 특정 유형의 소비자 데이터를 생성, 수신, 유지 관리 또는 전송하는 경우 BAA(Business Associate Agreement)를 체결해야 합니다.

BAA는 계약상 HIPAA 개인 정보 보호, 보안 및 위반 통지 규칙의 요구 사항을 준수하여 PHI를 적절히 보호해야 하므로 Adobe이 필요합니다.

Real-Time CDP용 Healthcare Shield 추가 기능을 사용하면 이제 Adobe은 Adobe Real-Time CDP B2C 및 Adobe Real-Time CDP B2P Edition의 소비자 흐름과 함께 이 기능을 사용하는 고객과 함께 BAA를 실행할 수 있습니다.

### Healthcare Shield for Real-Time CDP(및 향후 플랫폼 기반 애플리케이션)가 미국에서만 제공되는 이유는 무엇입니까?

HIPAA는 미국 법이므로, Hipaa는 미국 및 HIPAA의 적용을 받는 기업에 대해 Healthcare Shield의 가용성을 제한하고 있습니다. Adobe은 지역 요구 사항을 확장하고 이를 충족할 수 있다고 확신함에 따라 다른 관할구역으로 범위를 확장할 것입니다.

### Real-Time CDP의 Healthcare Shield란 무엇입니까?

Healthcare Shield for Real-Time CDP은 Covered Entity 또는 Business Associate를 운영하고 있으며 데이터 수집, 대상 생성 및 크로스 채널 활성화를 위해 Real-Time CDP에서 PHI를 사용하고 BAA를 실행하기 위해 Adobe을 사용하려는 고객을 위한 것입니다. 실시간 CDP를 위해 HIPAA를 사용해야 하는 Cover Entity에 Healthcare Shield가 필요합니다.

### Real-Time CDP의 의료 잠재 고객이 Healthcare Shield를 구매해야 하는 이유는 무엇입니까?

Real-Time CDP의 추가 기능으로서 Healthcare Shield는 애플리케이션을 &quot;HIPAA-ready&quot; 상태로 업그레이드합니다. 즉, 애플리케이션은 HIPAA 요구 사항에 따라 PHI를 사용할 수 있는 보호 기능을 갖추고 있습니다. 또한 Healthcare Shield를 통해 Adobe은 고객이 특정 유형의 허용된 중요 개인 데이터를 HIPAA 지원 애플리케이션에 가져올 수 있도록 권한을 부여하고 있습니다. Adobe은 호환되는 플랫폼 기반 응용 프로그램에 대해 Healthcare Shield를 라이선스를 제공하는 고객과 BAA(Business Associate Agreements)에 서명합니다.

### Healthcare Shield를 사용하는 Real-Time CDP에 대해 허용되는 데이터 유형은 무엇입니까(및 그렇지 않은 데이터 유형은 무엇입니까?)

Healthcare Shield를 통해 브랜드는 Real-Time CDP(허용된 중요 개인 데이터)와 같은 플랫폼 기반 애플리케이션에 다음과 같은 PHI를 도입할 수 있습니다.

* 개인의 재무 정보
* 의료
* 상태 정보

그러나 Adobe는 특히 아동 학대, 정신 건강, 유전자 건강 기록 또는 미성년자, 전체 계좌 번호, 전체 신용 카드 번호, 정부 식별자(예: SSN) 및 개인 정보 등의 건강 기록을 식별하는 데이터는 제외합니다. 아동은 모든 아동보호법(COPPA(Us Children&#39;s Online Privacy Act)에 정의된 개인 정보 등)에 따라 보호됩니다.

### Healthcare Shield를 통해 Real-Time CDP 고객은 모든 유형의 PHI를 사용하여 대상을 구축하고 활성화할 수 있습니까?

고객이 허용된 중요한 개인 데이터를 플랫폼 기본 애플리케이션으로 가져올 수 있더라도 고객은 의도한 방식으로 데이터를 사용할 수 있는 적절한 권한, 동의, 허가 및 승인을 얻을 수 있는 모든 해당 규정을 준수할 책임이 있음을 이해해야 합니다.

### HIPAA가 아닌 Adobe 애플리케이션을 사용하여 고객 데이터를 수집하고 활성화하는 뉘앙스는 무엇입니까?

고객 라이센스 의료 보호 서비스는 허가된 중요 개인 데이터를 HIPAA 전용 Adobe 애플리케이션 및 서비스와 사용, 수집, 수집, 공유 또는 통합할 수 없습니다.

예를 들어, 고객은 Audience Manager, Adobe Target, Adobe Analytics 등의 애플리케이션에서 PHI가 포함된 세그먼트를 활성화해서는 안 됩니다. Healthcare Shield 라이센스 고객은 데이터 소스가 HIPAA로 간주되는지 여부에 관계없이 HIPAA 지원 Adobe 애플리케이션에 허용된 중요 개인 데이터 또는 인증된 PHI를 수집할 수 있습니다.

### HIPAA가 아닌 Adobe이 아닌 애플리케이션을 사용하여 고객 데이터를 수집하고 활성화하는 뉘앙스는 무엇입니까?

고객 라이센스 Healthcare Shield는 Adobe 애플리케이션 외부에서 PHI가 포함된 세그먼트를 활성화하는 위치를 파악하기 위해 올바른 판단을 따라야 합니다. Adobe은 고객 스키마의 Adobe 데이터 사용 레이블에 따라 데이터 처리를 지원하지 않을 수 있는 타사 공급자 및 고객에 대한 데이터를 제어하지 않고, 책임을 지지 않습니다. 또한 Adobe은 고객에게 법률적인 조언을 제공할 수 없습니다.

## 주요 의료 보호 활용 사례

![RTCDP를 사용한 사용 사례](assets/use-cases.png)

| RTCDP B2C Edition Standard 사용 사례 | 설명 |
|-----|-----|
| 스트리밍 데이터 수집 | <ul><li>Adobe 및 비Adobe 연결에서 사용할 수 있는 정규화된 유연한 데이터 모델<li>B2C 마케팅을 위해 설계된 개인 및 계정 기반 데이터 스키마.<li>태그 관리 및 이벤트 전달 은 이벤트 수준 데이터를 실시간으로 수집하고 배포합니다.<li> 경험 전달을 가속화하는 최적화된 프로필입니다.</li></ul> |
| 신뢰할 수 있는 프로필 관리 | <ul><li>소비자 속성, 행동 및 기본 설정 데이터를 포함하는 통합 프로필.<li> 데이터 거버넌스 프레임워크는 유연하고 투명하며 정책 생성 및 자동 적용을 통해 통합 프로필에 적용되어 데이터 오용을 방지할 수 있습니다. </li></ul> |
| 실시간 활성화 | <ul><li>B2C 마케터를 위해 설계된 드래그 앤 드롭 세그멘테이션.<li>크로스 채널 활성화를 위한 개인 및 계정 수준 ID 확인 및 프로필 보강<li> 채널 및 환경(Adobe 및 비Adobe)에서 Audience Orchestration과 실시간 활성화를 통한 일관된 고객 경험.</li></ul> |
| 고객 확보 | <ul><li>인증되지 않은 사용자를 인식된/인증된 사용자로 전환하기 위한 통찰력.<li>등록되지 않은 사용자가 멤버십에 등록하도록 장려합니다.<li> 구독을 늘리거나 다시 늘리십시오.<li> 고객 프로필을 분석하여 성향(예: . 높은 값 세그먼트를 성과가 낮은 세그먼트와 비교하고 획득을 최적화합니다.</li></ul> |
| 고객 참여 | <ul><li>Target 오퍼은 오퍼의 최신성 및 빈도(온라인 및 오프라인)를 기반으로 합니다.<li>연결된 경험에 대한 디지털 속성을 통합합니다(예: 모바일 앱 다운로드를 장려하고 채널 간에 세그먼트 활성화를 사용하여 경험을 연결합니다).</li></ul> |
| 규모에 따른 개인화 | <ul><li> 실시간으로 동일한 페이지 및 다음 페이지 개인화를 위해 에지에서 세그먼트를 평가합니다.<li>여정 간에 세션을 포기한 방문자에게 고유하고 타깃팅된 경험을 제공하여 참여를 늘립니다(예: 장바구니 포기, 전환하지 않은 재방문자).<li> 오프라인 및 온라인 행동을 통합하고 연결하여 사용자를 최적화하고 참여시킵니다.</li></ul> |
| 크로스셀 / 업셀 | <ul><li>기존 사용자와 고객의 관계를 지속적으로 유지하고 성장하면서 고객을 유지합니다.<li>교차 비즈니스 단위/브랜드/오퍼로 새로운 수익 흐름을 창출하여 고객 생애 가치를 높일 수 있습니다.<li>제품 및 SKU에서 AOV에 대한 통찰력을 얻을 수 있습니다(예: 잦은 번들, 가격 민감도).</li></ul> |
| 고객 유지/충성도 | <ul><li> 고객을 다시 활성화하여 충성도를 유도하고 고객 이탈을 방지합니다&lt;.li>환경 설정과 성향 기반으로 고부가가치 고객을 위한 개인화된 제품 추천을 조정합니다.<li>충성스런 고객을 위한 참여 및 특별 오퍼에 대한 표준 케이던스를 만듭니다.<li> 온라인 및 오프라인 환경 설정을 연결하여 여러 채널에서 오퍼를 최적화합니다.</li></ul> |
| 데이터 공동 작업 | <ul><li> UI 내에서 핸드셰이크를 만들어 데이터 공동 작업 워크플로우를 빌드할 수 있습니다.<li>(업계 전반에서 자사 데이터가 중복되는 것을 활용하여 전략적 비즈니스 의사 결정 및 캠페인을 설명합니다.<li>데이터 사일로를 분류하고 전체적인 고객 여정을 이해합니다.<li> 사용 사례별로 환경 설정 및 동의를 처리합니다.</li></ul> |
| 미디어/마케팅 효율성 및 최적화 | <ul><li> 하나의 기록 시스템에서 고객 데이터 및 활성화 채널을 중앙 집중화 및 유지하여 조직의 효율성을 높일 수 있습니다.<li>효과적인 미디어 비용/효율성을 위한 억제 캠페인을 지원합니다.<li> 정부 및 정책 집행을 통해 IT 정책에 부합합니다.<li>필요한 경우 실시간으로 데이터에 액세스하여 적시에 캠페인을 지원할 수 있습니다.</li></ul> |

## 관련 기술 기능

![실시간 cdp](assets/real-time-cdp.png)

### 차이점

| 유형 | 즉시 사용 가능 | 의료 보호 |
|-----|-----|-----|
| 암호화 | [AEP의 데이터 암호화](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html?lang=en) | [AEP의 데이터 암호화](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html?lang=en) + 고객 관리 키 |
| 데이터 위생 | **기본:** 고객이 데이터의 라이프사이클을 관리할 수 있는 셀프서비스 도구입니다. 여기에는 고객 데이터 삭제, 필드 수준 업데이트 및 데이터 세트에 대한 데이터 만료 설정이 포함됩니다. 이 경우 데이터가 만료되면 데이터를 제거합니다.<ul><li>제한 **10,000개의 삭제 요청** 월별<li>데이터 집합 TTL 2개 제한</li></ul> | **Premium**: 데이터 위생 기능의 일별 용량/임계값을 확장하여 짧은 시간에 더 큰 데이터 세트를 조정합니다.<ul><li>제한 **2,000,000개의 삭제 요청** HealthCare Shield의 일부로 매월<li>데이터 집합 TTL 20개 제한</li></ul> |
| 동의 | **기본**: 대상 세그멘테이션에 동의 및 기본 설정 관련 특성을 수동으로 추가하여 세분화된 동의 및 환경 설정을 지정합니다. | **Premium**: 동의 및 기본 설정을 기반으로 고객 데이터 사용 방법에 대한 정책을 만들고 자동으로 적용합니다. |

### 거버넌스

**데이터 위생**

* [데이터 위생 개요](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-hygiene/overview.html?lang=en)
* [Adobe Experience Platform 데이터 위생](https://experienceleague.adobe.com/docs/experience-platform/hygiene/home.html?lang=en)

**정책 적용**

* [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en)
* [데이터 사용 정책 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en)
* [Adobe Experience Platform의 거버넌스, 개인 정보 및 보안](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/overview.html?lang=en#consent)

### 개인 정보 보호

**동의**

* [자동 정책 적용](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html?lang=en#consent-policy-evaluation)

### 보안

**향상된 암호화**

유용한 링크:

* [AEP 보안 백서](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf)

* [Adobe Experience Platform의 데이터 암호화](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html)

* [데이터 준비의 해시 함수](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html?lang=en#hashing)

* [태그 데이터 암호화](https://experienceleague.adobe.com/docs/experience-platform/tags/api/guides/encrypting-values.html?lang=en)

**액세스 제어**

* [속성 기반 액세스 제어 개요](https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/overview.html)

**사용자 활동 감사**

* [감사 로그](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html)

**향상된 암호화**

* [Adobe Experience Platform 보안 개요](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf)
* [값 암호화](https://experienceleague.adobe.com/docs/experience-platform/tags/api/guides/encrypting-values.html?lang=en)
* [Adobe Experience Platform의 데이터 암호화](https://experienceleague.adobe.com/docs/experience-platform/catalog/data-protection.html)
* [데이터 준비 매핑 함수 - 해시](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html?lang=en#hashing)

**Experience Cloud**

* [Adobe Real-time Customer Data Platform 및 Healthcare Shield](https://experienceleague.adobe.com/docs/customer-data-management-voices-events/events/governance/healthcare-shield.html?lang=en)

   적은 데이터에 대한 액세스 권한을 통해 경험 약속을 이행합니다. 이 비디오에서는 Adobe Experience Platform 기반 애플리케이션에 대한 Adobe Experience Platform 추가 기능인 Adobe Real-Time CDP 및 Healthcare Shield에 대해 자세히 알아보십시오. Hipaa는 이러한 애플리케이션을 준비하고 PHI(Protected Health Data)의 처리 및 사용과 관련된 HIPAA 요구 사항을 충족하도록 설계되었습니다.

**Experience Platform**

* [감사 로그 개요](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html)

   감사 로그를 통해 Adobe Experience Platform에서 누가 어떤 작업을 수행했는지 확인하는 방법에 대해 알아봅니다.

* [데이터 위생 개요](https://experienceleague.adobe.com/docs/experience-platform/hygiene/home.html?lang=en)

   Adobe Experience Platform 데이터 위생에서는 오래된 레코드 또는 부정확한 레코드를 업데이트하거나 삭제하여 데이터 주기를 관리할 수 있습니다.

* [자동 정책 적용](https://experienceleague.adobe.com/docs/experience-platform/data-governance/enforcement/auto-enforcement.html?lang=en)

   이 문서에서는 Experience Platform의 대상에 세그먼트를 활성화할 때 데이터 사용 정책이 자동으로 적용되는 방식을 다룹니다.

* [속성 기반 액세스 제어 개요](https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/overview.html)

   Adobe Experience Platform의 속성 기반 액세스 제어에 대해 알아봅니다.

## HIPAA 및 Adobe 제품 및 서비스

Adobe은 고객의 특정 개인 정보 보호 및 보안 요구 사항을 충족하기 위해 의료 업계에서 고객의 요구 사항을 충족하기 위해 지속적으로 혁신하고 적응하고 있습니다.

자세한 내용은 [HIPAA 및 Adobe 제품 및 서비스](https://www.adobe.com/trust/compliance/hipaa-ready.html).

## 높은 수준 마케팅 다이어그램

HIPAA가 아닌 제품:

**마케팅 다이어그램**

* 회색으로 표시된 애플리케이션은 아직 HIPAA가 준비되지 않았습니다.

![Hippa Ready](assets/HIPAA-readiness.png)

## 접근 방법

이 섹션에서는 구현 단계 및 인터뷰 단계를 설명합니다.

### 구현 단계

![구현 단계](assets/implementation-stages.png)

각 단계에서 고려할 사항:

![구현 고려 사항](assets/considerations.png)

이 섹션에서는 따라야 할 몇 가지 우수 사례를 간략하게 설명하고 다음 세 단계로 구분됩니다.

### 인터뷰 단계

이해 관계자와 인터뷰하는 프로세스는 다음 측면을 이해하는 데 중요합니다.

* 목표: 사용 사례 유형 - 전환, 전망, 참여 등
* 성능: 모든 서비스 수준 Target 예상
* 데이터 소스: 웹/Analytics, 오프라인/온라인, CRM, 충성도 등
* 데이터 볼륨
* SLT/SLA 요구 사항
* ID - ID 수, 인증된 데이터와 익명의 데이터 처리
* 데이터 형식: JSON, CSV 등.
* 데이터 품질, 데이터 변환 필요
* 파트너와의 세그먼트 일치(공유)에 대한 모든 계획
* 가져올 모든 외부 대상
* 암호화: 기본값과 고객 관리 키
* 데이터 결합: 는 e-PHI로 간주됩니다
* 동의 데이터 수집 - OneTrust, 동의 SDK
* 대상 필요: 빈도 및 지연 및 액세스 제어 요구 사항
* 액세스 제어
* 데이터 정리 요구 사항
* 데이터 업데이트 요구 사항
* 경고 요구
* API 액세스

### 디자인 단계

면접 프로세스에 따라 디자인 단계에서 다음 사항을 다룹니다. 말할 필요도 없이, 설계 설명서는 검토 및 승인되어야 합니다. 디자인 문서는 다음 측면을 다룹니다.

* 데이터 값:
   * 볼륨 - 수집된 데이터 양
   * 타임라인 - 수집된 데이터가 있어야 하는 시간 길이입니다
   * Fidelity - 프로필 품질
* SLT/SLA 요구 사항과 함께 AEP 보호 기능을 고려하십시오
* 라이선스 사용
* 데이터 격리 요구 - 단일 또는 여러 조직의 여러 샌드박스
* 데이터 필터링
* 데이터 위생 요구 사항(데이터 및 빈도)
* 데이터 삭제/업데이트 요구 사항을 충족하는 프로세스 및 방법
* 데이터 변환 요구 사항 - 업스트림, 데이터 준비, 쿼리 서비스
* 기본 및 기타 ID 이해 및 결정
* [XDM 스키마 디자인](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* 프로파일링된 데이터 세트와 프로파일링되지 않은 데이터 세트 수 확인
* 병합 정책 디자인
* 동의 데이터 관리
* 거버넌스: 역할, 레이블, 정책, 마케팅 작업 및 액세스 제어
* [프로필 보강](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)
* 에지/스트리밍/배치를 위한 세그먼테이션 설계 요구 사항
* 예상 대상 및 활성화 계획. HIPAA 전용 대상 요구 사항 고려
* Analytics 플랜
* 경고
* API 액세스 요구 사항 추가

### 구현 단계

디자인 문서를 검토하고 승인하면 구현 단계에서 다음 영역을 처리할 수 있습니다.

* 필요한 샌드박스 수: 개발/테스트/제품
* 샌드박스에 대한 컨트롤 액세스
* 배포 방법론
* TTL 요구 사항 및 빈도(데이터 위생)
* XDM 스키마 및 액세스 제어
* 동의 적용
* 거버넌스: 역할, 레이블, 정책 및 마케팅 작업
* 세그먼테이션
* 데이터 세트 및 액세스 제어
* 데이터 위생 설정
* 대상 설정 및 액세스 제어
* 경고 설정
* API 액세스 요구 사항 구현
* 샘플 데이터로 테스트 종료
