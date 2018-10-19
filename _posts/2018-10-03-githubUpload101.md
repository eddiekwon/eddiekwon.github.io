---
layout: post
title: 무작정 github에 파일을 올려보기.
date: 2018-10-03 21:42:01 +0900
category: git
comments: true
permalink: /git/:year/:month/:day/:title/
typora-copy-images-to: ../images
---


제목: 무작정 github에 파일을 올려보기.

새 레포지토리를 생성

![AFDD42E9-B207-49D0-9914-15B12E396269](/images/AFDD42E9-B207-49D0-9914-15B12E396269.png)

다음

![D997327A-1C1A-42CF-AA94-8CE29E1D351E](/images/D997327A-1C1A-42CF-AA94-8CE29E1D351E.png)

Create repository를 해주고나면 준비가 되었다는 페이지로 이동됩니다.

![9898E56C-C00F-4B94-B78D-B2555C144097](/images/9898E56C-C00F-4B94-B78D-B2555C144097.png)

그다음 다음 명령오로 git 에 푸시합니다.

```bash
eddiek@ek.local:/Users/eddiek/Documents  $ mkdir helloGithub
eddiek@ek.local:/Users/eddiek/Documents  $ cd helloGithub
eddiek@ek.local:/Users/eddiek/Documents/helloGithub  $ touch hello.swift
```

hello.swift라는 파일을 github 에 올리기전에 에디터로 열고 아무 내용이나 적어줍니다.


```bash
eddiek@ek.local:/Users/eddiek/Documents/helloGithub  $ git init
Initialized empty Git repository in /Users/eddiek/Documents/helloGithub/.git/
eddiek@ek.local:/Users/eddiek/Documents/helloGithub  git:(master*) $ git add .
eddiek@ek.local:/Users/eddiek/Documents/helloGithub  git:(master*) $ git commit -m "first commit hahaha"
[master (root-commit) a31eb7b] first commit hahaha
 1 file changed, 2 insertions(+)
 create mode 100644 hello.swift
```
로컬 저장소(현재 맥)와 서버 리모트(깃헙)를 `git remote add origin`라는 명령어를 사용하여 연결해줍니다.
```bash
eddiek@ek.local:/Users/eddiek/Documents/helloGithub  git:(master) $ git remote add origin https://github.com/eddiekwon/upload101.git
```
이제 `git push -u origin master`명령어로 push합니다.

```bash
eddiek@ek.local:/Users/eddiek/Documents/helloGithub  git:(master) $ git push -u origin master
Username for 'https://github.com': eddiekwon
Password for 'https://eddiekwon@github.com':
Counting objects: 3, done.
Writing objects: 100% (3/3), 244 bytes | 244.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/eddiekwon/upload101/pull/new/master
remote:
To https://github.com/eddiekwon/upload101.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
eddiek@ek.local:/Users/eddiek/Documents/helloGithub  git:(master) $
```

이제 github으로 가서 웹페이지를 새로고침해보면 hello.swift가 올라온 것이 보입니다.

![1769BF94-03FE-479F-AAF4-26304C719186](/images/1769BF94-03FE-479F-AAF4-26304C719186.png)

이상입니다.