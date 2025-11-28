Django 디버깅 과목평가 대비 ! ✏️ 헷갈리는 것들 정리

- 할일 수정 기능 오류 디버깅
Django의 `ModelForm`을 사용하여 기존 객체를 수정하려면, 폼을 초기화할 때 **수정하고자 하는 기존 객체**를 `instance` 인수로 반드시 넘겨주어야 함 ! 이 인수가 없으면 `form.save()`는 새로운 데이터로 **새로운 객체를 생성**하게 됨

```
def update(request, pk):
  todo = Todo.objects.get(pk=pk)
  if request.method == 'POST':
    form = TodoForm(request.POST, request.FILES, instance=todo)
    if form.is_valid():
      todo = form.save(commit=False)
      todo.user = request.user
      todo.save()
		  return redirect('todos:detail', pk=pk)
  else:
    form = TodoForm(instance=todo)
  context = {
    'form': form,
    'todo': todo
  }
  return render(request, 'todos/update.html', context)
```

- 할일 작성 버튼 출력 제어 (**로그인하지 않은 사용자에게는 표시하지 않게** 하기)

```
{% if request.user.is_authenticated %}
    <a href="{% url 'todos:create' %}" class="btn btn-primary mb-3">할일 작성</a>
{% endif %}
```

- 할일 수정 권한검사 (**요청자 == 작성자인지** 확인)

```
def update(request, pk):
  todo = Todo.objects.get(pk=pk)
  if request.user != todo.user:
    return redirect('todos:detail', pk=pk)

  if request.method == 'POST':
    form = TodoForm(request.POST, request.FILES, instance=todo) 
    if form.is_valid():
      todo = form.save(commit=False)
      todo.user = request.user
      todo.save()
      return redirect('todos:detail', pk=pk)
  else:
    form = TodoForm(instance=todo)
  context = {
    'form': form,
    'todo': todo
  }
  return render(request, 'todos/update.html', context)
```

- 이미지 업로드 기능

| **구성 요소** | **위치** | **역할** |
| --- | --- | --- |
| **`enctype="multipart/form-data"`** | `<form>` 태그 | **파일 데이터를 전송**하겠다는 브라우저와의 약속 |
| **`<input type="file">`**  | 폼 렌더링 | 사용자가 **파일을 선택**할 수 있도록 하는 HTML 요소 |
| **`request.FILES`** | `views.py` | 서버에서 **전송된 파일 데이터를 수신**하는 Python 변수 |

```
{% extends 'base.html' %}

{% block title %}할일 작성{% endblock title %}

{% block content %}
<div class="card">
    <div class="card-body">
        <h1 class="card-title">새 할일 작성</h1>
        <form method="POST" enctype="multipart/form-data">
            {% csrf_token %}
            {{ form.as_p }}
            <button type="submit" class="btn btn-primary">할일 작성</button>
            <a href="{% url 'todos:index' %}" class="btn btn-outline-secondary">취소</a>
        </form>
    </div>
</div>
{% endblock content %}
```

- 기본 이미지 표시 누락 .. 헷갈림 ㅜ.ㅜ

`<img src = “{% **static** ‘(절대경로)’ %}” >`

```
{% if todo.image %}
        <img src="{{ todo.image.url }}" alt="Todo Image" class="card-img-top" style="width: 100%; height: 300px; object-fit: cover;">
    {% else %}
        <img src="{% static 'assets\default_image.png' %}" alt="Default Todo Image" class="card-img-top" style="width: 100%; height: 300px; object-fit: cover;">
    {% endif %}
```

- 그외 기본 문법 (제발 헷갈리지 말자 ㅜ.ㅜ)
```
python -m venv venv

source venv/Scripts/activate

pip install -r requirements.txt

pip install django

django-admin startproject new_pjt .

python manage.py startapp articles

python manage.py makemigrations
python manage.py migrate

python manage.py runserver

deactivate
```