---
layout: post
title: git 실수로 push한 파일을 히스토리 삭제하기
category: git
permalink: /git/:year/:month/:day/:title/

tags: [git]
comments: true
date: 2018-08-29 16:47:00 +0900
---

### git의 remote 주소를 변경하고 싶을 때
```
git remote set-url origin git://new.url.here
```

### git 실수로 push한 파일을 히스토리 삭제하기 

```
##### 문제의 머지가 발생한 곳에서 임시브랜치를 만들면서 체크하웃 함. (create and check out a temporary branch at the location of the bad merge)
`git checkout -b tmpfix <sha1-of-merge>`

##### 잘못 추가한 파일을 제거
`git rm somefile.orig`

##### commit the amended merge
`git commit --amend`

##### master branch 로 이동
`git checkout master`

##### replant the master branch onto the corrected merge
`git rebase tmpfix`

##### 임시 branch 삭제
`git branch -d tmpfix`
 

원문: https://github.com/honux77/practice/wiki/git-remove-sensitive-file-from-history