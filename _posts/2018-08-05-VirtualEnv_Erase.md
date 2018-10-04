---
layout: post
title: VirtualEnv 삭제방법
date: 2018-08-05 21:40:00 +0900
category: Python
permalink: /Python/:year/:month/:day/:title/
---

Anaconda 패키지를 설치한 환경이라면 따로 VirtualEnv를 설치할 필요가 없다.

`source venv/bin/activate` 가 잘 동작하기는 하는데 이제 필요가 없어졌다.

삭제하는 방법 은?

그냥 폴더를 삭제하면 된다.

```bash
$ ls
Untitled.ipynb  Untitled1.ipynb venv
```

venv라는 폴더에 만들어 졌기 때문에 폴더를 삭제하자.
`rm -r venv`
