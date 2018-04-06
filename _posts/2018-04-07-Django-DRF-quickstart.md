---
title: "[Django] DRF QuickStart (Django 2.0)"
date: 2018-04-07 12:00:00
tags: [Django, DRF]
published: false
---

# QuickStart

여러분과 같이 admin 유저가 한 시스템의 users와 groups를 관리할 수 있는 간단한 API를 생성해 보겠습니다.

## Project setup
`tutorial` 이름의 Django 프로젝트를 생성해 주시고, 프로젝트 안에 `quickstart`라는 새로운 앱을 만들어 주세요.

```shell
# 프로젝트 디렉토리 생성
mkdir tutorial
cd tutorial

# 로컬 패키지 의존성을 위해 virtualenv 생성
virtualenv env
source env/bin/activate # 윈도우에서는 `env\Scripts\activate`

# virtualenv에 Django 와 Django REST Framework 패키지 설치
pip install django
pip install djangorestframework

# 새로운 Django 프로젝트와 프로젝트내 앱 생성
django-admin.py startproject tutorial .    # 뒤의 '.' 문자 주의
cd tutorial
django-admin.py startapp quickstart
cd ..
```


생성된 프로젝트 레이아웃은 아래와 같이 보여야 합니다:

```shell
$ pwd
# <해당 아래 경로>/tutorial
$ find .
.
./manage.py
./tutorial
./tutorial/__init__.py
./tutorial/quickstart
./tutorial/quickstart/__init__.py
./tutorial/quickstart/admin.py
./tutorial/quickstart/apps.py
./tutorial/quickstart/migrations
./tutorial/quickstart/migrations/__init__.py
./tutorial/quickstart/models.py
./tutorial/quickstart/tests.py
./tutorial/quickstart/views.py
./tutorial/settings.py
./tutorial/urls.py
./tutorial/wsgi.py
```

프로젝트 디렉토리 안에 생성된 앱이 이상하게 보일 수도 있지만,

프로젝트의 namespace를 사용함으로써 외부 모듈과의 충돌을 피할 수 있습니다. ##(주제는 quickstart의 scope 밖으로 향합니다???)

이제 데이터베이스와 동기화 시켜주세요:

```shell
python manage.py migrate
```

`admin` 계정명과 `password123` 암호를 가진 최초 유저를 생성해주세요. 이는 후에, 예제에서 생성한 유저를 통해 인증을 진행할 겁니다.

```shell
python manage.py createsuperuser --email admin@example.com --username admin
```

데이터베이스와 초기 유저를 설정했다면, 준비는 끝났습니다. 앱의 디렉토리를 열고, 코딩을 진행해보죠...


## Serializers

맨 처음으로, 우리는 몇 개의 serializer를 정의할 겁니다.

`tutorial/quickstart/serializers.py`라는 새로운 모듈을 만들어주세요. 이는 우리가 만든 데이터를 표현하는데 쓰일 겁니다.

```python
from django.contrib.auth.models import User, Group
from rest_framework import serializers


class UserSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = User
        fields = ('url', 'username', 'email', 'groups')


class GroupSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Group
        fields = ('url', 'name')
```

이번의 경우, `HyperlinkedModelSerializer`로 hyperlinked 관계를 쓰고 있다는 걸 주목해주세요. 물론 primary key와 다른 여러 관계도 사용할 수 있지만, hyperlinking으로 멋지게 RESTful한 디자인을 만들 수 있습니다.


## Views

이제, 약간의 view를 만들어 볼까요? `tutorial/quickstart/views.py`를 열어 주시고, 아래와 같이 코드를 써주세요.

```python
from django.contrib.auth.models import User, Group
from rest_framework import viewsets
from tutorial.quickstart.serializers import UserSerializer, GroupSerializer


class UserViewSet(viewsets.ModelViewSet):
    """
    API endpoint that allows users to be viewed or edited.
    """
    queryset = User.objects.all().order_by('-date_joined')
    serializer_class = UserSerializer


class GroupViewSet(viewsets.ModelViewSet):
    """
    API endpoint that allows groups to be viewed or edited.
    """
    queryset = Group.objects.all()
    serializer_class = GroupSerializer
```

여러개의 view를 작성하는 대신 `ViewSets`라는 클래스들로 공통된 속성들을 분류했습니다.

필요하다면 각각의 view로 나누어 정의할 수 있지만, viewset을 사용하여 view logic을 간결하게 정리된 상태로 유지시켜 줍니다.


## URLs

자, 이제 API URL을 연결해 볼까요? `tutorial/urls.py`에서 작업을 해보죠...

#### 이거 2.0 맞춰서 써줘야할 것
```python
from django.urls import path, include
from rest_framework import routers
from tutorial.quickstart import views

router = routers.DefaultRouter()
router.register(r'users', views.UserViewSet)
router.register(r'groups', views.GroupViewSet)

# Wire up our API using automatic URL routing.
# Additionally, we include login URLs for the browsable API.
urlpatterns = [
    url(r'^', include(router.urls)),
    url(r'^api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
```

현재 view 대신에 viewset을 사용하고 있기 때문에, 우리는 viewset을 router class로 등록하여 API를 위한 URL을 자동으로 생성할 수 있습니다.

#### ???
API URL 이상으로 더 많은 제어가 필요할 경우, regular class-based view를 사용하고, URL 설정을 명시적으로 작성하여 적용시킬 수 있습니다.

마침내, 열람 가능한(browsable) API에 쓰일 기본 login과 logout view를 포함시켰습니다. 이는 선택 사항이지만, 여러분이 만든 API에 인증을 요구하고, 열람하여(browsable) 사용할 수 있도록 설계한다면 이를 유용하게 사용하실 수 있습니다.


## Settings

`rest_framework`를 `INSTALLED_APPS` 안에 추가해주세요. 설정 모듈은 `tutorial/settings.py`에 있습니다.

```python
INSTALLED_APPS = (
    ...
    'rest_framework',
)
```

네, 끝났습니다.


## API 테스트하기

이제 우리가 만든 API를 테스트할 수 있습니다. 커맨드로 서버를 작동시켜 볼까요?

```shell
python manage.py runserver
```

이제 command-line과 `curl` 같은 툴로 API에 접근할 수 있습니다.

```shell
bash: curl -H 'Accept: application/json; indent=4' -u admin:password123 http://127.0.0.1:8000/users/
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "email": "admin@example.com",
            "groups": [],
            "url": "http://127.0.0.1:8000/users/1/",
            "username": "admin"
        },
        {
            "email": "tom@example.com",
            "groups": [                ],
            "url": "http://127.0.0.1:8000/users/2/",
            "username": "tom"
        }
    ]
}
```

아니면 `httpie`를 통해서도 가능합니다.

```shell
bash: http -a admin:password123 http://127.0.0.1:8000/users/

HTTP/1.1 200 OK
...
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "email": "admin@example.com",
            "groups": [],
            "url": "http://localhost:8000/users/1/",
            "username": "paul"
        },
        {
            "email": "tom@example.com",
            "groups": [                ],
            "url": "http://127.0.0.1:8000/users/2/",
            "username": "tom"
        }
    ]
}
```

물론 브라우저에서 `http://127.0.0.1:8000/users/`라는 URL을 통해 바로 확인할 수도 있지만요.

#### IMG

만약 브라우저에서 진행한다면, 우측 상단에 있는 control을 통해 로그인한 상태인지 꼭 확인하시길 바랍니다.

완벽하네요, 생각보다 쉬웠죠?

REST framework가 어떻게 서로 맞물려 실행되는지 더 깊게 알고 싶으시다면, `tutorial`, 또는 `API guide`를 둘러보세요.

