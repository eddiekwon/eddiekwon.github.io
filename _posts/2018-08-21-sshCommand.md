---
layout: post
title: 현재 ssh key를 알고 싶을때.
category: git
permalink: /git/:year/:month/:day/:title/

tags: [git, ssh]
comments: true
date: 2018-07-22 21:40:00 +0900
---

현재 ssh key를 알고 싶을때.
그리고 terminal 의 파일 내용을 clipboard로 복사하고 싶다면.
cd ~./ssh로 들어가서
`cat xxxx.rsa | pbcopy` 하면 현재 내용을 보여준다.

아무것도 없네..보자.

```
eddiek@ek.local:/Users/eddiek/.ssh  $ ls -al
total 0
drwx------   2 eddiek  staff    64 Aug 22 14:44 .
drwxr-xr-x+ 72 eddiek  staff  2304 Aug 24 09:00 ..

eddiek@ek.local:/Users/eddiek/.ssh  $ open .
```
다른 맥에서 id_rsa파일 두개를 복사해서 현재 폴더에 복사한 후 다시 `ls`명령어를 타이핑해본다.

```
eddiek@ek.local:/Users/eddiek/.ssh  $ ls -al
total 16
drwx------   4 eddiek  staff   128 Aug 24 09:00 .
drwxr-xr-x+ 72 eddiek  staff  2304 Aug 24 09:04 ..
-rw-r--r--   1 eddiek  staff  3243 Jul  7 13:44 id_rsa
-rw-r--r--   1 eddiek  staff   732 Jul  7 13:44 id_rsa.pub
eddiek@ek.local:/Users/eddiek/.ssh  $ cat ./id_rsa.pub
ssh-rsa BBQAAB3NzaC1yc2EVVDsaaaAACAeeeYZofLk6i8D3IN7MG4Uf6iSEPRlXf2dxlKu3Yy0V7v4vINFp3ILSB+MCZK7C3vbr/mqDy69liU49+ZESQD0vOw1obKw81icqiaAAzqnNySEH4bd3Ocoq9EMp6eqa49599OYJ88hZqcGfH...

```


권한 관련 ssh에 문제가 생기면 `chmod 400 ~/.ssh/id_rsa`로 해서 해결했다.
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for '/Users/tudouya/.ssh/vm/vm_id_rsa.pub' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
bad permissions: ignore key: /Users/tudouya/.ssh/vm/vm_id_rsa.pub
Permission denied (publickey,password).
```

사이트: https://stackoverflow.com/questions/29933918/ssh-key-permissions-0644-for-id-rsa-pub-are-too-open-on-mac

