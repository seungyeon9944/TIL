# Static files (정적 파일)
서버 측에서 변경되지않고 고정적으로 제공되는 파일. 정적 파일이 사용자에게 보이려면, 그 파일에 접근할 수 있는 고유한 주소(URL)이 반드시 필요함

1. **기본 경로** (`app폴더/static/`)
- `{% load %}` : 특정 라이브러리의 태그와 필터를 현재 템플릿에서 사용할 수 있도록 불러옴

- `{% static '경로' %}` : settings.py 파일의 STATIC_URL 값을 기준으로, 해당 정적 파일의 전체 URL 경로를 계산하여 생성. ex) `img src="{% static "images.png" %}"`

### STATIC_URL
정적 파일의 '웹 주소', 오직 웹(브라우저)에서만 사용되는 주소임

2. **추가 경로**
  ### `STATICFILES_DIRS`
  문자열로 추가적으로 탐색할 경로의 목록을 지정
  ```
  # settings.py
  STATICFILES_DIRS = [
    BASE_DIR / 'static',
  ]
  ```

---
## Media files
사용자가 웹사이트를 통해 직접 업로드하는 파일

### `ImageField()`
이미지 파일을 업로드하기 위해 사용하는 Django 모델 필드
```
image = models.ImageField(upload_to='images/')
```
제공하기 전 준비사항
1) settings.py에 `MEDIA_ROOT`, `MEDIA_URL` 설정
2) 작성한 MEDIA_ROOT와 MEDIA_URL에 대한 URL 지정

### `MEDIA_ROOT`
미디어 파일의 '실제 창고' 주소 (어디에 저장될지 지정하는 **절대 경로**)
`MEDIA_ROOT = BASE_DIR / 'media'`

### `MEDIA_URL`
미디어 파일의 '웹 주소' 별명
`MEDIA_URL = 'media/'`

그리고 project의 urls.py에서
```
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
  path('admin/', admin.site.urls),
  path('articles/', include('articles.urls')),
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```
```
# articles/models.py

class Article(models.Model):
  image = models.ImageField(upload_to='images/', blank=True)
```
Pillow 설치 후 migrations 재진행
(43쪽부터 정리)