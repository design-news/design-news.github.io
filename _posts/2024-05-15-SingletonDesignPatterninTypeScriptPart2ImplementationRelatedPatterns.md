---
title: "TypeScript에서의 싱글톤 디자인 패턴 파트 2 구현, 관련 패턴"
description: ""
coverImage: "/assets/img/2024-05-15-SingletonDesignPatterninTypeScriptPart2ImplementationRelatedPatterns_0.png"
date: 2024-05-15 23:16
ogImage:
  url: /assets/img/2024-05-15-SingletonDesignPatterninTypeScriptPart2ImplementationRelatedPatterns_0.png
tag: Tech
originalTitle: "Singleton Design Pattern in TypeScript (Part 2): Implementation , Related Patterns"
link: "https://medium.com/@hooman.the1/singleton-design-pattern-in-typescript-part-2-implementation-related-patterns-9ee431f3773e"
---

제1부에서는 Singleton 디자인 패턴의 동기, 구조 및 결과에 대해 다루었습니다. 이제 구현과 관련 패턴을 다루겠습니다.

언제나처럼, 이 글의 주요 참고 자료는 책 "디자인 패턴: 재사용 가능한 객체 지향 소프트웨어의 요소"입니다.

# 구현

Singleton 패턴을 사용할 때 고려해야 할 구현 문제들은 다음과 같습니다:

- 유일한 인스턴스를 보장합니다. 싱글톤 패턴은 클래스의 단일 인스턴스를 보통의 클래스 인스턴스로 만듭니다. 그러나 해당 클래스는 한 번 만들 수 있는 인스턴스만 생성되도록 작성됩니다. 이를 위한 일반적인 방법은 인스턴스를 생성하는 작업을 유일한 인스턴스가 생성되도록 보장하는 클래스 정적 메소드 뒤에 숨기는 것입니다. 이 작업은 유일한 인스턴스를 보유하는 변수에 접근하며, 이 변수가 유일한 인스턴스로 초기화된 후 값을 반환하기 전에 이를 보장합니다. 이 접근 방법은 싱글톤이 처음 사용되기 전에 생성 및 초기화되도록 보장합니다.

```js
class Logger {
  private static instance: Logger;

  protected constructor() {
    // 외부에서의 인스턴스화 방지
  }

  static getInstance(): Logger {
    if (!Logger.instance) {
      Logger.instance = new Logger();
    }
    return Logger.instance;
  }

  log(message: string): void {
    console.log(`[LOG] ${message}`);
  }
}

// 사용법
const logger1 = Logger.getInstance();
const logger2 = Logger.getInstance();

console.log(logger1 === logger2); // 출력: true

logger1.log("이것은 로그 메시지입니다.");
logger2.log("또 다른 로그 메시지입니다.");
```

인스턴스 속성은 클래스의 모든 인스턴스에서 공유되도록 정적으로 설정되어야 합니다. 인스턴스 속성으로 만들 경우 싱글톤 클래스의 각 인스턴스가 고유한 인스턴스 속성을 갖게되어 싱글톤 패턴의 목적을 무효화시킵니다.
생성자가 protected로 선언되어 있음에 유의하십시오. 직접적으로 싱글톤을 인스턴스화 하려는 클라이언트는 컴파일 시간에 오류를 받게 됩니다. 이는 단 하나의 인스턴스만 생성될 수 있도록 보장합니다.

2. 싱글톤 클래스의 서브클래싱. 주된 문제는 서브클래스를 정의하는 것이 아니라 해당 고유의 인스턴스를 설치해서 클라이언트가 사용 가능하도록 하는 것입니다. 본질적으로 싱글톤 인스턴스를 참조하는 변수는 서브클래스의 인스턴스로 초기화되어야 합니다. 가장 간단한 기술은 싱글톤의 인스턴스 작업에서 사용할 싱글톤을 결정하는 것입니다. 예시:

```js
class MazeFactory {
    private static _instance: MazeFactory | null = null;

    protected constructor() {
        // 생성을 방지하기 위한 protected 생성자
    }

    static Instance(): MazeFactory {
        if (MazeFactory._instance === null) {
            const mazeStyle: string | undefined = process.env.MAZESTYLE;
            if (mazeStyle === "bombed") {
                MazeFactory._instance = new BombedMazeFactory();
            } else if (mazeStyle === "enchanted") {
                MazeFactory._instance = new EnchantedMazeFactory();
                // 필요에 따라 다른 가능한 하위 클래스 추가
            } else { // 기본값
                MazeFactory._instance = new MazeFactory();
            }
        }
        return MazeFactory._instance;
    }
}

class BombedMazeFactory extends MazeFactory {
    // BombedMazeFactory에 특정 구현을 추가하세요
}

class EnchantedMazeFactory extends MazeFactory {
    // EnchantedMazeFactory에 특정 구현을 추가하세요
}

// 사용법
const instance1: MazeFactory = MazeFactory.Instance();
const instance2: MazeFactory = MazeFactory.Instance();

console.log(instance1 === instance2); // 출력: true
```

싱글톤의 하위 클래스를 선택하는 또 다른 방법은 getInstance의 구현을 상위 클래스에서 가져와서 하위 클래스에 넣는 것입니다.

```js
class MazeFactory {
    protected constructor() {
        // 생성을 방지하기 위한 protected 생성자
    }
}

class BombedMazeFactory extends MazeFactory {
    private static _instance: BombedMazeFactory | null = null;

    private constructor() {
        super();
    }

    static Instance(): BombedMazeFactory {
        if (BombedMazeFactory._instance === null) {
            BombedMazeFactory._instance = new BombedMazeFactory();
        }
        return BombedMazeFactory._instance;
    }
}

class EnchantedMazeFactory extends MazeFactory {
    private static _instance: EnchantedMazeFactory | null = null;

    private constructor() {
        super();
    }

    static Instance(): EnchantedMazeFactory {
        if (EnchantedMazeFactory._instance === null) {
            EnchantedMazeFactory._instance = new EnchantedMazeFactory();
        }
        return EnchantedMazeFactory._instance;
    }
}

// 사용법
const bombedInstance1: BombedMazeFactory = BombedMazeFactory.Instance();
const bombedInstance2: BombedMazeFactory = BombedMazeFactory.Instance();

console.log(bombedInstance1 === bombedInstance2); // 출력: true

const enchantedInstance1: EnchantedMazeFactory = EnchantedMazeFactory.Instance();
const enchantedInstance2: EnchantedMazeFactory = EnchantedMazeFactory.Instance();

console.log(enchantedInstance1 === enchantedInstance2); // 출력: true
```

보다 유연한 접근 방식은 싱글톤 레지스트리를 사용하는 것입니다. Instance가 모든 가능한 Singleton 클래스를 알 필요 없이, Singleton 클래스는 잘 알려진 레지스트리에 이름별로 싱글톤 인스턴스를 등록할 수 있습니다. 레지스트리는 문자열 이름과 싱글톤 간의 매핑을 제공합니다. Instance가 싱글톤을 필요로 할 때, 레지스트리에게 이름별로 싱글톤을 요청합니다. 레지스트리는 해당 싱글톤을 찾아 반환합니다. 이 접근 방식은 Instance를 모든 가능한 Singleton 클래스나 인스턴스를 알 필요 없이 자유롭게 만듭니다.

```js
class Singleton {
    private static registry: Map<string, any> = new Map();

    protected constructor() {
        // Protected constructor to prevent instantiation
    }

    static registerInstance(name: string, instance: any): void {
        if (!Singleton.registry.has(name)) {
            Singleton.registry.set(name, instance);
        } else {
            console.error(`Singleton with name '${name}' is already registered.`);
        }
    }

    static getInstance(name: string): any | null {
        if (Singleton.registry.has(name)) {
            return Singleton.registry.get(name);
        } else {
            console.error(`Singleton with name '${name}' is not registered.`);
            return null;
        }
    }
}
```

싱글톤 클래스는 어디에 자신을 등록할까요? 한 가지 가능성은 생성자에 등록하는 것입니다. 예를 들어 MySingleton 서브클래스는 다음과 같이 할 수 있습니다:

```js
class MySingleton extends Singleton {
  constructor() {
    super();
    // 추가 초기화 로직 ...
    Singleton.registerSingleton("MySingleton", this);
  }
}
```

물론, 클래스의 인스턴스를 생성하지 않으면 생성자가 호출되지 않을 것입니다. 이는 싱글톤 패턴이 해결하려고하는 문제를 반영합니다! MySingleton의 인스턴스를 정의하여이 문제를 해결할 수 있습니다. 예를 들어 다음과 같이 정의할 수 있습니다.

```js
const theSingleton: MySingleton = new MySingleton();
```

MySingleton의 구현 내용을 포함한 파일에서 코드를 변경해주세요. 이제 더 이상 싱글톤 클래스가 싱글톤을 생성하는 역할을 하지 않습니다. 대신, 주요 역할은 서브클래스 레지스트리를 사용하여 시스템 내에서 선택한 싱글톤 객체를 접근할 수 있도록 하는 것입니다. 이 방식에는 여전히 모든 가능한 Singleton 서브클래스의 인스턴스가 생성되어야 하는 잠재적인 단점이 있습니다. 그렇지 않으면 등록되지 않습니다.

# 관련 패턴

Singleton 패턴을 사용하여 많은 패턴을 구현할 수 있습니다. Abstract Factory, Builder, 그리고 Prototype을 참고하세요.
