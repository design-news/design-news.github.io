---
title: "호밍 프로젝타일 만들기"
description: ""
coverImage: "/assets/img/2024-05-15-CreatingaHomingProjectile_0.png"
date: 2024-05-15 23:30
ogImage: 
  url: /assets/img/2024-05-15-CreatingaHomingProjectile_0.png
tag: Tech
originalTitle: "Creating a Homing Projectile"
link: "https://medium.com/@shane.makanuilopes/creating-a-homing-projectile-62e0aa0d61c5"
---


<img src="/assets/img/2024-05-15-CreatingaHomingProjectile_0.png" />

최종 플레이어 특별 탄약으로 호밍 미사일을 만들고 싶었습니다. 이를 통해 파워 업을 사용하여 얻게 되는 미사일을 만들고 싶었어요. 이를 위해 다음과 같은 작업이 필요했죠:

- 호밍 미사일 파워 업을 만들기
- 파워 업의 행동 결정하기 — 수집 시 다음 다섯 발의 총알이 호밍 미사일이 되는 방법
- 호밍 미사일 프리팹 만들기
- 호밍 미사일의 동작 결정하기 — 미사일이 가까운 적에게 잠금을 걸고 그 적으로 직접 이동하는 방법

## 호밍 미사일 파워 업 만들기



```markdown
![Homing missile creation step 1](/assets/img/2024-05-15-CreatingaHomingProjectile_1.png)

For the homing missile, I created a blue version of the regular Ammo Power Up. Just like when I made that Power Up, I added this new one to the Power Up ID list and then included it in the balancing system of my Spawn Manager. After ensuring that the new Power Up would spawn correctly, I needed it to trigger a method in the Player.

![Homing missile creation step 2](/assets/img/2024-05-15-CreatingaHomingProjectile_2.png)

In this case, I named it HomingMissileActive().
```



## '파워 업' 동작 결정하기

![이미지](/assets/img/2024-05-15-CreatingaHomingProjectile_3.png)

이 방법은 세 가지 새로운 변수를 사용했어요. 한 가지는 'Homing 미사일 파워 업'이 활성화되었는지를 추적하기 위한 것이고, 다른 하나는 수집 가능한 아이템을 수집할 때마다 미사일 5개 한도를 설정/재충전하는 데 사용되며, 새로운 오디오 클립을 위한 세 번째 변수도 있어요.

![이미지](/assets/img/2024-05-15-CreatingaHomingProjectile_4.png)



이 Power Up은 Triple Shot Power Up과 유사하게 작동하며, 시간 제한 대신 발사 횟수 제한이 있습니다. 따라서 FireLaser() 메서드를 수정하여 Homing Missile Power Up이 활성화되었을 때 실행되도록 if 문을 포함시켰어요.

이 경우에는 문이 해당 Power Up이 활성화되어 있는지, 그리고 _homingMissileCounter 발사 추적 변수에 남아있는 총알이 있는지 확인합니다. 그렇다면 새로운 _homingMissilePrefab을 발사하게 됩니다. 또한 그 if 문 안에는 각 발사 후에 마지막인지 확인하는 또 다른 문도 있습니다. 그렇다면 _isHomingMissileActive bool를 비활성화하고 오디오 클립을 표준 레이저 샷으로 변경하게 됩니다.

## Homing Missile Prefab 생성하기

<img src="/assets/img/2024-05-15-CreatingaHomingProjectile_5.png" />



홈잉 미사일 프리팹은 유니티 에셋 스토어에서 발견한 무료 미사일 스프라이트에요. 플레이어에 사용하는 스프라이트와 동일한 스러스터 애니메이션도 포함했고, 주변의 적이 가까워지면 감지할 수 있는 레이더 빈 오브젝트를 추가했어요. 적들이 회피하는 방법을 만드는 데 사용한 방식과 유사해요.

또한, 이 회피 동작에 대해 생성한 스크립트와, 그리고 파워 업을 파괴하는 동작에 대한 스크립트를 차용해서 "EnemyRadar"를 "Radar"로 변경해서, 이 스크립트 아래에 앞으로 필요한 모든 레이더 작업을 담을 수 있도록 했어요.

![이미지](/assets/img/2024-05-15-CreatingaHomingProjectile_6.png)

스크립트 시작 부분에서, 홈잉 미사일 프리팹을 호출해요. 레이더는 프리팹의 자식 객체이기 때문에 transform.parent를 사용해서 찾을 수 있어요. 그렇게 함으로써 올바른 게임 오브젝트를 찾고 있는지 확인할 수 있어요. 홈잉 미사일은 레이저의 한 형태로 될 것이기 때문에(보호막 펄스와 같이 전체 새로운 스크립트가 아니에요), 호출해야 하는 컴포넌트는 레이저야.



```markdown
![Screenshot](/assets/img/2024-05-15-CreatingaHomingProjectile_7.png)

이 구체적인 레이더에 radarID를 2로 설정한 후, 적과 충돌할 때마다 Laser 스크립트(아래 참조)에서 HomingMissile(GameObject) 메소드를 호출합니다 (검출된 적을 GameObject 필드에 전달함).

## 호밍 미사일의 동작 결정

![Screenshot](/assets/img/2024-05-15-CreatingaHomingProjectile_8.png)
```



레이저 스크립트 내에서 HomingMissile(GameObject) 메서드는 두 가지 새 변수와 함께 작동합니다. 하나는 _lockedOn이 달성되었는지를 결정하고, 두 번째는 _lockedOnTarget을 결정하는 데 사용됩니다.

_lockedOnTarget이 결정되면, null인 if 문을 사용하여 호밍 미사일이 경로상의 다른 적에 잠기지 않도록 방지합니다. 이렇게 함으로써 애니메이션 및 게임 플레이가 더 부드럽고 직관적으로 보입니다.

![이미지](/assets/img/2024-05-15-CreatingaHomingProjectile_9.png)

이러한 변수들은 Update 메서드 내에서 사용되어 _lockedOnTarget으로 Vector3.MoveTowards를 수행합니다.



이 방법 이외에는, 호밍 미사일은 일반 레이저 발사와 동일하게 작동합니다. 그래서 새로운 레이저 ID를 만들거나 다른 동작을 지정할 필요가 없었습니다. 이는 표준 레이저가 사용하는 이동 및 파괴 명령을 사용합니다. 그리고 HomingMissile 방법은 오직 호밍 미사일 파워 업이 활성화된 경우에만 호출되며, 이는 순서상 Prefab이 생성될 때뿐입니다.

이 모든 것이 함께 작동하여, 플레이어는 다음 레벨로 진행하기 위해 특별한 호밍 미사일을 사용할 수 있습니다.