---
layout: post
title: Content Hugging vs Comression Resistance
category: swift기본
permalink: /swift/:year/:month/:day/:title/

tags: [swift,UIKit]
comments: true
date: 2020-06-14 08:11:10 +0900
typora-copy-images-to: ../images/2020-06-14-UIhugging
---

## Content Hugging vs Comression Resistance

두 개념을 가장 쉽게 이해하려면 XCode storyboard 를 켜서 UILable 두개를 그린후 속성을 250, 251 등 바꾸어 보면 된다.

![Hugging vs compression resistance](/images/2020-06-14-UIhugging/hugging.png)

두 가지는 상반된 개념인데 먼저 compression resistance를 이해하는게 수월하다, 왜냐하면 `Priority`값이 크면 뷰 크기가 커지는 것으로 이해하면 되기 때문이다.