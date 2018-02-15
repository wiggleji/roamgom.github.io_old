---
title: "pip list --format=(legacy|columns) 경고 해결하기"
date: 2017-09-19 13:00
layout: post
tags: [Dev, Python, Inde]
published: true
---



# pip list 출력 포맷 방식 변경


```
$ pip list
```
**Python3.6**에서 pip를 사용하다보면

```
DEPRECATION:The default format will switch to columns in the future. You can use --format=(legacy|columns) (or define a format=(legacy|columns) in your pip.conf under the [list] section) to disable this warning.
```

이라는 문구가 뜨면서 설치된 패키지의 리스트가 나온다.

매우 보기 싫은 문구이다. 고쳐보자.

<br>

#### 1. 디렉토리 생성하기
> Mac / Linux 동일

```
$ mkdir -p $HOME/.pip
$ vi $HOME/.pip/pip.conf
```

<br>

.pip 디렉토리를 만들어주고, pip.conf파일 생성


```
[global]
timeout = 60

[freeze]
timeout = 10

[list]
format = (legacy | columns)
```

위 내용을 안에 기재해준다.
format에서 legacy 또는 columns 형식을 정해주면 된다.
(개인적으로 columns가 마음에 든다)

<br>
> legacy의 경우

![]( = 200px)
<img src="/img_src/post/2017-09-19/legacy.png">


<br>
> columns의 경우

<img src="/img_src/post/2017-09-19/columns.png">


이제 `pip list`를 입력하면 깔끔하게 잘 나온다.
