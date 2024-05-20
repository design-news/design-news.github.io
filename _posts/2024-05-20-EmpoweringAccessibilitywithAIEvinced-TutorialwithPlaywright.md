---
title: "AI로 접근성 향상하기 Evinced - Playwright로 하는 튜토리얼"
description: ""
coverImage: "/assets/img/2024-05-20-EmpoweringAccessibilitywithAIEvinced-TutorialwithPlaywright_0.png"
date: 2024-05-20 23:35
ogImage: 
  url: /assets/img/2024-05-20-EmpoweringAccessibilitywithAIEvinced-TutorialwithPlaywright_0.png
tag: Tech
originalTitle: "Empowering Accessibility with AI: Evinced -Tutorial with Playwright"
link: "https://medium.com/@saifsahil/empowering-accessibility-with-ai-evinced-tutorial-with-playwright-bfe1657963c8"
---


디지털 환경은 끊임없이 진화하고 있으며, 이에 따라 포괄적 웹 애플리케이션을 만드는 책임이 발생합니다. 접근성은 더 이상 선택 사항이 아니라 필수 사항입니다. 수천만 명의 사용자가 보조 기술에 의존하거나 다양한 기능을 가지고 있기 때문에, 접근성 지원을 통해 이해 관계자들은

- 사용자 베이스 확장: 보다 다양한 사용자가 응용 프로그램과 상호 작용하고 혜택을 받을 수 있습니다.
- 브랜드 평판 향상: 접근성에 대한 헌신은 포용성과 사회적 책임을 나타냅니다.
- 법적 요구 사항 준수: W3C 웹 접근성 이니셔티브(WAI)의 웹 콘텐츠 접근성 가이드라인(WCAG) 2.1과 같은 접근성 표준은 준수가 점점 중요해지고 있습니다.

문제 제기

보통 접근성 테스트는 대부분 수동 방법이나 부분 자동화에 의존하며, 테스터는 브라우저 확장 프로그램인 WAVE나 Axe 등을 사용하여 접근성 문제를 꼼꼼하게 조사하거나 수동으로 처리하거나 자동화 도구를 사용하여 접근성 확장 기능과 상호 작용하도록 만든 후 문제를 식별하게 됩니다. 이는 시간이 많이 소요되고 주관적이며 오류가 발생할 수 있습니다. 또한 특정 접근성 기준에만 초점을 맞추거나 결과를 수동으로 해석해야 하기 때문에 테스트 커버리지에 잠재적인 공백이 발생할 수 있습니다.

<div class="content-ad"></div>

Evinced: AI 기반의 접근성 자동화 도구

Evinced는 접근성 문제를 자동으로 식별하고 보고하는 과정을 간소화하는 AI 기반 도구입니다. 기존 UI 테스트 자동화 스위트에 신속하게 통합되어 '플러그 앤 플레이' 솔루션으로 제공됩니다. 포괄적인 보고 기능을 제공하며 인기 있는 웹 자동화 도구(Selenium, Cypress, WebdriverIO, Playwright)용 SDK와 Java, C#, Ruby, JavaScript 같은 다양한 언어를 지원합니다.

Playwright (Typescript)와 함께 Evinced 설정하는 방법:

이 튜토리얼은 Typescript로 작성된 Playwright 테스트 스위트에 Evinced를 통합하는 방법에 대해 안내합니다:

<div class="content-ad"></div>

- npm 프로젝트의 종속성으로서 Evinced 라이브러리가 필요합니다. 현재 Evinced 라이브러리는 비공개로 접근 가능합니다. package.json에서 evinced를 종속성으로 추가하고 다운로드하기 위해 Evinced 팀에 문의해야 합니다. 설정이 완료되면 아래 명령을 실행하여 라이브러리를 다운로드할 수 있습니다.

```js
npm i
```

2. 라이센스 설정: 계속 진행하려면 유효한 Evinced 라이센스가 필요합니다. 오프라인 자격 증명이 있으면 setOfflineCredentials 메서드를 사용하여 구성해야 합니다:

```js
import { setOfflineCredentials } from '@evinced/js-playwright-sdk';

setOfflineCredentials({
    serviceId: process.env.AUTH_SERVICE_ID,
    token: process.env.AUTH_TOKEN,
});
```

<div class="content-ad"></div>

3. Evinced 서비스 초기화 (beforeEach):

`beforeEach` 훅 내에서 `evincedService`를 시작하여 테스트 중에 계속 스캔이 이루어지도록합니다:

```js
let evincedIssues: Issue[];

test.beforeEach(async ({ page }, testInfo) => {
  const evConfig = JSON.parse(fs.readFileSync(path.resolve(__dirname, '<evConfig.json 경로>'), 'utf8'));
  const evincedService = new EvincedSDK(page);
  await evincedService.evStart(evConfig);
});
```

위 코드는 Axe의 구성을 제어하는 추가 파일인 `evConfig.json`또한 설정합니다. 이 파일을 통해 스크린샷의 활성화/비활성화, 특정 로케이터/URL/유효성 검사 유형에 대한 유효성 검사 생략을 구성할 수 있습니다. 샘플 json 파일 구성은 아래에 제공되었습니다.

<div class="content-ad"></div>

```json
{
    "axeConfig": {
        "rules": {
            "link-name": {
                "enabled": false
            }
        }
    },
    "skipValidations": [
        {
            "selector": ".classname",
            "urlRegex": ".*google.com",
            "validationTypes": ["AXE-COLOR-CONTRAST"]
        }
    ]
}
```

4. Issue Collection (afterEach):

Stop the `evincedService` engine in the `afterEach` block and collect all identified issues:

```javascript
test.afterEach(async () => {
  evincedIssues = evincedIssues.concat(await evincedService.evStop());
});
```

<div class="content-ad"></div>

5. 보고서 작성 (afterEach 또는 afterAll):

evincedService.evSaveFile 메소드를 사용하여 접근성 보고서를 생성하세요. 아래는 HTML 보고서에 문제점을 저장하는 예시입니다:

```js
test.afterAll(async () => {
  await evincedService.evSaveFile(evincedIssues, 'html', 'results/evincedReport.html');
});
```

이 코드는 문제점을 HTML로 내보내는 방법을 보여줍니다. Evinced는 CSV 및 JSON과 같은 포맷도 지원합니다.

<div class="content-ad"></div>

Evinced Reports:

Evinced 보고서는 다음과 같은 소중한 통찰을 제공합니다:

- 문제 유형
- 심각도 수준
- 영향 받는 URL
- 요소 선택기
- 선택 사항으로 스크린샷

추가적으로 고려할 사항:

<div class="content-ad"></div>

- 이슈 필터링:  Evinced 내의 이슈 객체는 웹 접근성 결과를 더 상세히 분석하기 위한 필터링 기능을 제공합니다.
- 스크린샷 통합: evConfig.json 또는 EvInitOptions 구성 내에서 스크린샷을 활성화하면 보고된 이슈에 대한 가치 있는 시각적 맥락을 제공할 수 있습니다.

공식 문서 — https://developer.evinced.com/sdks-for-web-apps/playwright-js-sdk

웹 접근성은 지속적인 여정입니다. UI 자동화를 수행하는 동안 Evinced를 정기적으로 활용하면 접근성 장애물을 지속적으로 식별하고 개선할 수 있습니다. 이는 결국 모든 사용자를 위해 포용적인 디지털 환경을 구축하는 데 기여합니다.