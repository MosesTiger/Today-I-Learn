# Django URL 패턴과 뷰 연결

Django에서 `path` 함수를 사용하여 URL 패턴을 정의하고 이를 처리할 뷰와 연결하는 방법을 설명합니다.

## 1. 모듈 임포트

먼저, 필요한 모듈을 임포트합니다.

```python
from django.urls import path
from . import views
```

- `path`: Django의 URL 패턴을 정의하는 함수입니다.
- `views`: 현재 디렉토리의 뷰 모듈을 가져옵니다. 이 모듈에는 URL 요청을 처리하는 뷰 함수들이 정의되어 있습니다.

## 2. URL 패턴 정의

URL 패턴 리스트인 `urlpatterns`를 정의합니다.

```python
urlpatterns = [
    path('', views.index, name='index'),
]
```

- `path('', views.index, name='index')`:
  - `''`: 빈 문자열은 기본 URL, 즉 도메인의 루트를 의미합니다 (예: `example.com/`).
  - `views.index`: 루트 URL로 요청이 들어올 때 호출될 뷰 함수입니다. 여기서는 `views` 모듈의 `index` 함수가 호출됩니다.
  - `name='index'`: URL 패턴에 `index`라는 이름을 부여합니다. URL 이름은 템플릿에서 URL을 참조하거나, 뷰 함수나 다른 곳에서 URL을 역으로 찾을 때 유용합니다.

## 3. 뷰 함수 예시

`views` 모듈에는 `index`라는 이름의 뷰 함수가 정의되어 있어야 합니다. 예를 들어, `views.py` 파일은 다음과 같이 작성될 수 있습니다:

```python
# views.py

from django.http import HttpResponse

def index(request):
    return HttpResponse("Welcome to the Index Page")
```

- `index` 함수는 HTTP 요청을 받아들여 "Welcome to the Index Page"라는 텍스트를 포함한 HTTP 응답을 반환합니다.

## 4. 전체 흐름 요약

1. 사용자가 웹 브라우저에 `example.com/`을 입력합니다.
2. Django는 `urlpatterns`에서 일치하는 URL 패턴을 찾습니다.
3. 빈 문자열 `''`과 일치하는 패턴이 발견되면, `views.index` 함수가 호출됩니다.
4. `views.index` 함수는 "Welcome to the Index Page"라는 내용을 가진 HTTP 응답을 반환합니다.
5. 사용자는 브라우저에서 이 응답을 보게 됩니다.

이와 같은 방식으로 Django는 URL과 뷰 함수를 연결하여 요청을 처리합니다.
