---
title: "UX Drill 01  태그, 배지 및 칩"
description: ""
coverImage: "/assets/img/2024-05-15-UXDrill01TagsBadgesandChips_0.png"
date: 2024-05-15 19:53
ogImage:
  url: /assets/img/2024-05-15-UXDrill01TagsBadgesandChips_0.png
tag: Tech
originalTitle: "UX Drill 01 — Tags, Badges, and Chips"
link: "https://medium.com/@alexisyehachung/ux-drill-01-d69a1069945e"
---

# -태그 대 뱃지? 왜 난 그들을 계속 '태그'라고 부르고 있을까요?

![이미지](/assets/img/2024-05-15-UXDrill01TagsBadgesandChips_0.png)

1일차. 아이들을 뭘로 불러야 할까요?

CMU School of Design의 IXD 과정 중에 앱 디자인 프로젝트를 진행하면서 이 질문이 떠올랐어요.

TL;DR

이것은 상호작용이 없기 때문에 "배지"로 불려야 합니다. 저희 팀은 라벨과 정보를 나타내기 위해 배지를 사용해 보았지만, 이들은 필터 태그와 마찬가지로 클릭할 수 없었습니다. 그래서 이들은 배지였습니다.

배지와 태그가 구분이 없는 유사한 UI로 생각했지만, 실제로는 다른 것이었습니다.

![이미지](/assets/img/2024-05-15-UXDrill01TagsBadgesandChips_1.png)

간단한 구글 검색으로 찾아본 내용이에요. 지금까지 명확한 개념을 가지고 있지 못해 아쉬웠어요.

태그는 상호작용적이고(x 버튼과 함께 하는 경우가 많아요) 배지는 아니에요!!!

<img src="/assets/img/2024-05-15-UXDrill01TagsBadgesandChips_2.png" />

무제 UI 킷에서 배지의 추가 기능도 배울 수 있었어요. 새로운 상태나 읽지 않은 것을 강조하는 데 자주 사용돼요.

![이미지1](/assets/img/2024-05-15-UXDrill01TagsBadgesandChips_3.png)

![이미지2](/assets/img/2024-05-15-UXDrill01TagsBadgesandChips_4.png)

Google Material Design Guides에서 더 많은 것을 배울 수 있어요.

뱃지는 상태를 간단히 나타내기 위해 텍스트 없이 간소화된 기능을 가질 수 있어요.

하지만 곧 다시 혼동스러웠어요. 구글의 Material Design 가이드에는 태그가 아니라 "칩(chip)"만 있었거든요.

뭐지…

![이미지](/assets/img/2024-05-15-UXDrill01TagsBadgesandChips_5.png)

그래서, 칩이 더 인터랙티브하며 선택 및 비선택 상태로 나눠지고, 필터 기능과 직접적으로 관련이 있다는 걸 이해했어요.

하지만 다시 프로젝트로 돌아와서, 우리의 UI는 여전히 상호 작용이 없었지만 필터 카테고리를 나타내고 있었습니다. 이게 우리의 디자인 결정이 잘못되었음을 의미합니까?

그런 다음, LinkedIn에서 이 기사를 발견했습니다. 다행히도, 저만이 Chips, Badges, 그리고 Tags에 혼란스러워했던 것은 아니었습니다.

![image](/assets/img/2024-05-15-UXDrill01TagsBadgesandChips_6.png)

그분에 따르면, 제 혼란을 해소할 수 있었어요. Badges는 "상호 작용 없이 단순한 표시인자"라고 합니다. 반면에 tags와 chips는 모두 상호 작용이 가능하여 미래 사용자 작업으로 이어지며, 탭을 닫거나 선택 또는 선택 취소하거나 링크를 클릭하는 등의 작업을 수행할 수 있습니다.

요약하면, 우리의 핵심 의도는 앱의 범주화 시스템을 이해하고자 하는 사용자들에게 필터 카테고리에 대해 알려 주는 것이기 때문에, 마침내 UI 구성 요소를 '뱃지'로 명명할 수 있습니다!
