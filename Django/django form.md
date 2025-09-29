### HTML 'form'의 한계
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
    article = form.save()
    return ..

  # 2-2. 유효성 검사 통과하지못하면 해당 페이지를 다시 응답 (+ 에러메시지)
  context = {
    'form' : form,
  }
  return render(request, 'articles/new.html', context)

```