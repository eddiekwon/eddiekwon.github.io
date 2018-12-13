---
layout: post
title: 왜 Alpha속성만 Animatable 인가?
category: Swift
permalink: /swift/:year/:month/:day/:title/

tags: [swift]
comments: true
date: 2018-11-27 09:11:00 +0900
typora-copy-images-to: ../images/2018-11-27-Animatable
---

# Why
왜 Alpha속성만 Animatable 인가?
Constraint는 왜 애니메이션이 자동으로 안되고 꼭 애니메이션 클로져(블럭)속에 `layoutIfNeeded` 를 추가해야 하는가?

먼저 `UIView` 클래스의 Animatable properties를 봅시다:

- `frame`
- `bounds`
- `center`
- `transform`
- `alpha`
- `backgroundColor`
- `contentStretch`

결론부터 말하자면, Constraint의 경우에는 `Auto Layout의 Constraint의 변경된 값`이 실제로 View에 반영되려면 일련의 거치게 되는데, 이 때문에 `layoutIfNeeded`와 같은 처리가 필요하다고 합니다.

우선 발췌한 내용만 먼저 보자면 다음과 같습니다.
>1 변경될 값에 맞추어 시스템이 해당 Constraint를 포함하여 이와 연관되어 있는 Constrainte들의 모든 값을 재계산합니다.
2 layout 엔진이 재계산된 Constraint에 맞추어 연관되어 있는 모든 View들의 frame들의 값을 재계산하고 배치합니다.
3 재계산되고 재배치된 frame을 실제 화면에 그립니다.

좀 더 상세히 보기 위해서 예시를...

다음 시간에 update하겠습니다.ㅜㅜ.

ref:
http://baked-corn.tistory.com/107
http://tech.gc.com/demystifying-ios-layout/