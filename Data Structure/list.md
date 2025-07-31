# 리스트 값 
## 추가 및 삭제 메서드
### L.append(x) 
`none`을 반환하기 때문에 `print(L)`을 해줘야함
`my_list.append([4,5,6])`하면 `[1, 2, 3, [4, 5, 6]]`

### L.extend(m) 
**m 자리에는 iterable만 가능. 정수 입력하면 안됨**
`my_list.extend([4, 5, 6])` 하면 `[1, 2, 3, 4, 5, 6]`

### L.insert(위치, 항목)
ex. `my_list = [1, 2, 3]`
`my_list.insert(1, 5)`면 `print(my_list)`했을 때 `[1, 5, 2, 3]`

### L.remove(항목)
리스트에서 첫 번째로 일치하는 항목 삭제

### L.pop(항목)
리스트에서 지정한 인덱스의 항목을 반환하고 제거, 작성하지 않을 경우 마지막 항목을 반환 후 제거

### L.clear( )
모든 항목 삭제

---

## 리스트 탐색 및 정렬 메서드
### L.reverse( ) 
리스트의 순서를 역순으로 변경(정렬X), **none을 반환하기 때문에 print**를 해줘야 함

### L.sort( )
원본 리스트를 오름차순으로 정렬, **none을 반환하기 때문에 print**를 해줘야 함

---

### 오답노트
len 함수를 쓰지않고 list에서 가장 문자열이 긴 단어를 추출하라.

    def longest_string(str_list):
        num_list = []

        # 주어진 리스트의 문자열 순회
        for str in str_list:
            alpha_num = 0
            # 각 문자열의 알파벳 하나하나 순회해서 길이값을 저장
            for alphabet in str:
                alphabet_num += 1
            num_list.append(alphabet_num)

        # 길이값 저장 리스트 중 더 큰값이 있으면 max_num으로 대체하고 max_index도 해당 인덱스로 할당

        max_num = num_list[0]
        max_index = 0
        index = 0
        for number in num_list:
            if number > max_num:
                max_num = number
                max_index = index
            index += 1

    # 저장한 인덱스값으로 최종 문자열 반환        
    return str_list[max_index]

---
### 
주어진 matrix에서 최대값을 가지는 인덱스를 출력하라. 단 최대값이 중복일 경우 인덱스가 더 작은 것으로 출력하라.

    def find_max(matrix):

        max_number = matrix[1][2]
        max_number_list = []
        row_max = 0
        column_max = 0

        for each_list in matrix:
            length = len(each_list)
            for i in range(length):
                for j in range(length):
                    if matrix[i][j] > max_number :
                        max_number = matrix[i][j]
                        max_number_list.append(max_number)
                        if max_number_list.count(max_number) == 1:
                            row_max = i
                            column_max = j

        return (row_max, column_max)


    matrix1 = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]
    ]

    matrix2 = [
        [4, 2, 3],
        [9, 6, 5],
        [7, 8, 1]
    ]

    print(find_max(matrix1)) 
    print(find_max(matrix2))  


각각 [2,2]와 [1,0]이 금방 잘 나온다 ..
왜 막상 시험볼때는 못풀었는지 ㅜ.ㅜ