---
hold: true
title: 이메일 활동 추가
description: 오케스트레이션된 Campaign에서 다양한 이메일 채널 구성을 사용하여 개별 포크 분기에서 두 개의 이메일 활동을 추가하고 구성하는 방법을 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: e911a251-9f9f-484c-a2de-101b0fc2c417
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 0%

---


# 이메일 활동 추가

## 목표

다음 단계 세트에서는 두 개의 포크 활동 분기에 두 개의 이메일 활동을 추가하는 캠페인을 빌드합니다. 이전에 만든 이메일 채널을 사용하도록 두 개의 이메일 활동을 구성합니다. 마지막으로 이러한 각 이메일 활동에 기본 이메일 설정(제목 및 본문)도 추가합니다.

>[!CAUTION]
>
>계속하기 전에 두 이메일 채널 구성이 해당 상태에서 활성 상태로 표시되는지 확인해야 합니다.
>
>![활성 상태를 표시하는 두 전자 메일 채널 구성](assets/add-email-activities-email-channel-configs-active.png "전자 메일 채널 구성")



## 상위 분기 이메일 활동 추가

1. 상위 흐름의 **+**&#x200B;을(를) 클릭하고 **채널 활동**&#x200B;에서 **이메일**&#x200B;을(를) 선택합니다.

![전자 메일 활동 추가](assets/add-email-activities-select-email-activity.png)

**전자 메일** 세부 정보 창이 열립니다

![전자 메일 세부 정보 창](assets/add-email-activities-email-details-pane.png)

&#x200B;2. **전자 메일** 활동에 대해 **프로필 특성을 사용하는 전자 메일**(으)로 레이블 이름을 바꾸고 **전자 메일 편집**&#x200B;을 클릭합니다. 이메일 본문 생성은 테스트 목적으로만 사용됩니다

![전자 메일 활동 레이블 이름을 바꾸고 전자 메일 편집을 클릭합니다](assets/add-email-activities-rename-and-edit-email.png)

&#x200B;3. **작업** 탭을 선택하고 드롭다운에서 **프로필-이메일** 채널 구성을 선택합니다.

![작업 탭에서 프로필-전자 메일 채널 구성 선택](assets/add-email-activities-select-profile-email-channel.png)

&#x200B;4. 그런 다음 **콘텐츠 편집**&#x200B;을 클릭하여 일부 테스트 콘텐츠를 추가합니다.

![테스트 콘텐츠를 추가하려면 콘텐츠 편집을 클릭합니다](assets/add-email-activities-edit-content.png)

&#x200B;5. **제목 줄**(&quot;기본 계획 구성원을 위한 업그레이드 오퍼&quot;)을 제공하고 **이메일 본문 편집** 단추를 클릭하십시오.

![제목 줄 추가 및 전자 메일 본문 편집](assets/add-email-activities-subject-line-edit-body.png)

&#x200B;6. 이 테스트에는 **직접 코드 작성** HTML 옵션을 선택할 수 있는 다양한 옵션이 있습니다.

![자신의 HTML 옵션 코드 지정](assets/add-email-activities-code-your-own-html.png)

&#x200B;7. **이메일 Designer**&#x200B;에서 &quot;업그레이드 오퍼 사용 가능!&quot; 테스트 행을 삽입합니다. 표시된 대로 `</body></html>` 태그 바로 앞에서 **저장**&#x200B;을 클릭합니다.

![전자 메일 Designer에 테스트 줄을 삽입하고 저장을 클릭하세요](assets/add-email-activities-email-designer-save.png)

&#x200B;8. 오른쪽 아래 모서리에 확인 메시지가 나타날 때까지 기다립니다.

![확인 메시지가 표시됩니다](assets/add-email-activities-confirmation-message.png)

&#x200B;9. 종료하려면 **전자 메일 Designer** 옆에 있는 **왼쪽 화살표**&#x200B;를 클릭하십시오

![왼쪽 화살표를 클릭하여 전자 메일 Designer을 종료합니다](assets/add-email-activities-exit-email-designer.png)

&#x200B;10. 확인 대화 상자가 나타나면 **저장 및 닫기** 단추를 클릭합니다.

![저장 및 닫기 단추가 있는 확인 대화 상자](assets/add-email-activities-save-and-close-dialog.png)

&#x200B;11. 이메일 본문에 추가된 텍스트를 포함하여 이메일 속성 및 작업을 검토합니다. 캠페인 캔버스로 다시 이동하려면 **왼쪽 화살표**&#x200B;를 클릭하십시오.

![Campaign 캔버스로 다시 이동](assets/add-email-activities-back-to-campaign-canvas.png)

## 하단 분기 이메일 활동 추가

캠페인 캔버스로 돌아가서, 맨 아래 흐름의 **+**&#x200B;을(를) 클릭하고 **채널 활동**&#x200B;에서 **이메일**&#x200B;을(를) 선택합니다. 다음을 제외하고 위와 동일한 단계(2~11단계)를 수행합니다.

- **전자 메일** 활동에 대해 **Target Dimension을 사용하는 전자 메일**(으)로 레이블 이름을 바꾸십시오.
- 전자 메일 설정에서 **관계형 전자 메일** 전자 메일 채널 구성을 선택합니다

![관계형 전자 메일 채널로 구성된 두 번째 전자 메일 활동](assets/add-email-activities-bottom-branch-relational-email.png "두 번째 전자 메일 활동 추가")

## 요약

이제 이메일 채널을 사용하여 이메일 활동을 구성하는 방법을 보았습니다. 그런 다음 각 활동은 매우 기본적인 이메일 제목과 본문으로 구성되었습니다. 전체 캠페인은 다음에 테스트됩니다.
