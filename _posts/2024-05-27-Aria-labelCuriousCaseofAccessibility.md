---
title: "접근성에 대한 호기심 깊은 사례"
description: ""
coverImage: "/assets/img/2024-05-27-Aria-labelCuriousCaseofAccessibility_0.png"
date: 2024-05-27 19:30
ogImage: 
  url: /assets/img/2024-05-27-Aria-labelCuriousCaseofAccessibility_0.png
tag: Tech
originalTitle: "Aria-label: Curious Case of Accessibility"
link: "https://medium.com/@inigovignesh/aria-label-curious-case-of-accessibility-22c46d6b3def"
---


아리아 레이블에 대해 들어보셨나요?
저는 그 사건이 일어날 때까지 들어본 적이 없었어요...

# 아리아로 이끈 '그 사건'

우리 팀은 끝나지 않는 논쟁에 갇혔어요: 목록을 사용할지 테이블을 사용할지 여부에 대한 것이죠. 이 논쟁으로 팀이 두 그룹으로 나뉘었어요. 🤜 🤛

🙋 저는 다음과 같은 이유로 목록을 사용할 것을 주장했어요:

<div class="content-ad"></div>

- 리스트는 화면 공간을 효율적으로 활용하여 텍스트의 자르기나 가로 스크롤링을 피합니다. 특히 운동 능력이 제한된 사용자들에게는 도전적일 수 있습니다.

![이미지](/assets/img/2024-05-27-Aria-labelCuriousCaseofAccessibility_0.png)

2. 유연성과 적응성: 리스트는 유연하고 적응력이 있어 반응형 디자인에서 다양한 화면 크기에서 잘 작동합니다.

![이미지](https://miro.medium.com/v2/resize:fit:1400/1*DJQ_3ymyqWIbBpB2XetORA.gif)

<div class="content-ad"></div>

3. 리스트는 사용 사례, 맥락 및 환경에 따라 열 데이터를 그룹화할 수 있습니다.

🙋‍♂️ 제 동료들은 몇 가지 포인트로 반격을 했지만, 이것이 우리를 막았습니다:

- 테이블 요소는 데이터 셀, 행 및 헤더(`td`, `tr` 및 `th`) 사이의 관계를 전달하는 명확하고 의미 있는 구조를 제공합니다. 이는 스크린 리더의 접근성을 향상시키고 사용자의 이해를 돕습니다. 목록 구성요소는 이러한 내재적인 구조를 갖지 않아 접근성을 보장하지 못합니다.

<img src="https://miro.medium.com/v2/resize:fit:800/0*oJhSgKO9GazDco4a.gif" />

<div class="content-ad"></div>

접근성을 주제로 한 사논이 우리들을 당황하게 했어요. 결의책이 안 보이자 팀은 흩어졌어요. 아무도 목록이 미접근성으로 인해 다양한 화면에서 제대로 작동하지 않는다는 사실에 중요하게 생각하지 않은 것 같았어요. 모든 논쟁 뒤에 나는 지쳐 있었고, 처음으로 접근성 개념에 답답함을 느꼈어요. 😖

포기하고 싶지 않았지만, 선택의 여지가 없는 듯했어요...
고민할 때마다 구글과 마이크로소프트의 산업 트렌드를 참고할 수 있었어요. 특히, 마이크로소프트는 기업의 요구 사항을 충족시키는 다양한 구성 요소와 패턴으로 나의 최애였어요.

OneDrive의 열에 그룹화된 데이터를 본 기억이 나서, 그들이 테이블을 사용하지 않았다는 것을 암시했어요. 그러나 마이크로소프트가 정말로 접근성을 희생할까? 코드를 검사해보니 테이블이 사용되지 않았음을 확인했고, 절충안이 있을 것이라는 것이 나타났어요.

<div class="content-ad"></div>

하지만 어떤 일이 벌어지고 있었을까요? 🤔
맹목적인 열머리글이 없기 때문에 접근성을 희생하고 있는 걸까요? 무언가가 이상했고, 중요한 발견이 손에 미치지 못한 것 같았어요.

![이미지](/assets/img/2024-05-27-Aria-labelCuriousCaseofAccessibility_2.png)

제가 크롬에서 화면 리더기 익스텐션을 사용해 UI를 테스트하기 시작했어요. 놀랍게도, 화면 리더기가 UI에 표시되지 않는 내용을 읽어주며 청각 신호에 의존하는 사용자들을 돕기 위한 추가적인 맥락을 제공했어요.

![이미지](/assets/img/2024-05-27-Aria-labelCuriousCaseofAccessibility_3.png)

<div class="content-ad"></div>

OneDrive의 목록보기에서는 한 열에 두 줄의 데이터가 있었습니다: 파일 이름과 파일 위치입니다. 그러나 'Name'이라는 단일 열 머리글만 있었습니다. 위치 정보를위한 별도의 머리글이없었지만 화면 판독기가 이를 어떻게 처리하는지 깜짝 놀랐습니다. 먼저 파일 이름을 그대로 읽은 다음 두 번째 줄을 "파일 위치: [위치 이름]"으로 읽었습니다. 제가 깜짝 놀랐고, 놀라웠으며 기쁩니다.

하지만 작업은 아직 끝나지 않았습니다. 즉시 코드를 다시 확인하고 같은 문장이 aria-label 옆에 화면 판독기에 읽힌 것을 발견했습니다.

```js
<button role="link" class="nameCellBottom_f2481133" aria-label="위치: 내 파일" data-actions="[{&quot;key&quot;:&quot;item-open-location&quot;}]" data-is-focusable="true">내 파일</button>
```

그 순간 나를 깨우치게 한 것은 제 유레카 순간이었습니다. 빠르게 aria-label에 대해 온라인으로 검색하고 내 우승 주장을 초안으로 작성하기 시작했습니다 🤟

<div class="content-ad"></div>

```markdown
![image](https://miro.medium.com/v2/resize:fit:640/0*Df4ES0n4Skq8B5LO.gif)

Here it comes...

# 🚩 The Problem

Lack of semantic structure using column header for list:
```

<div class="content-ad"></div>

# 💡 솔루션

## 예시 1: (필터 칩)

![image](/assets/img/2024-05-27-Aria-labelCuriousCaseofAccessibility_4.png)

## 예시 2: (리스트)

<div class="content-ad"></div>

표 보기와 같이 내장된 의미 연결은 없지만, 목록 보기에서는 aria-label 속성을 사용하여 셀에 관련 의미를 추가할 수 있습니다. 이렇게 하면 목록이 표만큼 접근성이 높아지거나, 스크린 리더에 추가 정보를 전달하여 UI가 더 포괄적이 될 수도 있습니다.

# aria-label을 사용할 때 고려해야 할 사항:

## 1. 중복 피하기:

aria-label이 기존에 보이는 레이블이나 텍스트 내용을 중복하지 않도록하십시오. 이렇게 하면 사용자에게 혼란을 줄 수 있습니다.

<div class="content-ad"></div>

❌ 중복성의 예시:

```js
<button aria-label="제출" role="button">제출</button>
```

✅ 올바른 사용법:

```js
<button aria-label="주문을 제출하려면 클릭하세요" role=button>제출</button>
```

<div class="content-ad"></div>

## 2. 맥락적 연관성:

aria-label이 사용된 맥락을 주의 깊게 인지하고 해당 요소의 목적이나 기능을 정확히 반영하는지 확인하세요.

❌ 맥락적 무관성:

```js
<img src="icon.png" aria-label="Cog wheel">
```

<div class="content-ad"></div>

✅ 올바른 사용법:

```js
<img src="icon.png" aria-label="설정">
```

## 3. 다국어 고려 사항:

글로벌 대상을 대상으로 하는 경우, 다양한 사용자 그룹을 포함하기 위해 라벨에 다국어 지원을 제공하는 것을 잊지 마세요.

<div class="content-ad"></div>

❌ 언어 고려 없이

```js
<button aria-label="Add to cart">Ajouter au panier</button>
```

✅ 올바른 사용법:

```js
<button aria-label="Ajouter au panier">Ajouter au panier</button>
```

<div class="content-ad"></div>

## 4. 개성을 더하자:

웹 접근성이라고 해서 무미건조하고 지루할 필요는 없어요. aria-label에 약간의 개성을 더하면 당신의 웹사이트가 더 매력적이고 즐겁게 느껴질 수 있어요.

❌ 개성 없는 경우:

```js
<button aria-label="Search">🔍</button>
```

<div class="content-ad"></div>

✅ 개성을 담아:

```js
<button aria-label="다음 모험 찾기!">🔍</button>
```

# 목록 대 테이블

보고서 작성을 마치고 슬랙에 공유했어요. 슬라이드 덱을 만들어 팀에 제시할 수도 있었지만, 그들이 읽고 이해하며 숙고하기를 원했어요. Hin-and-forth conversations이 있었고, 모두가 List View 및 Aria-label의 매력에 동의했어요. 끝나지 않는 토론을 마감하기 위해 회의가 예정되었어요. List view에 대한 빨간 깃발은 던져지지 않았고, 결론이 도출되었어요. 메시지는 엔지니어링 팀에 전달되었어요.

<div class="content-ad"></div>

그런 다음 Flexbox가 List 구성 요소와 유사한 반응형 그리드를 만들 수 있다는 답변을 받았습니다. 와우, List와 Table 간의 대결이 아니라는 것이었군요.

이제 FLEXBOX 대 LIST 대 TABLE입니다. 끝없는 싸움이 시작됩니다!!!

![이미지](https://miro.medium.com/v2/resize:fit:680/0*gGHNr_xgHNkSEqry.gif)

# 결론:

<div class="content-ad"></div>

아리아 레이블의 호기심 많은 경우는 끝나지 않는 토론을 해결해 주지는 못했지만, 이것이 우리에게 미해결된 접근성 문제들의 열쇠를 제공해 주었습니다. 더 이상 접근성을 위해 아름다움을 희생할 필요가 없다는 희망의 빛이 비쳤습니다. ARIA는 접근성과 디자인 감각이 UI 영역에서 공존할 수 있음을 보장합니다.

끝.