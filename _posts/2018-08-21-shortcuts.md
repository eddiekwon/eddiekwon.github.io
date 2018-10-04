---
layout: post
title: Shortcuts
category: Tip
permalink: /tip/:year/:month/:day/:title/

tags: [tip, xcode, mac, conda]
comments: true
date: 2018-07-20 21:40:00 +0900
---

### 삭제

디렉토리 삭제  : 

`rm –r directory1`   // directory1 폴더 및 안의 파일 다 지우기
`rm –rf directory1`  // 묻지도 따지지도 않고 다 지우기 (–f 옵션 + –r 옵션)

### 아나콘다

버전 확인 및 업데이트
```bash
conda --version
conda update conda
```

* 환경 만들기
```bash
conda create -n myenv python=3.5 [패키지이름]
```

* 설치된 환경 확인
```bash
conda info --envs
```
현재 적용중인 환경에는 *이 붙어 있다.

* 적용
```bash
windows: activate myenv
mac: source activate myenv
```

* 추가 패키지 설치
 n 옵션은 없어도 되는 듯하다.

```bash
conda install -n myenv scipy
```

* 적용환경에서 나오기
```bash
source deactivate
```

* 환경 설정 삭제
```bash
conda remove -n myenv --all
```

참고: https://github.com/honux77/practice/wiki/conda--간단-사용법