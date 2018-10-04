---
layout: post
title: 리모트의 특정 브랜치로 checkout 하기
category: git
permalink: /git/:year/:month/:day/:title/

tags: [git]
comments: true
date: 2018-07-21 21:41:00 +0900
---
## 리모트의 특정 브랜치로 checkout 하기

리모트의 특정 브랜치를 로컬로 가져오고 싶다면 그냥 해당 branch이름으로 체크아웃하면 된다. 이때 옵션 `t`를 추가해야 한다. 즉 `git checkout -t remote이름/branch이름` 처럼 한다.

예시)
```bash
git checkout -t origin/network
```