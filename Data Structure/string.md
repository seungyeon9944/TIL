[1] 문자열
s.find(x) x의 첫번째 위치를 반환, 없으면 -1 반환
s.index(x) x의 첫번째 위치를 반환, 없으면 오류 발생
s.isupper( ) 모두 대문자
s.islower( ) 모두 소문자
s.isalpha( ) 모두 알파벳

[1-1] 문자열 조작(새로운 문자열 반환) 메서드 - 23페이지 표
s.replace(old, new[,count]) 
새로운 글자로 바꿔서 반환. text.replace(‘world’, ‘Python’, 1)이라고 하면 한 개만 replace됨

s.strip([chars]) 
문자열의 시작과 끝에 있는 공백 또는 지정 문자 제거

s.split(sep=None, maxsplit = -1)
sep를 구분자 문자열로 사용하여 문자열에 있는 단어들의 리스트를 반환.
sep 안넣으면 공백으로 split함. 
text.split(‘,’)면 콤마를 기준으로 split함. split된 결과에 공백도 포함되어있음

‘seperator’.join(iterable)
iterable의 문자열을 연결한 문자열을 반환
iterable은 리스트, 튜플 등등
ex. words = [‘Hello’, ‘world!’]일 때 text = ‘-‘.join(words)면 
print(text)하면 ‘Hello-world!’됨

s.capitalize( ) 가장 첫번째글자를 대문자로 변경
s.title( ) 각 단어의 첫글자만 대문자, 단어의 다른글자들은 소문자
s.upper( ) 모두 대문자로
s.lower( ) 모두 소문자로
s.swapcase( ) 대문자는 소문자로, 소문자는 대문자로
