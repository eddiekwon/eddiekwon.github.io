---
layout: post
title: Git pullRequest 하기 (터미널)
category: git
permalink: /git/:year/:month/:day/:title/

tags: [git]
comments: true
date: 2018-10-11 21:41:00 +0900
---
 

먼저 새로운 브랜치를 만들고 체크아웃을 동시에 합니다. `-b`명령어를 사용합니다.

```bash
git:(release/develop) $ git checkout -b helloBranch
```

작업하고
```bash
git:(helloBranch) $ git status
git:(helloBranch) $ git add .
git:(helloBranch) $ git commit -m "done xoxo something"
```
이후에 서버로 푸시합니다.

```bash
git:(helloBranch) $ git push origin helloBranch
```

푸시하면 다음과 비슷한 결과가 출력됩니다.
```bash
Counting objects: 11, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (11/11), 1.08 KiB | 1.08 MiB/s, done.
Total 11 (delta 9), reused 0 (delta 0)
remote:
remote: Create pull request for helloBranch:
remote:   https://mygit.xxxx.com/projects/repos/dep-ios-app/compare/commits?sourceBranch=refs/heads/helloBranch
remote:
To https://mygit.xxxx.com/scm/depdev/dep-ios-app.git
 * [new branch]        helloBranch -> helloBranch
 
```

끝입니다.!!