---
layout: post
title: git 에러 발생처리. REMOTE Url연결
category: git
permalink: /git/:year/:month/:day/:title/

tags: [git]
comments: true
date: 2018-08-30 16:47:00 +0900
---

### 이슈: 이미 remote 가 연결되어 있다는 에러가 발생하면~
```bash
Github “fatal: remote origin already exists”
```

### 해결:  새로운 remote url을 설정함.
현재 설정된 URL을 보고 변경하거나,  삭제하고 새로 url을 추가해줌.
* 현재 설정된 리모트 URL보기
```bash
$ git config --get remote.origin.url https://github.com/someUser/xxx.git
```
또는
```bash
$ git remote get-url origin
```

또는 어디에 연결되었나 볼때는 다음처럼 한다.
```bash
$ git remote -v
origin	https://github.com/xxx/yyyy.git (fetch)
origin	https://github.com/xxx/yyyy.git (push)
```



* 리모트  추가하기 ( 리모트 URL이 없을때)
```bash
$ git remote add origin https://github.com/someUser/xxx.git
```

* 리모트 URL 갱신
  이미 리모트 주소가 있다면 `fatal: remote origin already exists.` 가 발생함.  이때는 기존 주소를 삭제후 다시 add 하면 됨.
```bash
$ git remote rm origin
$ git remote add origin https://github.com/someUser/xxx.git
```

### 이슈: github에 잘못된 ID로 계속 나타남.
증상: 로컬에서 eddie로 커밋하고, push했으나,  github에 확인해보면 "hallomuzexxx Initial Commit" 이라고 나옴

![증상](https://i.imgur.com/ta8iWNv.jpg)

### 해결: 정확히는 모르겠으나 global email을 변경하고 나서 괜찮아짐. 

아래처럼 여러가지 시도후에 해결되었으나 정확히 어떻게 해결된 것인지는 모르겠음. @.@

의심 1: global email변경 ( email = hallomuzexxx@gmail.com를 eddiexxx@gmail로 변경했음. )
```bash
git config --global user.email "eddiexxx@gmail.com"
```
의심 2: xcode자체 이슈 ( 사실 xcode 가 아닌 terminal 에서 touch로 파일생성하면 문제가 없음.)
의심 3: 

* 유저명 변경
```
git config --global user.name "Jessica Lisa"
git config --local user.name "Jessica Lisa"
```

시스템영역의 git config 읽어보기
```
 cat ~/.gitconfig
```
결과
```bash
[core]
	excludesfile = /Users/eddiek/.gitignore_global
	precomposeunicode = true
	quotepath = false
[difftool "sourcetree"]
	cmd = opendiff \"$LOCAL\" \"$REMOTE\"
	path =
[mergetool "sourcetree"]
	cmd = /Applications/Sourcetree.app/Contents/Resources/opendiff-w.sh \"$LOCAL\" \"$REMOTE\" -ancestor \"$BASE\" -merge \"$MERGED\"
	trustExitCode = true
[user]
	name = eddiekwon
	email = hallomuzexxx@gmail.com
[commit]
	template = /Users/eddiek/.stCommitMsg
[alias]
  tre = log --graph --decorate --pretty=oneline --abbrev-commit --all --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)'

  lg1 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
  lg2 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
  lg = !"git lg1"

[mergetool "Kaleidoscope"]
	cmd = ksdiff --merge --output \"$MERGED\" --base \"$BASE\" -- \"$LOCAL\" --snapshot \"$REMOTE\" --snapshot
	trustexitcode = true
[merge]
	tool = Kaleidoscope
[difftool "Kaleidoscope"]
	cmd = ksdiff --partial-changeset --relative-path \"$MERGED\" -- \"$LOCAL\" \"$REMOTE\"
[difftool]
	prompt = false
[mergetool]
	prompt = false
[diff]
	tool = Kaleidoscope
```

도움 사이트: https://help.github.com/articles/setting-your-username-in-git/

 