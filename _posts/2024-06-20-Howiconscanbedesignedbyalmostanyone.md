---
title: "아이콘이 누구나 거의 디자인할 수 있다면"
description: ""
coverImage: "/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_0.png"
date: 2024-06-20 03:52
ogImage: 
  url: /assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_0.png
tag: Tech
originalTitle: "How icons can be designed by (almost) anyone"
link: "https://medium.com/back-market-engineering/how-icons-can-be-designed-by-almost-anyone-9243463a73a3"
---


우리가 어떻게 백마켓에서 일관성 있고 인식하기 쉬운 아이콘을 만들기 위해 많은 디자이너들이 참여하는 과정을 거쳤는지 알아보세요.

상형문자에서 플로피 디스크로, 아이콘은 인류에 퍼져있습니다. 그 이유는 간단합니다. 즉각적인 소통과 이해 때문이죠.

하지만 여러 디자이너로 구성된 팀에서 작업할 때 실제로 작동하는 아이콘을 만들고 확장하는 것은 어려운 일입니다. 이 일을 우리는 백마켓에서 해결했습니다.

# 도전 과제: 대규모로 아이콘 디자인하기

<div class="content-ad"></div>

Back Market에서는 사용자가 경험을 탐험하는 데 도움을 주는 것뿐만 아니라 브랜드의 일부로써 우리의 시각적 정체성의 한 표현으로 아이콘을 널리 사용합니다. 이게 우리에게 중요한 이유는 우리의 목표가 기술 수명 주기에 대해 다른 방법으로 생각하도록 사람들에게 보여주는 것이기 때문입니다.

과거에는 일러스트레이터에서 모든 아이콘을 만드는 디자이너 한 명이 있었습니다. 그 디자이너가 떠나면서 우리는 아이콘을 디자인할 디자이너 없이 남게 되었습니다.

우리는 이를 아이콘 디자인 방식을 재고함과 동시에 Back Market의 모든 디자이너가 우리의 디자인 시스템에 일관되고 인식하기 쉬운 아이콘을 기여할 수 있도록 하는 기회로 바라보았습니다. 그러면 우리는 어떻게 해결했을까요?

<div class="content-ad"></div>

# 우리가 한 방법

## 우리가 현재 가지고 있는 것을 감사하는 중

우리가 취한 첫 번째 단계는 이미 가지고 있는 아이콘들과 디자인 시스템에 아이콘을 기여하는 현재 과정을 검토하는 것이었습니다.

우리는 우리의 아이콘들에서 일부 공통된 패턴(선, 코너 반경, 갭, 단말기, ...)을 신속하게 확인했습니다.

<div class="content-ad"></div>

이를 통해 Back Market을 위한 명확한 아이콘 스타일을 정의할 수 있었습니다:

![How icon can be designed by almost anyone](/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_1.png)

다른 디자이너들이 이를 복제하고 일관된 아이콘을 만들 수 있도록 디자인 시스템에서 이 아이콘 스타일을 가이드라인을 통해 문서화했습니다.

## 새로운 기여 프로세스 정의

<div class="content-ad"></div>

저희 아이콘 기여 과정을 검토하면서 특히 이런 부분들에 결함이 있음을 알게 되었습니다:

- 도구: 저희는 아이콘을 일러스트레이터로 만들고 그것을 피그마로 내보내는 방식이었습니다. 모든 디자이너가 어도비 라이선스를 가지고 있지 않았죠.
- 검증: 만든 아이콘을 승인하는 프로세스가 없었습니다.

그래서 저희는 디자이너들과 함께 이상적인 아이콘 디자인 프로세스를 정의하기로 했습니다: 아이콘으로 개념을 시각적으로 어떻게 표현할지에 대한 초기 아이디어부터 디자인 시스템에서 사용할 준비가 된 아이콘까지.

도구 측면에서, 우리는 저희의 주요 디자인 도구이자 디자인 시스템 라이브러리가 있는 피그마로 아이콘 제작을 옮기기로 결정했습니다.

<div class="content-ad"></div>

<img src="/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_2.png" />

승인을 위해, 디자이너들이 아이콘을 검토하고 피드백을 제공할 수 있는 Slack 채널인 #designers-feedback을 사용하기로 결정했습니다.

## 아이콘 디자인을 위한 템플릿 생성

우리가 작성한 지침에 더하여, 디자이너들이 아이콘을 생성할 때 사용할 수 있는 특정 아이콘 템플릿을 Figma에서 만들었습니다.

<div class="content-ad"></div>

이 템플릿은 2개의 프레임으로 구성되어 있어요:

- 크기와 여백을 준수하는 템플릿 프레임
- 새 아이콘이 기존 아이콘들과 얼마나 일관성 있게 표시되는지를 테스트하고, 아이콘이 얼마나 쉽게 인식되는지 테스트하는 블러 테스트 프레임

<img src="/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_3.png" />

## 아이콘 디자인 가이드라인의 스트레스 테스트

<div class="content-ad"></div>

일반적인 디자인 프로젝트처럼, 우리는 디자이너들을 모아 우리가 디자인한 가이드라인과 작품들을 검토하였습니다.

이 디자인 비평의 목표는 결함을 찌르고, 우리가 고안한 것이 아이콘을 만들고 싶어하는 모든 디자이너에게 유용할 것임을 확인하는 것이었습니다.

## 소식 퍼뜨리기

마지막으로, 우리는 새로운 아이콘 가이드라인과 기여 프로세스에 대한 소식을 전달하였습니다. 이를 비동기적으로(다양한 Slack 채널에서) 및 제품 디자인 팀과의 공유 의례 중 하나에서 직접적으로 전달하였습니다.

<div class="content-ad"></div>

"라이브 공유 중에 디자이너들에게 자신이 선택한 아이콘을 디자인하는 실시간 디자인 과제를 주었고, 그래서 우리가 개발한 과정을 즉시 실험해 보았습니다.

# 배운 점

새로운 아이콘 가이드라인과 기여 프로세스를 디자인하는 동안 많은 것을 배웠습니다.

제게 남아 있는 상위 5가지 배운 점은 다음과 같습니다."

<div class="content-ad"></div>

## 1. 펜과 종이를 사용하세요

![이미지](/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_4.png)

Figma 파일을 300%로 확대해서 작업할 때 복잡한 아이콘을 디자인하는 데 열중하기 쉽습니다.

뚱뚱한 마커와 포스트잇, 혹은 심지어 FigJam은 간단한 아이콘을 그리는 데 적합한 추상화 수준입니다.

<div class="content-ad"></div>

## 2. 간단한 도형을 결합해 보세요

![image](/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_5.png)

피그마의 펜 도구로 모든 것을 그리기 시작하고 유혹당할 수도 있습니다. 하지만 사실은, 정사각형, 직사각형, 원 등과 같은 간단한 도형을 결합하는 것이 훨씬 빠르고 간단할 때가 많습니다.

## 3. 컨텍스트에서 테스트하기

<div class="content-ad"></div>

<img src="/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_6.png" />

Figma에서 복잡한 아이콘을 디자인하는 데 빠져들기 쉬운 것처럼, 아이콘이 사용될 맥락을 잊게 되기도 쉽습니다.

디자인한 아이콘을 사용될 화면 내부에 배치하는 것은 아이콘이 개념을 빠르게 전달하는 데 도움이 되는지 여부를 테스트하는 좋은 방법입니다.

## 4. 광학적 정렬

<div class="content-ad"></div>

```markdown
![image](/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_7.png)

Some asymmetric shapes, like triangles, don't have equal visual weight. Icons made of these shapes (e.g. send, play) should be optically aligned for better visual balance. This becomes clearer when placing an icon inside a rounded button.

Adding a circle around your icon can help you determine the correct position for your icon instead of automatically centering it both vertically and horizontally.

## 5. Keep a layered version
```

<div class="content-ad"></div>

![이미지](/assets/img/2024-06-20-Howiconscanbedesignedbyalmostanyone_8.png)

나중에 아이콘을 변경하고 싶어질 수도 있습니다. (예: 수정하거나 애니메이션화)

그러므로 언제나 아이콘의 최종 평면화된 버전 위에 계층화된 버전을 유지하는 것이 편리합니다.

## 보너스: Figma 단축키로 시간을 절약하세요

<div class="content-ad"></div>

길을 따라서, Figma에서 아이콘을 디자인할 때 클릭 수를 많이 줄일 수 있는 2가지 키보드 단축키를 발견했어요:

- ⌥⌘O: 획의 윤곽을 그리는 단축키입니다. 아이콘을 윤곽으로 디자인할 때 특히 도움이 됩니다.
- ⌘E: 아이콘을 펼치는 단축키입니다. 아이콘을 내보내기 전에 레이어를 합치는 데 특히 유용합니다 (하지만 레이어 버전을 미리 유지해 두는 것이 좋아요).

# 마지막으로

백마켓에서는 아이콘이 시간이 지남에 따라 발전해 왔어요. 디자이너가 더 많이 기여하면서 아이콘 라이브러리가 성장했을 뿐만 아니라 변화도 일어났어요.

<div class="content-ad"></div>

최근 리브랜딩을 위해 시스템을 테스트한 과정에서 아이콘을 모두 업데이트하기로 결정했어요. 그때 아이콘의 스트로크를 1에서 1.5픽셀로 변경하여 새로운 폰트 무게에 더 잘 어울리고 가독성을 높이기로 했죠. 리브랜딩을 구현하는 과정이 얼마나 빠른지를 보는 것도 정말 재미있었고, 모든 디자이너들이 일관된 아이콘을 만들고 검토하며 기여할 수 있는 능력을 가지게 된 것도 좋았어요.

지금까지 글을 읽어주셨다면 이 이야기가 도움이 됐다면 아래의 박수나 댓글 아이콘을 클릭하지 않으세요. 

만약 저희 디자인팀이나 다른 백마켓 부서에 합류하고 싶다면, 여기를 한번 들여다보세요. 우리 팀은 늘 성장 중이에요! ✨

이 글을 검토해주신 Eugena Ossi, Florian Lissot, 그리고 Ray Ho에게 특별히 감사드립니다!