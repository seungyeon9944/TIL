# 큐 Queue
먼저 들어온 데이터가 **먼저 나가는** 선형 자료구조
큐의 뒤에서는 삽입만 하고, 앞에서는 삭제만

    삭제 <- ㅁ ㅁ ㅁ ㅁ ㅁ ... ㅁ ㅁ ㅁ ㅁ ㅁ <- 삽입

       머리(Front)                  꼬리(Rear)
       첫번째원소                    마지막 원소

  
## 선입선출 FIFO (First In First Out)
가장먼저 넣은 자료가 가장먼저 나오는 것. 1 2 3 넣으면 1 2 3 순서로 나옴

- enqueue(item) : 큐의 뒤쪽(rear 다음)에 원소 삽입
- dequeue() : 큐의 앞쪽(front)에 원소 삭제하고 반환
- create_queue() : 공백 상태의 큐 생성
- is_empty() : 큐가 공백상태인지 확인
- is_full() : 큐가 포화상태인지 확인
- qpeek() : 큐의 앞쪽에 원소 삭제 없이 반환

1. 공백 큐 생성
front = rear = -1
2. 원소 A 삽입
front (마지막으로 삭제된 위치) = -1 / rear +=1하고 그 자리에 A
3. 원소 B 삽입
front (마지막으로 삭제된 위치) = -1 / rear +=1하고 그 자리에 B
4. 원소 반환/삭제
front가 가리키는 자리는 삭제된 자리
5. front == rear이면 큐가 빈 상태

## 선형 큐 Linear Queue
배열이나 연결형 리스트로 구현
- 초기 상태 : `front = rear = -1`
- 공백 상태 : `front == rear`
- 포화 상태 : `rear = n-1`

        enqueue(item) :
            global rear
            if is_full() : print("Queue_Full")
            else :
                rear <- rear + 1;
                q[rear] <- item

        dequeue()
            if(is_empty()) then queue_empty();
            else
                front <- front + 1;
                return Q[front];

        is_empty() :
            return front == rear

        is_full() :
            return rear = len(q) - 1
        
        def qpeek() :
            if is_empty() : print("Queue_Empty")
            else : return q[front+1]

## 원형 큐
- 초기 상태 : `front = rear = 0`
- index의 순환
- front가 있는 자리는 사용하지않고 항상 빈자리로
- 삽입 위치 : `rear = (rear + 1) mod n`
- 삭제 위치 : `front = (rear + 1) mod n`

        def enqueue(item) :
            global rear
            if is_full():
                print("Queue_Full")
            else:
                rear = (rear+1) % len(cq)
                cq[rear] = item

        def dequeue(item) :
            global front
            if is_empty():
                print("Queue_Empty")
            else:
                front = (front+1) % len(cq)
                return cq[front]

        is_empty() :
            return front == rear

        is_full() :
            return (rear+1) % len(cq) == front

## 연결 큐 Linked Queue
1. 공백 큐 생성 createLinkedQueue()

        front NULL
        rear NULL

2. 원소 A 삽입 enqueue(A)

        front 0x1000 -> A
        rear 0x1000 -> A

3. 원소 B 삽입 enqueue(B)

        front 0x1000 -> A
        rear 0x1008 -> B

4. 원소 삭제 dequeue()

        front 0x1008 -> B
        rear 0x1008 -> B

5. 원소 C 삽입 enqueque(C)

        front 0x1000 -> B
        rear 0x1010 -> C

### deque 덱
끝에서 빠르게 추가와 삭제를 할 수 있는 리스트류 컨테이너. 연결 리스트를 직접 만들지 않아도 됨

## 우선순위 큐 Priority Queue
FIFO 순서가 아니라 우선순위대로 ! 가장 앞에 우선순위의 원소가 위치. 원소의 재배치가 필요 .. 메모리 낭비 큼

---

## 버퍼 Buffer
데이터를 다른 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역 (버퍼링 = 버퍼를 채우는 것)