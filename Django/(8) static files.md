# Static files (정적 파일)
서버 측에서 변경되지않고 고정적으로 제공되는 파일. 정적 파일이 사용자에게 보이려면, 그 파일에 접근할 수 있는 고유한 주소(URL)이 반드시 필요함

1. 기본 경로 (`app폴더/static/`)
- `{% load %}` : 특정 라이브러리의 태그와 필터를 현재 템플릿에서 사용할 수 있도록 불러옴

- `{% static '경로' %}` : settings.py 파일의 STATIC_URL 값을 기준으로, 해당 정적 파일의 전체 URL 경로를 계산하여 생성. ex) `img src="{% static "images.png" %}"`

## STATIC_URL
정적 파일의 '웹 주소', 오직 웹(브라우저)에서만 사용되는 주소임

2. 추가 경로
  ## STATICFILES_DIRS
  문자열로 추가적으로 탐색할 경로의 목록을 지정
  ```
  # settings.py
  STATICFILES_DIRS = [
    BASE_DIR / 'static',
  ]
  ```