---
title: 관계형 구성
description: 오케스트레이션된 캠페인에 대해서만 관계형 스키마의 이메일 속성을 사용하여 이메일 채널을 구성하는 방법을 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: 6f299942-79a6-42c2-8a5b-dd4bccd6aad4
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 10%

---


# 관계형 구성

## 목표

다음 단계 집합에서는 관계형 스키마 `dep-rel: Customer Account`의 `email` 특성을 사용하여 오케스트레이션된 캠페인에서만 사용할 전자 메일 채널 구성을 만듭니다

## 채널 구성 만들기

1. **채널 관리 및 일반 설정** 메뉴에 있는 **채널 →**(으)→ 이동합니다.
2. **구성 만들기** 단추를 클릭합니다.

   ![채널 구성 만들기](assets/configure-for-profile-create-configuration-button.png)

3. 만들기 마법사에서 다음 값을 설정합니다.
   - **이름:** `Relational-Email`
   - **채널:** `Email`
   - **마케팅 액션:** `Email Targeting`

![채널 구성 세부 정보](assets/configure-for-relational-channel-configuration-name-values.png)

>[!NOTE]
>
>이메일을 채널로 선택하면 새 섹션 이메일 설정이 표시됩니다.





## 이메일 유형 구성

**이메일 유형**&#x200B;을(를) **마케팅**(으)로 설정

![전자 메일 설정](assets/configure-for-profile-set-email-type-marketing.png)

## 하위 도메인 구성

**하위 도메인** 드롭다운에서 **email.dep-labs.com**&#x200B;을 선택합니다.

![하위 도메인 드롭다운(email.dep-labs.com 선택)](assets/configure-for-profile-select-email-subdomain.png "하위 도메인 구성")

## IP 풀 세부 정보 구성

**IP 풀** 드롭다운에서 **마케팅**&#x200B;을 선택합니다.

![선택한 마케팅이 있는 IP 풀 드롭다운](assets/configure-for-profile-select-marketing-ip-pool.png "IP 풀 세부 정보 구성")

## 목록 구독 취소 구성

1. 목록 구독 취소에 대한 토글이 **활성화**&#x200B;인지 확인합니다.
1. 구독 취소 목록 기본 설정 영역에서 모든 확인란이 **선택됨**&#x200B;인지 확인하십시오.
1. 링크 관리에서 **Adobe 관리**&#x200B;가 선택되어 있는지 확인하십시오.
1. 동의 수준에 대해 **채널**(으)로 설정되어 있는지 확인하십시오.

![목록 구독 취소 구성](assets/configure-for-profile-configure-list-unsubscribe-settings.png)

## 헤더 매개 변수 구성

1. 다음 필드를 다음과 같이 설정합니다.
   - **보낸 사람 이름:** `DEP Labs`
   - **전자 메일 접두사:** `dep`
   - **이름에 대한 회신:** `DEP Labs Support`
   - **전자 메일에 회신:** `reply@email.dep-labs.com`
   - **오류 전자 메일 접두사:** `error`

![헤더 매개 변수](assets/configure-for-profile-email-header-parameters.png)

## BCC 이메일 구성

비워 둡니다.

>[!NOTE]
>
>보낸 이메일 사본을 BCC 받은 편지함으로 보내 보관할 수 있습니다. 전송된 모든 이메일이 이 BCC 주소로 숨은 참조로 자동 전송될 수 있도록 원하는 이메일 주소를 입력합니다. BCC 주소 도메인은 Adobe에 위임된 하위 도메인과 달라야 합니다. 이 기능은 선택 사항입니다. *이메일에 숨은 참조를 사용하는 방법*

## 이메일 재시도 매개 변수 구성

**시간**&#x200B;의 기본 설정을 **84**(으)로 설정한 상태로 둡니다.

## URL 추적 매개 변수 구성

기본 설정으로 둡니다.

## 실행 세부 정보

1. 오케스트레이션된 캠페인 탭에서 활성화 확인란을 **확인**&#x200B;합니다.

   ![오케스트레이션된 캠페인 구성](assets/configure-for-profile-enable-orchestrated-campaign-tab.png)

2. 실행 차원에서 다음을 구성합니다.
   - **한 번에 한 개의 메시지 배달:** `Target Dimension `
   - **프로필 대상 Dimension:** `dep-rel: Customer Account - customer_id`

   ![실행 차원](assets/configure-for-relational-execution-dimension-target-settings.png)

3. 실행 주소에서 다음을 구성합니다.
   - **Source:** `Target Dimension`
   - **게재 주소:** `click on the Edit button`

   ![Dimension 타깃팅](assets/configure-for-relational-execution-address-source-target-dimension.png)

4. 팝업에서 **딥렐: 고객 계정** 폴더를 클릭합니다.

   ![게재 주소 구성](assets/configure-for-relational-customer-account-folder.png)

5. **전자 메일**&#x200B;을 선택하고 **선택** 단추를 클릭합니다.

   ![배달 주소로 전자 메일 보내기](assets/configure-for-relational-select-email-as-delivery-address.png)

6. 완료되면 최종 실행 세부 사항이 아래 스크린샷과 같이 표시됩니다

![실행 차원이 구성됨](assets/configure-for-relational-execution-details-final-result.png)

>[!NOTE]
>
>오케스트레이션된 캠페인의 경우 이메일로 고객 계정을 타겟팅하므로 Target Dimension당 하나의 메시지만 전송하면 됩니다.  사용하는 실행 주소는 Target Dimension 자체(즉, **이메일** 주소의 **dep-rel: 고객 계정** 테이블에 저장된 주소)에서 가져옵니다.


## 검토 및 저장

1. 모든 세부 사항을 다시 검토하여 일치하는지 확인하십시오.
1. 위로 스크롤하여 **제출**&#x200B;을 클릭합니다.
1. 완료되면 두 개의 이메일 채널 구성이 보이는데 둘 다 &quot;처리&quot; 상태일 수 있습니다.

>[!WARNING]
>
>이메일 채널 구성 처리에 최대 2시간이 소요되는 것으로 관찰되었습니다.

## 요약

이제 오케스트레이션된 캠페인에 대한 관계형 스키마 속성을 사용하기 위해 이메일 채널 구성을 만드는 방법을 보았습니다.
