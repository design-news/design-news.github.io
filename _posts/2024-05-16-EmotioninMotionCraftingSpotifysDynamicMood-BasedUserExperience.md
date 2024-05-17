---
title: "감정이 흐르는 중 Spotify의 동적 분위기 기반 사용자 경험 만들기"
description: ""
coverImage: "/assets/img/2024-05-16-EmotioninMotionCraftingSpotifysDynamicMood-BasedUserExperience_0.png"
date: 2024-05-16 19:24
ogImage: 
  url: /assets/img/2024-05-16-EmotioninMotionCraftingSpotifysDynamicMood-BasedUserExperience_0.png
tag: Tech
originalTitle: "Emotion in Motion: Crafting Spotify’s Dynamic Mood-Based User Experience"
link: "https://medium.com/@josephinekim1591/emotion-in-motion-crafting-spotifys-dynamic-mood-based-user-experience-f28f0acd0e3e"
---


프레젠테이션: [여기를 클릭하여 Google 프레젠테이션을 확인하세요](https://docs.google.com/presentation/d/1cE0bltYeKXh4U4kmowe1C95n4yHTiHLKSNVCqGZQMLM/edit?usp=sharing)

현재 대학생들에게 가장 널리 사용되는 음악 청취 앱은 Spotify입니다. 플레이리스트를 공유하거나 친구들과 블렌드를 만들어내는 것부터 학생 할인 혜택을 제공하는 등, Spotify는 다른 사람들과 소통하기 쉽도록 만든 매우 다재다능한 플랫폼입니다.

그러나 과거 청취 습관에 관한 모든 데이터를 포함하고 있음에도 불구하고, Spotify의 추천은 역사적으로 부정확하고 보이기에 임의적이라고 알려져 왔습니다. 이 문제를 해결하기 위해 다음과 같은 문제를 도출했습니다.

사람들의 문제: Spotify 사용자로서, 현재 기분과 상황에 맞는 음악을 발견하여 청취 경험을 향상시키고 싶습니다. 그러나 이를 잘 할 수 없는 이유는...

<div class="content-ad"></div>

1. 스포티파이의 추천은 주로 지난 청취 습관을 기반으로 하며, 내 실시간 기분이나 특정 상황을 고려하지 않습니다.
2. 현재 기분에 맞는 재생 목록을 수동으로 검색하고 선별하는 과정은 시간이 많이 소요되며, 원하는 정확도가 아닙니다.

# 사용자 조사

나는 스포티파이 인터페이스와 기능에 익숙한 열정적인 음악 청취자인 세 명의 학생을 대상으로 사용자 조사를 진행하기로 결정했습니다. 각 사용자에게 전반적인 경험과 가장 자주 사용하는 스포티파이 기능을 설명하고, 어떻게 앱을 일반적으로 사용하는지 안내해달라고 요청했습니다. 이 세 가지 인터뷰에서 모두 사용자들이 앱에 대한 만족도가 높고 협업적인 재생 목록과 "Blended Playlists"와 같은 소셜 기능에 큰 관심을 가진다는 공통 주제가 나타났습니다.

그러나, 사용자들은 스포티파이의 추천 정확도와 홈페이지 인터페이스의 불편함에 대한 불만을 표현했습니다. 한 사용자는 맥북의 인터페이스가 모바일 앱 인터페이스보다 훨씬 좋아한다며 인터뷰에서 이를 보여주었습니다. 이러한 새로운 결과를 고려하여, 나는 사람들의 문제를 더 잘 다루기 위해 조정했습니다:

<div class="content-ad"></div>

사용자 문제: 다양한 음악 장르를 즐기는 Spotify 사용자로서 변화무순한 기분과 일상 활동에 맞는 사운드 트랙을 자주 찾는데, Spotify의 알고리즘 추천은 때로는 내 일반적인 취향을 반영하기는 하지만, 나의 음악 취향을 세심히 이해하지 못하여 제 관심과 무관한 노래를 추천하는 경우가 있어서,  
Spotify 모바일 앱의 인터페이스, 특히 홈 화면이 아이콘과 단어가 많아서 새로운 장르와 음악을 탐험하고 플레이리스트를 직접 만드는 것이 어려운 점이 있습니다.

# 아이디어 회의

이 새로운 사용자 문제에 따라 해결책을 고민하기 위해 다양한 개인을 모았습니다. 서영과 레이첼 두 명의 친구로, 각각 다른 대학 출신입니다.

<div class="content-ad"></div>

오랜 시간 동안 Figma Jam 보드 브레인스토밍 세션을 진행했는데, 어떻게 하면 우리가 깨달을 수 있을지부터 사용자 문제를 해결하기 위한 기능과 솔루션을 고안하는 것까지 했어요. 그 결과 몇 가지 솔루션을 좁히는 데에 성공했어요:

- 홈 화면 타일을 재배치하기 위한 드래그앤드롭
- 사용자의 건너뛰기 비율 및 듣는 시간을 추적하여 미래의 제안을 개선합니다.
- 노래 중에 바로 ‘좋아요’ 또는 ‘싫어요’를 위한 피드백 버튼 도입
- 사용자가 원하는 배경 이미지 또는 테마 설정 가능
- 최근 재생된 항목을 위한 홈 화면 캐러셀
- 시간에 따라 바뀌는 주/야간 모드 스위칭

# 상호작용 디자인

각 기능을 SWOT 분석하고 이 여섯 가지 기능의 실행 가능성 및 영향을 분석한 후, TA들로부터 피드백을 받은 결과, "노래 중에 바로 ‘좋아요’ 또는 ‘싫어요’를 위한 피드백 버튼"을 구현할 최종 기능으로 결정했어요.

<div class="content-ad"></div>

저는 다음을 충족시키는 이 기능을 선택했습니다:

- 추천에 직접적인 영향을 미침
- 사용자 참여와 제어
- 간단하고 효율적인 기능
- 비교 분석
- 실행 가능성
- 사용자 중심 디자인

게다가, 이 기능은 스포티파이가 제안하는 노래들의 적합성에 직접적인 영향을 미쳐 문제를 다룬다고 믿었습니다. 이는 스포티파이의 단점 중 하나로 관찰되었습니다.

저는 정보 계층도를 디자인하여 앱의 좋아하는 노래 기능과 일치하도록 만들었으며, 이를 통해 기능에 쉽게 접근할 수 있지만 너무 두드러지지 않는 디자인을 유지하면서 양측 사용자와 플랫폼에게 가치 있는 피드백 메커니즘을 제공하도록 했습니다.

<div class="content-ad"></div>

정보 계층 다이어그램을 만든 후에는 앱에서 그 기능을 활용하는 방법을 보여주는 '싫음' 기능에 대한 Low Fidelity Sketches를 만들었습니다. 이전 연구를 활용하여, Spotify의 기존 인터페이스에 적합하도록 앱에 어떻게 구현될 수 있는 아이디어를 생각해 냈습니다.

Low Fidelity Sketches를 만든 후에는 Figma를 활용하여 '싫어요' 기능에 대한 중간 확장을 구현했습니다. 제 탐구들은:

- 노래를 좋아하는 간단한 방법을 제공하여 사용자 참여를 증가시켰으며,
- 즉각적인 긍정적인 피드백을 통해 사용자 경험을 향상시켰습니다.

내 아이디어가 실제로 구현되는 것을 보게 돼 기뻤습니다. 한 걸음 이상 나아간 것 같아서 기분이 좋았습니다. 이제는 머릿속에 있던 단순한 생각이 실제로 현실이 되는 것을 볼 수 있었기 때문입니다.

<div class="content-ad"></div>

# 처음부터 다시 시작하기

하지만, 다른 사람들로부터의 피드백은 예상했던 것만큼 긍정적이지 않았어요. 사람들은 이 새로운 "싫어요" 기능이 내가 겪고 있는 문제를 정확하게 해결해주지 않는다고 생각했고, 이것이 스포티파이에서의 부정적인 경험들에 얼마나 많은 변화를 일으킬지 혼란스러워했어요. 또한, 제 탐구가 매우 중복되었다는 것을 깨달았어요. 제가 막힌 상황에 처해 있었죠.

나머지 시간에 대해 고려하고 여러 가지 선택지를 따져본 뒤, 스포티파이의 홈페이지에 감정 기능을 도입하는 새로운 아이디어를 냈어요. 이 아이디어가 내가 겪고 있는 문제에 훨씬 더 집중할 뿐만 아니라, 사용자의 실시간 감정에 더 적합한 추천을 제공할 수 있게 해줄 거라서 이 아이디어를 정말 좋아했어요.

이 새로운 기능에 대한 저해상도 스케치를 그리고, 이미 지난 중해상도 탐구에서 갖추고 있던 개요를 활용하여 창의적인 비전을 실행에 옮겼어요.

<div class="content-ad"></div>

"Mood(기분)" 기능은 사용자가 현재 기분에 맞게 제안된 앨범/곡 및 기분 플레이리스트를 선별할 수 있도록 해주며, 앱에서 누락된 실시간 적응형 추천 요소를 도입합니다. 위의 플로우는 홈페이지에서 "Choose your mood(기분 선택)" 기능을 보여주며, "Sad(슬픈)" 기분이 선택될 때 선별된 "Suggested albums for you(당신을 위한 추천 앨범)"이 나열됩니다. 또한, 변경 내용을 확인할 수 있는 확정 메시지도 있습니다.

또한, 노래/앨범에 할당된 이모티콘(emoji)도 중요한데, 사용자가 홈페이지로 이동하지 않아도 현재 노래/앨범의 기분을 파악할 수 있게 해줍니다. 이에 사용자의 현재 기분에 따른 선별된 플레이리스트를 제공하는 라이브러리에도 기분 플레이리스트를 추가했으며, 이를 사용자의 음악 취향을 기억하는 알고리즘과 결합했습니다. 추가로, 노래에 할당된 기분을 수동으로 변경할 수 있는 플로우도 만들어, Spotify의 알고리즘이 노래에 대한 기분을 사용자의 정의에 따라 어떻게 할당할지 학습하고 이해할 수 있도록 했습니다.

# 사용자 테스트 및 최종 탐구/프로토타입

내 프로토타입을 사용자 테스트한 후, 선택된 감정에 그림자 효과를 추가하여 홈페이지 배경을 기분에 맞게 변경하여 보다 명확한 확인이 가능하도록 하고, 사용자가 기분이 변경되었고 현재 기분이 무엇인지 명확하게 볼 수 있도록 했습니다. 이는 이모티콘 배경 색상과 블랙 스포티파이 테마 사이의 강렬한 대조를 완화시켜줍니다. 또한, 기쁨 이모티콘을 다른 이모티콘과 일관성이 있도록 보다 환영받는 눈웃음을 한 이모티콘으로 변경하여 모든 플로우에 일관성을 부여했습니다."

<div class="content-ad"></div>

# 결론

음악 스트리밍의 디지털 랜드스케이프가 발전함에 따라 Spotify와 같은 플랫폼은 개인 청취 경험을 계속 향상시키고 있습니다. 그러나 음악 추천을 사용자의 현재 기분과 일치시키는 것이 중요한 과제로 남아 있습니다. Spotify 홈페이지에 감정 기능이 도입된 것은 이러한 요구에 대한 전략적 대응으로, 청취자들이 실시간 감정을 기반으로 음악을 맞춤 설정하여 더 직관적이고 만족스러운 사용자 경험을 약속합니다. 이 기능은 인터페이스 조정이나 재생 목록 옵션과 같은 일반적인 향상보다 더 돋보이며, 일상적인 음악 청취를 더 매력적이고 감정적으로 공감할 수 있는 활동으로 변화시킬 수 있습니다.