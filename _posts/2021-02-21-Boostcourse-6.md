---
layout: post
title: 부스트코스 6주차 강의
subtitle: Data Structure
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Boostcourse]
comments: true
---

# 메모리 할당
## 1. realloc
기존에 할당된 배열의 크기를 바꾸기 위한 함수. 기존의 배열 크기를 수정하는 단계 중에서 ((1) 원하는 크기의 임시 메모리(tmp) 할당, (2) tmp에 기존 메모리(list)의 값을 복사,
(3) tmp에 새로운 값 추가 혹은 수정, (4) list 해제, (5) 새로운 list 정의하여 tmp 포인터 복사) (1)~(4)까지의 단계를 한 번에 수행해준다.

<pre><code>
int *list = malloc(3 * sizeof(int));        // list 포인터에 3개의 정수형 메모리 할당  
list[0] = 1;
...

int *tmp = realloc(list, 4 * sizeof(int));  // tmp 포인터에 4개의 정수 메모리를 할당하고 list가 가리키는 값 복사, 그 후 기존의 list는 free (해제)

list = tmp;     // 위에서 해제된 list 대신 새롭게 list를 만들어 tmp와 같은 위치 가리키게 만들기
list[2] = 4;    // 새로운 list 값 저장
</code></pre>

# Data Structure
## 1. linked list
배열은 인덱싱을 통해 값에 빠르게 접근할 수 있다는 장점이 있지만, 크기를 바꾸려면 <code>realloc</code> 등의 함수를 이용해 O(n)의 작업을 해야 한다는 단점이 있다.
연결 리스트란 배열처럼 연속된 메모리를 사용하는 대신 임의의 위치에 값을 저장한 후 다음 값이 위치한 메모리를 가리키는 포인터를 함께 저장하는 것이다.

<img src="https://user-images.githubusercontent.com/40853572/108630149-baa99080-74a6-11eb-9738-4e76248af900.png" width="400">

### 1.1 linked list 코딩
연결 리스트를 만들기 위해서 <code>node</code>라는 구조체를 정의한다.

<pre><code>
// node는 number와 pointer을 가지는 구조체이다. 이전과 다르게 struct 뒤에 node를 또 쓰는 이유는 typedef 안에서 'node'라는 문자를 사용하기 위함이다.

typedef struct node         
{
    int number;             // 저장하는 값 number
    struct node *next       // 다음 node를 가리키기 위한 포인터 *next
}
node;
</code></pre>

위에서 정의한 <code>node</code>를 이용하여 아래와 같이 연결 리스트를 만들 수 있다.

<img src="https://user-images.githubusercontent.com/40853572/108732073-8f8b7380-7570-11eb-895a-ae2336c6229e.png" width="400">

<pre><code>
node *list = NULL;                  // 우리가 만드려는 리스트를 초기화한다.

node *n = malloc(sizeof(node));     // node를 가리키는 메모리 주소를 저장하는 n을 만든다.
if (n == NULL){ return 1;}          // 정상적으로 할당되었는지 확인

if (n != NULL)
{
    n->number = 1;      // (*n).number = 2; 과 같은 의미이다. n.number 혹은 n.next가 아닌 이유는 n 자체는 포인터이기 때문이다.
    n->next = NULL;     // 다음 node를 정의하지 않았으므로 NULL로 초기화한다.
}

list = n;               // 위에서 정의한 list가 구조체 n을 가리키게 만들면 연결이 완료된다.

// 새로운 node를 만든다.
node *n = malloc(sizeof(node));
if (n == NULL){ return 1;} 

if (n != NULL)
{
    n->number = 2;      
    n->next = NULL;     
}

list->next = n;         // list의 다음 순서에 연결한다.
...
list->next->next = n;   // 그 이후는 아래와 같은 방식으로 연결한다.


// list를 출력한다. 마지막 node의 next가 NULL에 도달하면 루프를 종료한다.
for (node *tmp = list; tmp!=NULL; tmp=tmp->next)
{
    printf("%i",tmp->number);
}

// 메모리를 해제한다.
while (list != NULL)
{
    node *tmp = list->next;
    free(list);
    list = tmp;
}
</code></pre>

### 1.2 linked list의 장단점
장점
>1. 배열의 크기를 미리 정의하거나 새로운 변수를 삽입할 때 realloc 등의 과정을 거치지 않으므로 동적인 작업이 가능하다.

단점
>1. 모든 포인터를 따라가야하므로 list[0]과 같이 random access를 할 수 없다. 따라서 이진탐색이 불가능하다.
>2. 새로운 변수를 순서에 맞게 삽입할 때에도 모든 포인터를 따라가면서 대소 비교를 해야하므로 탐색과 삽입 모두 O(n)이다.

# 이진 탐색 트리 Binary Search Tree
포인터를 이용한 linked list의 장점과 이진 탐색이 가능한 array의 장점을 합친 것이 이진 탐색 트리이다.  
array에서 수행한 이진 탐색을 순서에 따라 높이를 다르게 주고, 순서에 맞는 포인터를 부여하면 아래 그림과 같다.

<img width="400" src="https://user-images.githubusercontent.com/40853572/108731666-1f7ced80-7570-11eb-87f2-65855c73a9da.png">

최대 두 개의 포인터를 가지고, 왼쪽의 포인터가 가리키는 값보다 오른쪽의 포인터가 가리키는 값이 항상 더 작은 구조체가 모여있다.
이를 이진 탐색 트리라고 부른다. 이진 탐색 트리는 동적으로 추가가 가능할 뿐 아니라 이진 탐색도 가능하다. 즉 O(log n)이다.  
이진 탐색 트리의 구조체, <code>node</code>는 아래와 같이 정의한다.

<pre><code>
typedef struct node
{
    int number;

    struct node *left;      // 두 개의 하위 구조체를 가리킨다.
    struct node *right;
} node;
</code></pre>

트리는 그 자체가 재귀적인 구조로, 각 node는 두 개의 하위 node를 거느리고 있다. 맨 위에 오는 node를 root node라고 부른다.
이진 탐색 트리에서 수행하는 이진 탐색의 과정은 다음과 같다.

<pre><code>
bool search(node *tree)
{
    // 트리가 비어있는 경우 ‘false’를 반환하고 함수 종료
    if (tree == NULL)
    {
        return false;
    }

    // 현재 노드의 값이 50보다 크면 왼쪽 노드 검색
    else if (50 < tree->number)
    {
        return search(tree->left);
    }
    // 현재 노드의 값이 50보다 작으면 오른쪽 노드 검색
    else if (50 > tree->number)
    {
        return search(tree->right);
    }
    // 위 모든 조건이 만족하지 않으면 노드의 값이 50이므로 ‘true’ 반환
    else {
        return true;
    }
}
</code></pre>

# 해시 테이블 Hash Table
실행 시간을 줄이기 위해 고안된 개념으로, 연결 리스트의 배열이라고 볼 수 있다.  
예를 들어 Ron, Harry, Hermione, Hagrid, Ginny... 등의 이름을 저장할 때 이들을 모두 하나의 배열이나 연결 리스트에 넣는 것이 아니라
첫 글자가 A, B, C...인 값을 저장하는 배열을 만들어서 그에 해당하는 이름들을 연결 리스트로 연결하는 것이다.  
이 경우에는 R: Ron, G: Ginny, H: Harry, Hermione, Hagrid가 들어가며 Harry~Hagrid는 연결 리스트로 연결 되어있다.

<img width="400" src="https://user-images.githubusercontent.com/40853572/108841675-7e4b7100-761b-11eb-9488-29867c07c725.png">

이렇게 하면 각각의 첫 글자에 해당하는 배열로 바로 진입할 수 있어 탐색에 걸리는 시간은 O(1)이지만, H처럼 여러 값이 리스트로 연결되어 있으면 결국 실행 시간은 O(n)이 된다.  
첫 두 글자를 기준으로 배열을 만들면(Ha, Hb, Hc, ...) 하나의 배열에 들어가는 변수의 개수는 줄어들지만 메모리가 많이 소모된다.
또한 매우 극단적인 상황에서는(예: 모든 이름의 첫 글자가 같은 경우) 결국 O(n)이 되기 때문에 메모리와 실행 시간을 적절히 고려해주어야 한다.
이러한 규칙을 정하는 함수를 **해시 함수**라고 부른다.

# 트라이 Tries
각 노드가 배열로 이루어진 트리 구조이다. 하나의 철자를 저장할 때마다 A~Z의 배열을 만들어 저장하는 방식이다.  
Harry의 경우 H&#8594;a&#8594;r&#8594;r&#8594;y 순으로 내려가면서 각 노드마다 A~Z의 배열을 만든 후 저장한다. 그림으로 나타내면 다음과 같다.  

<img width="400" src="https://user-images.githubusercontent.com/40853572/108843010-768ccc00-761d-11eb-9a1b-d3d49d4d2b71.png">

이렇게 저장하면 모든 이름은 자신만의 트리를 가지기 때문에 탐색에 드는 시간은 O(1)이다.
대신 메모리의 소모가 매우 큰 방식이다.

# 기타 자료구조
## 큐 Queues
선입선출 FIFO에서 사용하는 구조(예: 줄 서기). <code>enqueue</code>는 입력, <code>dequeue</code>는 큐에서 나오는 것을 의미한다.

## 스택 Stack
후입선출 LIFO에서 사용하는 구조(예: 메일함). <code>push</code>는 입력, <code>pop</code>은 스택에서 나오는 것을 의미한다.

## 딕셔너리 Dictionaries
key-value 쌍으로 이루어진 구조. 