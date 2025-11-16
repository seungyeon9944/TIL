# 분할 정복 (Top-down approach)
문제를 작은 하위 문제로 나누고(분할) 각각을 해결(정복)한 뒤, 그 결과를 결합(통합)하여 원래 문제를 해결하는 알고리즘 기법. 

|   |  병합 정렬  |  퀵 정렬  |
|---| ---------- | ----------|
|분할기준|단순히 배열을 반으로 나눔|기준 아이템(pivot item)을 중심으로 기준보다 작은 것을 왼편, 큰 것을 오른편에 위치 시킴|
|병합 처리|정렬된 부분을 다시 병합하는 과정이 필요함|별도의 병합과정 필요X|


## 병합 정렬 (Merge Sort)
다 분할하고 합치면서 정렬하자 ! 멀티코어 CPU나 다수의 프로세서에서 병렬화. 시간 복잡도 : **O(n log n)**

코딩테스트에서 sort 쓸 수 없고 시간 제한이 빡빡할 때 자주 사용
```
# 1. 분할 과정
merge_sort(LIST m)
  IF length(m) == 1 : RETURN m

  LIST left, right
  middle <- length(m) / 2
  FOR x in m before middle
    add x to left
  FOR x in m after or equal middle
    add x to right
  
  left <- merge_sort(left)
  right <- merge_sort(right)

  RETURN merge(left, right)

# 2. 병합 과정
merge(LIST left, LIST right)
  LIST result

  WHILE length(left) > 0 OR length(right) > 0
    IF length(left) > 0 AND length(right) > 0
      IF first(left) <= first(right)
        append popfirst(left) to result
      ELSE
        append popfirst(right) to result
    ELIF length(left) > 0
      append popfirst(left) to result
    ELIF length(right) > 0
      append popfirst(right) to result

  RETURN result
```
---

## 퀵 정렬 (Quick Sort)
기준값 중심으로 주어진 배열을 두개로 분할하고, 각각을 정렬해서 전체를 정렬
1 ) 작업 영억 지정 2 ) Pivot 결정 3 ) Pivot을 기준으로 배치 변경 순서로 !
- 평균 속도 : O(N logN)
- 최악의 경우 : O(N^2)
```
quicksort(A[], l, r)
  if l < r
    s <- partition(A[], l, r)
    quickSort(A[], l, s-1)
    quickSort(A[], s+1, r)
```
### 1. Hoare-Partition
### 2. Lomuto Partition
---

## 이진검색 (Binary Search)⭐
정렬된 데이터를 기준으로 특정 값이나 범위를 검색하는데 사용. 목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 검색 범위를 반으로 줄여나가면서 보다 빠르게 검색 수행
**Lower Bound**, **Upper Bound**

1) 반복 구조
```
binary_search(n, S[], key):
  low <- 0
  high <- n-1

  WHILE low <= high
    mid <- (low + high)/2

    IF S[mid] == key
      RETURN mid
    ELIF S[mid] > key
      high <- mid - 1
    ELSE
      low <- mid + 1
  RETURN -1
```

2) 재귀 구조
```
binary_search(a[], low, high, key)
  IF low > high
    RETURN -1
  ELSE
    mid <- (low + high)/2
    IF key == a[mid]
      RETURN mid
    ELIF key < a[mid]
      RETURN binary_search(a[], low, mid-1, key)
    ELSE
      RETURN binary_search(a[], mid+1, high, key)
```