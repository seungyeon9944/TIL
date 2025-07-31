### 오답노트 📝💯
✏️ **재귀 함수**를 이용하여 문자열 뒤집기

    def reverse_string(s):
        if len(s) <= 1:
            return s
        else:
            # 문자열의 두번째 글자부터 끝까지 뒤집고, 그 결과의 끝에 첫번째 결과를 붙임
            return reverse_string(s[1:]) + s[0]

    string1 = "hello!"
    print(reverse_string(string1)) 
    
하면 "!olleh"가 나옴
