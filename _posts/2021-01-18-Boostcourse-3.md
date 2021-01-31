---
layout: post
title: 부스트코스 3주차 강의
subtitle: Array
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Boostcourse]
comments: true
---

# Compiling 4단계
## 1. Preprocessing (전처리)
소스 코드 맨 위의 <code>#include <...> </code>에 해당하는 헤더 파일의 함수를 불러온다.
## 2. Compiling
소스 코드가 CPU가 이해할 수 있는 어셈블리 코드로 전환된다. 
## 3. Assembling
어셈블리 코드가 머신 코드로 전환된다.
## 4. Linking
모든 소스 코드를 (예: stdio.h, cs50.h, ...) 한꺼번에 처리하여 하나의 a.out 파일로 만든다.

# Array and String
## 1. Array
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

## 2. String
### 1) string = array of char
string은 char의 array이다. 즉 s[0], s[1]
...와 같이 사용할 수 있다. 그러나 이는 **stdio.h에 포함된 자료형이 아니라는 데 주의해야 한다.**  
cs50.h나 string.h 헤더파일 없이 선언하려면 아래와 같이 작성해야 한다.
<pre>
<code>
char str[] = "Hello";
printf("%s",str); // 이상하게도 %s는 작동한다.
</code>
</pre>

### 2) string의 크기
string의 크기는 문자열의 크기에 비례한다. 문자열의 끝, 즉 길이를 결정하는 것이 null character '\0'이다. 따라서 실제 문자열의 크기보다 1바이트 더 크다.

### 3) string indexing
string 내 문자는 2차원 배열로 표현할 수 있다.
<pre>
<code>
string names[4];
names[0] = "Soo";
...

// 아래 코드는 동일한 기능을 한다.
printf("%s", names[0]);
printf("%c%c%c", names[0][0], names[0][1], names[0][2]);
</code>
</pre>


## 3. 기타
### 1) Constant 상수 정의
C에서 상수는(파이썬의 tuple과 같은 것) 아래와 같이 정의한다.
이는 global variable (전역 변수)라고 부른다.  
참고: type casting이란 자료형을 바꾸는 것을 말한다

<pre>
<code>
const int N = 3; // 대문자

int main(void) // main 상단에 정의
{ ... }
</code>
</pre>

### 2) for 문 활용
아래의 코드는 동일한 기능을 한다.

<pre>
<code>
string s = "HI"

for (int i = 0; i < strlen(s); i++) {}
for (int i=0, n=strlen(s); i < n; i++) {} // 초기화를 통해 불필요한 함수 호출 횟수를 줄였다. 참고로 i와 n 모두 같은 자료형이기 때문에 굳이 n 앞에 int를 붙일 필요가 없다.
</code>
</pre>

### 3) 명령행 인자
<pre>
<code>
int main(int argc, string argv[])
{
    // argc (argument count): 입력된 변수의 개수
    // argv (argument vector): 입력된 변수가 저장되는 vector
    
    if (argc == 2)     // 프로그램을 실행할 때 INPUT argument가 하나 들어왔는지 확인한다.
    ...                // argc가 1이 아닌 2인 이유는 ./program INPUT 에서 "./program"이 첫 번째 argument이기 때문이다.
}
</code>
</pre>

### 4) return 0;
일반적으로 return 0는 프로그램에 문제가 없음을 의미한다. Python에서 code exit with 0인 것과 같은 의미.  
main 함수에서 에러가 발생했음을 알리려면 retrun 1;을 하면 된다.

### 5) pointer
int *ip는 integer 자료형 변수의 주소를 저장하는 ip를 정의한다는 뜻이다. 굳이 변수명이 아닌 포인터를 사용하는 이유는 함수에 변수를 넣는 등의 행위를 할 때마다 메모리가 소모되기 때문이다.
<pre>
<code>
int num = 1;
int *ip = &num;          // &변수 = 변수의 메모리 주소. 실행할 때마다 주소는 달라진다.

printf("Address of the variable: %p", ip);
printf("Address of the variable: %p", &num); // 두 출력의 결과는 같다. ex) 0x7ffff6cdffa8

printf("Variable in address: %i", *ip);      // 해당 주소의 변수를 출력한다. ex) 1 
</code>
</pre>

또한 pointer는 array 내에서 메모리를 옮겨다닐 때 매우 유용하다. 서로 다른 변수는 메모리에 랜덤으로 배치가 되지만, array 안의 변수는 메모리에 순서대로 들어가기 때문에 pointer을 바꿈으로써 다른 변수에 접속할 수 있기 때문이다.
<pre>
<code>
int x = 1;
int y = 2;
int *xip = &x;

xip++;              // 주소에서 1만큼 이동
printf("Variable in xip++: %i", *xip);      // y를 출력하지 않고 NaN을 출력한다.

int nums[] = {1, 2, 3, 4};
int *numip = &nums[0];

printf("Variable in xip: %i", *numip);         // 1 을 출력한다.
numip++;
printf("Variable in xip++: %i", *numip);      // 2를 출력한다.
</code>
</pre>
