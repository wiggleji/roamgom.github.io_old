---
title: "htop 사용하기"
date: 2018-04-17 12:00:00
tags: [Ubuntu, BachBach]
published: true
---

# top

<img src="/img_src/post/2018-04-17/top.png">

보통 `top`을 리눅스에서 프로세스 관리자로 많이 사용

기본 명령어로 딸려와 사용하기 나쁘지 않지만

이보다 보기 좋게 출력해주는..

# htop

> 설치

```shell
sudo apt-get install -y htop
```

> 실행

```shell
htop
```

> 실행화면

<img src="/img_src/post/2018-04-17/htop.png">

cpu 코어 당 사용량, 메모리 등

사용자가 보기 쉽게 나타내준다.

**결론**: htop > top