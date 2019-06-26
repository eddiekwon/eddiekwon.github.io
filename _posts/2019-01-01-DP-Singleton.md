---
layout: post
title: swift design pattern
category: swift기본
permalink: /swift/:year/:month/:day/:title/

tags: [swift,design pattern]
comments: true
date: 2019-01-01 08:11:10 +0900
typora-copy-images-to: ../images/2019-01-01-DP-Singleton
---

## 싱글턴



언제 쓰나요?

하나 이상의 인스턴스를 만들때 문제가 생긴다면 싱글턴을 써볼만합니다.

### 싱글턴의 기본

가장 간단한 생성방법은 다음과 같습니다.

````swift
public class MySingleton { 
  static let shared = MySingleton()
  private init() { } // 추가로 인스턴스 생성을 방지케하기 위함입니다.
}
````



싱글턴을 두번 이상 생성하려면 아래처럼 에러가 발생합니다.

![6E0FD66E-619D-4B26-968A-7FFE34FDFDF7](/Users/eddie/eddiekwon/images/2019-01-01-DP-Singleton/6E0FD66E-619D-4B26-968A-7FFE34FDFDF7.png)

그리

여기서 혹시...init()에 private를 적지 않는다면? 궁금하신 분들은 위해 해보죠~

```swift
public class MySingleton { 
  static let shared = MySingleton()
  init() { } // private가 아님.
}
```

결과를 볼까요?

```swift
let mySingleton = MySingleton.shared
let mySingleton2 = MySingleton() // 아무 이상없습니다. 컴파일 성공합니다.
```

즉 여러 인스턴스를 만들어도 아무 문제 없습니다. 대신 이렇게 하면 싱글턴이 일까요? 아닐까요?

자 다음을 봅시다.

```swift
let defaultFileManager = FileManager.default
let customFileManager = FileManager()
```

이 처럼 FileManager는 분명 싱글턴으로 사용할 수 있는데, 이상하게도 별도의 인스턴스를 또 만들 수 있습니다.

위 같은 패턴을 `싱글턴 플러스 패턴` 이라고 한답니다. 왜 필요한지는 정확히 모르겠네요 @.@.

### 싱글턴의 단점

싱글턴은 상태값을 저장하고 있기 때문에, 순서가 다르면 결과도 다르게 됩니다. Unit Test 같은 것을 할 때 취약합니다.



### 정리

여기까지가 singleton 의 기초입니다. 그럼 다음 시간에 만나요~





