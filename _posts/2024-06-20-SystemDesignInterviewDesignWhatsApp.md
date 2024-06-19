---
title: "시스템 디자인 면접 WhatsApp 디자인하기"
description: ""
coverImage: "/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_0.png"
date: 2024-06-20 03:49
ogImage: 
  url: /assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_0.png
tag: Tech
originalTitle: "System Design Interview: Design WhatsApp"
link: "https://medium.com/gitconnected/system-design-interview-design-whatsapp-779fa385ef08"
---


<img src="/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_0.png" />

이 시스템 디자인 인터뷰 시나리오에서는 WhatsApp과 유사한 메시징 앱을 설계하라는 요청을 받았습니다.

실제 인터뷰에서는 앱의 하나 이상의 기능에 초점을 맞출 수 있지만, 이 기사에서는 시스템 구조에 대한 고수준 개요를 살펴보고, 필요한 경우 특정 영역을 더 깊게 탐구할 수 있습니다.

# 기능 요구 사항 명확히하기

<div class="content-ad"></div>

인터뷰어에게 몇 가지 질문으로 범위를 좁히겠습니다. 1시간 안에 전체 WhatsApp 플랫폼을 설계하는 것은 현실적이지 않습니다:

![WhatsApp Design Image](/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_1.png)

- 주요 사용 사례: 앱의 기본 목적은 메시지를 보내고 확인하고 수신하며 메시지를 읽고 읽은 것으로 표시하는 것입니다.
- 그룹: 그룹 메시징은 다루지 않겠습니다. 일대일 메시징만 다룰 것입니다.
- 콘텐츠 유형: 텍스트 메시지만 지원하며 이미지나 비디오는 지원하지 않을 것입니다.

# 비기능 요구사항 명확히하기

<div class="content-ad"></div>

규모: 먼저, 규모에 대해 이야기해 보겠습니다. 시스템의 크기와 처리할 메시지의 양을 의미합니다. 매일 100억 건의 메시지가 전송된다고 가정하고, 1년 내에 그 양을 두 배로 늘리려고 합니다.

![System Design Interview Design WhatsApp](/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_2.png)

가용성: 가용성 측면에서, 시스템이 항상 사용 가능하고 작동 중이어야 합니다.

지연 시간: 시스템의 지연 시간에 대해, 거의 즉시 발생하도록 원합니다. 대부분의 API 요청이 100ms 내에 완료되어야 합니다.

<div class="content-ad"></div>

# 추정: 데이터 수학

매일 100억 건의 메시지가 있으므로 매 초 약 10억 메시지 / 86,400초 = 초당 115,740개의 메시지 (MPS)가 있습니다. 1년 내에 두 배로 증가한다는 것은 우리가 115,740 * 2 = 231,480 MPS에 대비해야 한다는 것을 의미합니다.

메시지당 200바이트를 가정하면, 매일 저장해야 하는 용량은 100억 메시지 * 200바이트 = 2 테라바이트 (TB)입니다. 그리고 성장을 고려한 연간 저장 용량은 약 2TB * 365일 * 2 = 1.5 페타바이트 (PB)입니다.

![이미지](/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_3.png)

<div class="content-ad"></div>

중요한 점은 평균을 계산했지만, 시스템은 평균 MPS보다 훨씬 높은 피크 트래픽을 처리해야 할 수도 있다는 것입니다. 피크 시간에 따라 확장이 필요할 수 있습니다.

# 고수준 API 설계

보다 넓은 호환성을 위해 대부분 RESTful API 스타일을 사용할 것으로 예상됩니다. 가능한 Endpoints에 대한 분해는 다음과 같습니다:

- 메시지 전송 (POST /messages): 요청 본문에 수신자 ID와 메시지 내용이 포함됩니다. 성공 응답(200)은 고유한 메시지 식별자를 반환합니다. 오류 코드(400, 500)는 누락된 매개변수나 서버 문제를 처리합니다.
- 새 메시지 확인 (GET /messages): 응답은 읽지 않은 메시지의 배열이 포함된 200이거나 없을 경우 204입니다.
- 특정 메시지 확인 (GET /messages/:messageId): 특정 메시지를 반환합니다(200) 또는 찾을 수 없는 경우 404를 반환합니다.
- 메시지를 읽음으로 표시 (PUT 또는 PATCH /messages/:messageId): 성공 응답(200)은 변경을 확인하고, 404는 메시지를 찾을 수 없음을 나타냅니다.

<div class="content-ad"></div>

![Table](/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_4.png)

추가 고려 사항: 실시간 업데이트를 위해 웹소켓을 통합할 것입니다. API는 인증 및 초기 연결 설정을 처리할 것이며, '새 메시지 확인' 엔드포인트에 대한 페이징이 필요할 수 있습니다. 입력 유효성 검사와 같은 보안 조치도 필요합니다.

# 고수준 시스템 디자인

모바일 앱: 사용자의 기본 인터페이스는 모바일 앱(iOS, Android)입니다. 이 앱은 메시지 보내기 및 받기, 연락처 관리, 대화를 처리합니다.

<div class="content-ad"></div>

로드 밸런서: 들어오는 요청을 효율적으로 처리하기 위해 여러 서버에 트래픽을 분배하는 로드 밸런서를 사용할 것입니다. 이렇게 함으로써 응용 프로그램의 신뢰성이 향상됩니다.

![](/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_5.png)

API 서버: 모든 요청은 우리가 이전에 개요를 설명한 RESTful API를 처리하는 API 서버로 전송됩니다. 메시징 로직을 관리합니다. API 서버 자체는 상태를 가지지 않을 수 있습니다. 이렇게 하면 트래픽이 증가함에 따라 (서버를 추가하여) 수평으로 확장할 수 있습니다.

WebSocket 연결: WhatsApp과 유사한 앱은 실시간 통신을 위해 웹소켓에 크게 의존합니다. 채팅 서버들은 모바일 앱과 지속적인 웹소켓 연결을 유지할 것입니다. 메시지가 도착하면 즉시 수신자의 기기로 푸시될 수 있습니다.

<div class="content-ad"></div>

메시지 분배자: 다음으로 메시지 분배자 서비스가 준비되어 있습니다. 이 서비스의 주요 목적은 API 서버를 직접적인 데이터베이스 쓰기로부터 분리하는 것입니다. 특히 높은 쓰기 부하를 처리하는 데 중요합니다.

![이미지](/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_6.png)

여기에 메시지 대기열인 Kafka 또는 RabbitMQ가 잘 맞습니다. 다음은 작동 방식입니다:

- API 서버가 "메시지 보내기" POST 요청을 받습니다.
- 이는 메시지를 대기열에 넣고 즉시 클라이언트에 성공/확인 응답을 반환합니다.
- 별도의 워커 프로세스가 대기열에서 비동기적으로 읽고 메시지를 데이터베이스에 작성합니다.

<div class="content-ad"></div>

```
데이터베이스 (NoSQL): 우리는 최종 일관성이 허용 가능하다고 합의했고, 이것은 NoSQL을 고대로 메시지 양에 대해 확장 가능한 선택으로 만듭니다.

두 가지 강력한 옵션을 고려해 봅시다:

- Cassandra: 확장 가능성, 고가용성 및 기록 성능으로 유명한 와이드 컬럼 스토어. 특히 ID로 메시지 검색하는 간단한 패턴을 예상할 경우 (주로 ID로 메시지 가져오기) 매우 유용합니다.
- DynamoDB: AWS에서 제공하는 완전히 관리되는 키-값 및 문서 데이터베이스. 우리가 쉽게 확장 가능한 최소 유지 관리 데이터베이스 솔루션을 원할 경우 유리합니다.

<img src="/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_7.png" />
```

<div class="content-ad"></div>

샤딩 및 분할: 1.5 페타바이트 저장 공간이 필요하기 때문에 단일 데이터베이스로는 처리할 수 없으므로 데이터를 샤딩(수평 분할)하는 것이 중요합니다.

하지만 이 데이터를 어떻게 샤딩하고 분할하며, API 서버들은 이 데이터를 어디에서 요청해야 하는지 어떻게 알 수 있을까요?

유저 ID를 기반으로 분할할 수 있습니다. 한 유저와 관련된 모든 메시지는 동일한 샤드/분할에 저장됩니다. 그리고 API 서버들은 데이터를 찾는 두 가지 방법이 있습니다:

<div class="content-ad"></div>

```
![2024-06-20-SystemDesignInterviewDesignWhatsApp_9.png](/assets/img/2024-06-20-SystemDesignInterviewDesignWhatsApp_9.png)

- Consistent Hashing Ring: 파티션 키를 기반으로 데이터 위치를 결정하여 API 서버가 올바른 데이터베이스 샤드로 요청을 직접 라우팅할 수 있습니다.
- 메타데이터 서비스: 별도의 서비스가 파티션 키와 샤드 위치의 매핑을 유지합니다. API 서버는 먼저 이 서비스를 쿼리한 다음 데이터베이스 호출을 수행합니다.

# 결론 및 현재 시스템 병목 현상

이것은 WhatsApp과 유사한 응용 프로그램을 위한 주요 아키텍처를 개략적으로 소개합니다. 이제 현재 시스템의 잠재적인 병목 현상과 개선할 수 있는 부분을 살펴보겠습니다.
```

<div class="content-ad"></div>

- 데이터베이스 쓰기: 높은 쓰기 양은 잠재적인 병목 현상이 될 수 있습니다. Sharding, 메시지 대기열 및 최적화된 데이터베이스 선택이 중요합니다.
- 엔드 투 엔드 암호화: WhatsApp 모델은 보안을 강조합니다. 엔드 투 엔드 암호화를 구현하는 것은 중요한 논의가 될 것입니다.
- 그룹 채팅: 이 기능은 메시지 라우팅 및 저장에 추가 복잡성을 불러옵니다.
- 미디어 처리: 이미지 및 비디오 업로드를 처리하는 시스템을 구현할 수 있습니다. 압축을 사용하는 것과 썸네일을 위한 여러 저장 크기를 사용할 수 있습니다.

만약 여기서 논의한 각 구성 요소에 대해 더 알고 싶다면, 상세한 내용을 다루는 무료 시스템 디자인 면접 개념 튜토리얼이 있습니다.