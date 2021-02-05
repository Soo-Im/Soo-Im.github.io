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

string을 직접 정의하면 아래와 같다. <code>char *</code>은 이 값의 형태가 문자의 주소가 된다는 의미이다.
<pre><code>typedef char *string;</code></pre> 

이제 string 혹은 char &#8727; 변수의 여러 특성을 출력해보자.
<pre><code>
char *s = "hi";

printf("%s\n",s);   // hi
printf("%p\n",s);   // 0x42... (hi의 주소)
printf("%p\n",&s);  // 0x7f... (s 자체의 주소)
printf("%c\n",*s);  // h (s는 기본적으로 문자열의 첫 번째 주소를 저장한다. 따라서 *s를 출력하면 h만 나온다.)
</code></pre>

### 문자열의 복사
string은 포인터이기 때문에 <code>t = s;</code>와 같은 방식으로는 내부에 들어있는 값을 복사할 수 없다.
<pre><code>
string s = "hello";
string t = s;

t[0] = toupper(t[0]);   // 우리는 t가 Hello, s가 hello이기를 기대하지만

print("%s",t);
print("%s",s);      
// t와 s 모두 Hello를 출력한다. t는 포인터를 복사했을 뿐 문자열 자체를 복사한 게 아니기 때문에 포인터가 가리키는 문자열이 바뀌어 t와 s 모두 Hello를 출력한다.
</code></pre>

그렇다면 문자열은 어떻게 복사할 수 있을까? 미리 빈 메모리를 할당한 다음에 기존 메모리 안의 값을 하나하나 복사하면 된다. 
메모리를 할당하는 함수는 <code>stdlib.h</code> 안의 <code>strcpy</code>이다.
<pre><code>
char *s = "hi";
char *t = malloc(strlen(s)+1);          // +1은 null 종단문자 (\0)을 위한 공간이다.

// strcpy는 아래와 같은 루프로 표현할 수 있다. 
    // for (int i=0, n=strlen(s)+1; i<n; i++) 
    // {
    //     t[i] = s[i];
    // }

strcpy(t, s);

t[0] = toupper(t[0]);

printf("%s\n",s);   // hi
printf("%s\n",t);   // Hi
</code></pre>