---
title: "MESOP, 새로운 UI 프레임워크"
description: ""
coverImage: "/assets/img/2024-06-20-MESOPaNewUIframework_0.png"
date: 2024-06-20 06:11
ogImage: 
  url: /assets/img/2024-06-20-MESOPaNewUIframework_0.png
tag: Tech
originalTitle: "MESOP, a New UI framework"
link: "https://medium.com/analytics-vidhya/mesop-a-new-ui-framework-a68e49137007"
---


## Google에서 나온 새로운 친구들

![이미지](/assets/img/2024-06-20-MESOPaNewUIframework_0.png)

## 왜 또 다른 UI 프레임워크인가요?

UI 프레임워크의 세계에서 Streamlit와 Gradio 같은 도구들은 이미 상당한 영향을 미쳐왔습니다. 그들은 특히 머신러닝과 데이터 과학 프로젝트를 위한 웹 애플리케이션을 구축하고 배포하는 과정을 간소화했습니다. 그러나 Google 엔지니어들이 개발한 Mesop은 독특한 기능과 장점을 가져와요. Mesop이 기존 UI 프레임워크에 가치 있는 추가물임과 Streamlit와 Gradio와 다른 점을 살펴봅시다.

<div class="content-ad"></div>

큰 언어 모델(Large Language Models, LLMs)을 사용하는 애플리케이션을 개발하는 것은 독특한 도전을 야기합니다. 이러한 애플리케이션을 테스트하고 사용자 피드백을 빠르게 받는 것이 중요합니다. 이러한 도전에 대한 하나의 해결책은 구글이 개발한 새로운 프레임워크인 Mesop입니다. 이 프레임워크는 Python으로 웹 UI를 만드는 프로세스를 간단하게 만들기 위해 설계되었습니다. 이 블로그에서는 Mesop이 무엇인지, 다른 도구들과 비교했을 때 어떤 장단점이 있는지, 그리고 어떻게 Mesop을 사용하여 애플리케이션을 신속하게 구축하고 테스트할 수 있는지 살펴볼 것입니다.

## Mesop 소개

Mesop은 구글 엔지니어들이 20% 프로젝트 시간 중에 개발한 프레임워크입니다. 주로 프론트엔드 기술에 제한이 있는 엔지니어들이 웹 UI를 빠르게 만들 수 있도록 목표로 합니다. Mesop은 다음과 같은 요소들을 제공하여 시작할 수 있도록 도와줍니다:

1. 고수준 구성요소: 채팅 인터페이스, 텍스트 대 텍스트, 이미지 변환 등과 같은 미리 제작된 요소들.
2. 저수준 구성요소: 텍스트 상자, 마크다운 지원, 버튼 등과 같은 요소들을 포함하여 사용자 정의 디자인이 가능합니다.
3. 데모: LLM 플레이그라운드와 같은 예제 프로젝트들을 제공하여 Mesop을 사용하여 다양한 도구를 만드는 방법을 보여줍니다.

<div class="content-ad"></div>

## 주요 기능

1. 빠른 UI 구축: Mesop을 사용하면 UI를 빠르게 만들 수 있어 아이디어를 테스트하고 피드백을 빨리 받을 수 있습니다.
2. Python 기반: Python으로 구축되어 있어 많은 개발자들의 업무 흐름에 매끄럽게 통합됩니다.
3. 오픈 소스: Mesop은 오픈 소스로 모두에게 접근 가능하며 커뮤니티 기여를 장려합니다.
4. 고수준 구성 요소: 채팅 인터페이스, 텍스트 입력, 버튼과 같은 미리 제작된 구성 요소를 제공합니다.
5. Flask 통합: Mesop은 백엔드 처리를 담당하기 위해 Flask를 사용하여 서버 측 작업을 간소화합니다.

## 다른 도구와의 비교

1. Streamlit: 이전에 Google 내에서 인기 있었던 Streamlit은 Snowflake에 인수되어 현재 내부에서 덜 선호되는 것으로 보입니다. Mesop은 Google의 내부 대안으로 볼 수 있습니다.
2. Gradio: Hugging Face에 인수된 Gradio는 빠르게 UI를 구축하는 또 다른 인기 있는 도구입니다. 그러나 Mesop은 Google 엔지니어들을 위해 더 많은 제어와 사용자 정의 옵션을 제공합니다.

<div class="content-ad"></div>

## 간단한 챗봇 만들기

Mesop, LangChain 및 Groq를 사용하여 간단한 챗봇을 만드는 방법을 살펴봅시다.

- Mesop 설정: 먼저 필요한 패키지를 가져와야 합니다.

```js
import Mesop as me
import Mesop.labs as mel
```

<div class="content-ad"></div>

2. 채팅 기능 정의: 채팅 상호작용을 처리하는 기능을 생성해보세요.

```js
def transform(user_input, chat_history):
    # 히스토리를 하나의 문자열로 결합
    history_string = "\n".join([f"{msg['role']}: {msg['content']}" for msg in chat_history])
    response = run_conversation_chain(user_input, history_string)
    return response
```

3. 채팅 인터페이스 초기화: Mesop의 구성 요소를 사용하여 채팅 인터페이스를 만들어보세요.

```js
me.app.chat(transform)
```

<div class="content-ad"></div>

## 어플리케이션 실행하기

Mesop 어플리케이션을 로컬 환경에서 또는 Google Colab과 같은 클라우드 환경에서 실행할 수 있습니다. Mesop는 앱을 배포하는 간소화된 프로세스를 제공하여 다른 사람들과 공유하고 테스트하는 것이 쉽습니다.

## 예시: 기억력을 가진 챗봇

Mesop와 LangChain을 사용하여 챗봇을 설정하는 더 자세한 예시를 보여드리겠습니다.

<div class="content-ad"></div>

- 패키지 초기화:

```js
import Mesop as me
import Mesop.labs as mel
from langchain import ConversationChain
from groq import Groq
```

2. API 및 프롬프트 설정:

우리는 여기서 Groq를 사용하여 대형 언어 모델을 사용하고 있습니다.

<div class="content-ad"></div>

```js
groq_api_key = "your_api_key"
groq_model = Groq(api_key=groq_api_key, model="Llama 3 70B")

def transform(user_input, chat_history):
   history_string = "\n".join([f"{msg['role']}: {msg['content']}" for msg in chat_history])
   response = groq_model.generate(user_input, history_string)
   return response
```

하지만 Hugging Face 모델을 사용해볼 수도 있어요.

```js
from langchain_huggingface import HuggingFaceEndpoint

# "your_access_token"을 사용자의 Hugging Face 액세스 토큰으로 대체하세요
HUGGINGFACEHUB_API_TOKEN = "your_access_token"

# Hugging Face 모델 ID를 정의하세요 (예: meta-llama/Meta-Llama-3-70B-Instruct)
model_id = "meta-llama/Meta-Llama-3-70B-Instruct"

def transform(user_input, chat_history):
  history_string = "\n".join([f"{msg['role']}: {msg['content']}" for msg in chat_history])

  # Hugging Face Endpoint를 인스턴스화하세요
  llm = HuggingFaceEndpoint(
      repo_id=model_id,
      task="text-generation",
      max_new_tokens=512  # 생성할 최대 토큰 수
  )

  # 사용자 입력과 채팅 기록을 사용하여 응답을 생성하세요
  response = llm.generate(history_string + "\n" + user_input)
  return response
```

연습: 위의 코드를 수정하여 Meta의 Llama 대신 Google의 gemma를 사용해볼 수 있을까요?

<div class="content-ad"></div>

3. 채팅 인터페이스를 생성하고 실행하세요:

```js
me.app.chat(transform)
```

## 향후 응용 프로그램

Mesop는 다양한 응용 프로그램에 사용할 수 있으며 챗봇 이외의 다양한 용도로 활용될 수 있습니다.

<div class="content-ad"></div>

1. 이미지를 조작하기 위한 도구: 이미지 조작을 위한 도구를 만들어보세요.
2. 대화형 데모: LLM 모델을 위한 대화형 데모를 만들어보세요.
3. 테스트 플랫폼: 사용자 피드백을 수집하기 위한 빠른 프로토타입을 개발해보세요.

## 결론

Mesop은 빠르게 애플리케이션을 구축하고 테스트하려는 개발자들에게 강력한 도구입니다. 그것의 Python 기반 접근 방식, 고수준 구성 요소 및 오픈 소스의 성격은 여러분의 툴킷에 가치 있는 추가 요소로 작용합니다. 챗봇이나 복잡한 UI를 구축하고 있다면 Mesop은 작업을 단순화시켜 주어 애플리케이션의 기능에 집중할 수 있도록 도와줍니다.

오늘 Mesop을 탐험하고 개발 작업 흐름을 향상시킬 수 있는 방법을 확인해보세요. 자세한 정보는 아래에 있습니다:

<div class="content-ad"></div>

아래 그림을 클릭하거나 LinkedIn을 방문하여 저자에 대해 더 알아보세요

![author](/assets/img/2024-06-20-MESOPaNewUIframework_1.png)