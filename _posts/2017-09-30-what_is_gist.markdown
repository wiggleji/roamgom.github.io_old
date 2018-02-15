---
title: "What is gist?"
date: 2017-09-30 11:30
layout: post
tags: [Dev, BachBach]
published: true
---



# gist란?

커뮤니티나 채팅방에 자신이 만든 코드에 대해 피드백을 받으려는 경우, 대부분 작성한 코드를 전부 복사하여 그대로 붙여넣는 경우가 많습니다.

이는 보는 입장에서 가독성이 매우 떨어지고, 채팅방에서 피드백을 원할하게 전달하는데 어려움을 겪죠.

Github에서 지원해주는 Gist를 사용하면 이 모든 걸 편하게 해결할 수 있습니다.


<img src="/img_src/post/2017-09-30/gist_page.png">


> gist 주소 : https://gist.github.com/

gist는 주로 오픈소스, 또는 프로젝트를 진행할 때 서로 작성한 코드를 공유하거나 피드백을 요구할 때 자주 쓰입니다.

<br>

## gist의 장점

1. 확장자(python의 경우 .py / C++의 경우 .cpp .h)에 따라 작성한 code에 syntax highlight를 적용시켜 줍니다.
2. 작성한 코드에 대해 comment를 작성하여 피드백을 즉시 받을 수 있습니다.
3. 코드를 단순히 url을 공유하는 걸 넘어, 블로그의 글에 embed하여 작성할 수 있습니다.
4. Markdown 문법을 지원합니다.

<br>

음.. 아직은 무슨 말인지 이해가 안될수도 있지만...
이 글을 통해 gist에 대해 완벽하게 짚고 넘어가시길 바랍니다.

<img src="/img_src/post/2017-09-30/gist_info.png">

> gist main page

* Gist description - 자신이 작성한 코드에 대해 간단한 설명을 기재합니다.
* Filename - 자신이 작성할 파일명입니다. 확장자까지 입력해줘야 syntax highlight가 처리됩니다.
* 코드 입력부분은 자신이 사용한 언어에 따라 highlight가 자동 처리됩니다.

<br>

> 예를 들어, python에서 "hello world!"를 입력할 경우,

<img src="/img_src/post/2017-09-30/gist_write.png">

처럼 입력을 한 뒤, public gist로 저장을 합니다.

검색을 통해 열람할 수 있는 public gist와 달리, secret gist는 URL만을 통해 열람할 수 있습니다.

이렇게 gist를 생성하면..

<br>

<img src="/img_src/post/2017-09-30/gist_post_info.png">

제가 사용한 python 언어에 따라 syntax highlighting이 처리된 코드가 나옵니다.

* Embed - 블로그 혹은 카페의 글에 해당 코드를 포함하고 싶을때, embed 코드로 넣을 수 있습니다.
* comment - 자신 혹은 다른 사람이 해당 코드에 대해, 피드백 또는 설명을 넣을 수 있습니다. (코드 작성할 때와 동일합니다.)

만약, 자신이 코드 파일의 형태가 아니라 설명과 코드를 같이 넣고 싶다 하는 분은 **Markdown** 양식을 통해 gist를 올려도 무방합니다.

<img src="/img_src/post/2017-09-30/write_markdown.png">

> gist 작성

<img src="/img_src/post/2017-09-30/write_markdown_result.png">

> 작성한 글 형태

**하지만**

저는 위에는 코드 파일로 기재를 하고, comment와 주석을 통해 추가 설명을 하는게 편합니다만..

선택은 스스로 편한 방식으로 사용하시면 될것 같습니다.  ^_^
