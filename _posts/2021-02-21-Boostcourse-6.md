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