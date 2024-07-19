
# Django 사이트 실행 방법 및 에러 해결

## Django 기본 실행 절차

Django에서 사이트를 실행하기 위한 기본적인 절차는 다음과 같습니다:

1. **Django 설치:**
   ```bash
   pip install django
   ```

2. **프로젝트 생성:**
   ```bash
   django-admin startproject mysite
   cd mysite
   ```

3. **앱 생성:**
   ```bash
   python manage.py startapp myapp
   ```

4. **앱을 설정에 추가:**
   `mysite/settings.py` 파일을 열고 `INSTALLED_APPS` 리스트에 새로 생성한 앱을 추가합니다.
   ```python
   INSTALLED_APPS = [
       ...
       'myapp',
   ]
   ```

5. **모델 작성 (선택사항):**
   `myapp/models.py` 파일에 모델을 정의합니다.
   ```python
   from django.db import models

   class MyModel(models.Model):
       name = models.CharField(max_length=100)
   ```

6. **마이그레이션 생성 및 적용:**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

7. **뷰 작성:**
   `myapp/views.py` 파일에서 뷰를 작성합니다.
   ```python
   from django.http import HttpResponse

   def index(request):
       return HttpResponse("Hello, world!")
   ```

8. **URL 설정:**
   `myapp/urls.py` 파일을 생성하고 URL 패턴을 정의합니다.
   ```python
   from django.urls import path
   from . import views

   urlpatterns = [
       path('', views.index, name='index'),
   ]
   ```

   그리고 `mysite/urls.py` 파일에서 앱의 URL을 포함시킵니다.
   ```python
   from django.contrib import admin
   from django.urls import include, path

   urlpatterns = [
       path('admin/', admin.site.urls),
       path('myapp/', include('myapp.urls')),
   ]
   ```

9. **서버 실행:**
   ```bash
   python manage.py runserver
   ```

10. **브라우저에서 확인:**
    웹 브라우저를 열고 `http://127.0.0.1:8000/myapp/`에 접속하여 "Hello, world!" 메시지를 확인합니다.

## 에러 해결: IntegrityError

### 에러 메시지
```plaintext
django.db.utils.IntegrityError: NOT NULL constraint failed: polls_question.pub_date
```

### 원인
이 에러는 `Question` 모델의 `pub_date` 필드가 `NOT NULL` 제약 조건을 가지고 있지만, 객체를 저장할 때 `pub_date` 값을 제공하지 않아서 발생합니다.

### 해결 방법

1. **객체 생성 시 `pub_date` 값을 포함:**
   ```python
   from django.utils import timezone

   q3 = Question(question_text="아이스크림vs햄버거", pub_date=timezone.now())
   q3.save()
   ```

2. **객체 생성 후 `pub_date` 값을 설정:**
   ```python
   from django.utils import timezone

   q3 = Question(question_text="아이스크림vs햄버거")
   q3.pub_date = timezone.now()
   q3.save()
   ```

### 기본값 설정으로 문제 예방

모델 정의 시 기본값을 설정하여 이러한 문제를 예방할 수 있습니다:
```python
from django.db import models
from django.utils import timezone

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField(default=timezone.now)
```

이렇게 하면 `pub_date` 값을 명시적으로 설정하지 않아도 객체 생성 시 현재 시간이 자동으로 설정됩니다.
