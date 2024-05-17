---
title: "오픈 소스 리액트 UI 라이브러리 구축하기 - 2일째"
description: ""
coverImage: "/assets/img/2024-05-16-BuildinganOpenSourceReactUILibraryDay2_0.png"
date: 2024-05-16 19:18
ogImage:
  url: /assets/img/2024-05-16-BuildinganOpenSourceReactUILibraryDay2_0.png
tag: Tech
originalTitle: "Building an Open Source React UI Library — Day 2"
link: "https://medium.com/@m.cavallo1011/building-an-open-source-react-ui-library-day-2-f865e355ecb9"
---

<img src="/assets/img/2024-05-16-BuildinganOpenSourceReactUILibraryDay2_0.png" />

두 번째 날 다시 방문해 주셔서 환영합니다. 오픈 소스 React UI 라이브러리를 만드는 시리즈의 두 번째 날입니다!

오늘은 모든 것을 준비하는 과정이었습니다. 우리가 지금까지 얼마나 진전했는지 살펴봅시다.

# 프로젝트 설정하기

<div class="content-ad"></div>

## 1. Git 저장소 구성하기

우선, GitHub의 EtnaUI라는 조직 아래 etna-ui라는 새로운 Git 저장소를 설정했습니다. 여기서 저장소를 확인할 수 있어요. 이 저장소는 앞으로 코드와 협업을 위한 중앙 허브 역할을 할 거에요.

![GitHub 저장소](/assets/img/2024-05-16-BuildinganOpenSourceReactUILibraryDay2_1.png)

## 2. React 프로젝트 부트스트래핑하기

<div class="content-ad"></div>

다음은 React 프로젝트를 처음부터 시작하는 방법을 설명하겠습니다. Create React App을 사용하는 대신에 번들러로 Vite를 선택했습니다. Vite는 빠르고 간단하다는 것으로 알려져 있어서 개발 프로세스를 효과적으로 해결하는 데 도움이 될 것입니다. 아래는 설정하는 방법입니다:

```js
pnpm add react react-dom
pnpm add -D vite @vitejs/plugin-react
```

또한, vite.config.ts 파일을 구성하여 React 플러그인을 포함하도록 설정했습니다:

```js
// vite.config.ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
});
```

<div class="content-ad"></div>

## 3. 패키지 매니저 선택

페키지 관리를 위해 pnpm@9를 사용하기로 결정했어요. PNPM은 다른 패키지 매니저에 비해 디스크 공간을 더 효율적으로 사용하며 빠릅니다. 게다가, 서로 다른 개발 환경에서도 일관성을 유지하기 위해 Node.js 버전을 관리하기 위해 Volta를 사용하고 있어요.

## 4. 첫 번째 컴포넌트 생성

기본 설정이 완료되었으니, 첫 번째 컴포넌트를 만들었어요: 간단한 `Button` 컴포넌트입니다. 이 초기 컴포넌트를 사용하여 모든 것이 정상적으로 작동하는지 테스트할 예정이에요.

<div class="content-ad"></div>

아래는 Button 컴포넌트를 간단히 살펴볼 수 있어요:

```js
import { ButtonHTMLAttributes } from "react";

import "./Button.scss";

export interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: "primary" | "secondary";
  size?: "small" | "medium" | "large";
}

export const Button = ({ className, size = "medium", variant = "primary", ...props }: ButtonProps) => (
  <button className={`button button--${variant} button--${size}`} {...props} />
);
```

그리고 함께 사용되는 SCSS 파일은 아래와 같아요:

```js
.button {
  border: 1px solid #ccc;
  border-radius: 4px;
  cursor: pointer;
  display: inline-block;
  font-size: 14px;
  font-weight: 500;
  line-height: 1.5;
  padding: 8px 16px;
  text-align: center;
  text-decoration: none;
  transition:
    background-color 0.3s,
    border-color 0.3s,
    color 0.3s;

  &--primary {
    background-color: #8a4dff;
    color: #ffffff;

    &:hover {
      background-color: #6f3aff;
    }

    &:active {
      background-color: #4d1aff;
    }
  }

  &--secondary {
    background-color: #d6baff;
    color: #000000;

    &:hover {
      background-color: #b38cff;
    }

    &:active {
      background-color: #8a4dff;
    }
  }

  &--small {
    font-size: 12px;
    padding: 6px 12px;
  }

  &--medium {
    font-size: 16px;
    padding: 10px 20px;
  }

  &--large {
    font-size: 18px;
    padding: 12px 24px;
  }
}
```

<div class="content-ad"></div>

## 5. Sass 지원 추가하기

우리의 컴포넌트를 스타일링하기 위해, 종속성으로 Sass 지원을 추가했어요:

```js
pnpm add sass
```

## 6. TypeScript 구성하기

<div class="content-ad"></div>

TypeScript은 우리의 설정에서 중요한 부분으로, 타입 안전성과 개발자 경험을 향상시켜줍니다. tsconfig.json을 설정하는 데 시간을 소비해서, 프로젝트의 요구에 맞게 맞추었어요. TypeScript 구성에 대해 더 깊이 파고들고 싶다면, 이 가이드가 매우 유용했어요.

```js
{
  "compilerOptions": {
    /* 언어 및 환경 */
    "target": "ESNext",                                  /* 생성된 JavaScript에 대한 JavaScript 언어 버전 및 호환 라이브러리 선언을 포함하도록 설정. */
    "jsx": "react-jsx",                                /* 생성된 JSX 코드를 지정합니다. */

    /* 모듈 */
    "module": "ESNext",                                /* 생성된 모듈 코드를 지정합니다. */
    "moduleResolution": "Bundler",                     /* TypeScript가 지정된 모듈 지정자에서 파일을 어떻게 찾는지를 지정합니다. */
    "noEmit": true,                                   /* 컴파일 중에 파일을 생성하지 않도록 설정합니다. */

    /* 타입 확인 */
    "strict": true,                                      /* 모든 엄격한 타입 확인 옵션을 활성화합니다. */
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```

## 7. Prettier 설정하기

코드를 깔끔하고 일관되게 유지하기 위해 Prettier를 설치하고 구성했어요. 지금은 우리의 요구에 충분한 기본 구성을 사용하고 있어요.

<div class="content-ad"></div>

```js
pnpm add -D prettier
```

## 프로젝트 실행하기

모든 것이 올바르게 설정되었는지 확인하기 위해 dev 스크립트를 사용하여 프로젝트를 실행했습니다. 이 스크립트는 웹 서버를 시작하고 데모 페이지를 로드하여 Button 구성 요소를 테스트했습니다.

```js
pnpm dev
```

<div class="content-ad"></div>

<img src="/assets/img/2024-05-16-BuildinganOpenSourceReactUILibraryDay2_2.png" />

앞으로는 더 포괄적인 컴포넌트 설명과 테스트를 위해 Storybook을 사용할 계획입니다.

# Package Configuration

여기에 필요한 모든 종속성과 스크립트가 포함된 package.json 파일을 살펴보겠습니다:

<div class="content-ad"></div>

```json
{
  "name": "etna-ui",
  "author": "Matteo Cavallo",
  "description": "EtnaUI는 이탈리아에서 사랑을 담아 만들어진 종합적인 디자인 시스템입니다.",
  "type": "module",
  "files": ["dist"],
  "scripts": {
    "dev": "vite"
  },
  "peerDependencies": {
    "react": "^18.3.0",
    "react-dom": "^18.3.0"
  },
  "devDependencies": {
    "@types/react": "^18.3.2",
    "@types/react-dom": "^18.3.0",
    "@vitejs/plugin-react": "^4.2.1",
    "prettier": "^3.2.5",
    "sass": "^1.77.1",
    "typescript": "^5.4.5",
    "vite": "^5.2.11"
  }
}
```

# 다음 단계

기초 세팅이 완료되었으므로 나머지 컴포넌트를 구축할 준비가 되었습니다. 아직 해야 할 몇 가지 항목들이 있습니다:

- 적절한 폴더 구조 설정
- 컴포넌트 문서화 및 테스트를 위해 Storybook 구현
- Jest를 이용한 단위 테스트 구성
- CI/CD 파이프라인 설정
- 변형에 대해 CVA 사용 여부 고려
- 스타일링을 위해 BEM 사용 여부 고려
- 코드 품질을 위한 ESLint 추가

<div class="content-ad"></div>

일상적인 진행 상황 업데이트를 계속해서 공유할 테니 기다려주세요. 지금 당장은 GitHub에서 프로젝트의 현재 상태를 확인할 수 있어요.

이 여정을 따라와 주셔서 감사합니다. 아래 댓글에 궁금한 점이나 제안 사항을 자유롭게 남겨주세요. 함께 멋진 것을 만들어봐요!

즐거운 코딩 되세요!
