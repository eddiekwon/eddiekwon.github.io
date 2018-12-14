---
layout: post
title: swift기본 문법. stride
category: swift기본
permalink: /swift/:year/:month/:day/:title/

tags: [swift기본]
comments: true
date: 2018-12-13 08:11:10 +0900
typora-copy-images-to: ../images/2018-12-13-SwiftBasic-Stride
---

for를 뒤에서 부터 돌려볼까요. `reversed()`라는 것을 써도 되지만 `stride` 를 사용해 보겠습니다.

```swift
for i in stride(from: 0, to: 5, by: 1){
   print("i:\(i)")
}
//결과는 아래와 같습니다.
i:0
i:1
i:2
i:3
i:4
```

```swift
for x in stride(from: 5, to: 0, by: -1){
  print("x:\(x)")
}
//결과는 아래와 같습니다. 거꾸로 진행됩니다.
x:5
x:4
x:3
x:2
x:1

```

