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


# 문자열 = 포인터
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


# 메모리 할당
## 메모리 할당을 통한 문자열 복사
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
<code>stdlib.h</code>의 <code>malloc</code>(memory allocation)은 할당한 메모리의 주소를 전달한다.
 
 
<pre><code>
char *s = "hi";
char *t = malloc(strlen(s)+1);  // +1은 null 종단문자 (\0)을 위한 공간이다. 메모리의 주소는 t에 저장된다.

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


## 메모리의 해제
메모리 할당을 반복하다보면 메모리 부족 문제를 겪을 수 있다. 이는 <code>$ valgrind code.c</code> 라는 리눅스 커맨드를 통해 확인할 수 있다.
'memory leaks' 라는 출력이 나오면 메모리 손실이 발생했다는 의미이다. 이는 <code>free</code>를 이용해 메모리를 해제함으로써 해결할 수 있다.  
위의 코드에서 <code>free(t);</code>를 입력하면 t 주소에 할당된 메모리가 해제된다.

## 메모리 할당 구역과 함수의 사용
프로그램을 실행하면 아래 그림과 같이 메모리가 할당된다.  
  <src="https://user-images.githubusercontent.com/40853572/107961217-ef21d600-6fe8-11eb-8ccb-4d93e9d21225.png">  
  machine code는 문자 그대로 프로그램 머신코드 자체, globals는 전역 변수가 저장되는 곳이고
heap은 <code>malloc</code>을 이용해 할당한 변수, stack은 main 혹은 함수의 지역 변수가 저장되는 곳이다.
main을 포함한 함수를 사용하면 stack 공간에 함수별로 각 변수가 저장된다. 즉, 함수 내의 변수는 섞이지 않는다. 
(사이트 이름이기도 한 stack overflow는 잘못된 재귀함수 호출로 인해 stack이 넘친다는 뜻이다.)
  따라서 main 안의 변수를 함수의 인자로 전달하면 main의 지역 변수가 실제로 들어가는 것이 아니라 지역 변수의 복사된 값이 들어가게 되면서 main의 변수는 변하지 않는다.


<pre><code>
int main(void){
    int x = 1;
    print("%i", x);
    func(x);
    print("%i", x);     // 우리는 func를 통해 변화한 x가 나오기를 기대하지만 main 안의 x는 변하지 않는다.
}

void func(int a){
    a++;                // 그 이유는 x가 func 안에 직접 들어간 것이 아니라 x의 값이 복사된 a가 변했기 때문이다.
}
</code></pre>


위 문제는 포인터를 전달하는 것으로 해결할 수 있다. 즉 x 자체를 함수에 전달하는 것이 아니라 x의 주소를 전달하는 것이다.  


<pre><code>
int main(void){
    int x = 1;
    print("%i", x);
    func(&x);           // x가 아닌 x의 주소를 전달한다.
    print("%i", x);
}

void func(int *a){
    int tmp = *x;       // tmp에 x가 가리키는 값(*x)를 저장한다.
    ...
}

</code></pre>


동일한 이유로 <code>scanf("%i",&x);</code>와 같은 함수를 사용할 때에는 변수 자체가 아닌 변수의 주소를 전달해 주어야 한다.
만약 <code>char *s</code>와 같은 포인터 변수라면 그냥 <code>scanf("%s",s)</code>와 같이 변수(=주소) 그 자체를 넘기면 된다.  

