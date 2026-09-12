---
title: 콘텐츠 시뮬레이션
description: 샘플 프로필 데이터와 함께 Adobe Journey Optimizer의 시뮬레이션 도구를 사용하여 개인화된 필드, 콘텐츠 변형 및 대체 동작을 확인하는 방법에 대해 알아봅니다.
doc-type: article
solution: Experience Platform
exl-id: 3e2b064f-5680-461c-a49e-2a61514e146f
source-git-commit: 3076f01e06023cebd30ead73d61f4540da9ce791
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# 콘텐츠 시뮬레이션

**목적:** Adobe Journey Optimizer의 시뮬레이션 및 증명 도구를 사용하여 개인화, 조건부 논리 및 콘텐츠 변형을 확인합니다.

## 학습 목표

이 단원을 마치면 다음과 같은 작업을 수행할 수 있습니다.

1. 시뮬레이션을 위해 테스트 프로필 데이터를 업로드하고 사용합니다.
1. 개인화된 필드 및 변형 논리의 유효성을 검사합니다.
1. 누락되었거나 일치하지 않는 데이터에 대한 대체 동작을 테스트합니다.

## 소개

이 최종 모듈에서는 Adobe Journey Optimizer의 시뮬레이션 도구를 사용하여 **2개의 조건부 변형**&#x200B;으로 이메일을 테스트합니다.
이렇게 하면 다양한 고객이 개인화된 메시지를 어떻게 경험할지 미리 볼 수 있으므로 캠페인을 시작하기 전에 정확성을 확보할 수 있습니다.

툴킷에서 샘플 테스트 프로필 파일 **sample.csv**&#x200B;을 사용합니다.

![툴킷의 샘플 테스트 프로필 파일 sample.csv](assets/content-simulation-sample-csv-toolkit-file.png)

## 시뮬레이션 도구 열기

1. 완료된 이메일을 엽니다.
1. **콘텐츠 시뮬레이션**&#x200B;을 클릭합니다.
1. **콘텐츠 변형 시뮬레이션**&#x200B;을 선택합니다.

![콘텐츠 시뮬레이션을 클릭하고 콘텐츠 변형 시뮬레이션을 선택합니다](assets/content-simulation-click-simulate-content-variation.png)

몇 초 후에 시뮬레이션 패널이 열립니다.

## 테스트 프로필 데이터 업로드

1. 도구 키트 폴더에서 **sample.csv**&#x200B;을 엽니다.
   - **Alex** → 40세 이상
   - **Jason** → 40세 미만
2. **입력 데이터 업로드**&#x200B;를 클릭합니다.

   ![시뮬레이션 패널의 입력 데이터 업로드 단추](assets/content-simulation-click-upload-input-data.png)

3. **sample.csv**&#x200B;을 선택하고 **계속**&#x200B;을 클릭합니다.

![sample.csv 선택 및 계속 클릭](assets/content-simulation-choose-sample-csv-continue.png)

AJO은 파일을 처리하고 미리 보기를 준비합니다.


## 변형 렌더링 검토

AJO은 업로드된 프로필을 기반으로 두 변형을 나란히 표시합니다.

**예상 결과:**

- **Alex** → **Variant 1**(40세 이상) 표시

![40세 이상의 Alex 프로필 렌더링 변형 1](assets/content-simulation-variant-1-age-above-40.png)

위로 스크롤하면 아래에서 볼 수 있듯이 지금 이름이 인 개인화된 필드도 표시됩니다.

![변형 1](assets/content-simulation-personalized-name-field-variant-1.png)의 Alex에 대해 표시된 개인 맞춤화된 이름 필드

- **Jason** → **Variant 2**(40세 미만) 표시

![40세 미만의 Jason 프로필 렌더링 변형 2](assets/content-simulation-variant-2-age-below-40.png)

Jason의 풀네임도 포함해서요. 정말 멋지다!

![Variant 2의 Jason에 대한 개인 맞춤화된 전체 이름 필드 표시](assets/content-simulation-personalized-name-field-variant-2.png)



## 대체 동작 확인

**폴백 및 기본값:** 전자 메일이 누락된 데이터 또는 일치하지 않는 시나리오를 정상적으로 처리하는지 확인하십시오. 예를 들어, 빈 생년 필드가 있는 프로필 또는 타겟팅된 오퍼에 적합하지 않은 프로필을 시뮬레이션하십시오. 미리 보기에는 깨지거나 빈 콘텐츠 대신 기본 콘텐츠 블록 또는 현명한 자리 표시자가 표시되어야 합니다. 시뮬레이션에 콘텐츠가 있어야 하는 빈 섹션이 표시되는 경우 디자인에서 대체 오퍼 또는 기본 텍스트를 구성해야 할 수 있음을 나타냅니다.


## 요약

이 단원에서는 다음과 같은 작업을 성공적으로 수행합니다.

- 샘플 프로필을 사용하여 개인화된 콘텐츠 시뮬레이션
- 검증된 변형 스위칭 논리
- 확인된 개인화된 필드가 올바르게 채워짐

이제 다음 모듈(**브랜드 정렬**)을 사용할 준비가 되었습니다.
여기서 AI를 사용하여 연결 5G 브랜드 지침에 대해 이메일을 평가합니다.
