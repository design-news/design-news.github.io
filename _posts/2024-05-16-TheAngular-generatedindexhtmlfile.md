---
title: "앵귤러에서 생성된 indexhtml 파일"
description: ""
coverImage: "/assets/img/2024-05-16-TheAngular-generatedindexhtmlfile_0.png"
date: 2024-05-16 23:30
ogImage:
  url: /assets/img/2024-05-16-TheAngular-generatedindexhtmlfile_0.png
tag: Tech
originalTitle: "The Angular-generated index.html file"
link: "https://medium.com/ngconf/the-angular-generated-index-html-file-0918248c082a"
---

## Angular 프레임워크에서 생성된 초기 HTML 마크업을 줄 단위로 검토

![Angular](/assets/img/2024-05-16-TheAngular-generatedindexhtmlfile_0.png)

2012년 런던 올림픽 개회식에서 팀 버너스-리는 1989년의 선구적 제안을 상기시키는 상징적인 출연을 했다. 그가 제안한 하이퍼텍스트 문서와 표준 일반화 마크업 언어(SGML) 기반의 마크업 언어를 포함한 그 구조로부터 지금까지 3십년이 넘도록 사용되는 HTML 태그는 콘텐츠를 명확히 구조화하는 코드와 구분하기 위해 삼각형 괄호를 사용했습니다. 이 결정은 후에 Angular 프레임워크의 어원에 영향을 미쳤습니다.

버너스-리는 이 기술을 스위스 제네바의 CERN에서 근무하며 개발했는데, 이는 인터넷을 통해 과학 문서를 공유하기 위한 것이었고, 그것은 WorldWideWeb라고 이름 붙였습니다.

<div class="content-ad"></div>


<img src="/assets/img/2024-05-16-TheAngular-generatedindexhtmlfile_1.png" />

이 컴퓨터 과학자는 HTML 외에도 Web이 오늘날 우리가 알고 있는 Web에 필수적인 기술로 자리 잡은 다른 주요 기술들, 즉 URI, HTTP 응용 계층 프로토콜, 첫 번째 웹 서버, 그리고 첫 번째 웹 브라우저를 개발했습니다.

지금은 Angular CLI와 같이 강력한 도구를 사용하여 웹 애플리케이션 프레임을 만들고, 초기 HTML 코드부터 관련된 멀티미디어 자원까지 해석해 사용자에게 컨텐츠를 표시하거나 설명할 수 있는 최신 브라우저가 있습니다.

# 시작 시퀀스의 간략한 개요


<div class="content-ad"></div>

Angular 애플리케이션의 전형적인 로딩 순서는 다음 단계를 따릅니다 - 프로세스를 설명하기 위해 과도하게 단순화했습니다:

- 브라우저가 웹 서버에 웹 콘텐츠를 가져오기 위해 초기 요청을 보냅니다.
- 서버가 HTML 파일로 응답합니다.
- 이 HTML 파일을 다운로드하고 구문 분석한 후, 브라우저는 Angular에서 선언된 로직을 실행하고 사용자의 이동을 활성화하는 데 필요한 폰트, 이미지 및 JavaScript 코드와 같은 추가 리소스를 가져와야 함을 발견합니다.
- 브라우저가 이러한 추가 리소스를 가져오기 위해 서버에 요청을 보내고, 서버는 요청된 파일로 응답할 수 있습니다.
- 그 사이에 브라우저는 DOM을 생성하고 유지합니다. DOM은 각 노드가 결과 HTML 문서의 요소를 나타내는 트리 구조입니다. 그 중에는 `app-root`도 있으며, 이는 Angular 앱의 다른 컴포넌트의 부모 요소가 됩니다.
- 최초 DOM 트리 버전이 작성되면, 브라우저는 이를 사용하여 접근성 트리, CSSOM 및 렌더 트리와 같은 다른 모델을 만듭니다. 이 모델은 내용 및 스타일 정보를 기반으로 하여 화면에 그려지기 전에 시각적 요소의 레이아웃을 최종적으로 계산합니다.
- 사용자가 애플리케이션과 상호 작용하는 동안, Angular 프레임워크가 앱 로직을 처리하고 필요에 따라 사용자 인터페이스를 업데이트합니다.

이 모든 것은 웹 서버에서 호스팅되는 다음 텍스트 파일에 대한 요청으로 시작됩니다:

코드 에디터에서 가독성 있는 타이포그래피 및 색상 강조를 사용하여 파일 콘텐츠가 렌더링되었음을 유의하십시오. 기계 간 데이터 처리시 이 문자의 시각적 표현은 중요하지 않으며, 컴퓨터는 단지 라틴 문자 자체가 아니라 내부 코드를 해석합니다. 이 주제에 대한 자세한 내용은 문자 인코딩 섹션을 확인하십시오.

<div class="content-ad"></div>

# 한 줄씩 세심하게 살펴보기

앵귤러 CLI로 'ng new' 명령어를 실행한 후 생성된 기본 HTML 코드를 더 자세히 살펴봅시다.

## 1번째 줄: 문서 유형 선언

```js
<!doctype html>
```

<div class="content-ad"></div>

이렇게 문서 유형 선언을 담은 필수적인 줄은 웹 브라우저가 받는 첫 번째 지시이며, 문서가 특정 HTML 또는 XML 버전으로 작성되었는지를 나타냅니다. 이를 통해 다른 브라우저 및 플랫폼 간 일관성을 보장합니다. 레거시 브라우저에서 doctype이 없으면 잘못된 렌더링 모드가 적용될 수 있어 레이아웃 및 스타일링에 일관성이 무너질 수 있습니다.

HTML 4.01 및 XHTML에서 복잡한 `!doctype ...` 선언을 기억하시나요? W3C가 2008년 1월에 HTML5의 첫 번째 초안을 공식 발표했을 때, 대부분의 사람들은 새로운 doctype이 대소문자를 구분하지 않는 단일 줄로 간소화되어 파일 내용을 더 깔끔하고 읽기 쉽게 만들었다는 것을 기쁘게 알게 되었습니다.

## 라인 #2: HTML 요소

간단히 말해, `html` 요소는 최상위 HTML 문서의 루트를 나타냅니다. 다른 모든 요소는 그 자손이어야 합니다.

<div class="content-ad"></div>

문서의 내용에 대한 자연 언어를 선언하기 위해 RFC 5646에서 정의된 유효한 언어 태그와 함께 lang 속성을 제공해야 합니다. 이는 검색 엔진 및 스크린 리더와 같은 기계가 문서 내용과 메타데이터에 사용된 언어를 올바르게 식별할 수 있도록 도와줍니다. 언어를 지정하지 않으면 보조 기술이 운영 체제의 언어 설정으로 기본 설정되어 발음이 틀릴 수 있습니다.

lang 속성이 루트 요소에 국한되지 않는다는 점을 감안할 가치가 있습니다. 전역 속성으로, 다른 모든 요소에도 적용될 수 있어 다국어 콘텐츨 다루기가 쉽습니다.

HTML 요소에는 텍스트 방향을 나타내는 dir 속성도 포함될 수 있습니다. 히브리어, 아랍어, 페르시아어, 쿠르드어와 같은 오른쪽에서 왼쪽으로 스크립트를 사용하는 언어로 작성된 내용의 경우, dir 속성을 dir="rtl"로 설정하여 올바른 표시가 되도록 할 수 있습니다.

## 줄 #3: 문서의 헤드

<div class="content-ad"></div>

웹 문서가 올바르게 작동하고 검색 엔진이 내용을 이해할 수 있도록 하려면 HTML 파일의 `head`에 모든 필요한 메타데이터를 포함해야 합니다. 이는 스타일 정의, 스크립트 및 필요한 외부 리소스로의 링크를 포함합니다.

## Line #4. 기계 문자 집합

웹 문서를 표시하려면 브라우저가 웹 서버로부터 받은 바이트를 사용자가 이해할 수 있는 콘텐츠로 변환하는 방법을 알아야 합니다. 문자 집합 정의는 브라우저에게 다운로드된 데이터를 해독하여 이해할 수 있는 문자와 가청 가능한 구절로 전환하는 방법을 알려줍니다. 심지어 서버가 HTTP 헤더에서 올바른 정보를 제공하지 않아도 브라우저가 어떻게 디코딩해야 하는지 알려줍니다.

웹에서 가장 많이 사용되는 문자 인코딩인 UTF-8은 1992년 Ken Thompson과 Rob Pike에 의해 처음 제안된 것으로, 거의 모든 인간 언어의 가능한 모든 문자를 나타내는 방법으로 사용되고 있습니다. 10년 후에는 IETF에 의해 표준화되었습니다. `meta charset="utf-8"`은 일반적으로 `head` 요소의 첫 번째 자식으로 배치되지만, 이 줄 이전에 추가 메타데이터나 분석 트래커를 포함해야 할 수도 있습니다. HTML 파일의 첫 1024바이트 내에 문자 집합 정의를 선언하여 성능 저하를 방지해야 합니다. 그렇지 않으면 브라우저가 페이지 로드 중에 다른 기술을 사용하여 문자 집합을 추측하기 위해 소중한 밀리초를 낭비하게 됩니다.

<div class="content-ad"></div>

## Line #5: 제목

Angular는 라우팅 로직을 통해 각 URI에 대해 정적 텍스트를 index.html 파일의 `title` 요소에 하드코딩하는 대신 별도로 선언할 수 있도록 합니다. 각 라우트마다 명확한 제목을 작성해야 하는 이유는 여러 가지가 있습니다:

- UX: 사용자가 여러 브라우저 탭, 창 또는 공간을 가지고 있을 때 현재 보고있는 페이지나 섹션을 이해하는 데 도움이 됩니다.
- SMO 및 북마킹: 사용자가 현재 경로에 해당하는 링크를 저장하거나 공유하기로 결정할 때, 설명적인 제목은 콘텐츠를 빠르게 파악하는 데 도움이 될 수 있습니다.
- SEO 및 구문 분석: 검색 엔진은 페이지 색인 작업 중에 `title` 요소를 우선적으로 고려하므로, 누군가 웹 콘텐츠와 관련된 검색을 수행할 때 페이지 제목에서 키워드 일치가 검색 결과에서 높은 순위로 나타날 수 있습니다. 게다가, 제목 요소는 일반적으로 클릭 가능한 제목으로 사용됩니다.
- 접근성: 시각 장애가 있는 사용자나 화면이 없는 장치를 사용하는 사용자는 웹 문서 제목에 의존하여 콘텐츠를 빠르게 파악합니다. 명확한 제목은 스크린 리더나 유사 기술을 사용하는 모든 사용자의 경험을 크게 향상시킬 수 있습니다.

## Line #6: 베이스 루트

<div class="content-ad"></div>

`base` 요소를 사용하면 웹 응용 프로그램의 모든 상대 경로에 대한 기본 URL을 지정할 수 있습니다. Angular CLI는 기본적으로 href 속성을 /로 설정하므로 Angular 라우터는 응용 프로그램의 루트를 도메인 루트로 처리합니다. 이 설정은 이미지, 스타일, 스크립트 및 기타 연결된 리소스에 대한 상대 URL의 해상도를 용이하게 합니다.

웹 앱이 하위 디렉토리에 배포되거나 다른 도메인에 있는 경우, `base` 태그가 잘못 구성되어 필요한 리소스를 찾지 못하는 Angular 런타임 로직 실패를 방지하기 위해 기본 URL을 업데이트해야 할 수도 있습니다.

## Line #7: 브라우저 뷰포트

웹 개발 문맥에서 "뷰포트"라는 용어는 매력적입니다. "뷰"는 웹 인터페이스의 가시 영역을 의미하며, "포트"는 시각적 콘텐츠가 사용자에게 전달되는 경로로 해석될 수 있습니다.

<div class="content-ad"></div>


![Screenshot](/assets/img/2024-05-16-TheAngular-generatedindexhtmlfile_2.png)

웹페이지의 레이아웃 및 스케일링을 다양한 화면 크기에 맞게 관리하는 방법은 해당 메타 태그에 특정 값을 설정하는 것입니다. 반응형 디자인 요구 사항을 충족하는 데 유용합니다.

이 HTML 태그에는 viewport 매개변수를 지정하는 content 속성이 있습니다:

- 너비와 높이: viewport의 크기를 제어합니다.
- interactive-widget: 시각 키보드, 브라우저 익스텐션, 접근성 도구와 같은 상위 UI 요소의 동작을 지정합니다.
- initial-scale, minimum-scale, maximum-scale: 초기 확대 수준을 설정하고 추가 확대를 제한합니다.
- user-scalable=no: 사용자 스케일링을 막아 WCAG 지침의 일부를 방해하는 것을 방지합니다.


<div class="content-ad"></div>

## 라인 #8: 앱 아이콘

1990년대 이후 웹에서 사용되어온 상징적인 favicon.ico는 현재 다양한 기기와 플랫폼에서 웹사이트를 시각적으로 식별하는 아이콘을 표시하는데 기반이 되었습니다. 현재에도 WebP의 널리히 지원되고 있고 적응형 아이콘을 만들기 위한 SVG의 벡터 기능이 있음에도 불구하고 PNG과 JPG는 웹에서 가장 널리 사용되는 이미지 파일 형식입니다.

각 새 Angular 프로젝트에 포함된 기본적인 favicon.ico를 고정된 비트맵 형식으로 보강하려는 경우 — 이는 크기를 조정할 때 픽셀과 이미지 품질이 희생되는 것을 의미합니다 — 다양한 미디어 상황에서 명확하게 보이는 유동 아이콘의 환상을 만들기 위해 전통적인 픽셀 크기인 16x16, 32x32, 192x192 및 512x512를 사용하는 것이 좋습니다. 그러나 이 기술은 파일 크기, HTTP 요청의 숫자, 그리고 인식된 이미지 품질과 관련된 잠재적인 문제로 인해 성능이 좋지 않을 수 있습니다.

기본 Angular 아이콘의 크기를 조정하는 더 나은 방법은 간단한 SVG 기반 솔루션을 구현하는 것입니다. 이 적응형 방법은 전통적인 점진적 향상 기술을 사용하여, SVG 형식을 읽을 수 없는 경우 이전 브라우저가 ICO 파일 또는 지정된 크기의 PNG 파일을로드할 수 있도록 허용합니다.

<div class="content-ad"></div>

```js
<link rel="icon" type="image/x-icon" href="favicon.ico"> <!-- 예비 아이콘 -->
<link rel="icon" type="image/svg+xml" href="favicon.svg"> <!-- 적응형 아이콘 -->
```

## Line #9, #12, #13: 닫히는 태그

HTML 태그는 마치 경계와 같아요: 요소가 시작되고 끝나는 곳을 브라우저에게 알려줍니다. 이 태그들이 없다면 문서 마크업은 큰 난잡함이 될 것입니다. 슬래시 구문을 사용하여 태그를 닫음으로써 중첩된 요소가 올바르게 부모 요소에 연결되도록 할 수 있어요.

```js
<!-- 내용을 감싸는 태그는 닫혀 있어야 함 -->
<element attribute1="value1">내용</element>
<element attribute1="value1"><child>하위 내용</child></element>
```

<div class="content-ad"></div>

속성 값만 포함하고 내부 콘텐츠가 없는 요소에는 닫는 태그가 필요하지 않습니다. Angular 15.1.0 버전에서는 내용 예측이 없는 사용자 지정 요소에 대한 자체 닫히는 태그를 도입하여 HTML 템플릿의 보일러플레이트를 줄였습니다.

```js
<!-- 자체 닫히는 태그 구문 -->
<element attribute1="value1" attribute2="value2" />
```

## 10번째 줄: 문서의 본문

이것은 문서의 주요 콘텐츠를 둘러싼 필수 HTML 요소입니다. `html` 태그의 두 번째 자식이어야 합니다.

<div class="content-ad"></div>

DOM 내의 다른 요소들과 마찬가지로, 해당하는 HTMLBodyElement 인터페이스는 `body` 태그의 객체지향적 표현입니다. 웹 페이지 레이아웃을 구성하는 요소를 조작하고 제어하는 데 사용할 수 있는 다양한 속성과 메소드가 있습니다.

## Line #11: Angular 앱의 루트 요소

이 목록의 마지막 항목은 `app-root` 태그와 해당합니다. Angular 런타임 프로세스가 애플리케이션이 부트스트래핑 단계를 완료한 후, 메인 컴포넌트의 결과 HTML을 삽입하거나 교체할 루트 요소의 자리 표시자입니다. 메인 컴포넌트의 데코레이터 선언에서 이 태그의 이름을 원하는 대로 바꿀 수 있다는 점을 유의하십시오.

# 기본 요소 이상으로

<div class="content-ad"></div>

SEO 및 SMO를 위해 메타 태그를 추가해야 할 수도 있습니다. 또한, 분석 및 웹 성능 모니터링을 위한 추적 코드를 포함할 수도 있습니다. 특정 코드를 인라인으로 추가해야 하는 경우를 제외하고, 외부 스타일 및 스크립트는 Angular 구성 파일에서 선언하여 이러한 리소스가 효율적으로 로드되도록 해야 합니다.

Google 구조화된 데이터 테스트 도구를 사용하여 유효성을 검사할 수 있는 Schema 표시 방법을 고려해보세요. 또한 JavaScript가 비활성화된 드문 상황을 다루기 위해 'noscript' 요소를 포함할 수 있습니다.

추가로, 검색 엔진이 로봇 메타 태그와 관련된 robots.txt 파일, 웹 저자 humans.txt, 법률 부서의 license.txt 등을 기억하세요. 이러한 파일들은 모두 루트 디렉토리에 위치해야 합니다.

Angular 애플리케이션을 PWA로 변환할 계획이 있다면, Angular CLI는 'ng add @angular/pwa' 명령을 실행한 후 index.html 파일을 자동으로 업데이트하여 테마 색상 메타데이터 선언과 manifest.webmanifest 파일에 대한 링크를 포함합니다.

<div class="content-ad"></div>

제품 전략 및 Angular의 성능에 적합한 요소만 포함하여 HTML 콘텐츠를 최소화해보세요.

또한 브라우저가 일반적으로 문법 오류를 허용하더라도 index.html 및 이어지는 템플릿 파일이 유효한 HTML 코드를 포함하도록 하는 것이 중요합니다. Angular 컴파일러는 많은 오류를 방지하는 데 도움을 줄 뿐만 아니라 Angular Language Service나 ESLint와 같은 도구는 마크업을 작성하는 동안 추가적인 피드백을 제공할 수 있습니다. 이를 통해 다양한 플랫폼 및 브라우저 유형에 견고한 품질의 HTML 전달이 확보됩니다.

# 배포 준비가 되었나요?

마무리 전에 몇 분 동안 ng build 명령을 실행하고 /dist 폴더에 있는 index.html의 출력물을 확인해보세요. 이 파일은 사용자의 브라우저가 웹 서버로부터 가져올 HTML 코드의 최종 버전을 보유하고 있습니다.

<div class="content-ad"></div>

소스 HTML 파일에 추가된 사항을 주목해 주세요. 예를 들어, data-critters-container 속성은 Critters 라이브러리의 부산물로, 애플리케이션의 중요한 스타일을 인라인 처리하여 더 나은 CLS(콘텐츠 레이아웃 안정성) 시각적 안정성을 위한 최적화를 실행합니다.

TypeScript 코드를 대상으로 하는 JavaScript 버전으로 변환하고 선택한 스타일 구문을 순수 CSS로 처리한 후, 웹팩 또는 esbuild를 기반으로 하는 빌드 시스템이 angular.json 파일에 구성된 파일을 압축하고 번들링합니다.

Angular 프레임워크는 기본적으로 다음과 같은 캐시 버스트 해시가 파일 이름에 포함된 연결된 파일을 생성합니다:

- main.js는 Angular 애플리케이션을 부트스트랩하는 데 책임 있는 런타임 코드를 포함한 애플리케이션의 논리를 담고 있습니다.
- styles.css는 애플리케이션과 해당 구성 요소의 전반적인 모양을 정의하는 사용자 정의 스타일을 포함하고 있습니다.
- polyfill.js는 브라우저에 추가 코드를 로드하는 데 도움이 되는 선택 사항 파일입니다. 프레임워크의 초기부터 해당 파일은 현대적인 JavaScript 명령을 오래된 브라우저에서 올바르게 해석할 수 있도록 보장하기 위해서 필수적이었지만, Angular가 레거시 브라우저 지원을 중단하면서 이제 이 파일의 기본 콘텐츠에는 Zone.js 라이브러리 코드만 포함됩니다. Angular 18부터 Zoneless 아키텍처를 실험하는 애플리케이션은 변경 감지를 실행하는 데 이 종속성이 더 이상 필요하지만, 임시로 하이브리드 메커니즘을 지원해야 할 경우 외에는 필요하지 않습니다.

<div class="content-ad"></div>

angular.json 파일 설정과 라우터 레벨의 lazy loading 전략에 따라, 초기 선언 또는 필요 시 로드되는 파일이 더 많이 생성될 수 있습니다.

서버 측 렌더링된 앱에서는 Angular 빌더가 서버에서 Angular 컴포넌트의 초기 HTML 상태를 렌더링하고, 브라우저 배포 디렉토리에 index.html의 사전 컴파일된 버전이 생성됩니다. 이 때 client-side-rendered 버전인 index.csr.html 파일도 함께 생성됩니다.

또한 서버 디렉토리에는 index.server.html 파일이 있어 이 파일에는 이벤트 디스패치 및 UI 상호작용을 관리하는 스크립트가 포함되어 있습니다. 이 경우에는 Critters가 `html` 요소를 클라이언트 측 처리대로 처리하지 않기 때문에 서버 렌더링 중에 크리티컬 CSS 인라인이 수행됩니다.

왜 출력이 압축되지 않았는지 궁금할 수 있습니다. Angular 6에서 공식적으로 중단된 이 기술은 HTML 파일의 크기를 줄이기 위해 불필요한 문자(공백 및 줄 바꿈)를 제거하는 것이었습니다. 이제 이를 다시 빌드 프로세스에 복원하는 것에 대한 제한된 관심이 있으며, 추가로 마크업 압축을 처리하기 위한 새로운 종속성을 도입하는 추가 작업만큼 아주 작은 성능 향상이 충분치 않습니다. 또한 이 주제는 특히 SSR에서 HTML이 원본 마크업에 의존하는 수화 메커니즘을 위해 코멘트 노드까지 보존해야 하는 경우에 특히 관련이 있습니다.

<div class="content-ad"></div>

그만큼 index.html 파일의 성능 최적화가 더 이루어지고 있습니다. CORS 지원 및 폰트 인라인화와 같은 사항이 있습니다. 또한 NgOptimizedImage 지시어를 사용할 때, 미리 연결하는 힌트가 문서의 `head`에 추가되어 사용자 정의 또는 제3자 로더 도메인과 미리 연결하거나, SSR 모드에서는 브라우저에서 중요 자원의 가져오기를 가속화하기 위해 우선적으로 미리 로드해야 할 중요 이미지를 LCP 요소로 설정하기도 합니다. 최적화된 이미지에 대한 자동 조정 사항을 더 알아보려면 이 글을 참고해 주세요:

# 마무리

빌드 시 자동으로 생성된 index.html 파일의 각 세부 사항을 이해하면 Angular 프레임워크 팀과 기여자들이 내린 기술적 설계 결정과 최적화 노력을 알아볼 수 있습니다.

Chrome DevTools나 Firefox 개발자 도구와 같은 검사 도구를 사용하면 Angular 컴포넌트 라이프사이클, 응용 프로그램 상태 및 사용자 상호작용의 다양한 단계에서 결과 DOM 구조를 조사하여 성능, 사용성 및 찾을 수 있도록 응용 프로그램을 최적화할 수 있습니다.