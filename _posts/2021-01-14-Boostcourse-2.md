---
layout: post
title: 부스트코스 2주차 강의
subtitle: Computational thinking
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Boostcourse]
comments: true
---

## C
### C 기초 
1. printf의 'f'는 'formated'. 즉 형식화된 문자를 출력함을 의미한다.
2. &#35;includ <stuio.h>는 stdio.h 파일을 불러옴을 의미한다. import와 같은 개념인 듯?
3. source code &#8594; **compiler** &#8594; machine code (binary code*: *은 기계가 실행 가능한 코드라는 의미)

### 외부 프로그램과 make

두 커맨드는 동일하게 작동한다.

    $ clang program.c -lcs50
    $ make program


첫번째는 clang 컴파일러를 이용할 때 cs50이라는 외부 프로그램을 link(-l)한다는 의미이고, make는 위 과정을 자동으로 진행한다.  
주의할 점은 make를 사용할 때 확장자를 붙여서 쓰면 안된다.

### loop
1. syntactic sugar란 아래와 같이 syntax를 간결하게 표현하는 것을 말한다.

<pre>
<code>
var = var + 1;    
var += 1;
var++;
</code>
</pre>
  
2. while과 for은 다음과 같은 차이가 있다.  

<pre>
<code>
while(True){}    
for(int i=0; i<50; i++){}
</code>
</pre>    
  
while은 조건문 하나를 받지만, for은 루프를 위해 세 개의 인자를 받는다.  
   
