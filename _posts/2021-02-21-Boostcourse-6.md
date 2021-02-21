---
layout: post
title: 부스트코스 6주차 강의
subtitle: Data Structure
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Boostcourse]
comments: true
---

# 메모리 주소
## realloc
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
## linked list
배열은 인덱싱을 통해 값에 빠르게 접근할 수 있다는 장점이 있지만, 크기를 바꾸려면 <code>realloc</code> 등의 함수를 이용해 O(n)의 작업을 해야 한다는 단점이 있다.
연결 리스트란 배열처럼 연속된 메모리를 사용하는 대신 임의의 위치에 값을 저장한 후 다음 값이 위치한 메모리를 가리키는 포인터를 함께 저장하는 것이다.

<img src="https://user-images.githubusercontent.com/40853572/108630149-baa99080-74a6-11eb-9738-4e76248af900.png" width="300">

연결 리스트는 다음과 같은 구조체, 즉 <code>struct</code>로 정의할 수 있다.

<pre><code>
// node는 number와 pointer을 가지는 구조체이다. 이전과 다르게 struct 뒤에 node를 또 쓰는 이유는 typedef 안에서 'node'라는 문자를 사용하기 위함이다.

typedef struct node         
{
    int number;             // 저장하는 값 number
    struct node *next       // 다음 node를 가리키기 위한 포인터 *next
}
node;
</code></pre>