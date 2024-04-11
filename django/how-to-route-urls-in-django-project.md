# Django 프로젝트에서 URL 라우팅하는 방법

`Django`는 `URL`을 `View`와 연결하여 웹 애플리케이션의 동작을 결정하는 `URL` 라우팅을 제공합니다.

## URLconf 설정하기

`Django`에서 `URL` 라우팅은 `URLconf(Uniform Resource Locator configuration)`를 통해 이루어집니다. `URLconf`는 `URL`과 해당하는 뷰를 매핑하는데 사용됩니다. `Django` 프로젝트의 루트 `URLconf`는 보통 프로젝트 폴더 내에 있는 `urls.py` 파일에 정의됩니다.

```py
# config/urls.py
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("admin/", admin.site.urls),
    path(
        "polls/",
        include("polls.urls"),
    ),
]
```

## URL 패턴 정의하기

`urls.py` 파일에서는 `urlpatterns` 리스트에 `URL` 패턴과 해당하는 뷰를 매핑합니다. 각 `URL` 패턴은 `path()` 또는 `re_path()` 함수를 사용하여 정의됩니다. `path()` 함수는 단순한 경로 기반 매핑에 사용되고, `re_path()` 함수는 정규 표현식을 사용하여 복잡한 `URL` 패턴에 사용됩니다.

```py
# app/urls.py
from django.urls import path

from . import views

urlpatterns = [
    # ex: /polls/
    path("", views.index, name="index"),
    # ex: /polls/5/
    path("<int:question_id>/", views.detail, name="detail"),
    # ex: /polls/5/results/
    path("<int:question_id>/results/", views.results, name="results"),
    # ex: /polls/5/vote/
    path("<int:question_id>/vote/", views.vote, name="vote"),
]
```

## View와 URL 매핑하기

`URL` 패턴에서 지정한 뷰는 요청을 처리하고 적절한 응답을 반환합니다. 뷰는 함수 또는 클래스로 정의될 수 있으며, 요청을 처리하여 응답을 반환하는 로직이 작성됩니다. 이러한 뷰 함수는 클라이언트의 요청을 처리하고 동적인 웹 페이지를 생성하는데 사용됩니다.

```py
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")


def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)


def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)


def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```
