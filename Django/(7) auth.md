## HTTP (HyperText Transfer Protocol)
HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 규약 (웹에서의 모든 데이터 교환의 기초)
- 비 연결 지향 (connectionless)
- 무상태 (stateless)

## 쿠키
서버가 사용자의 웹 브라우저에 전송하는 작은 데이터 조각

- 쿠키 동작 예시
1) 브라우저가 웹 서버에 웹 페이지 요청
2) 웹 서버는 요청된 페이지와 함께 쿠키를 포함한 응답을 전송
3) 브라우저는 받은 쿠키를 저장소에 저장하고 쿠키의 속성(만료 시간, 도메인, 주소 등) 함께 저장
4) 이후 같은 웹페이지 요청하면 저장된 쿠키 중 해당 요청에 적용 가능한 쿠키 포함하여 전송
5) 받은 쿠키 정보 확인, 필요에 따라 사용자 식별, 세션 관리 등 수행
6) 웹 서버는 요청에 따라 응답 보내고 필요하면 새로운 쿠키 설정하거나 기존 쿠키 수정가능

- 쿠키 작동 원리와 활용
  - 브라우저는 쿠키를 KEY-VALUE의 데이터 형식으로 저장
  - 쿠키에는 이름, 값 외에도 만료 시간, 도메인, 경로 등의 추가 속성이 포함됨
  - 서버는 **HTTP 응답 헤더**와 **Set-Cookie 필드** 통해 클라이언트에게 쿠키 전송
  - 상태가 없는 HTTP 프로토콜에서 상태 정보를 기억시켜 주는 역할

- 쿠키 사용 목적
1) 세션 관리
2) 개인화
3) 추적, 수집

## 세션
서버 측에서 생성되어 클라이언트와 서버 간의 **상태를 유지**, 상태 정보를 **서버 쪽에 저장하고 유지하는** 데이터 저장 방식
- 세션 작동 원리
1) 클라이언트가 로그인 요청 후 인증 성공하면 서버가 세션 데이터를 생성 후 저장
2) 생성된 세션 데이터에 인증할 수 있는 세션 아이디 발급
3) 세션 아이디를 클라이언트에게 응답
4) 클라이언트는 응답받은 세션 아이디를 쿠키에 저장
5) 다시 동일한 서버 접속하면 요청과 함께 쿠키 서버에 전달
6) 서버에서 세션 아이디를 확인해 로그인되어있다는 것을 계속해서 확인
7) 사용자의 요청을 처리하고 응답

---

### Django Authentication System
- User Model 대체 -> 확장할 수 있음
- Session 관리
- 기본 인증 (ID/Password)

### User model 대체하기
두번째 app accounts 생성 및 등록하기

```
# accounts/models.py

from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
  pass
```

```
# settings.py
# Django는 프로젝트 중간에 AUTH_USER_MODEL 바꾸는걸 싫어함 ! migrate 전에 변경해두어야함
AUTH_USER_MODEL = 'accounts.User'
```

```
# accounts/admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from .models import User

admin.site.register(User, UserAdmin)
```

## 로그인
인증(id/password)을 완료하고, Session을 만들고 클라이언트와 연결하는 것
```
# accounts/urls.py

app_name = 'accounts'
urlpatterns = [
  path('login/', views.login, name='login'),
]
```
로그인 인증에 사용할 데이터를 입력받는 built-in form (**AuthenticationForm**) 사용
```
# accounts.views.py

from django.contrib.auth.forms import AuthenticationForm

def login(request):
  if request.method == 'POST':
    pass
  else:
    form = AuthenticationForm()
  context = {
    'form' : form,
  }
  return render(request, 'accounts/login.html', context)
```
```
# accounts/login.html

method = "POST" 이고 다음줄에 {% csrf_token %}
```

로그아웃 기능
```
from django.contrib.auth import logout as auth_logout

def logout(request):
  # 요청 객체(request)에 이미 유저 정보가 담겨있어서 조회할 필요 없음
  auth_logout(request)
  return redirect('articles:index')
```

---
회원가입 
```
# accounts/urls.py

app_name = 'accounts'
urlpatterns = [
  path('signup/', views.signup, name='signup'),
]
```

```
# views.py
def signup(request):
  if request.method == 'POST':
    pass
  else:
    form = UserCreationForm()
  context = {
    'form': form,
  }
  return render(request, 'accounts/signup.html', context)
```
그리고 signup.html 수정