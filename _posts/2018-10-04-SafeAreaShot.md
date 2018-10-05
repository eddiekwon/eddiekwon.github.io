---
layout: post
title: Safe Area를 사용할 때 Tabbar 아래 text 표기
date: 2018-10-04 21:42:01 +0900
category: Swift
comments: true
permalink: /swift/:year/:month/:day/:title/
---

### Starting

safe Area 를 쓴 것과 안 쓴 것의 차이점을 그림으로 이해해봅시다.

다음 그림은 `superView` 로 부터 inset을 설정했을 때와 `safeArea`를 적용했을 때 화면을 캡쳐한 것입니다.

![InsetOftabbarFromSafeArea](/images/Swift/tabbarInset.png)

두 이미지을 볼 때 Tabbar 아래로 text가 가려지거나 보이거나 하는 차이점이 있습니다.

 

