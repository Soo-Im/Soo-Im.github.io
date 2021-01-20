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

## Array and String
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

### 2. String
#### 1) string = array of char
string은 char의 array이다. 즉 s[0], s[1]
...와 같이 사용할 수 있다. 그러나 이는 **stdio.h에 포함된 자료형이 아니라는 데 주의해야 한다.**  
cs50.h나 string.h 헤더파일 없이 선언하려면 아래와 같이 작성해야 한다.
<pre>
<code>
char str[] = "Hello";
printf("%s",str); // 이상하게도 %s는 작동한다.
</code>
</pre>

#### 2) string의 크기
string의 크기는 문자열의 크기에 비례한다. 문자열의 끝, 즉 길이를 결정하는 것이 null character (\0)이다. 따라서 실제 문자열의 크기보다 1바이트 더 크다.

#### 3) string indexing
string 내 문자는 2차원 배열로 표현할 수 있다.
<pre>
<code>
#include <cs50.h>
...

string names[4];
names[0] = "Soo";
...

// 아래 코드는 동일한 기능을 한다.
printf("%s", names[0]);
printf("%c%c%c", names[0][0], names[0][1], names[0][2]);
</code>
</pre>

### 3. 기타
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
