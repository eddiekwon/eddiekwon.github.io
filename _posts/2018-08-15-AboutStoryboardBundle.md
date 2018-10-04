---
layout: post
title: UIStoryboard의 번들 옵션이 nil 이라 함은?
date: 2018-08-15 21:40:00 +0900
category: Swift
permalink: /Swift/:year/:month/:day/:title/
---

```swift
let storyBoard = UIStoryboard(name: "Chart", bundle: nil)
```

bundle 의 파라미터값으로 `nil`이 들어가면 기본번들을 사용한다는 것을 뜻함.