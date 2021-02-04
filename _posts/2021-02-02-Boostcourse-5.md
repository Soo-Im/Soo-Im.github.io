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
그리고 혼선을 방지하기 위해 맨 앞에 0x를 붙인다. (예: 0x12345678)

## 포인터
<code>&</code>는 변수가 저장된 메모리의 주소, 즉 포인터를 보여준다. printf 구문에서는 <code>%p</code>로 출력할 수 있다. 
반대로 <code>*</code>은 해당 주소에 저장된 값을 보여준다.  
포인터는 아래와 같이 가리키는 변수의 자료형과 &#8727; 표기를 이용해 정의한다. (참고로 포인터는 long과 같은 8바이트이다.)
<pre><code>
int n = 50;
int *p = &n;

print("%p\n",p);    // 16진수 포인터를 출력한다.
print("%i\n",*p);   // 포인터에 저장된 변수(50)를 출력한다.
</code></pre>

## 문자열 = 포인터
지금까지 <code>cs50.h</code>라이브러리를 이용해서 사용한 string은 사실 포인터이다.  
예를 들어 <code>string s = "HI";</code>라고 정의한다면 s에 저장된 값은 "H"의 포인터이다. 
즉 다음과 같이 표현할 수 있다.
<pre><code>
string s = "HI";
char *s = "HI";
</code></pre>
그래서 string을 <code>s == t</code>와 같이 직접 비교할 수 없는 것이다. <code>s</code>와 <code>t</code>에는 각각의 주소가 들어있기 때문이다.

string을 직접 정의하면 아래와 같다.
<pre><code>typedef char *string;</code></pre> 
<code>char *</code>은 이 값의 형태가 문자의 주소가 된다는 의미이다.
