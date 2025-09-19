### web application (web service) 개발
사용자에게 제공되는 소프트웨어 프로그램 구축 .. 다양한 디바이스 (모바일, 태블릭, PC 등)에서 웹 브라우저를 통해 접근하고 사용

### 클라이언트와 서버
- Client : 서비스를 **요청**하는 주체 (사용자의 웹 브라우저, 모바일 앱)
- Server : 클라이언트의 요청에 **응답**하는 주체 (웹 서버, 데이터베이스 서버)

## 웹 개발에서의 Frontend
사용자 인터페이스 (UI)를 담당. HTML, CSS, JavaScript 등 및 Vue.js와 같은 프론트엔드 프레임워크

## 웹 개발에서의 Backend
서버 측에서 동작, 클라이언트 요청에 대한 처리 담당. 서버 언어 (Python, Java 등) 및 백엔드 프레임워크, 데이터베이스, API, 보안 등

---

## Web Framework
웹 어플리케이션을 빠르게 개발할 수 있도록 도와주는 구조로, 개발에 필요한 기본 구조, 규칙, 라이브러리 등을 제공 (로그인/로그아웃, 회원관리, 데이터베이스, 보안 등)

# django
파이썬 기반의 대표적인 웹 프레임워크
- 다양성, 확장성, 보안, 커뮤니티 지원
- 대규모 트래픽 서비스 (스포티파이, 인스타그램, 드랍박스 등)에서도 안정적인 서비스 제공

---

# 가상 환경 (Virtual Environment)
하나의 컴퓨터 안에서 또 다른 **'독립된'** 파이썬 환경

1) 가상 환경 **생성** (맨 뒤 venv는 가상환경의 이름 !)
```
$ python -m venv venv
```

2) 가상 환경 **활성화**
```
$ source venv/Scripts/activate
```

3) 가상 환경 **종료**
```
$ deactivate
```

## 의존성 (Dependencies)
하나의 소프트웨어가 동작하기 위해 필요로 하는 다른 소프트웨어나 라이브러리
## 의존성 패키지
프로젝트가 의존하는 "개별 라이브러리"들
1) 패키지 목록 확인
```
$ pip list
```
2) 의존성 기록 (가상환경에 설치된 모든 패키지를 버전과 함께 **특정한 형식으로** 출력)
```
$ pip freeze > requirements.txt
```

---

Django 프로젝트 !
1) Django 설치
```
$ pip install django
```
2) 프로젝트 생성
```
$ django-admin startproject firstpjt .
```
3) 서버 실행
```
$ python manage.py runserver
```

## 디자인 패턴 (Design Pattern)
소프트웨어 설계에서 반복적으로 발생하는 문제에 대한, 검증되고 재사용 가능한 일반적인 해결책

ex. MVC 디자인 패턴 (Model, View, Controller)

시각적 요소와 뒤에서 실행되는 로직을 서로 영향 없이, 독립적이고 쉽게 유지 보수할 수 있는 애플리케이션을 만들기 위함

## MTV 디자인 패턴 (Model, Template, View)
Django에서 애플리케이션을 구조화하는 디자인패턴. 걍 MVC랑 똑같음 !


1) 앱 생성
```
$ python manage.py startapp articles
```
2) 앱 등록

(반드시 생성 후 !! 등록해야함)

`settings.py`의 `INSTALLED_APPS` 리스트 상단에 `'articles'` 추가하기

---
프로젝트 구조
`settings.py`, `urls.py`
그리고 그외 구조 4개 ..

앱 구조 `admin.py`, `models.py`, `views.py` 그리고 그외 구조 2개 ..

![Django 요청과 응답](https://www.interviewbit.com/blog/wp-content/uploads/2022/06/Model-1024x351.png)

## View
view 함수가 정의되는 곳 : 특정 경로에 있는 template과 request 객체를 결합해 응답 객체를 반환
```
# views.py에 첫번째 인자로 요청 객체를 필수로 받음

from django.shortcuts import render

def index(request):
  return render(request, 'articles/index.html')
```

## Template
1) articles 앱 폴더 안에 templates 폴더 생성
2) templates 폴더 안에 articles 폴더 생성
3) articles 폴더 안에 템플릿 파일 생성

# Django Template system
파이썬 **데이터(context)를 HTML 문서(template)와 결합**하여, **로직과 표현을 분리**한 채 동적인 웹페이지를 생성하는 도구.

'페이지 틀'에 '데이터'를 동적으로 결합하여 수많은 페이지를 효율적으로 만드는게 목적

`views.py`에서
```
def index(request):
  context = {
    'name' : 'Jane',
  }
  return render(request, 'articles/index.html', context)
```
하고나서 딕셔너리의 키를 삽입
`index.html`의 <body> 부분에 `Hello, {{ name }}` 이렇게

# Django Template Language (DTL)
Template에서 조건, 반복, 변수 등의 프로그래밍적 기능을 제공하는 시스템

## 1. Variable
render 함수의 세번째 함수로 **딕셔너리 타입**으로 전달, 딕셔너리 key에 해당하는 문자열이 template에서 사용가능한 변수명
`{{ variable }}`
`{{ variable.attribute }}`


## 2. Filters
변수를 수정할 때 사용 (변수 + '|' + 필터)
`{{ variable|filter }}`
`{{ name|truncatewords:30 }}`

## 3. Tags
반복 또는 논리를 수행하여 제어 흐름 만듦
`{% tag %}`
```
{% if %} 
  <h1>이거 출력해줘<h1>
{% else %}
  <h1>이거 출력하지마<h1>
{% endif %}
```

## 4. Comments
- 주석
  - inline
  `<h1>Hello, {# name #}</h1>`
  - multiline
  ```
  {% comment %}
  ...
  {% endcomment %}
  ```
  
---
 
# 템플릿 상속 (Template inheritance)
1. 페이지의 **공통요소**를 포함
2. 하위 템플릿이 **재정의할 수 있는 공간**을 정의 

→ 여러 템플릿이 공통요소를 공유할 수 있게 해주는 기능.
`extends` tag와 `block` tag가 있음

상위 템플릿 (base.html) 의 body 부분에
```
{% block content %}
{% endblock content %}
```

하위 템플릿 (index.html) 의 반드시 **최상단**에
```
{% extends 'articles/base.html' %}
{% block content %}
...
{% endblock content %}
```

---

# 요청과 응답
데이터를 보내고 가져오기 .. HTML `form` element를 통해서 !

## `'form'` element
사용자로부터 할당된 데이터를 서버로 전송하는 HTML 요소
`https://search.naver.com/search.naver?query=hello`에서
query가 input의 name 속성, hello는 input의 데이터

### action
### method
- 데이터를 어떠너 방식으로 보낼 것인지 정의
- 데이터의 HTTP request method(GET, POST)를 지정

#### throw 로직 - catch 로직
#### request 객체

((PPT 60페이지 그림 비슷한거 찾아보기))

## `'input'` element
type 속성 값에 따라 다양한 유형의 입력 데이터를 받음. 핵심 속성 - 'name'이자 사용자가 입력 데이터에 붙이는 이름(key)

### Query String Parameters
'&'로 연결된 key=value쌍으로 URL 주소에 파라미터를 통해 서버로 보내는 방법
`http://host:port/path?key=value&key=value`

### URL dispatcher (운항 관리자, 분배기)
URL 패턴을 정의하고 해당 패턴이 일치하는 요청을 처리할 view 함수를 연결(매핑)
#### Variable Routing

#### APP URL
각 앱의 urls.py에서 각자의 URL 관리
명시적 상대 경로 `from . import views` 이렇게
```
from django.urls import path, include

urlpatterns = [
  path('admin/', admin.site.urls)
  # 클라이언트 요청 추가 /articles/까지 일치하면
  # 나머지 주소는 articles 앱의 urls.py로 넘김
  path('articles/', include('articles.urls'))
]
```

### `include ('app.urls')`
프로젝트 내부 앱들의 URL을 참조할 수 있도록 매핑

### `'url' tag`
`{% url 'url_name' arg1 arg2 %}`
주어진 URL 패턴의 이름과 일치하는 절대 경로 주소 반환

### 'app_name'
여러 개의 앱 URL 이름이 겹칠 때 성(key) 지정해주기로.

`app_name = 'articles'` 먼저 써줌
그리고 url 태그도
`{% url 'app_name:path_name' arg1 arg2 %}`처럼 변경시켜줘야함