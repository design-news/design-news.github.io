---
title: "Figma 디자인 시스템 구축하기 원시 색상 변수"
description: ""
coverImage: "/assets/img/2024-05-27-BuildingYourFigmaDesignSystemPrimitiveColorVariable_0.png"
date: 2024-05-27 19:38
ogImage: 
  url: /assets/img/2024-05-27-BuildingYourFigmaDesignSystemPrimitiveColorVariable_0.png
tag: Tech
originalTitle: "Building Your Figma Design System: Primitive Color Variable"
link: "https://medium.com/@daniasyrofi/building-your-figma-design-system-primitive-color-variable-446009fdf8d5"
---


## 디자인 시스템 학습

![이미지](/assets/img/2024-05-27-BuildingYourFigmaDesignSystemPrimitiveColorVariable_0.png)

Figma에서 디자인 시스템을 만드는 것은 디지털 제품을 개발할 때 일관성을 유지하는 데 중요합니다. 디자인 시스템의 기본 요소 중 하나는 색상 팔레트를 정의하는 것입니다. 그러나 색상 팔레트를 설정하는 것은 종종 시간이 많이 소요될 수 있습니다. 이 기사에서는 이 프로세스를 가속화하는 방법을 공유하고, 디자인 시스템이 확장 가능하고 유지하기 쉽며 다양한 테마에 적응할 수 있도록 보장합니다.

# 왜 기본 색상 변수를 사용해야 할까요?

<div class="content-ad"></div>

원시 색상 변수는 디자인 시스템에서 가장 기본적이고 단순한 색상입니다. 색상의 영역에서는 여러 수준이 있으며, 점점 복잡해집니다: 원시 색상 - 시맨틱 색상 - 별칭 색상. 원시 색상을 사용하는 장점은 다음과 같습니다:

- 초보자에게 이해하기 쉬움: 원시 색상은 직관적이며 디자인 시스템에 익숙하지 않은 사람들도 쉽게 이해할 수 있습니다.
- 소규모 프로젝트에 적합: 이러한 색상은 단순함과 속도가 우선시되는 소규모 프로젝트에 이상적입니다.
- 빠른 설정: 원시 색상 변수를 설정하는 것이 빠르기 때문에 초기 디자인 단계를 신속히 진행할 수 있습니다.

# 피그마에서 원시 색상 변수 만들기 단계별 안내

![원시 색상 변수 만들기](/assets/img/2024-05-27-BuildingYourFigmaDesignSystemPrimitiveColorVariable_1.png)

<div class="content-ad"></div>

# 1. 색상 팔레트 정의하기

먼저 핵심 색상 팔레트를 정의하세요. 일반적으로 주 색상, 보조 색상 및 중립 색상이 포함됩니다. 다음 사항을 고려하여 색상을 선택해보세요:

- 주요 색상: 주요 작업 및 강조에 사용되는 주요 색상입니다.
- 보조 색상: 보조 작업과 강조에 사용되는 색상입니다.
- 중립 색상: 배경, 텍스트, 테두리에 사용되는 회색 계열의 색상입니다.
- 상태 색상: 성공, 경고, 정보, 위험 등과 같은 각각 다른 상태를 나타내기 위해 사용되는 색상입니다.

![색상팔레트](/assets/img/2024-05-27-BuildingYourFigmaDesignSystemPrimitiveColorVariable_2.png)

<div class="content-ad"></div>

# 2. 플러그인을 사용해서 색상 변형 생성하기

기본 색상의 변형을 생성하기 위해 피그마 플러그인을 사용해보세요. “Color, Tint & Shade Generator”와 같은 플러그인을 사용하면 원본 색상에서 음영, 틴트 및 기타 파생 색상들을 생성할 수 있습니다. 이 단계를 통해 다양한 UI 요소에 대한 포괄적인 색상 세트를 보유할 수 있습니다.

![이미지](https://miro.medium.com/v2/resize:fit:1400/1*EHDzwrIJEa-KyoLgWe4RsA.gif)

![이미지](https://miro.medium.com/v2/resize:fit:1400/1*8rOJHNgz6lewcqKz0spvxw.gif)

<div class="content-ad"></div>


![Figma Color Libraries](/assets/img/2024-05-27-BuildingYourFigmaDesignSystemPrimitiveColorVariable_3.png)

## 3. 색상을 색상 라이브러리에 추가하기

![Styler Plugin](https://miro.medium.com/v2/resize:fit:1400/1*ko3D5s6_SUPsm6PWrGfutg.gif)

피그마 색상 라이브러리에 색상을 추가하기 위해 플러그인을 사용하세요. "Styler"와 같은 플러그인을 사용하면 이 프로세스를 간소화할 수 있어 색상 스타일을 효율적으로 관리할 수 있습니다. 이 단계를 통해 색상 변수를 다른 프로젝트에서 쉽게 접근하고 재사용할 수 있습니다.

<div class="content-ad"></div>

플러그인을 사용하려면 다음 단계를 따르세요:

- 추가하고 싶은 색상을 선택합니다.
- 마우스 오른쪽 버튼을 클릭하여 Styler 플러그인을 찾고 "스타일 생성"을 선택합니다.
- 그럼 지역 스타일에 결과가 표시됩니다.

![이미지](https://miro.medium.com/v2/resize:fit:1400/1*efH_ZjX-RUU74jkyz3VuTw.gif)

![이미지](/assets/img/2024-05-27-BuildingYourFigmaDesignSystemPrimitiveColorVariable_4.png)

<div class="content-ad"></div>

# 4. 로컬 변수에 색상 추가하기

마지막 단계는 색상을 로컬 변수에 추가하는 것입니다. 이것은 의미 있는 색상이나 별칭과 같이 추가적인 색상을 유도하는 데 도움이 됩니다. 플러그인 "Styles to Variable"을 사용하면 로컬 스타일을 자동으로 로컬 변수로 변환할 수 있습니다.

![image](https://miro.medium.com/v2/resize:fit:1400/1*J2h9cNF77frpF9cMhs9Q5w.gif)

# 결론

<div class="content-ad"></div>

Figma에서 원시 색상 변수를 사용하여 디자인 시스템을 구축하면 일관성 있고 유지보수가 용이한 디자인 작업 환경을 확립할 수 있어요. 위에서 안내한 단계를 따라하면 팀 내의 일관성과 협업을 향상시킬 수 있는 확장 가능한 색상 시스템을 만들 수 있어요. 지금부터 색상 변수를 정의하고 디자인 시스템을 더욱 발전시켜 보세요!

# 축하합니다

축하합니다! 성공적으로 원시 색상 디자인 시스템을 구축했어요. 이 글이 도움이 되었다면 박수 버튼을 클릭하여 저를 지원해주세요.

다른 플랫폼에서도 저를 만날 수 있어요: Dribbble | LinkedIn

<div class="content-ad"></div>

읽어 주셔서 감사합니다 :)

# 크레딧

Figma Design System: 02 Primitive Color Variables에 대한 통찰력 있는 비디오로 유명한 YouTube 채널 Christopher Deane에게 특별한 감사를 전합니다. 그들의 자세한 설명과 실용적인 팁은 이 글에서 제시된 개념을 보다 정교하게 다듬는 데 큰 도움이 되었습니다.