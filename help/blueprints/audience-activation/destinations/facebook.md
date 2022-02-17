---
title: facebook 사용자 지정 대상에 활성화
description: facebook 사용자 지정 대상에 대한 활성화.
solution: Experience Platform, Real-time Customer Data Platform, Data Collection
kt: 7086
source-git-commit: f1477d39a2b2349708ad74625bab6c5f4012ae1e
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 3%

---


# facebook 사용자 지정 대상에 활성화

여러 소스에서 고객 데이터를 수집하여 고객의 단일 프로필 보기를 작성하고, 이러한 프로필을 세그먼트화하여 마케팅 및 개인화를 위한 대상자를 만든 다음 이러한 대상을 Facebook과 같은 Social Ad Network에 공유하여 해당 대상에 대한 타겟팅 및 개인화 캠페인을 수행할 수 있습니다.

## 사용 사례

* 소셜 및 광고 대상의 알려진 대상자 타겟팅
* 온라인 및 오프라인 특성을 활용한 온라인 개인화
애플리케이션
* Real-time Customer Data Platform   

## 아키텍처

<img src="../assets/facebook.png" alt="facebook 사용자 지정 Audience Activation을 위한 참조 아키텍처" style="width:80%; border:1px solid #4a4a4a" />

## 구현 단계

1. 프로필 데이터 소스에서 사용할 ID 네임스페이스를 구성합니다.
   * 이메일, SHA256 해시(사용 가능한 경우)와 같은 기본 네임스페이스 를 사용하십시오.
   * Facebook에는 지원되는 ID 목록이 있습니다. facebook 사용자 지정 대상으로 활성화하려면 활성화된 ID 중 하나가 프로필에 있어야 합니다.
   * 현재 Facebook에서는 다음 ID를 지원합니다. GAID, IDFA, phone_sha256, email_lc_sha256, extern_id.
   * 자세한 내용은 [Facebook 대상 안내서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html?lang=en).
   * 적용 가능한 ID에 기본 네임스페이스를 사용할 수 없는 사용자 지정 네임스페이스를 만듭니다.
1. 프로필 데이터 소스 스키마 및 데이터 세트를 구성합니다.
   * 모든 프로필 레코드 원본 데이터에 대해 프로필 레코드 스키마를 만듭니다.
      * 각 스키마에 대한 기본 ID 및 보조 ID를 지정합니다.
      * 프로필 수집을 위한 스키마를 활성화합니다.
   * 모든 프로필 레코드 소스 데이터에 대한 프로필 레코드 데이터 세트를 만들고 관련 스키마를 할당합니다.
      * 프로필 수집을 위해 데이터 세트를 활성화합니다.
   * 모든 프로필 시계열 기반 소스 데이터에 대한 프로필 경험 이벤트 스키마 를 만듭니다.
      * 스키마의 기본 ID 및 보조 ID를 지정합니다.
   * 프로필 수집을 위한 스키마를 활성화합니다.
   * 모든 프로필 경험 이벤트 소스 데이터에 대한 프로필 경험 이벤트 데이터 세트를 만들고 관련 스키마를 할당합니다.
      * 프로필 수집을 위해 데이터 세트를 활성화합니다.
1. 소스 커넥터를 사용하여 소스 데이터를 위에 구성된 관련 데이터 세트에 수집합니다.
   * 자격 증명으로 소스 커넥터 계정을 구성합니다.
   * 지정된 일정에 따라 소스 파일 또는 폴더 위치에서 지정된 데이터 세트에 데이터를 수집하도록 데이터 흐름을 구성합니다.
   * 소스 데이터의 모든 필드를 대상 스키마에 매핑합니다.
   * 모든 필드를 Experience Platform으로 수집하기 위한 올바른 형식으로 변환합니다.
      * 날짜 변환
      * 적절한 경우 소문자로 변환(예: 이메일 주소)
      * 패턴 변형(예: 전화 번호)
      * 소스 데이터에 없는 경우 경험 이벤트 레코드에 대한 고유 레코드 ID를 추가합니다.
      * 어레이와 맵 유형 필드를 변형하여 Experience Platform에서 세그멘테이션을 위한 배열과 맵을 올바르게 매핑하고 모델링할 수 있습니다.
1. 프로필 병합 정책을 구성하여 ID 그래프와 프로필 병합에 포함해야 하는 데이터 세트를 올바르게 구성합니다.
1. 데이터 흐름이 실행된 후 프로필 데이터 수집이 오류 없이 성공했는지 확인하십시오.
   * Inspect은 여러 프로필의 id 그래프로 ID 관계를 정확하게 처리할 수 있습니다.
   * Inspect에 프로필 속성과 이벤트를 매핑하여 속성 및 이벤트를 프로필에 올바르게 수집합니다.
1. 세그먼트를 작성하여 프로필 대상자 만들기
   * 속성 및 이벤트에 대한 규칙을 사용하여 세그먼트 빌더에서 세그먼트를 만듭니다.
   * 평가를 위해 세그먼트를 저장합니다. 세그먼트는 지정된 일정에서 하루에 한 번 평가됩니다.
      * 세그먼트 규칙이 스트리밍 세그먼테이션을 수행할 수 있는 경우, 프로필에 대해 새 스트리밍 데이터를 수집할 때 세그먼트가 평가됩니다. 스트리밍 세그먼트는 예약된 배치 세그먼테이션 중에 하루에 한 번씩 평가됩니다.
1. 세그먼트 결과가 예상대로 표시되는지 확인하십시오.
   * 주어진 세그먼트에 대한 세그먼트 결과 수를 검토합니다.
   * 세그먼트에 포함해야 하는 프로필을 조사하여 세그먼트 멤버십이 프로필의 세그먼트 멤버십 부분에 포함되어 있는지 확인합니다.
1. 대상 구성에서 대상에 대한 대상의 전달을 구성합니다.
   * 자세한 내용은 [Facebook 대상 안내서](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html?lang=en) facebook 대상 구성에 대한 자세한 내용은
   * 대상을 구성할 때 대상에 활성화할 대상을 선택합니다.
   * 대상 데이터 플로우에서 대상을 대상으로 배달할 예약된 시작 날짜를 결정합니다.
   * 각 대상에는 전송될 필수 및 선택적 속성이 있습니다.
      * facebook의 경우 필수 ID 중 하나를 포함해야 하며 Experience Platform 내의 대상자의 프로필을 Facebook에서 타겟팅할 프로필과 일치시키는 데 사용됩니다.
   * 또한 각 대상에는 스트리밍 또는 배치, 파일 기반 또는 JSON 페이로드 등 지정된 게재 유형이 있습니다.
      * facebook의 경우 대상 멤버십은 JSON 형식으로 Facebook 종단점에 스트리밍 방식으로 전달됩니다.
      * 대상 멤버십은 Experience Platform에서 스트리밍 또는 배치 세그먼테이션 평가 이후 스트리밍 방식으로 제공됩니다.
1. 대상 흐름이 대상에 예상대로 전달되었는지 확인합니다.
   * 모니터링 인터페이스를 확인하여 예상 프로필 수와 함께 대상이 전달되었는지 확인합니다. 대상 크기는 활성화된 예상 프로필 수를 반영해야 합니다. Facebook과 같은 특정 대상에 이메일 해시 ID와 같은 특정 필드가 필요하며 대상의 구성원인 프로필에 없으면 대상에 활성화되지 않습니다.
   * 생략된 프로필에서 프로필 ID가 누락되었거나 필수 속성을 누락했는지 확인합니다.
   * 해결해야 할 다른 오류가 있는지 확인합니다.
1. 예상 대상 멤버십 수로 대상이 최종 대상에 활성화되었는지 확인합니다.
   * facebook 사용자 지정 대상 포털에 로그인하여 Real-time Customer Data Platform의 대상이 전달되었고 Facebook 대상의 프로필 일치율이 Real-time Customer Data Platform 대상의 프로필 수와 합리적으로 일치하는지 확인합니다.

## 가드레일

[프로필 및 세그멘테이션 보호 기능](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=ko)

## 관련 설명서

facebook 사용자 지정 대상에 활성화 - [대상 구성](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/social/facebook.html?lang=en)