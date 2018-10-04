---
layout: post
title: Swift 코드 컨벤션
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift, code, convention]
comments: true
date: 2018-09-11 11:40:00 +0900
---

Swift 코드 컨벤션

### Dictionary변수 선언의 두가지 방법

1. 변수로 선언하는 방식
   간단히 Dictionary형태로 변수를 선언하여 값을 하나하나 차곡차곡 넣는 방식이다.
```swift
var params :[String:String] = [:]
params["grant_type"] = "wowo"
params["username"] = userName
params["password"] = password
```

2. 상수로 선언
  상수로 한번에 선언하는 것인데, 변수보다 더 안전하다고 볼 수 있겠다(종종 버그의 원흉이 되는 변수 선언 `var`를 사용하지 않기 때문).
```swift
let params = [
    "grant_type" : "wowo",
    "username": userName,
    "password": password
]
```

