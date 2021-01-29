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
   
## 2. \omega
Big O와 반대로 최선의 경우에 걸리는 시간을 표기한다.  
위의 예시를 가져오면 두 알고리즘 모두 \omega(1)이다(한 번에 찾을 수 있기 때문에).

