---
layout: post
title: SSH로 git push 오류
category: git
permalink: /git/:year/:month/:day/:title/

tags: [git, ssh]
comments: true
date: 2018-07-21 21:40:00 +0900
---
## 문제의 발단 - SSH로 git push가 되지 않는다!
git 에 프로젝트 만들기 부터, git clone 하려는데 온갖종류의 에러가 발생했다.
예전에 gitlab 에서 ssh설정을 해 두었는데 정확히 이해하지 못하고 설정한 것이 원인이었다.
그래서 ssh를 맨처럼 설정했던 mac pro에서 우선 터미널로 key가 있는지 확인부터 해보았다.


가장먼저 git프로젝트를 만들고 local 프로젝트를 gitlab 에 push하려는데

```bash
(auto-trading)  trading (master) git push origin master
ssh: connect to host gitlab.com port 22: Network is down
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
(auto-trading)  trading (master) git remote add origin-https https://gitlab.com/hallomuze/auto-trading.git
(auto-trading)  trading (master) git push -u origin-https master
fatal: unable to access 'https://gitlab.com/hallomuze/auto-trading.git/': Could not resolve host: gitlab.com

```
so의 도움을 받아서 우선 차선책으로 해결은 했다.
ssh키가 설정되지 않은 맥에서 진행을 했기 때문에 ssh설정하기 전까지는 https로 올려야 하나보다.
```bash
(auto-trading)  trading (master) git push -u origin-https master
Username for 'https://gitlab.com': xxxxxx
Password for 'https://xxxxxx@gitlab.com': 
Counting objects: 11, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (11/11), 1.88 KiB | 1.88 MiB/s, done.
Total 11 (delta 0), reused 0 (delta 0)
To https://gitlab.com/xxxxxx/auto-trading.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin-https'.
```


## 문제풀이 ssh세팅된 파일?을 새로 산 맥에 복사해보자.
 
가장 많은 도움된 사이트
https://superuser.com/questions/1256286/mac-os-x-high-sierra-missing-ssh-folder

요약하자면

```
- In the terminal, enter cd ~
- Then mkdir .ssh; chmod 700 ~/.ssh
```


In macOS, you need to generate your public and private keys from the Terminal. If you haven't yet done this, the .ssh directory will not exist. To create them:

Open the terminal App and enter the following command: 

`ssh-keygen`

You'll get a prompt to choose the location for the keys. It will say **“Enter file in which to save the key (/Users/your-username/.ssh/id_rsa)”**. If you’re happy with the default location(~/.ssh/) just tap Return. Within your shell the `~` character is equivalent to `/Users/your-username/`. It stands for your home directory.

It will now say **“Enter passphrase (empty for no passphrase):”**. Enter your passphrase and press Return. You are asked to re-enter the password to confirm you typed it correctly. This passphrase is used to encrypt the private key and it's recommended you set one.

The prompt will now say **“Your identification has been saved in /Users/your-username/.ssh/id_rsa”** and **“Your public key has been saved in /Users/your-username/.ssh/id_rsa.pub.”** It'll then show you the key's Fingerprint and Randomart. The Fingerprint matches the public key and can be used in some situations for authentication, and the Randomart file is designed to match the Fingerprint but be easier to visually identify that it is the right key. You don't need to copy these down for most purposes. 

Now you can view the newly-created .ssh directory and find your key within.

You can find a pretty readable guide on the subject [here](https://www.ssh.com/ssh/keygen/#sec-SSH-Keys-and-Public-Key-Authentication).

**Edit:** If you want to copy in previously-saved public and private keys:

- In the terminal, enter `cd ~`
- Then `mkdir .ssh; chmod 700 ~/.ssh`

This will create the directory and give it adequate permissions. Within this directory, you can now paste in your two files which contain the matching public and private key pair. These will be your id_rsa.pub and id_rsa files respectively. Once this is done, double-check their permissions are what they need to be by running:

```
ls -l ~/.ssh/id_rsa*

```

The output should look like this(except the numbers 1766 and 388): 

```
-rw------- 1 user root 1766 Oct 04  2017 .ssh/id_rsa
-rw-r--r-- 1 user root  388 Oct 04  2017 .ssh/id_rsa.pub

```

In case you get something that doesn't look like this, set the permissions of these files with:

```
$ chown user:user ~/.ssh/id_rsa*
$ chmod 600 ~/.ssh/id_rsa
$ chmod 644 ~/.ssh/id_rsa.pub

```

Note that with **chown user:user ~/.ssh/id_rsa\*** just above, user is the user account you're logged in with, not literally "user".


## 궁금한점



아래 사이트를 보면 https://m.blog.naver.com/PostView.nhn?blogId=writer0713&logNo=220841133255&proxyReferer=https%3A%2F%2Fwww.google.com%2F

SSH AGENT 를 활성화 해야한다고하는데,,,나는 안해도 왜 잘되지???

```
5. ssh-agent 동작 확인 | 동작 시키기 
리눅스/맥에서 ssh-agent가 동작하고 있어야 bitbucket에 ssh 프로토콜로 접속을 요청할때 ssh 키를 확인할 수 있다. 

1) $ ps -e | grep ssh-agent 
위 명령어 입력시 만약 동작중일 경우 프로세스가 뜬다.

2) $ ssh-agent /bin/bash
프로세스가 안돌고 있을 경우 위 명령어로 실행 시킨다.

3) $ ssh-add ~/.ssh/kjung_blog
위에서 만든 ssh 키를 agent에 등록시킨다.

4) $ ssh-add -l
리스트에 내가 만든 키가 들어있다면 등록 성공.
```

관련 깃헙글
https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/


## 아래는 ssh정상 등록된 맥에서 해본 시험이다.


이전에 push에 아무 문제 없던 맥에서 한번 clone을 해보자. 근데 또 에러가 발생하네?
(자랑은 아니고, 어쩌다 내가 사용하는 맥은 두대다.)

```bash
eddies-MacBook-Pro-2:~ eddie$ git clone git@gitlab.com:xxxxxx/auto-trading.git
Cloning into 'auto-trading'...
The authenticity of host 'gitlab.com (35.231.145.151)' can't be established.
ECDSA key fingerprint is SHA256:8zUjNSWg2Bq1x8xdGUrliXFzSnUw.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'gitlab.com,35.231.145.151' (ECDSA) to the list of known hosts.
Authentication failed.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

여기저기 찾아보니 핑거프린트에 대한 사이트는 다음과 같았다.
한번 확인해보자. : https://docs.gitlab.com/ee/user/gitlab_com/



네트웍에 무슨 일이 생겼었나? 정확히 무슨일인지 모르겠지만 다시 시도하니 또 clone 성공했다. @.@
```bash
eddies-MacBook-Pro-2:~ eddie$ git clone git@gitlab.com:xxxxxx/auto-trading.git
Cloning into 'auto-trading'...
remote: Enumerating objects: 14, done.
remote: Counting objects: 100% (14/14), done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 14 (delta 1), reused 0 (delta 0)
Receiving objects: 100% (14/14), done.
Resolving deltas: 100% (1/1), done.
eddies-MacBook-Pro-2:~ eddie$ open .
eddies-MacBook-Pro-2:~ eddie$
```


## 참고사이트

git init 부터 ssh , 전반적 사용법까지 요약해주는 사이트. 좋다!
http://wanochoi.com/?p=1551

