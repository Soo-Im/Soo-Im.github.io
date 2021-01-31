---
layout: post
title: 부스트코스 4주차 강의
subtitle: Algorithm
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Boostcourse]
comments: true
---

# 알고리즘 효율 표기법
## 1. Big O
알고리즘을 수행하는데 필요한 시간/계산 횟수의 상한선(최악의 경우)을 표기하는 기법.  
n 사이즈의 배열에서 특정 값을 찾는 알고리즘을 생각해보면 1) 처음부터 차례대로 확인한다(선형), 
2) 정렬이 된 상태에서 중간값을 확인하여 절반씩 줄여나간다(이진) 등이 있다.
선형 방법은 최악의 경우 n개의 값을 모두 확인해야하고, 이진 방법은 log2(n)번 확인해야 한다.  
이를 Big O 기법으로 표기하면 각각 O(n), O(log n)이다.
   
## 2. $$ \Omega $$
Big O와 반대로 최선의 경우에 걸리는 시간을 표기한다.  
위의 예시를 가져오면 두 알고리즘 모두 Omega(1)이다(한 번에 찾을 수 있기 때문에).

# 선형 탐색 Linear search
처음부터 마지막 자료까지 차례대로 검색하는 방식. 정확도는 높지만 비효율적이다. 따라서 자료가 정렬되어 있지 않은 경우에 유용한 방식이다.
따라서 정렬은 효율적인 탐색을 위해 필수이다.

# 정렬
## 버블 정렬 Bubble sort
인접한 두 자료의 크기/성질을 비교해서 위치를 교환하는 방식. 버블처럼 떠올라 위치를 바꾼다는 뜻에서 이러한 이름이 붙었다.  
n개의 값이 주어졌을 때 i, i+1의 값 비교는 총 n-1회 이루어지고 이 비교는 총 n-1회 이루어지므로 (n-1)*(n-2)회의 작업이 발생한다. 따라서 O(n^2), Omega(n^2)이다(이미 정렬되어 있어도 루프를 반복하기 때문).  
선형 탐색이 O(n)인 점을 감안하면 버블 정렬을 한 후 이진 탐색을 하는 것이 더 효율적이라고 보기 어렵다.

## 선택 정렬 Selection sort
n개의 자료를 거쳐 가장 작거나 큰 값을 찾고 이를 마지막 자리에 옮겨 n-1, n-2, ... 1개의 원소가 남을 때까지 반복하는 방식.  
전체 횟수는 n + (n-1) + (n-2) + ... + 1 = n(n+1)/2 이므로 결국 O(n^2), Omega(n^2)가 된다.


# 기타
## 사용자 정의 자료형(구조체)
<code>typedef struct</code>를 이용해 사용자가 직접 자료형을 정의할 수 있다. 예를 들어 name과 address를 한 번에 저장하는 자료형 <code>per_info</code>를 아래와 같이 정의할 수 있다.
<pre>
<code>
typedef struct
{
    string name;
    string address;
}
per_info;
</code>
</pre>
이제 새로 정의한 <code>per_info</code>를 사용해 딕셔너리와 같이 정보에 접근할 수 있다.
<pre>
<code>
per_info person[4];

person[0].name = "Soo"
person[0].address = "Seoul"
</code>
</pre>

## Loop에서 나가는 방법
Loop 안의 조건문을 기준으로 Loop를 나가는 방법에는 여러 방법이 있다.
<code>break</code>를 사용할 수도 있고, 코드 자체가 종료된다면 아래와 같이 <code>return</code>를 사용하는 방법도 있다.
<pre>
<code>
for (int = 0; int < n; i++)
{
    if (...)
    {
        printf("Yes");
        return 0;           // Main code 종료
    }
}
printf("No");
return 1;
</code>
</pre>
