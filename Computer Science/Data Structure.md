# Data Structure 자료구조

## 배열(Array)

#### 배열 회전 프로그램

##### 기본적인 회전 알고리즘

- temp를 활용해서 첫번째 인덱스 값을 저장 후 arr[0]~arr[n-1]을 각각 arr[1]~arr[n]의 값을 주고, arr[n]에 temp를 넣어준다.
- 원하는 회전 수(n) 만큼 이동 가능

```c++
void leftRotatebyOne(int arr[], int n){
    int temp = arr[0], i;
    for(i = 0; i < n-1; i++){
       arr[i] = arr[i+1];
    }
    arr[i] = temp;
}
```

##### 저글링 알고리즘

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201014134454531.png" alt="image-20201014134454531" style="zoom:67%;" />

- 최대공약수를 이용해 집합을 나누어 여러 요소를 한꺼번에 이동시킴
- Ex) arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12} 에서 1,2,3을 옮기려 할 때
  - 12와 3의 최소공약수는 3
  - 인덱스를 3개씩 묶고 회전시킴
  - a) arr [] -> { **4** 2 3 **7** 5 6 **10** 8 9 **1** 11 12}
  - b) arr [] -> {4 **5** 3 7 **8** 6 10 **11** 9 1 **2** 12}
  - c) arr [] -> {4 5 **6** 7 8 **9** 10 11 **12** 1 2 **3** }

```c++
void leftRotate(int arr[], int d, int n) 
{ 
    for (int i = 0; i < gcd(d, n); i++) { 
       
        int temp = arr[i]; 
        int j = i; 
  
        while (1) { 
            int k = j + d; 
            if (k >= n) 
                k = k - n; 
  
            if (k == i) 
                break; 
  
            arr[j] = arr[k]; 
            j = k; 
        } 
        arr[j] = temp; 
    } 
} 
```

##### 역전 알고리즘

- 회전시키는 수(피벗)에 대해 구간을 나누어 reverse로 구현

1. d=2라면 1,2 / 3,4,5,6,7 로 구간을 나누고
2. 첫번째 구간을 reverse: 2,1
3. 두번째 구간을 reverse: 7,6,5,4,3
4. 합치면 2,1,7,6,5,4,3
5. 합친 배열을 reverse: 3,4,5,6,7,1,2

```c++
void reverseArr(int arr[], int start, int end){
    while (start < end){
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;

        start++;
        end--;
    }
}

void rotateLeft(int arr[], int d, int n){
	reverseArr(arr, 0, d-1);
	reverseArr(arr, d, n-1);
	reverseArr(arr, 0, n-1);
}
```

#### 배열의 특정 최대 합 구하기

- arr가 있을 때, arr를 회전하면서 i*arr[i]의 합이 가장 큰 경우를 찾기
- Ex) arr[] = {1, 20, 2, 10}일 때 2번 회전해서 2\*0 + 10\*1 + 1\*2 + 20\*3 = 72가 최대
- 접근 방법
  - 회전 횟수에 따라 R0 = 0\*arr[0] + 1\*arr[1] +...+ (n-1)\*arr[n-1]
  - R1 = 0\*arr[n-1] + 1\*arr[0] +...+ (n-1)\*arr[n-2]
  - R1 - R0 = arr[0] + arr[1] + ... + arr[n-2] - (n-1)\*arr[n-1]
  - R2 - R1 = arr[0] + arr[1] + ... + arr[n-3] - (n-1)\*arr[n-2] + arr[n-1]
  - 즉, Rj - Rj-1 = arrSum - n \* arr[n-j] 이라는 규칙을 찾을 수 있다.
  - R0부터 구하고, 차이를 이용해서 비교하고 최댓값 갱신하면 됨

#### 특정 배열을 arr[i] = i로 재배열 하기

..?

## 연결 리스트(Linked List)

연속적인 메모리 위치에 저장되지 않는 선형 데이터 구조

- 포인터를 사용해서 연결

- 각 노드는 **데이터 필드**와 **다음 노드에 대한 참조**를 포함하는 노드로 구성

  ```c++
  // A linked list node 
  struct Node 
  { 
    int data; 
    struct Node *next;
  }; 
  ```

- Linked List를 사용하는 이유

  - 배열은 비슷한 유형의 선형 데이터를 저장하는데 사용할 수 있지만, 제한 사항이 있음..
    - 배열이 크기가 고정되어 있어 미리 요소 수에 대해 할당을 받아야 함
    - 새로운 요소를 삽입하는 것이 비용이 많이 듦(공간을 만들고, 기존 요소 전부 이동)

- 장점

  - 동적 크기
  - 삽입/삭제 용이

- 단점

  - 임의의 노드에 액세스가 안됨.. 첫번째 노드부터 순차적으로 요소에 액세스해야 함. (binary search도 불가능)
  - 포인터의 여분 메모리 공간이 목록의 각 요소에 필요???

#### Single Linked List(Java)

```java
class LinkedList {
    
    Node head;

    static class Node {
        int data;
        Node next;
        Node(int d) { // 생성자
            data = d; next = null;
        }
    }

    public void printList() 
    { 
        Node n = head; 
        while (n != null) 
        { 
            System.out.print(n.data+" "); 
            n = n.next; 
        } 
    }

    public static void main(String[] args){

        LinkedList llist = new LinkedList();

        llist.head = new Node(1);
        Node second = new Node(2);
        Node third = new Node(3);
    
        llist.head.next = second; // 첫번째 노드에 두번째 노드 연결
        second.next = third; // 두번째 노드에 세번째 노드 연결
        
        llist.printList(); 
    }
}
```

#### 노드 추가(C)

- 앞쪽에 노드 추가

```c
void push(struct Node** head_ref, int new_data){
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));

    new_node->data = new_data;

    new_node->next = (*head_ref);

    (*head_ref) = new_node;
}
```

- 특정 노드 다음에 추가

```c
void insertAfter(struct Node* prev_node, int new_data){
    if (prev_node == NULL){
        printf("이전 노드가 NULL이 아니어야 합니다.");
        return;
    }

    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));

    new_node->data = new_data;
    new_node->next = prev_node->next;

    prev_node->next = new_node;
}
```

- 끝쪽에 노드 추가

```c
void append(struct Node** head_ref, int new_data){
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    struct Node* last = *head_ref;

    new_node->data = new_data;

    new_node->next = NULL;

    if (*head_ref == NULL){
        *head_ref = new_node;
        return;
    }

    while(last->next != NULL){
        last = last->next;
    }

    last->next = new_node;
    return;
}
```

## Array & ArrayList & LinkedList

#### 개요

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201014172241120.png" alt="image-20201014172241120" style="zoom:67%;" />

- **Array**: <u>index</u>로 빠르게 값을 찾는 것이 가능
- **LinkedList**: 데이터의 <u>삽입 및 삭제가 빠름</u>
- **ArrayList**: 데이터를 <u>찾는데 빠르지만</u>, <u>삽입 및 삭제가 느림</u>

> **상황에 맞는 자료구조를 잘 선택하는 것이 중요!**

#### Array(배열)

- 선언할 때 크기와 데이터 타입을 지정해야 함
- 즉, 메모리 공간에 <u>할당할 사이즈를 미리 정해놓고</u> 사용하는 자료구조
- 장점
  - index가 존재하므로 검색에 편하다
- 단점
  - 계속 데이터가 늘어날 때, 최대 사이즈를 알 수 없을 때, 중간에 데이터를 삽입/삭제할 때 비효율적!!!
    - 특정 index 값에 새로운 값을 넣으려면 원래 값을 뒤로 밀어내고 해당 index에 덮어씌워야 함..

#### List

- Array의 단점을 보완하기 위해 나옴
- <u>크기를 정해주지 않아도 됨!</u>
  - 대신 array는 index가 중요했다면, list에서는 <u>순서</u>가 중요!
- 장점
  - 크기가 정해져있지 않으므로 중간에 데이터를 추가/삭제하더라도 괜찮다.
  - index를 가지고 있으므로 검색도 빠르다
- 단점
  - 중간에 데이터를 추가/삭제할 때 시간이 오래 걸림
    - 더하거나 뺄 때 줄줄이 당겨지거나 밀려나는데 이때 연산이 추가되고, 메모리 또한 낭비된다.

#### LinkedList

- **한 노드에 연결될 노드의 포인터 위치를 가리키는 방식**
- 단일(뒤 노드만 가리킴), 다중(앞뒤 노드 모두 가리킴) 등 여러가지 존재
- 장점
  - 데이터를 중간에 삽입/삭제할 때 전체를 돌지 않아도 이전 값과 다음 값이 가리켰던 주소 값만 수정하고 연결시켜주면 되므로 빠르다.
- 단점
  - List의 k번째 값을 찾는 것은 비효율적임..
    - Array나 ArrayList의 경우 index를 갖고 있어 검색이 빠르지만, LinkedList는 처음부터 순차검색해야 하므로 시간이 더 걸린다..

## 스택 & 큐

#### 스택(Stack)

- 입력과 출력이 같은 한 곳(방향)으로 제한됨

- LIFO(Last In First Out, 후입선출): 늦게 들어온 원소가 먼저 나옴
- 사용 예) 함수의 call stack, 문자열 역순 출력, 연산자 후위표기법, DFS

##### 구현

- 스택 포인터(SP)

  - push와 pop할 때 해당 위치를 기억하는 변수
  - 처음에는 -1로 초기화
  - 마지막 원소의 위치를 기억하는듯..

  ```java
  private int sp = -1;
  ```

- push

  ```java
  public void push(Object o) {
      if (isFull(o)) { // 스택 포인터가 최대 크기와 같으면 return
          return;
      }
      
      stack[++sp] = o; // 아니면 스택의 최상위 위치에 값을 넣음
  }
  ```

- pop

  ```java
  public Object pop() {
      if (isEmpty(sp)) { // 스택 포인터가 0이 되면 null로 return
          return null;
      }
      
      Object o = stack[sp--]; // 아닌 경우 스택의 최상위 위치의 값을 꺼내오고, 스택 포인터의 값이 하나 내려감
      return o;
      
  }
  ```

- isEmpty

  ```java
  private boolean isEmpty(int sp) {
      return sp == -1 ? true : false; // sp가 초기화값과 같다면 true, 아니면 false
  }
  ```

- isFull

  ```java
  private boolean isFull(int sp) {
      return sp + 1 == MAX_SIZE ? true : false; // sp+1 값이 MAX_SIZE와 같으면 true, 아니면 false
  }
  ```

#### 동적 배열 스택

- 위처럼 구현하면 스택에는 MAX_SIZE라는 최대 크기가 정해짐
- 최대 크기가 없는 스택이 동적 배열 스택!

##### arraycopy(동적 배열)를 활용한 구현

```java
public void push(Object o) {
    
    if (isFull(sp)) { // 스택 포인터가 최대 크기에 도달한 경우
        Object[] arr = new Object[MAX_SIZE * 2]; // 2배 크기의 새로운 배열을 할당
        System.arraycopy(stack, 0, arr, 0, MAX_SIZE); // 값 복사
        stack = arr; // 참조값 할당
        MAX_SIZE *= 2; // MAX_SIZE 2배로 증가
    }
    
    stack[sp++] = o;
}
```

##### LinkedList를 활용한 구현

```java
public class Node {
    public int data;
    public Node next;

    public Node() {
    }

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class Stack {
    private Node head; // 제일 "아래" 노드. stack[0] 이라서 head인듯
    private Node top; // 제일 위 노드

    public Stack() {
        head = top = null;
    }

    private Node createNode(int data) {
        return new Node(data);
    }

    private boolean isEmpty() {
        return top == null ? true : false;
    }

    public void push(int data) {
        if (isEmpty()) { // 스택이 비어있다면
            head = createNode(data);
            top = head;
        }
        else { //스택이 비어있지 않다면 마지막 위치를 찾아 새 노드를 연결시킨다.
            Node pointer = head;

            while (pointer.next != null)
                pointer = pointer.next;

            pointer.next = createNode(data);
            top = pointer.next;
        }
    }

    public int pop() {
        int popData;
        if (!isEmpty()) { // 스택이 비어있지 않다면!! => 데이터가 있다면!!
            popData = top.data; // pop될 데이터를 미리 받아놓는다.
            Node pointer = head; // 현재 위치를 확인할 임시 노드 포인터

            if (head == top) // 데이터가 하나라면
                head = top = null;
            else { // 데이터가 2개 이상이라면
                while (pointer.next != top) // top을 가리키는 노드를 찾는다.
                    pointer = pointer.next;

                pointer.next = null; // 마지막 노드의 연결을 끊는다.
                top = pointer; // top을 이동시킨다.
            }
            return popData;
        }
        return -1; // -1은 데이터가 없다는 의미로 지정해둠.
    }
}
```

#### 큐(Queue)

- 입력과 출력이 서로 다른 한 곳(rear, front)으로 제한됨

- FIFO(First In First Out, 후입선출): 먼저 들어온 원소가 먼저 나옴
- 사용 예) 버퍼, BFS
- 큐의 가장 첫 원소를 front, 가장 끝 원소를 rear로 부름
- 큐에서는 원소가 rear로 들어와 front로 빠진다
- 가장 첫 원소와 끝 원소에만 접근 가능

##### 구현

- 기본값

  ```java
  private int size = 0; 
  // 데이터를 넣고 뺄 때 해당 값의 위치를 기억하기 위해 필요
  private int rear = -1; // enQueue할 위치 기억
  private int front = 0; // deQueue할 위치 기억
  
  Queue(int size) { 
      this.size = size;
      this.queue = new Object[size];
  }
  ```

- enQueue

  ```java
  public void enQueue(Object o) {
      
      if (isFull()) return;
      
      queue[++rear] = o; // 아니면 rear+1에 값을 넣음
  }
  ```

- deQueue

  ```java
  public Object deQueue() {
      
      if (isEmpty()) return null;
      
      Object o = queue[front++];
      return o;
  }
  ```

- isEmpty

  ```java
  public boolean isEmpty() {
      return front == rear+1;
  }
  ```

- isFull

  ```java
  public boolean isFull() {
      return (rear == queueSize-1);
  }
  ```

##### 단점

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201019151125822.png" alt="image-20201019151125822" style="zoom:50%;" />

- 일반 큐(선형 큐)의 경우 front, reat 모두 -1에서 시작하여 삽입과 삭제가 반복될 수록 두 변수 모두 계속 증가하게 된다.
- 이러한 과정이 반복되면 rear가 queue(크기 n)의 마지막 인덱스인 n-1에 도달하게 되는데, 이 경우 앞의 데이터가 비어있는 경우에도 rear == queueSize-1 이 되어 isFull()이 true가 된다.
- <u>즉, 앞이 비어있는 경우에도 큐가 꽉 찼다고 인식하게 됨!</u>

#### 원형 큐(Circular Queue)

- 논리적으로 배열의 처음과 끝이 연결되어 있는 것으로 간주
  - 선형 큐의 단점을 보완
- <u>empty와 full을 쉽게 구분하기 위해 자리 하나를 항상 비워둠</u>
- **(index + 1) % size** 로 순환시킴

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201019163012570.png" alt="image-20201019163012570" style="zoom:67%;" />

##### 구현

- 기본값

  ```java
  private int size = 0; 
  private int rear = -1; 
  private int front = 0;
  
  Queue(int size) {
      this.size = ++size; // 한 자리 더 할당하고 빈 자리로 사용
      this.queue = new Object[size];
  }
  ```

- enQueue

  ```java
  public void enQueue(Object o) {
      
      if (isFull()) return;
      
      rear = (rear + 1) % size; // 더해주고 mod
      queue[rear] = o;
  }
  ```

- deQueue

  ```java
  public Object deQueue() {
      
      if (isEmpty()) return null;
      
      Object o = queue[front];
      front = (front + 1) % size;
      return o;
  }
  ```

- isEmpty

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201019165452008.png" alt="image-20201019165452008" style="zoom:67%;" />

  ```java
  public boolean isEmpty() {
      return ((rear + 1) % size) == front;
  }
  ```

- isFull

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201019165505212.png" alt="image-20201019165505212" style="zoom:67%;" />

  ```java
  public boolean isFull() {
      return ((rear + 2) % size) == front;
  }
  ```

##### 단점

- 메모리 공간에 대한 활용은 좋지만, 어쨌든 <u>배열로 구현</u>되어 있기 때문에 <u>큐의 크기가 제한됨!</u>

#### 연결리스트 큐

- LinkedList를 이용하여 큐를 구현하여 크기의 제한이 없고, 삽입 및 삭제가 편리
  - 원형 큐의 단점을 보완

##### 구현

- enQueue
  - 데이터 추가는 tail에 한다
  - 기존의 tail은 보관하고, 새로운 tail 생성
  - 큐가 비었으면 head = tail
  - 큐가 비어있지 않으면 기존 tail의 next에 새로 만든 tail을 설정

```java
public void enqueue(Object item) {
    Node oldlast = tail; // 기존의 tail 임시 저장
    tail = new Node; // 새로운 tail 생성
    tail.item = item;
    tail.next = null;
    
    if (isEmpty()) head = tail;
    else oldlast.next = tail;
}
```

- deQueue
  - 데이터 꺼내기는 head에서 한다
  - head의 데이터를 미리 저장해둠
  - head가 가리키는 값을 현재 head의 다음 노드로 설정
  - 저장해둔 데이터를 return

```java
public Object dequeue() {
    // 비어있으면
    if (isEmpty()) {
        tail = head;
        return null;
    }
    // 비어있지 않으면
    else {
        Object item = head.item; // 빼낼 현재 front 값 저장
        head = head.next; // front를 다음 노드로 설정
        return item;
    }
}
```

삽입은 tail, 제거는 head로.. O(1)에 가능!

## 힙(Heap)

우선순위 큐(Priority Queue)를 위해 만들어진 자료구조

- 우선순위 큐
  - 데이터들이 우선순위를 가지고, 우선순위가 높은 데이터가 먼저 나감
  - Ex) 시뮬레이션 시스템, 작업 스케줄링, 수치해석 계산
  - 배열, 연결리스트, 힙으로 구현이 가능한데 <u>힙으로 구현하는 것이 가장 효율적!</u>
    - 삽입, 삭제: O(log n)

##### 특징

- 완전 이진 트리의 일종
  - 여러 값 중 max와 min을 빠르게 찾아내도록 만들어진 자료구조
- 반 정렬 상태
  - max heap 기준으로 큰 값이 상위 레벨에 있고 작은 값이 하위 레벨에 있다 정도로..
- 중복된 값 허용(이진 탐색 트리는 중복 허용 X..)
- 최대 힙(max heap, 루트 노드가 max인 이진트리), 최소 힙(min heap, 루트 노드가 min인 이진트리)

##### 구현(배열로 구현)

- 구현의 편의를 위해 index 0은 사용하지 않음
- 특정 노드의 인덱스가 i일 때
  - 왼쪽 자식은 2i
  - 오른쪽 자식은 2i+1
  - 부모 노드는 i/2
- 힙의 삽입(Max heap)
  1. 힙에 새로운 원소가 들어오면, 힙의 마지막 노드로 삽입
  2. 새로운 노드를 부모 노드들과 비교하며 교환

```java
void insert_max_heap(int x) {
    
    maxHeap[++heapSize] = x; 
    // 힙 크기를 하나 증가하고, 마지막 노드에 x를 넣음
    
    for( int i = heapSize; i > 1; i /= 2) {
        
        // 마지막 노드가 자신의 부모 노드보다 크면 swap
        if (maxHeap[i/2] < maxHeap[i])
            swap(i/2, i);
        else
            break;
    }
}
```

- 힙의 삭제(Max heap)
  1. 힙에서의 삭제는 루트 노드의 삭제를 의미
     - max heap의 경우 최대값, min heap의 경우 최소값을 삭제하는 셈
  2. 삭제된 루트 노드에 힙의 마지막 노드를 가져옴
  3. 루트 노드에 들어온 새 노드를 자식 노드들과 비교하며 교환
     - 이 때, 왼쪽 오른쪽 모든 노드와 swap이 가능할 경우 둘 중 더 큰 노드와 swap해야 함!!! 둘중 아무나 하면 힙의 의미가 깨질 수 있음.

```java
int delete_max_heap() {
    
    if (heapSize == 0) // 배열이 비어있으면 리턴
        return 0;
    
    int item = maxHeap[1]; // 루트 노드의 값을 저장
    maxHeap[1] = maxHeap[heapSize]; // 마지막 노드 값을 루트로 이동
    
    for(int i = 1; i*2 <= heapSize;) {
        
        // 새 루트 노드가 왼쪽 노드와 오른쪽 노드 이상이면 끝
        if (maxHeap[i] >= maxHeap[i*2] && maxHeap[i] >= maxHeap[i*2+1]) {
            break;
        }
        
        // 왼쪽 자식이 더 큰 경우 왼쪽 자식과 swap
        if (maxHeap[i*2] > maxHeap[i*2+1]) {
            swap(i, i*2);
            i = i*2;
        }
        
        // 오른쪽 자식이 더 큰 경우
        else {
            swap(i, i*2+1);
            i = i*2+1;
        }
    }
    
    return item;
    
}
```

## 이진 탐색 트리(Binary Search Tree)

<u>이진탐색</u>(**탐색 O(logN)**, 삽입 삭제 불가) + <u>연결리스트</u>(**삽입 삭제 O(1)**, 탐색 O(N))

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201119233027564.png" alt="image-20201119233027564" style="zoom:50%;" />

##### 특징

- 각 노드의 자식이 2개 이하
- 왼쪽 자식 < 부모 노드 < 오른쪽 자식
- 중복된 노드가 없어야 함
  - 중복을 허용하면 검색 속도가 느려짐..
  - 트리에 삽입하지 말고 노드에 count값을 가지게 하여 처리하는 것이 더 효율적
- 중위순회(inorder)로 읽으면 정렬된 순서대로 읽을 수 있음

##### 핵심 연산

- 검색

  ```java
  public boolean find(int id){
  	Node current = root;
      // O(h)
  	while (current != null){
  		//현재 노드와 찾는 값이 같으면
  		if (current.getData() == id){
  			return true;
  		}
          //찾는 값이 현재 노드보다 작으면
          else if (current.getData() > id){
  			current = current.getLeft();
  		}
          //찾는 값이 현재 노드보다 크면
          else {
  			current = current.getRight();
  		}
  	}
  	return false;
  }
  ```

- 삽입

  ```java
  public void insert(int id){
  	Node newNode = new Node(id);
  	if (root==null){
  		root = newNode;
  		return;
  	}
  	Node current = root;
  	Node parent = null;
      // O(h)
  	while (true){
  		parent = current;
  		if (id < current.getData()){				
  			current = current.getLeft();
  			if (current==null){
  				parent.setLeft(newNode);
  				return;
  			}
  		} 
          else {
  			current = current.getRight();
  			if (current==null){
  				parent.setRight(newNode);
  				return;
  			}
  		}
  	}
  }
  ```

- 삭제

  - 자식이 없는 leaf 노드일 때: 그냥 삭제
  - 자식이 1개인 노드일 때: 지워진 노드에 자식을 올린다
  - 자식이 2개인 노드일 때: 오른쪽 자식노드들 중 가장 작은 값 or 왼쪽 자식노드들 중 가장 큰 값을 올린다

  ```java
  public boolean delete(int id){
  	Node parent = root;
  	Node current = root;
  	boolean isLeftChild = false;
      // 지울 노드의 위치로 가는 과정 O(h)
  	while (current.getData()!= id){
  		parent = current;
  		if (current.getData() > id){
  			isLeftChild = true;
  			current = current.getLeft();
  		}
          else {
  			isLeftChild = false;
  			current = current.getRight();
  		}
  		if (current == null){
  			return false;
  		}
  	}
  	//Case 1: 자식노드가 없는 경우
  	if (current.getLeft()==null && current.getRight()==null){
  		if (current==root){
  			root = null;
  		}
  		if (isLeftChild==true){
  			parent.setLeft(null);
  		}
          else{
  			parent.setRight(null);
  		}
  	}
  	//Case 2: 하나의 자식을 갖는 경우
  
  	else if (current.getRight()==null){
  		if (current==root){
  			root = current.getLeft();
  		}
          else if (isLeftChild){
  			parent.setLeft(current.getLeft());
  		}
          else{
  			parent.setRight(current.getLeft());
  		}
  	}
      else if (current.getLeft()==null){
  		if (current==root){
  			root = current.getRight();
  		}
          else if (isLeftChild){
  			parent.setLeft(current.getRight());
  		}
          else{
  			parent.setRight(current.getRight());
  		}
  	}
  	//Case 3: 두개의 자식을 갖는 경우
  	else if (current.getLeft()!=null && current.getRight()!=null){
  		// 오른쪽 서브트리의 값중 가장 작은 값을 택하는 경우로 구현
  		Node successor = getSuccessor(current);
  		if (current==root){
  			root = successor;
  		}
          else if (isLeftChild){
  			parent.setLeft(successor);
  		}
          else{
  			parent.setRight(successor);
  		}			
  		successor.setLeft(current.getLeft());
  	}		
  	return true;		
  }
  
  public Node getSuccessor(Node deleleNode){
  	Node successsor = null;
  	Node successsorParent = null;
  	Node current = deleleNode.getRight();
  	while (current!=null){
  		successsorParent = successsor;
  		successsor = current;
  		current = current.getLeft();
  	}
      // succeessor에 오른쪽 서브트리 중 가장 작은 노드가 들어옴
      
      // 이 노드가 지울 노드와 직접 연결되어 있다면 바로 리턴하여 붙이면 되고,
      
      // 이 노드가 지울 노드와 직접 연결되어 있지 않다면
  	if (successsor!=deleleNode.getRight()){
          // 이 노드가 있어야 할 자리(sP의 왼쪽 자식)를 이 노드의 오른쪽 자식(왼쪽 자식은 없을것임)으로 채우고,
  		successsorParent.setLeft(successsor.getRight());
          // 이 노드의 오른쪽 자식을 오른쪽 서브트리로 채운다.
  		successsor.setRight(deleleNode.getRight());
  	}
  	return successsor;
  }
  ```

- 트리 생성

- 트리 삭제

##### 시간복잡도

- 균등 트리: O(logN)
- 편향 트리: O(N)
  - 이렇게 한쪽만 뻗어있는 편향 트리는 시간복잡도가 O(N)이 나오므로 트리를 사용할 이유가 사라짐..
  - 이를 바로잡도록 개선된 트리가 AVL Tree, RedBlack Tree (self-balanced tree)

즉, 시간복잡도는 트리의 depth에 비례

## 해시(Hash)

- 데이터의 효율적 관리를 위해, <u>임의의 길이 데이터</u>를 <u>고정된 길이의 데이터</u>로 매핑
- 해시 함수를 구현하여 데이터 값을 해시값으로 매핑
  - 그런데 데이터가 많아지면 서로 다른 데이터가 같은 해시값으로 충돌나는 현상이 발생하게 됨(collision)

##### 해시 테이블을 쓰는 이유

- 적은 자원으로 많은 데이터를 효율적으로 관리하기 위해!
- 언제나 동일한 해시값을 return하므로 index를 알면 빠른 데이터 검색 가능
- 시간복잡도 O(1)
  - 이진탐색트리는 O(logN)

##### 충돌 문제 해결

- 체이닝

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120025756163.png" alt="image-20201120025756163" style="zoom: 67%;" /> 

  - linked list로 노드를 계속 추가해 나가는 방식
  - 장점: 제한 없이 계속 연결 가능
  - 단점: 메모리 문제

- Open addressing

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120025847694.png" alt="image-20201120025847694" style="zoom:67%;" /> 

  - 해시함수로 얻은 주소가 아닌 다른 주소에 데이터를 저장할 수 있도록 허용
    - 해당 키 값에 이미 저장이 되어있으면 다음 주소로 가도록
    - 장점: 메모리 문제가 발생하지 않음
    - 단점: 해시 충돌이 발생할 수 있음

- 선형 탐사

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120030500135.png" alt="image-20201120030500135" style="zoom:67%;" /> 

  - 정해진 고정 폭으로 옮겨 해시값의 중복을 피함
  - 단점: 이동폭이 고정되어 있어 특정 해시값 주변 버킷이 모두 채워져 있는 primary clustering 문제에 취약

- 제곱 탐사

- ![image-20201120030445188](C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120030445188.png) 

  - 정해진 고정 폭을 제곱수로 옮겨 해시값의 중복을 피함
  - 처음에 1칸, 또 충돌이면 (원래 위치로부터) 4칸, 또 충돌이면 (원래 위치로부터) 9칸
  - 단점: 여러개의 서로 다른 키들이 동일한 초기 해시값을 갖는 secondary clustering에 취약
    - ![image-20201120031050302](C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120031050302.png) 
    - 위와 같이 13으로 나눈 나머지를 저장할 때, 15, 28, 41, 54, 67이 모두 같은 해시값을 가질 때 멀리씩 점프해도 연산수가 줄어들지 않는 현상
    - 선형 탐사에서도 같은 현상이 발생하겠지만, 제곱 탐사는 식이 더 복잡한데도 문제가 해결이 안된다는 의미에서 단점이라고 한듯

## 트라이(Trie)

**문자열**에서 검색을 빠르게 도와주는 자료구조

- 정수 데이터들에서 BST를 이용하면 O(logN)
- 하지만 문자열 데이터들에서 BST를 이용하면 문자열 최대 길이가 M일 때 O(MlogN)..
- 트라이를 사용하면 **O(M)**

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120031534465.png" alt="image-20201120031534465" style="zoom:67%;" />

```java
static class Trie { // ???
    boolean end;
    boolean pass;
    Trie[] child;

    Trie() {
        end = false;
        pass = false;
        child = new Trie[10];
    }

    public boolean insert(String str, int idx) {

        //끝나는 단어 있으면 false 종료
        if (end) return false;

        //idx가 str만큼 왔을때
        if (idx == str.length()) {
            end = true;
            if (pass) return false; // 더 지나가는 단어 있으면 false 종료
            else return true;
        }
        //아직 안왔을 때
        else {
            int next = str.charAt(idx) - '0';
            if (child[next] == null) {
                child[next] = new Trie();
                pass = true;
            }
            return child[next].insert(str, idx+1);
        }

    }
}
```

## B Tree & B+ Tree

<span style="color:red">대충 훑어서 이해 잘 안됨. 나중에 필요할 것 같으면 더 자세히 보자</span>

- 이진트리는 하나의 부모가 두개의 자식밖에 가지지 못하며, 균형이 맞지 않으면 검색 효율이 선형검색 급으로 떨어짐
- 하지만 이진트리 구조의 간결함과 균형이 맞다면 검색, 삽입, 삭제 모두 O(logN)의 성능을 보이는 장점이 있으므로 이를 활용하는 것이 중요!

#### B Tree

이진트리를 확장해서, **더 많은 수의 자식을 가질 수 있게 일반화**시킨 트리 자료구조의 일종

- 자식 수의 일반화
  - 하나의 노드 아래에 더 저장될 수 있을 뿐만 아니라
  - 트리의 균형을 자동으로 맞춰줌
  - 즉, 단순하고 효율적이며 균형을 맞추고 있는 트리!

- 데이터베이스, 파일 시스템에서 널리 사용됨
  - 대량의 데이터를 처리해야 할 때, 검색 구조의 경우 하나의 노드에 많은 데이터를 가질 수 있다는 점은 상당히 큰 장점이다.
    - 대량의 데이터는 메모리보다 블럭 단위로 입출력하는 하드디스크 or SSD에 저장해야하기 때문!
    - ex) 한 블럭이 1024 바이트면, 2바이트를 읽으나 1024바이트를 읽으나 똑같은 입출력 비용 발생. 따라서 하나의 노드를 모두 1024바이트로 꽉 채워서 조절할 수 있으면 입출력에 있어서 효율적인 구성을 갖출 수 있다.
  - B-Tree는 이러한 장점을 토대로 많은 데이터베이스 시스템의 인덱스 저장 방법으로 애용하고 있음

##### 규칙

- 노드의 자료 수가 N개면 자식 수는 N+1 이어야 함
- 각 노드의 자료는 정렬된 상태여야 함
- 루트 노드는 적어도 2개 이상의 자식을 가져야 함
- 루트 노드를 제외한 모든 노드는 적어도 M/2개의 자료를 가지고 있어야 함
- 외부 노드로 가는 경로의 길이는 모두 같음
- 입력 자료 중복 X

#### B+ Tree

기존의 B-Tree와 데이터의 linked list로 구현된 색인 구조

- 데이터의 빠른 접근을 위한 index 역할만 하는 non-leaf 노드가 추가로 있음
- B-Tree의 변형 구조(index + leaf)
  - 인덱스 부분의 key값은 leaf에 있는 key값을 직접 찾아가는데 사용

##### 장점

- 블럭 사이즈를 더 많이 이용할 수 있음(key값에 대한 하드디스크 액세스 주소가 없으므로)
- leaf 노드끼리 linked list로 연결되어 있어 범위 탐색에 유리

##### 단점

- B-Tree의 경우 최선의 경우 루트에서 끝날 수 있는데, B+ Tree는 무조건 leaf까지 내려가봐야 함

#### 비교

- B-Tree는 각 노드에 데이터가 저장되지만, B+Tree는 index노드와 leaf노드로 분리되어 저장됨
  - leaf 노드는 서로 연결되어 있어서 임의접근/순차접근 모두 우수한 성능
- B-Tree는 각 노드에서 key, data 모두 들어갈 수 있고, data는 disk block으로 포인터가 될 수 있음.. 그러나 B+Tree는 각 노드에서 key만 들어가므로 data는 모두 leaf만 존재
- B+Tree는 add와 delete 모두 leaf에서만 이루어짐