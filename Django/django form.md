a### HTML 'form'의 한계
비정상적 혹은 악의적인 요청을 필터링할 수 없으므로

### Django Form의 유효성검사
를 해야함 .. 자동으로 점검하는 기능 !

## Django Form
사용자 입력 데이터를 수집하고 **처리 및 유효성 검사를 수행**하기 위한 도구

```
# articles/forms.py

from django import forms

class ArticleForm(forms.Form):
  title = forms.CharField(max_length=10)
  content = forms.CharField()
```

```
# articles/view.py

from .forms import ArticleForm

def new(request):
  form = ArticleForm()
  context = {
    'form' : form,
  }
  return render(request, 'articles/new.html', context)
```
```
# articles/new.html

{{ form }} 추가
```

## Widgets
HTML 'input' element의 표현 담당
```
# articles/forms.py

from django import forms

class ArticleForm(forms.Form):
  title = forms.CharField(max_length=10)
  content = forms.CharField(widget=forms.Textarea)
```

## Django ModelForm
사용자 입력 데이터를 DB에 저장해야 할 때
```
# articles/forms.py

from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
  # 모델 폼에 대한 추가정보
  class Meta:
    model = Article
    fields = '__all__'
```

`fields = ('title',)` 대신 `exclude = ('title',)` 로 모델에서 포함하지 않도록 필드를 지정할 수도있음

---
### ModelForm 적용
```
# articles/views.py

from .forms import ArticleForm

def create(request):
  # 1. 사용자 입력 데이터를 통째로 form 클래스의 인자로 넣어서 인스턴스를 생성
  form = ArticleForm(request.POST)

  # 2. 유효성 검사
  if form.is_valid():

    # 2-1. 유효성 검사 통과하면 저장
    # save 메서드가 저장된 객체를 반환
    article = form.save()
    return redirect('articles:detail', article.pk)

  # 2-2. 유효성 검사 통과하지못하면 해당 페이지를 다시 응답 (+ 에러메시지)
  context = {
    'form' : form,
  }
  return render(request, 'articles/new.html', context)

```
### edit
```
# articles/views.py

def edit(request, pk):
  article = Article.objects.get(pk=pk)
  form = ArticleForm(instance=article)
  context = {
    'article' : article,
    'form' : form,
  }
  return render(request, 'articles/edit.html', context)

# articles/edit.html
{{ form }}
```

### update
```
# articles/views.py
def update(request, pk):
  # 1. 수정할 게시글을 pk를 이용하여 조회
  article = Article.objects.get(pk=pk)

  # 2. 사용자가 입력한(수정한) 데이터를 통째로 받음 + 기존 데이터
  form = ArticleForm(request.POST, instance=article)

  # 3. 유효성 검사
  if form.is_valid():
    form.save
    return redirect('articles:detail', article.pk)
  context = {
    'article' : article,
    'form' : form,
  }
  return render(request, 'articles/edit.html', context)
```

### `new` + `create`
```
def create(request):
  # 요청 메서드가 POST라면 (과거 create함수의 역할)
  if request.method == 'POST':
    form = ArticleForm(request.POST)
    if form.is_valid():
      article = form.save()
      return redirect('articles:detail', article.pk)

  # 요청 메서드가 POST가 아니라면 (과거 new함수의 역할)
  else:
    form = ArticleForm()
  # context의 위치가 중요함 !!
  context = {
    'form' : form,
  }
  return render(request, 'articles/new.html', context)

```

이후에 articles/urls.py에서 `path('new/', views.new, name='new')` 제거


articles/index.html에서 `<a href = "{% url 'articles: create' %}> CREATE</a>"` 제거


articles/create.html에서 `<h1>CREATE</h1> <form action="{% url 'articles:create' %}" method="POST">` 제거


articles/view.html에서 `new.html`를 `create.html`로 변경

### `edit` + `update`
```
def update(request):
  article = Article.objects.get(pk=pk)
  if request.method == 'POST':
    form = ArticleForm(request.POST, instance=article)
    if form.is_valid():
      form.save()
      return redirect('articles:detail', article.pk)

  else:
    form = ArticleForm(instance=article)
  context = {
    'article' : article,
    'form' : form,
  }
  return render(request, 'articles/edit.html', context)
```
그리고 new+create처럼 똑같이 주석처리 or 변경해주면 됨 !