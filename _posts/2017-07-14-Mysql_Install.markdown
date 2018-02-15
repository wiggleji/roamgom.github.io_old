---
title: "Query My SQL - Install Mysql Using Homebrew on Mac"
date: 2017-07-11 13:00
layout: post
category: ["Backend"]
tagline: ""
published: false
---


### Mac에서 Homebrew를 통한 Mysql 설치

#1.Homebrew 설치

"링크"

#2. Mysql 설치

```$ brew install mysql```

Homebrew로 mysql을 설치합니다.


```$ mysql.server start```

mysql 시작

```$ mysql_secure_installation```

'root'의 비밀번호를 설정해줍니다.

<br>
<br>

#### ```$ mysql_secure_installation``` 실행시 나오는 설정들
<br>

* ```$ Would like to setup VALIDATE PASSWORD?``` : 
복잡한 비밀번호로 설정하도록 제한해주는 플러그인의 사용여부.<br>
`yes` __ - 보안성 높은 비밀번호 사용  __  `no`__ - ~~아 귀찮.. 그런거 없다.~~__

<br><br>

* ```$ Remove anonymouse users?``` : 
익명사용자의 삭제/유지 여부. 'uroot' 없이 '$ mysql'만으로 접속 가능.<br>
`yes -u` __ - 삭제  __ `no`__ - 유지__

<br><br>

* ```$ Disallow root login remotely?``` : 
localhost 외 다른 ip에서 root로 원격접속을 가능하게 할지 여부.<br>
`yes` __ - 원격접속 불가  __ `no`__ - 원격접속 가능__

<br><br>

* ```$ Remove test database and access to it?``` : 
mysql에 기본적으로 생성된 test DB 삭제 여부.<br>
`yes` __ - 삭제  __ `no`__ - 유지__

<br><br>

* ```$ Reload privilege tables now?``` : 
위와 같이 작성한 mysql의 권한 설정을 적용할지 여부.<br>
__`yes` - 적용  __ `no`__ - 건너뛰기__. &nbsp;&nbsp;&nbsp; (*yes를 선택하는게 편합니다.*)
<br>









