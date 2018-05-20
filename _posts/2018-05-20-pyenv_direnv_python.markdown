---
title: "Pyenv, Direnv로 파이썬 개발환경 구축하기"
date: 2018-05-20 12:00:00
tags: [BachBach, Dev]
published: false
---

파이썬으로 개발하면서 꼭 필요한 것 중 하나가 바로 개발환경 분리하기 입니다.

저도 다른 사람들과 마찬가지로 이전에 많이 사용한게 `virtualenv`에 `autoenv`를 사용해 디렉토리마다 환경 분리 시켜줌과 동시에 터미널에서 쉽게 작업할 수 있었죠.

하지만 가끔 회사 또는 특정 상황에서 패키지 버전 뿐 아니라 파이썬 버전이 달라지는 경우도 종종 생길 수 있다고 생각하여 `pyenv`와 `direnv`로 갈아탔습니다.

# Pyenv

한 컴퓨터에서 2개 이상의 파이썬 버전을 사용하는 건 정말 힘들죠. 추가적인 설치와 환경변수 변경 없이 원하는 파이썬 버전을 골라 사용하게 도와주는 친구가 `pyenv`입니다.

적용된 개발환경을 보자면,

[이미지] - 쉘 pyenv (python --version)

이렇게 원하는 파이썬 버전을 그때그때 사용할 수 있습니다.

> 설치 

[pyenv 링크](https://github.com/pyenv/pyenv)

* macOS

```shell
$ brew update
$ brew install pyenv
```

* Linux

```shell
 $ git clone https://github.com/pyenv/pyenv.git ~/.pyenv

$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile

$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
```

**Zsh를 사용할 경우 ~/.zshenv 파일에 추가해주세요.**

> 명령어

```shell
# 파이썬 버전 리스트
$ pyenv versions

* system (set by /Users/roamgom/SCV/pypy_test/.python-version)
  3.4.2
  3.4.6

# 파이썬 특정 버전 설치
$ pyenv install 3.6.5

# 현재 디렉토리에서만 파이썬 버전 변경
# 실행시 디렉토리 안에 생긴 .python-version에 버전 명시
$ pyenv local 3.4.6

# 전체 시스템에서 파이썬 버전 변경
$ pyenv global 3.4.6

# system은 OS에 설치된 파이썬의 기본 버전
$ pyenv local system

# 특정 버전 삭제
$ pyenv uninstall 3.4.6
```

위의 명령어로 원하는 버전을 설치하여 각 디렉토리에 버전을 지정해주면 나머지는 `direnv`에서 처리해줍니다!

---

# Direnv

이 친구.. 정말 좋은 친구에요 :smile:

`autoenv`를 사용하며 안타까웠던 것 중 하나가 디렉토리에 입을 할때와 달리 이탈했을 때 환경이 비활성화가 안되는 점이었습니다. 매번 `deactivate`를 써야했죠.

그런데, `direnv` 이 친구는 둘 다 가능합니다! 앞서 `pyenv`로 버전을 명시한 디렉토리에 진입/이탈할 경우 알아서 환경을 활성/비활성화 해줍니다.

이제 우리는 초기 환경 세팅만 해주면 그 후에는 신경쓰지 않고 편하게 작업할 수 있다는 얘기죠.

> 설치

[direnv 링크](https://direnv.net/)

```shell
# 설치
$ git clone https://github.com/direnv/direnv
$ cd direnv
$ make install

# shell 환경변수
# BASH
$ eval "$(direnv hook bash)"

# ZSH
$ eval "$(direnv hook zsh)"
```

**마찬가지로 shell마다 다르게 작성해줘야 합니다.**

기타 쉘 설정은 [여기에서](https://direnv.net/)

> 명령어

```shell
# 현재 디렉토리에서 direnv 활성화
$ direnv allow
```

---

자, 그러면 본격적으로 개발환경을 구축해보도록 하겠습니다.

```shell
# 프로젝트 디렉토리 생성 후 진입
$ mkdir project
$ cd project

# 원하는 파이썬 버전 선택
$ pyenv local 3.4.6

# 해당 디렉토리에 파이썬 패키지 폴더 생성
$ python -m venv .venv

# 개발환경 활성화를 해주는 트리거 파일 작성
# direnv 에러가 뜨면 정상 (아직 활성화를 안해줬기 때문)
$ echo 'source .venv/bin/activate' > .envrc
direnv: error .envrc is blocked. Run `direnv allow` to approve its content.

# direnv 활성화
$ direnv allow
```

세팅이 완료된 후 컴퓨터 글로벌과 프로젝트의 파이썬 버전, 패키지를 살펴보면

```shell
roamgom$ python --version
Python 3.6.5
roamgom$ pip list
Package                  Version
------------------------ -------
beautifulsoup4           4.6.0
boto3                    1.7.16
botocore                 1.10.21
...

roamgom$ cd project
direnv: loading .envrc
direnv: export +VIRTUAL_ENV ~PATH

project$ python --version
Python 3.4.6

project$ pip list
pip (1.5.6)
setuptools (2.1)

project$ ls -a
.               .envrc          .venv
..              .python-version

project$ cd ..
direnv: unloading

$ python --version
Python 3.6.5
```

짜잔!

이제 특정 디렉토리에 개발환경을 맞출 뿐 아니라
진입/이탈할 경우 알아서 환경까지 변경해 줍니다.

이제 여러분은 패키지 뿐 아니라 파이썬 버전까지 분리와 개발환경 자동 활성화/비활성화까지 가능하겠군요.


