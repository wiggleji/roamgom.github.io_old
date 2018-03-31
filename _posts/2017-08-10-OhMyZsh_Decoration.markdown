---
title: OhMyZsh로 터미널 꾸미기
date: 2017-08-10 11:32
layout: post
thumbnail: img_src/post/2017-08-10/ohmyzsh_logo.png
tags: [Dev, BachBach]
---
published: true
---


> <span style="color:red"> **MacOS / Linux ONLY** </span>

> <span style="color:red"> 이 가이드는 MacOS에서 작성했습니다. </span>

<br>
맥과 리눅스에서 개발용으로 터미널을 많이 사용하게 됩니다. 처음 터미널을 접했을 때, 사용방법은 물론이고 화면을 보는게 매우 불편했습니다...

그래서 좀더 예쁜 터미널로 꾸미기 위해 Bash 대신 Zsh를 사용하기 시작!
<br><br>




### iTerm2 설치
> Mac OS


Mac에서 쓰이는 터미널 iTerm2를 먼저 설치를 해주세요.

![](/img_src/post/2017-08-10/iterm2.png)

* [Official Download Page](https://www.iterm2.com/downloads.html)

**Stable Releases**에서 가장 최신을 받아주시면 됩니다.
.zip파일을 열고 iTerm2를 응용프로그램으로 옮겨주세요.

<br>

***


### HomeBrew 설치
> Mac OS

Ubuntu에 APT가 있다면 Mac에는 HomeBrew가 있다!

APT와 마찬가지로 각종 프로그램 패키지를 관리해주는 프로그램입니다. `brew` 명령어로 패키지를 관리합니다.
![](/img_src/post/2017-08-10/homebrew.png)

* [Official Page](https://brew.sh/)


**설치 명령어**

```$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```

<br><br>

- #### Brew 사용법 <link#>


<br><br>

***
### Zsh 설치
> Mac OS / Linux


Shell 종류는 다양합니다. Bash, sh, csh, ksh...
그 중 우리가 사용할 쉘은 바로 Zsh입니다!
![](/img_src/post/2017-08-10/zsh.jpg)

왜 Zsh를 쓰냐고요?

Zsh 는 Bash에 비해 확장성이 뛰어납니다.


* cd/ls 자동완성
  `$ cd / ls <TAB>` 사용 시 현재 Directory를 표시해줘 빠른 이동이 가능하다.
![](/img_src/post/2017-08-10/cd_completion.png)


* history 검색
`<Ctrl>+R` 을 통해 이전에 쓴 명령어를 쉽게 찾을 수 있다.
![](/img_src/post/2017-08-10/find_command.png)


이 외에 많은 [이유](https://code.joejag.com/2014/why-zsh.html)가 있습니다.

**하지만 제일 중요한 이유!**

![](/img_src/post/2017-08-10/zsh_pretty.png)

...

![](/img_src/post/2017-08-10/pretty.jpg)


위에서 설치한 `brew`를 통해 zsh를 설치합니다.

**설치 명령어**

```$ brew install zsh```

자 그러면 이렇게 예쁜 쉘을 만들어봅시다.

<br>
***

### Oh-My-Zsh
> Mac OS / Linux

OhMyZsh는 Zsh에 각종 Plugin과 Theme을 적용시켜주는 Framework입니다.

![](/img_src/post/2017-08-10/ohmyzsh_logo.png)


* [Official Page](http://ohmyz.sh/)

<br>

**설치 명령어**


```$ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"```

설치가 완료되면

![](/img_src/post/2017-08-10/ohmyzsh.jpeg)

멋진 로고가 나타납니다.

마지막으로 테마와 폰트를 설정해줘야겠죠?
테마에는 여러 종류가 있으니 마음에 맞는 테마를 고르세요!

* [Theme Link](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)



<br><br>



**테마 설정**


이제 원하는 테마를 적용해야겠죠?

설정을 해주기 위해 .zshrc파일을 열어줍니다. (Sublimetext3, Atom, vim 등)

vim으로 열 경우

```vim ~/.zshrc```

파일에서 10번 줄에 있는 설정이 바로 테마를 정해주는 부분입니다.
![](/img_src/post/2017-08-10/zshrc.png)


```ZSH_THEME="THEME_NAME"```

THEME_NAME에 원하는 테마 이름을 입력하고 iTerm2를 재부팅 해주면 해당 테마가 적용됩니다.
제가 사용하고 있는 Zsh테마는 `agnoster`입니다.

<br>

**폰트/색테마 설정**

폰트를 설정해주려면 우선 폰트 파일이 필요합니다.
구글링해서 원하는 폰트를 설치해도 무방하지만 이번 가이드에서는 링크를 통해 설정합시다.


* [Font Link](https://www.slant.co/topics/67/~best-programming-fonts)

<br>

**설치가 완료되면 iTerm을 종료하고 다시 실행시켜 주세요. 설정에서 설치한 폰트를 로드하지 못할 수 있습니다.**

<br>

iTerm을 다시 실행하고 메뉴창에서
*iTerm2-Preferences...*

![](/img_src/post/2017-08-10/preferences.png)

*Profiles-Default-Text-Change Font*
로 들어가서 Collection을 **고정폭**으로 설정해주세요. 그리고 Family에서 해당 폰트를 선택해주세요.
(안그러면 시스템 상 설치된 모든 폰트가 나와요)

![](/img_src/post/2017-08-10/preferences_text.png)

자 이제는 **색테마**차례군요.
색테마는 현재 적용한 Zsh테마에서 폰트 색상 및 배경을 따로 설정해주는거라 보시면 돼요.

테마는 구글에서 `itermcolors`로 검색해서 마음에 드는 걸로 설치하면 됩니다.

제가 마음에 들었던 테마 링크를 올려드릴게요.

<br>

![](/img_src/post/2017-08-10/facebook.png)

* [Facebook-iterm-Theme](https://github.com/slwen/facebook-iterm-theme)

![](/img_src/post/2017-08-10/oceanic.png)

* [Oceanic-next-theme](https://github.com/mhartington/oceanic-next-iterm)

이제 불러오기만 하면 끝나겠군요.

폰트를 설정했을때와 동일하게
*iTerm2-Preferences...*

![](/img_src/post/2017-08-10/preferences.png)

*Profiles-Default-Colors-Color Presets...* 에서 *Import...* 로 해당 파일을 불러와 적용하면 끝납니다.

![](/img_src/post/2017-08-10/preferences_color.png)


<br>

***
### zsh-syntax-highlighting
> Mac OS / Linux

zsh-syntax-highlighting은 시스템 PATH에 등록된 명령어들을 알아서 Syntax처리 해주는 친구입니다.
한번에 명령어의 가능 여부를 확인할 수 있죠.

![](/img_src/post/2017-08-10/zsh_syntax.png)


**설치 명령어**

```$ brew install zsh-syntax-highlighting```

또는

```$   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
$ echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```

<br>

---

<br>

**끝!**