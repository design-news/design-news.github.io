---
title: "리듬 퀘스트 데브로그 66 - 새로운 캐릭터, 새로운 동료"
description: ""
coverImage: "/assets/img/2024-05-17-RhythmQuestDevlog66NewCharactersNewCompanions_0.png"
date: 2024-05-17 22:16
ogImage:
  url: /assets/img/2024-05-17-RhythmQuestDevlog66NewCharactersNewCompanions_0.png
tag: Tech
originalTitle: "Rhythm Quest Devlog 66 — New Characters, New Companions"
link: "https://medium.com/@ddrkirbyisq/rhythm-quest-devlog-66-new-characters-new-companions-e46b43dc4d08"
---

또 다른 달, 또 다른 개발일지입니다. 적어도 일관성은 있군요. 지금까지 8년 동안 그 일관성을 의지해왔는데 (정말 그렇게 오래된 걸까요!?), 이제 앞으로도 나를 이끌어줄 것이라고 희망합니다.

# Rain Girl

이번 달에도 (다시 한번!) 주로 새로운 캐릭터 그래픽에 초점을 맞추었습니다! 먼저, 2014년에 출시된 우리의 Cocoa Moss 게임 "Rain"의 소녀입니다:

![Rain Girl](https://miro.medium.com/v2/resize:fit:1000/0*mUGM-eT-49NiMojD.gif)

<div class="content-ad"></div>

![image](https://miro.medium.com/v2/resize:fit:224/0*TM7X5GwfNjhykmfp.gif)

우산을 추가했기 때문에 조금 더 복잡한 스프라이트 세트였습니다. 왼쪽에서 오른쪽으로 이동하는 것을 주의를 산만하게 하지 않으면서 어떤 곳에선 조그마한 서브픽셀 이동을 느끼게 하려고 했습니다. 포화도도 상당히 높여 색감이 더 다채로운 Rhythm Quest 세계에 잘 어울리도록 했습니다 (이 게임은 완전히 다른 미학을 가지고 있습니다).

![image](https://miro.medium.com/v2/resize:fit:236/0*cpceSlt6_sHL4Cdw.gif)

점프 애니메이션은 꽤 간단했습니다. 왼쪽에서 오른쪽으로의 움직임을 제거하고 후드 운동을 일부 유지하려고 했습니다. 다른 캐릭터들 중에도 점프 시작할 때 움직임의 장면을 짧게 제공하는 잠시 숙이는 프레임이 있습니다.

<div class="content-ad"></div>

Flying도 마찬가지입니다. 날개 그래픽이 포함되어 있습니다.

정말 재미있는 작업이었습니다! 이런 유형의 공격 애니메이션을 만드는 방법을 정말 잘 알게 된 느낌입니다. 사유리의 공격을 참조하여 모션 스미어를 충분히 활용하고, 충격 시 약간의 스트레칭을 넣어서 "회복" 포즈로 돌아가기 전에 등을 돌릴 수 있도록 했습니다. 또한 공격할 때 몸 전체를 사용하여 무게감을 주는 데 도움이 되도록 했습니다.

<div class="content-ad"></div>

![활주](https://miro.medium.com/v2/resize:fit:444/0*pYweRAeTVOAymDEg.gif)

여기 날개 달린 버전이 있어요. 이번에는 더 빠른 속도로 재생됩니다. 빠른 처음 두 프레임에서 스미어가 많은 정보를 전달하는 것을 알 수 있어요.

# 동료들

물론, 'Rain'의 소녀를 추가했다면, 'Rain'의 검은 아가미냥이를 추가할 수 있어야 하는 건 당연하겠죠:

<div class="content-ad"></div>

<img src="https://miro.medium.com/v2/resize:fit:1000/0*YrxGRyH67bRiS2dp.gif" />

<img src="https://miro.medium.com/v2/resize:fit:162/0*zPodiaMrVR6gP92m.gif" />

‘여자 아이’의 스프라이트세트에 또 다른 요소를 추가할 수도 있었지만, 그러면 너무 정적으로 느껴졌을 것 같아요. 이번에는 당신과 미야우미(meowmie) 사이에서 시각적인 차이를 주어, 조금 더 동행자처럼 당신을 따라다니는 느낌을 주고 싶었어요. 그 결과, 당신의 움직임을 따라다니고 일치시키는 동행자를 가질 수 있는 시스템을 만들었답니다:

<img src="https://miro.medium.com/v2/resize:fit:1000/0*eGL7E4t_v-E-uQz1.gif" />

<div class="content-ad"></div>

물론, 이 시스템을 갖추게 되어 다른 귀여운 동료들도 추가할 수 있게 되었어요. 여기엔 덕을 따라다니기 딱 좋은 귀여운 병아리가 있어요:

![Chicky](https://miro.medium.com/v2/resize:fit:120/0*hHUewglOmPdUtzjs.gif)

![Chicky](https://miro.medium.com/v2/resize:fit:1000/0*O51wAukZXv4m-7X_.gif)

# 미아미 프린세스

<div class="content-ad"></div>

다른 게임을 생각하면서 "Watch for Falling Rocks"의 공주가 이 게임에 어울릴 것 같다는 것을 깨달았어요!

![Princess from "Watch for Falling Rocks"](https://miro.medium.com/v2/resize:fit:1000/0*OG2Aq4etRDO2G45K.gif)

그녀의 공격 애니메이션(?)이 실제로 어떻게 작동할지 확신이 없었지만, 그녀의 뛰기/걷기 사이클로 어떻게 할지 보고 결정하기로 했어요.

![Princess running/walking cycle](https://miro.medium.com/v2/resize:fit:186/0*3iajAGJZGsGmYuBW.gif)

<div class="content-ad"></div>

여기 제 초안입니다. 여왽이하는 모습을 정확히 살리고 싶었는데, 그녀의 팔의 부드러운 느낌이 그녀의 디자인의 핵심 요소였다고 생각했기 때문이다. 사실, 여기에서 이를 표현하기 위해 추가 프레임의 애니메이션이 필요했기 때문에, 프린세스의 런 사이클은 다른 캐릭터들과 달리 6프레임이 아닌 8프레임을 가지게 되었습니다!

![이미지](https://miro.medium.com/v2/resize:fit:186/0*_e6k1X1OyQQeEUmn.gif)

여기 손질된 버전입니다. 그녀의 머리는 움직임이 고정되어 있어 너무 정적이고 로봇 같다고 느꼈습니다. 그리고 그녀의 드레스는 형태적으로 원뿔이라서 좌우 움직임을 표현하기에는 적합하지 않았습니다. 그래서 얼굴에 약간의 측면 움직임을 줄 수 있도록 서브픽셀 움직임에 작업했습니다. 추가된 애니메이션 프레임을 가지게 되어 더욱 순수한 느낌이 들게 하였네요. 멋져요!

![이미지](https://miro.medium.com/v2/resize:fit:192/0*meQlcoJbyCok2GVe.gif)

<div class="content-ad"></div>

오랜 시간 동안 점프와 날기 애니메이션을 어떻게 처리해야 할지 고민했어요. 처음에는 레인의 소녀처럼 팔과 발을 고정시켜 놓는 것을 시도했지만, 달리는 애니메이션과 비교했을 때 너무 딱딱해 보여서, 대신에 이런 생각을 떠올렸어요. 팔을 퍼덕이고 자전거를 타듯 움직이게 해보기로 했는데, 그것이 너무 좋아서, 하하. 이 애니메이션의 매력 중 하나는 그녀의 머리가 앞쪽으로 조금 더 기울어져 있는 것인데, 마치 진짜 날려고 노력하는 듯한 느낌이에요. 달리기 애니메이션보다 빠른 속도로 재생하는 것도 이런 "허젼대는" 느낌을 도와줘요.

![image](https://miro.medium.com/v2/resize:fit:1000/0*eOKgfWPERKBg1piv.gif)

![image](https://miro.medium.com/v2/resize:fit:234/0*hunaEHSH93MN5os0.gif)

날기 애니메이션은 팔을 퍼덕이는 동작은 같지만, 이제는 날개가 있어서 더 편안한 느낌이에요. 날개 애니메이션 주기는 3프레임인데, 팔을 퍼덕이는 동작을 잘 보여주려면 4프레임이 필요해서, 맞지 않는 부분이 조금 있어요. 그래도 그것에도 불구하고, 꽤 잘 보이지 않을까 싶어요.

<div class="content-ad"></div>

![Image](https://miro.medium.com/v2/resize:fit:492/0*Juwm0tWIeuB_r8k-.gif)

![Image](https://miro.medium.com/v2/resize:fit:1000/0*uENiD4TC49ndNDGW.gif)

공격 애니메이션은 나쁜데루 알아주면서도 재미있는 요소가 많습니다. 뭔가 마음에 드는 버전을 찾기까지 여러 가지 시도를 거쳤어요. 실은 이것이 제 첫 시도였고, 정말 썩 좋지 않았죠 (하하). 가시 공을 던지는 아이디어가 시각적으로 타당하게 보이는지도 확신이 없었어요. 고만고만한 걸 테스트하려고 대충 넣어본 것 뿐이었죠. 실제로 한 번 히트 후 화면에서 튕겨 나가는 회전하는 공을 만들었어요. 회전하는 발사물이 재미있어 보였다고 느껴졌어요 (비록 좀 이상하지만), 그런데 던지기 애니메이션이 잘 읽히지 않았어요. 그냥 공주가 적을 머리로 밀치는 것만 같아 보였거든.

![Image](https://miro.medium.com/v2/resize:fit:492/0*Zfhz0FCQ8wpt8MGb.gif)

<div class="content-ad"></div>

![이미지](https://miro.medium.com/v2/resize:fit:1000/0*j5PWgnPiNkW5W74r.gif)

2번 시도에서는 약간 야구 투구 움직임을 추구하고 더 명확하게 만드려고 노력했습니다. 그녀의 머리가 더 이상 오른쪽으로 너무 앞으로 굽히지 않게 했으므로 머리로 대리더가 아니라고 보이지 않게끔 노력했습니다. 이것은 분명히 개선되었지만, 여전히 약간 이상하게 읽히고, 가까운 거리에서 투사체를 던지는 개념 전체가 이상하게 보였습니다. (또한, 그녀가 공을 이렇게 던질 수 있다면, 그녀가 왜 적들을 멀리서 공격할 수 없는지 알겠죠..??)

![이미지](https://miro.medium.com/v2/resize:fit:546/0*4S8nAIRV9-vPz2y1.gif)

![이미지](https://miro.medium.com/v2/resize:fit:1000/0*4L6MVsB1Amx6vCec.gif)

<div class="content-ad"></div>

이전 초안을 고려해보고 새 방향으로 나아가기로 결정했어요. 캐릭터가 순간적인 공격을 수행하는 장면이며, 그림자를 던지는 대신 오버헤드 슬램을 하도록 했어요. 이것이 좀 더 합리적인 선택으로 여겨졌고(투사체를 던지는 것이 아닌 가까운 사거리 공격임), 머리 위에 고즈넉한 180도 움직임 구역이 생성되어 잘 드러났어요. 애니메이션 작업을 정리해야 하는 부분이 있지만, 이 새로운 개념에 만족했어요.

![image](https://miro.medium.com/v2/resize:fit:594/0*IydbwQiwsUCPhILx.gif)

![image](https://miro.medium.com/v2/resize:fit:594/0*iVAJ15FfzFer7TL_.gif)

![image](https://miro.medium.com/v2/resize:fit:1000/0*ucpwMaEnnuLNuDIf.gif)

<div class="content-ad"></div>

최종 버전이에요! 처음에는 'Watch for Falling Rocks'의 색상을 기반으로한 가시 공 그래픽을 다른 것으로 교체했고, 몇 프레임에만 나타나는 머리 위의 호를 명확히하기 위해 많은 모션 스미어를 추가했어요.

애니메이션이 적절한 지점에 도달하면, 볼 발사체가 별도의 개체로 스폰되어 올바르게 배치되고 일정한 매개변수가 부여되어 공중을 통과하며 회전을 시작합니다. 여기까지 도달하는 데 많은 노력이 필요했지만, 결과물에 만족해요!

Steam에서 Rhythm Quest를 소망 목록에 오늘 등록하세요! https://store.steampowered.com/app/1635640/Rhythm_Quest/
