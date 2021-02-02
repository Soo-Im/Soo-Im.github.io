---
layout: post
title: 부스트코스 5주차 강의
subtitle: Memory
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Boostcourse]
comments: true
---

# 메모리 주소
## 16진법
1, 2, 3 ... 9, A, B, ...F(15)와 같이 센다. 이진법으로 11111111 (8자리, 256)는 16진법의 FF와 같다. 이러한 표기는 RGB에서도 볼 수 있다. 
그리고 혼선을 방지하기 위해 맨 앞에 0x를 붙인다.

## 포인터
<code>&</code>는 변수가 저장된 메모리의 주소, 즉 포인터를 보여준다. printf 구문에서는 <code>%p</code>로 출력할 수 있다. 
반대로 <code>*</code>은 해당 주소에 저장된 값을 보여준다.  
포인터는 아래와 같이 가리키는 변수의 자료형과 &#8727; 표기를 이용해 정의한다. (참고로 포인터는 long과 같은 8바이트이다.)
<pre>
<code>
int n = 50;
int *p = &n;

print("%p\n",p);    // 16진수 포인터를 출력한다.
print("%i\n",*p);   // 포인터에 저장된 변수(50)를 출력한다.
</code>
</pre>
