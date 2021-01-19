---
layout: post
title: 부스트코스 3주차 강의
subtitle: Array
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Boostcourse]
comments: true
---

## Compiling 4단계
### 1. Preprocessing (전처리)
소스 코드 맨 위의 #include <...>에 해당하는 헤더 파일의 함수를 불러온다.
### 2. Compiling
소스 코드가 CPU가 이해할 수 있는 어셈블리 코드로 전환된다. 
### 3. Assembling
어셈블리 코드가 머신 코드로 전환된다.
### 4. Linking
모든 소스 코드를 (예: stdio.h, cs50.h, ...) 한꺼번에 처리하여 하나의 a.out 파일로 만든다.

## Array and else
### 1. Array
같은 자료형을 가진 값의 리스트를 의미한다.  
<pre>
<code>
int scores[3];
scores[0] = 55;
...
</code>
</pre>
주의해야 할 점은 첫째, **변수를 이용해 배열의 길이를 설정할 수 없으며** 둘째, **C의 배열은 길이를 기억하지 않는다**. 따라서 아래의 코드는 syntax error가 발생한다.
<pre>
<code>
numbers = 3;
int scores[numbers]; // 에러 발생!
</code>
</pre>
### 2. 일종의(?) 튜플
C에서 상수는(파이썬의 tuple과 같은 것) 아래와 같이 정의한다.
이는 global variable (전역 변수)라고 부른다.  
참고: type casting이란 자료형을 바꾸는 것을 말한다

<pre>
<code>
const int N = 3; // 대문자

int main(void) // main 상단에 정의
{
...
</code>
</pre>
