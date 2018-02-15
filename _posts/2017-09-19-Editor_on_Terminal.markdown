---
title: "Sulime / VScode를 Terminal로 열어보자"
date: 2017-09-19 13:00
layout: post
tags: [Dev, Inde]
published: true
---

다들 코딩을 하다보면, 터미널과 IDE를 왔다리 갔다리 하는게 일상일거라 생각하며 터미널에서 편집기를 열어보는 방법을 작성해봅니다.


## VScode

정말 간단합니다.

> VScode를 열어주세요.

> `⇧⌘P`로 Command Palette를 열어주고

`> shell command: Install 'code' command in PATH`

를 통해 PATH에 code 명령어를 설치해줍니다.

<br>

이제 터미널에서 원하는 디렉토리에서 `code .`을 입력하면 뙇!

<br><br>

## Sublime Text

> 디렉토리 생성

```
$ mkdir ~/bin
```

<br>
> Sublime 실행경로 복사

```
$ ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" ~/bin/subl
```

**Sublime 앱의 명칭을 Finder를 통해 정확히 기재해주셔야합니다.**
<br>
```
"Applications/서브라임_이름.app/..."
```

이런식으로~

다음은 터미널을 뭘 쓰냐에 따라 방식이 나눠집니다.

<br><br>


#### 1. Bash를 쓸 경우

> ~/.bash_profile 파일에 복사

```
$ echo 'export PATH=$PATH:$HOME/bin' >> ~/.bash_profile
```

<br>

> Sublime을 기본 에디터로 설정

```
echo "export EDITOR='subl' -w">> ~/.bash_profile
```

<br><br>

#### 2. Zsh를 쓸 경우

> ~/.zshrc 파일에 복사

```
echo 'export PATH=$PATH:$HOME/bin' >> ~/.zshrc
```

<br>

> Sublime을 기본 에디터로 설정

```
echo "export EDITOR='subl' -w" >> ~/.zshrc
```


<br><br>
**자 모든 설정이 끝났습니다!**

터미널 재시작 후

자신이 열고 디렉토리에서 `subl .`이라고 입력하면

바로 서브라임이 사용가능합니다~~~	    '\\(- 3-)/`
