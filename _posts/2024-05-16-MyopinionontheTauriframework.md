---
title: "Tauri 프레임워크에 대한 나의 의견"
description: ""
coverImage: "/assets/img/2024-05-16-MyopinionontheTauriframework_0.png"
date: 2024-05-16 23:20
ogImage:
  url: /assets/img/2024-05-16-MyopinionontheTauriframework_0.png
tag: Tech
originalTitle: "My opinion on the Tauri framework"
link: "https://medium.com/@nfrankel/my-opinion-on-the-tauri-framework-1721255f3abf"
---

![Screenshot](/assets/img/2024-05-16-MyopinionontheTauriframework_0.png)

저는 항상 GUI를 좋아했어요. 데스크톱 기반과 브라우저 기반 둘 다요. 특히 후자는 예전에는 필요했던 5년의 교육을 받아야 했죠. 그래서 저는 Vaadin을 사랑했고 지금도 사랑합니다. HTML, JavaScript, CSS를 한 줄도 작성하지 않아도 웹 UI를 개발할 수 있어서 그래요. 몇 년 전에는 JVM 데스크톱 프레임워크의 상태를 분석했죠.

저는 Rust 프로그래밍 언어를 아주 좋아해요.

Tauri는 Rust 기반의 데스크톱 애플리케이션을 만들기 위한 프레임워크에요. 여기에 제 의견을 적어봤어요.

<div class="content-ad"></div>

# 개요

Tauri 앱은 두 가지 모듈로 구성되어 있습니다: 표준 웹 기술(HTML, Javascript 및 CSS)로 작성된 클라이언트 측 모듈과 Rust로 작성된 백엔드 모듈입니다. Tauri는 UI를 전용 Chrome 브라우저 인스턴스에서 실행합니다.

사용자는 UI와 평소와 같이 상호 작용합니다. Tauri는 클라이언트 측 JavaScript와 백엔드 Rust 간에 특정 JS 모듈인 window.**TAURI**.tauri를 통한 바인딩을 제공합니다. 또한 파일 시스템, OS, 클립보드, 창 관리 등 로컬 시스템과 상호 작용하기 위한 다른 모듈도 제공합니다.

바인딩은 문자열을 기반으로 합니다. 다음은 클라이언트 측 코드입니다:

<div class="content-ad"></div>

```js
const { invoke } = window.__TAURI__.tauri;

let greetInputEl;
let greetMsgEl;
greetMsgEl.textContent = await invoke("greet", { name: greetInputEl.value }); //1
```

- greet 명령을 호출합니다.

아래는 해당하는 Rust 코드입니다:

```rust
#[tauri::command]                                                              //1
fn greet(name: &str) -> String {                                               //1
    format!("안녕, {}! 러스트에서 인사 받았어요!", name)
}
```

<div class="content-ad"></div>

- greet라는 Tauri 명령어를 정의하세요.

이후 섹션에서는 Tauri의 좋은 점, 그저 그런 점, 나쁜 점을 나열하겠습니다. 제 의견은 이전 경험에 기반한 주관적인 것이라는 점을 기억해 주세요.

# 좋은 점

- 시작하기:
  다행히도, 최근에는 점차 드문 일이지만, 어떤 기술은 전문가가 되기 전에는 초심자라는 것을 명심해야 합니다. 모든 사이트의 첫 번째 섹션은 기술에 대한 간단한 설명이어야 하며, 두 번째 섹션은 시작하는 방법이어야 합니다. Tauri는 이를 제대로 해냅니다; Quick start 가이드를 따라 몇 분 만에 첫 번째 Tauri 앱을 만들 수 있었습니다.
- 문서:
  Tauri의 문서는 포괄적이고 내용이 풍부하며(제가 훑어 본 한계 내에서), 잘 구조화되어 있습니다.
- 훌륭한 피드백 루프:
  변화의 결과를 보는 데 걸리는 시간인 피드백 루프가 기술을 사용할 수 없게 만드는 경우가 있습니다. GWT, 당신을 바라봅니다. 짧은 피드백 루프는 개발자 경험을 향상시킵니다.
  이 면에서 Tauri는 좋은 평가를 받았습니다. 간단한 cargo tauri dev 명령으로 앱을 실행할 수 있습니다. 앞단이 변하면 Tauri가 다시 로드됩니다. tauri.conf.json에 저장된 것과 같은 메타데이터가 변경되면 Tauri가 앱을 재시작합니다. 유일한 단점은 두 동작 모두 UI 상태가 손실된다는 것입니다.
- 완전한 라이프사이클 관리:
  Tauri는 앱을 개발하는 데 도움을 줄 뿐만 아니라 디버그, 테스트, 빌드 및 배포를 위한 도구도 제공합니다.

<div class="content-ad"></div>

# 그저그런 부분

처음에는 데스크톱 앱을 위한 보편적인 쇼케이스, 파일 이름 변경 앱을 만들고 싶었습니다. 그러나 파일 브라우저 버튼을 사용해 디렉토리를 선택하려고 할 때 문제가 발생했습니다. 먼저, Tauri는 일반적인 JavaScript 파일 관련 API를 사용할 수 없습니다. 대신, 더 제한적인 API를 제공합니다. 더 나쁜 점은 빌드 시 사용 가능한 파일 시스템 경로를 명시적으로 구성해야 하며, 이것들은 열거형의 일부입니다.

현대 소프트웨어에서 더욱 증가하는 것은 보안이라는 것을 알아요. 하지만 모든 다른 앱이 어떠한 디렉토리든 접근할 수 있는 데스크톱 앱에서 이런 제한을 이해하지 못합니다.

# 더 나쁜 부분

<div class="content-ad"></div>

그러나 Tauri의 가장 큰 문제는 그 디자인인데, 보다 구체적으로 말하면 프론트엔드와 백엔드 사이의 분리입니다. 저는 Vaadin의 점이 프론트엔드 관리를 잘한다는 것이며, 프레임워크만 배우면 된다는 것입니다. 이는 백엔드 개발자가 HTML, CSS 및 JavaScript을 다루지 않고도 웹 앱을 개발할 수 있게 합니다.

반면에 데스크톱 프레임워크인 Tauri는 정반대의 선택을 했습니다. 여러분의 개발자들은 프론트엔드 기술을 알아야 할 것입니다.

더 나쁜 점은 이 분리가 브라우저 기술을 사용하여 UI를 만드는 데 만든 요청-응답 모델을 재현한다는 것입니다. 알림: 초기 데스크톱 앱은 사용자 상호작용에 더 잘 맞는 Observer 모델을 사용했습니다. 우리는 이 모델을 웹으로 이식한 후에야 앱을 요청-응답 모델을 통해 설계했습니다. 데스크톱 앱에서 이 모델을 사용하는 것은 내 의견으로는 역행하는 것입니다.

# 결론

<div class="content-ad"></div>

타우리는 개발자 경험을 중심으로 하는 모든 것을 주로 좋아합니다. 웹 기술을 사용하고 좋아하는 경우, 타우리를 시도해보세요.

하지만 나에게는 맞지 않아요: 간단한 데스크톱 앱을 만들기 위해 div의 가운데 정렬 방법이나 플렉스박스 레이아웃에 대해 배우고 싶지 않아요.

더 알아보려면:

- 타우리

<div class="content-ad"></div>

친구야, 2024년 5월 12일자로 A Java Geek에서 원래 발행되었습니다.



