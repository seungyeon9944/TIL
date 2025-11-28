월말평가 대비 !

views.py

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework import status

from django.shortcuts import get_object_or_404

from .models import Article
from .serializers import (
    ArticleSerializer,
    ArticleListSerializer
)

@api_view(['GET', 'POST'])
def article_list(request):
    if request.method == 'GET':
        article = Article.objects.all()
        serializer = ArticleListSerializer(article, many=True)
        return Response(serializer.data)
    # Body 탭에서 raw와 JSON을 선택
    elif request.method == 'POST':
        # 1. 클라이언트가 보낸 데이터를 Serializer에 전달
        serializer = ArticleSerializer(data=request.data)

        # 2-1. 데이터 유효성 검사
        if serializer.is_valid(raise_exception=True):
            # 3. 유효하면 저장
            serializer.save()

            # 4. 201 Created 상태 코드와 함께 생성된 객체 정도 응답
            return Response(serializer.data, status=status.HTTP_201_CREATED)
    # 2-2. 유효성 검사 실패 시 400 Bad Request 응답
    return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

@api_view(['GET', 'PUT', 'DELETE'])
def article_detail(request, article_pk):
    article = get_object_or_404(Article, pk=article_pk)

    if request.method == 'GET':
        serializer = ArticleSerializer(article)
        return Response(serializer.data)
        
    # Body 탭에서 raw와 JSON을 선택
    # PUT 요청은 인스턴스와 새로운 데이터 이렇게 2개를 전달해야함
    elif request.method == 'PUT':
        # 1. 기존 객체와 클라이언트가 보낸 데이터를 Serializer에 전달
        serializer = ArticleSerializer(article, data=request.data)

        # 2. 데이터 유효성 검사
        if serializer.is_valid(raise_exception=True):
            # 3. 유효하면 저장
            serializer.save()

            # 4. 수정된 객체 정보 반환
            return Response(serializer.data)
        
    elif request.method == 'DELETE':
        # 1. 객체 삭제
        article.delete()

        # 2. 메시지와 204 No Content 상태 코드 반환
        data = {'msg' : f'{article.pk}번 파일 삭제'}
        return Response(data, status=status.HTTP_204_NO_CONTENT)
```

serializers.py

```python
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.ModelSerializer):
    class Meta:
        model = Article
        fields = '__all__'

class ArticleListSerializer(serializers.ModelSerializer):
    class Meta:
        model = Article
        fields = ('id','title',)
```