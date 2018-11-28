---
layout: post
title: Swift 기본 문법 정리
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift]
comments: true
date: 2018-10-20 08:49:00 +0900
typora-copy-images-to: ../images/2018-10-20-SwiftBasicTest
---

오버플로우 연산자 배우기

![05722647-41A3-4EE4-BACE-6A78A277227F](/Users/eddiek/Documents/eddiekwon.github.io/images/2018-10-20-SwiftBasicTest/05722647-41A3-4EE4-BACE-6A78A277227F.png)

해결: `&+` 는 오버플로우 연산자입니다. 최대값에서 1을 더하면 0이 됩니다.

![D7A0924E-2FAA-41A2-BBD2-32D344DA28A1](/Users/eddiek/Documents/eddiekwon.github.io/images/2018-10-20-SwiftBasicTest/D7A0924E-2FAA-41A2-BBD2-32D344DA28A1.png)

오버플로우 마이너스 연산자 배우기

![3FC6070A-97D0-4177-8D7D-1E2984EFC2F0](/Users/eddiek/Documents/eddiekwon.github.io/images/2018-10-20-SwiftBasicTest/3FC6070A-97D0-4177-8D7D-1E2984EFC2F0.png)

해결: `&-` 역시 오버플로우 연산자입니다. 0에서  1을 빼면 최대값이 됩니다.

![9B98D1D9-3B2C-497F-BDC3-91DDCF6CCBDD](/Users/eddiek/Documents/eddiekwon.github.io/images/2018-10-20-SwiftBasicTest/9B98D1D9-3B2C-497F-BDC3-91DDCF6CCBDD.png)

이상