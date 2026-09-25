---
title: 대상자 작성 #3
description: iPhone 14 제품 페이지 방문자의 대상을 작성하고 대상 대상을 사용하여 다른 대상과 결합하여 스트리밍 활성화를 활성화합니다.
doc-type: article
solution: Experience Platform
exl-id: 999f9a20-1655-4eab-a796-a19d69a06879
source-git-commit: 96308d5726def849ef22540a5d13618017c40cc3
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 0%
---

# 대상 #3 작성

## 실습 목표

iPhone 14 제품 페이지를 방문한 대상 작성



## 분석 작업

이 대상은 앞으로 곧게 표시되어야 합니다.  여러 제품 페이지가 있을 수 있지만 여기에는 까다로운 사항은 없습니다.



## 대상자 만들기(모든 페이지 방문)

1. 왼쪽 레일의 이벤트 유형 아래에 있는 이벤트 탭에서 페이지 보기 이벤트를 찾아 대상에 추가합니다.

   ![왼쪽 레일의 이벤트 유형에서 페이지 보기 이벤트 찾기](assets/build-audience-3-find-page-view-event.png)

   >[!NOTE]
   >
   >**이벤트 유형 사용**
   >
   >페이지 보기 이벤트를 사용하면 대상자가 페이지 보기의 컨텍스트에서 페이지 이름만 평가할 수 있습니다. 페이지 이름 은 페이지 보기에만 존재하지만 두 가지 이점을 제공하므로 중복되어야 합니다.
   >
   >- UI를 볼 때 사용자에게 높은 수준의 시각적 설명서 제공
   >- 새 이벤트가 추가되면 의도하지 않은 경우 포함되지 않도록 필터링을 제공합니다
   >
   >이러한 이유로 빌드하는 각 이벤트 스키마는 사용하는 이벤트 유형에 많은 생각을 해야 하는 것이 좋습니다. 필터링 및 시각적 안내서의 기본입니다.



2. 설명을 제공하고 스트리밍으로 만듭니다.

3. 배치된 이벤트 위에서 &quot;모든 시간&quot;을 &quot;오늘&quot;로 변경합니다.

   ![이벤트 시간 필터를 임의의 시간에서 오늘로 변경](assets/build-audience-1-change-any-time-to-today.png)

4. 이 대상자를 &quot;*방문한 모든 페이지*&quot;로 저장

5. 대상에 대한 파란색 단추 **대상 활성화**&#x200B;를 클릭합니다.

6. **스트리밍 DEP Webhook** 대상을 선택하고 다음을 클릭합니다.

7. 다음 을 클릭하고 마침 을 클릭합니다.

## 대상 만들기(iPhone 14 페이지 방문, 소유/주문하지 않음)

1. 새 대상 만들기 및 페이지 보기 이벤트 추가

   ![새 대상자를 만들고 페이지 보기 이벤트 추가](assets/build-audience-3-create-a-new-audience-and-add-the-page-views-event.png)



2. 페이지 이름이 있는 위치로 이동하고 이벤트에 페이지 이름 필드를 추가하여 필터링할 수 있습니다.

   - XDM ExperienceEvent —> 웹 —> 웹 페이지 세부 사항 —> 이름

   ![XDM ExperienceEvent > 웹 > 웹 페이지 세부 정보 > 이름으로 이동](assets/build-audience-3-navigate-to-page-name-field.png)



3. 추가 = &quot;iPhone 14&quot; 포함

   ![&quot;iPhone 14&quot;에 대한 포함 조건 추가](assets/build-audience-3-add-contains-iphone-14.png)

   >[!TIP]
   >
   >**&quot;페이지&quot; 검색 중**
   >
   >필드로 이동하지 않고 &quot;페이지&quot;를 검색해 보십시오.
   >
   >페이지 이름이 표시되지 않습니다. 이는 이름 지정 방법 때문입니다.
   >
   >- XDM ExperienceEvent > 웹 > 웹 페이지 세부 정보 > 이름
   >
   >따라서 폴더가 표시되지만 필드 자체는 표시되지 않습니다. 이름 지정 규칙을 함께 입력할 때는 사용자가 검색할 수 있는 이 용어와 다른 일반적인 용어를 고려하여 해당 용어를 사용자 이름에 통합합니다.
   >
   >검색은 설명을 검색하지 않음
   >
   >![&quot;페이지&quot;를 검색해도 페이지 이름 필드가 표시되지 않습니다](assets/build-audience-3-searching-for-page-does-not-find-field.png)



4. 배치된 이벤트 위에서 &quot;모든 시간&quot;을 &quot;오늘&quot;로 변경합니다.

   ![이벤트 시간 필터를 임의의 시간에서 오늘로 변경](assets/build-audience-1-change-any-time-to-today.png)

   >[!NOTE]
   >
   >오늘 발생한 이벤트를 기반으로 활성화하므로 오늘의 페이지 보기에만 중점을 둡니다.



5. 스트리밍인지 확인하고 설명을 입력하십시오.

6. 대상을 &quot;*방문한 iPhone 14 페이지*&quot;(으)로 저장

   ![대상자를 &quot;방문한 iPhone 14 페이지&quot;로 저장](assets/build-audience-3-save-audience-as-visited-iphone-14-page.png)



7. 대상에 대한 파란색 단추 **대상 활성화**&#x200B;를 클릭합니다.

8. **스트리밍 DEP Webhook** 대상을 선택하고 다음을 클릭합니다.

9. 다음 을 클릭하고 마침 을 클릭합니다.



## 대상의 대상 만들기

1. 왼쪽 상단 탐색의 대상 탭으로 이동합니다.
1. Experience Platform으로 드릴 다운
1. 이전에 만든 세 개의 다른 대상 가져오기
1. iPhone 14 및 주문 iPhone 14를 소유하는 경우 포함 을 포함하지 않음으로 변경합니다.

   ![iPhone 14를 소유하고 iPhone 14를 대상자 대상에 포함하지 않도록 순서 지정](assets/build-audience-3-audience-of-audiences-does-not-include.png)



1. 설명을 입력합니다.

1. 스트리밍으로 변경

1. &quot;*방문한 iPhone 14 페이지는 소유/주문하지 않음*&quot;(으)로 저장

1. 대상에 대한 파란색 단추 **대상 활성화**&#x200B;를 클릭합니다.

1. **스트리밍 DEP Webhook** 대상을 선택하고 다음을 클릭합니다.

1. 다음 을 클릭하고 마침 을 클릭합니다.

>[!NOTE]
>
>**시간 필터**
>
>이 요건은 시간 요건이 없었기 때문에 3년 전에 누군가가 방문했다면 자격을 갖추게 된다. 사용 사례에 따라 작동할 수도 있고 작동하지 않을 수도 있습니다. 그것은 물어볼 가치가 있다. 오늘 저희 웹사이트를 방문한 분들을 토대로 활성화 하고 있어서 추가하였습니다.  일부 사용 사례에서는 작동하지 않을 수 있습니다.  시간 필터를 추가하면 Edge 대상이 스트리밍 또는 일괄 처리로 되기 전까지 얼마나 과거로 이동할 수 있습니까?

>[!NOTE]
>
>**이 작업을 중단한 결과**
>
>몇 가지 이유로 간단한 요구 사항을 여러 대상으로 분할했습니다. 스트리밍에 대한 요구 사항이지만 이 두 가지 요구 사항은 Audience를 일괄 처리로 바꿉니다. 스트리밍 자격 규칙에 대한 자세한 내용은 여기 를 참조하십시오.
>
>[https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html?lang=ko](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html?lang=ko)

>[!NOTE]
>
>**스트리밍 중인 대상의 종류**
>
>*대상 아래에서 엿보기* 블로그(아래 링크)에서 아래에 이에 대해 알아봅니다. 대상자의 결과가 프로필에 저장되는 방식을 보여 줍니다. 이는 데이터 스트림이 프로필에 저장된 대상자의 결과를 볼 때 해당 시점에서 대상자를 재실행하지 않으므로 중요합니다. 단순한 뉘앙스지만 이해할 만한 가치가 있다. 대부분의 프로필 속성은 주기적으로 업데이트되므로 이 접근 방식은 적절합니다.
>
>대상 내에서 대상을 사용할 때 AEP은 가능한 경우 순서를 지정하려고 시도한다는 것을 이해해야 합니다. 이를 수행할 수 없는 경계 사례가 있습니다. 예: 대상자 대상을 사용하는 경우 24시간마다 프로필 결격이 발생합니다.
>
>[https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-blogs/peeking-underneath-the-hood-of-segments-in-aep-adobe-experience/ba-p/453535?profile.language=ko](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-blogs/peeking-underneath-the-hood-of-segments-in-aep-adobe-experience/ba-p/453535?profile.language=ko)



## 여러 대상을 만드는 이유

이러한 모든 대상을 4개가 아닌 하나의 대상에 구축했다면 각 대상이 개별적으로 스트리밍인데도 불구하고 일괄 평가 방법을 얻게 됩니다.

![결합된 대상을 한 개 만들면 스트리밍 대신 일괄 처리가 평가됩니다](assets/build-audience-3-why-are-we-creating-multiple-audiences.png)



이러한 대상을 분류하고 대상 대상을 사용하면 이러한 동작이 수행됩니다.  에서 데이터 스트림으로 이러한 대상의 실시간 자격 조건

- iPhone 14 주문
- iPhone 14 소유
- iPhone 14 페이지 방문

>[!WARNING]
>
>현재 대상자는 매일 24시간 동안 지연 자격을 상실합니다



요점: 24시간 동안 지연되어 대상자를 탈락시킴으로써 더 빠른 대상자 진입을 교환했습니다.

>[!TIP]
>
>**선택적 Challenge Lab**
>
>일찍 끝났나요?
>
>오래된 핸드폰이 있으면 이메일로 타겟팅하고 싶습니다.  &quot;이전 휴대폰 있음&quot;의 대상을 만듭니다.  어떻게 그들을 타겟으로 삼을 수 있지?
