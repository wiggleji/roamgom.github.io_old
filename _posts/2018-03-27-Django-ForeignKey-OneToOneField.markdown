---
title: "[Django] ForeignKey와 OneToOneField의 차이"
date: 2018-02-11 23:45:02
tags: [Django]
published: true
---


# ForeignKey와 OneToOneField 차이

[Stackoverflow 링크](https://stackoverflow.com/questions/5870537/whats-the-difference-between-django-onetoonefield-and-foreignkey)


Django에서 Model을 설계할 때 많이 헷갈리는 ForeignKey와 OneToOneField

`ForeignKey(SomeModel, unique=True)`

`OneToOneField(SomeModel)`

이 둘의 차이는 reverse side of the relation, 즉, 역관계에 있다.

<br>

> 역관계

```python
# models.py
from django.db import models


class User(models.Model):
    username = models.Charfield(max_length=50)

    def __str__(self):
        return self.name
    

class Snippet(models.Model):
    title = models.Charfield(max_length=100)
    user = models.ForeignKey(Group)

    def __str__(self):
        return self.title
```

위의 모델에서 `Snippet`은 ForeignKey인 `user`를 통해 `user_id`값을 가지고 있기 때문에 `User`에 접근이 가능하다.

역으로, `User`에서 `Snippet`에 접근하려면, `id`값을 가지는 ForeignKey가 없기 때문에 `Snippet`에 접근 가능한 **snippet**`_set`을 사용해줘야한다.

```python
>>> from test_app.models import User, Snippet

# Test 객체 생성
>>> user_in = User(username='roamgom')
>>> user_in.save()

>>> snippet_in = Snippet(title='코딩코딩', user=user_in)
>>> snippet_in.save()

# 객체 호출
>>> user1 = User.objects.get(id=1)
>>> snippet1 = Snippet.objects.get(id=1)

>>> user1
<User: roamgom>

>>> snippet1
<Snippet: 코딩코딩>

# 정방향 참조
>>> snippet1.user.username
'roamgom'

# 잘못된 참조
>>> user1.snippet.title
AttributeError: 'User' object has no attribute 'snippet'

# 역방향 참조
# ForeignKey가 없는 모델에서는 model_set으로 접근해야 한다.
>>> user1.snippet_set(id=user1.id).title
'코딩코딩'
```

> ForeignKey와  OneToOneField

코드는 Stackoverflow의 모델을 그대로 가져왔다.

```python
# models.py
from django.db import models


class Engine(models.Model):
    name = models.CharField(max_length=25)

    def __unicode__(self):
        return self.name


class Car(models.Model):
    name = models.CharField(max_length=25)
    engine = models.OneToOneField(Engine)

    def __unicode__(self):
        return self.name


class Engine2(models.Model):
    name = models.CharField(max_length=25)

    def __unicode__(self):
        return self.name


class Car2(models.Model):
    name = models.CharField(max_length=25)
    engine = models.ForeignKey(Engine2, unique=True)

    def __unicode__(self):
        return self.name
```

아래는 `python3 manage.py shell`을 통해 실행해본 결과

* `OneToOneField` 예시
```python
>>> from testapp.models import Car, Engine

>>> c = Car.objects.get(name='Audi')

>>> e = Engine.objects.get(name='Diesel')

>>> e.car
<Car: Audi>

>>> print(type(e.car))
<class 'blog.models.one_to_one.Car'>
```

* `ForeignKey(unique=True)` 예시
```python
>>> from testapp.models import Car2, Engine2

>>> c2 = Car2.objects.get(name='Mazda')

>>> e2 = Engine2.objects.get(name='Wankel')

>>> e2.car2_set.all()
[<Car2: Mazda>]

>>> print(type(e2.car2_set.all()))
<class 'django.db.models.query.QuerySet'>
```

결국, OneToOneField로 연결해준 모델은 `Car` Object를 반환해주며, `Engine`은 `Car`에 접근하기 위한 `_set`을 사용할 필요가 없다.

반면, `Car2`와 `Engine2`의 경우, `Engine2`는 `_set`을 이용해야 `Car2`에 접근할 수 있다. 그리고 반환되는 Type은 `QuerySet`이다.

<br>

> 용도

OneToOne은 1개의 객체에 1개의 값만 가져야할 경우,
예를 들어, 유저당 하나의 블로그를 가지게 설계한다.

`User`와 `Blog`가 있다면, 두개는 반드시 한번의 매칭만 이루어진다.

Django에 있는 `auth.models`의 `User`를 오버라이딩하는 대신, 하나의 모델을 생성하여 Field를 추가하여 사용할 수도 있다.
