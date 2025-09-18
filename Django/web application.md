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
