---
title: Adobe Experience Platform 데이터 흐름 아키텍처 다이어그램
description: 이 아키텍처 다이어그램은 데이터가 Adobe Experience Platform에 들어오고 나가는 흐름을 보여 줍니다.
solution: Data Collection
kt: 7198
thumbnail: null
exl-id: 5016f657-dd55-4ab7-859d-c97bc5edff76
source-git-commit: 21b688109ee8c3d209f2cac5267eb95258851dae
workflow-type: ht
source-wordcount: '118'
ht-degree: 100%

---

# Adobe Experience Platform 데이터 흐름 아키텍처    다이어그램

## 데이터 흐름 다이어그램

아래 다이어그램은 Adobe Experience Platform에서 데이터를 수집하고 내보내는 다양한 경로를 보여 줍니다.

<img src="assets/aep_data_flow.svg" alt="Experience Platform 데이터 흐름" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" />

## 데이터 유입 및 송출 패턴

모든 데이터 수집과 유입 패턴의 자세한 목록은 [데이터 준비 및 수집 블루프린트](../data-ingestion/ingestion.md)를 참조하십시오.

모든 데이터 송출과 액세스 패턴의 자세한 목록은 [데이터 액세스 및 내보내기 블루프린트](../data-ingestion/egress.md)를 참조하십시오.

## 데이터 수집 가드레일

아래 다이어그램은 Adobe Experience Platform에 데이터를 수집할 때의 평균 성능 가드레일과 지연 시간을 보여줍니다.

<img src="assets/aep_data_flow_guardrails.svg" alt="Experience Platform 데이터 흐름" style="border:1px solid #4a4a4a; width:90%; margin-bottom: 15px;" class="modal-image" class="modal-image" />