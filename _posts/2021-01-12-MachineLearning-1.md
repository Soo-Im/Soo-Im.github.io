---
layout: post
title: 머신러닝 야학 1일차 강의
subtitle: 머신러닝 이론
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Boostcourse]
comments: true
---

## 머신러닝 분류
<img src="https://user-images.githubusercontent.com/40853572/104329526-57842000-5530-11eb-9da8-77e18c1f812e.jpeg" width="550">  

출처: 생활코딩
### &nbsp;&nbsp;&nbsp;&nbsp;1) 지도학습 Supervised Learning
기계를 데이터를 이용해 '가르친다'. 데이터를 학습시켜 모델을 만드는 것을 의미한다.
### &nbsp;&nbsp;&nbsp;&nbsp;2) 비지도학습 Unsupervised Learning
지도학습에 포함되지 않는 학습. 기계가 데이터의 성격을 파악하거나 정리하는 등의 작업에 사용한다.
### &nbsp;&nbsp;&nbsp;&nbsp;3) 강화학습 Reinforcement Learning
지도학습과 유사하나 정답을 직접 알려주는 지도학습과 달리, 상벌과 반복을 통해 기계가 더 좋은 결과를 만든다.
  
  
## 지도학습
과거의 데이터(독립변수-종속변수)를 학습하여 미지의 결과를 추측하는 데 주로 사용함
### &nbsp;&nbsp;&nbsp;&nbsp;1) 분류 classification
종속 변수가 범주형 데이터(이름 등)인 경우 (예: 스팸 메일 여부, 합격 여부, 등급...)
### &nbsp;&nbsp;&nbsp;&nbsp;2) 회귀 regression
종속 변수가 양적 데이터인 경우
  
  
## 비지도 학습
독립/종속 변수 구분 없이 데이터 자체의 특성을 파악하고 그룹을 만드는 데 주로 사용함
### &nbsp;&nbsp;&nbsp;&nbsp;1) 군집화 clustering
어떤 대상으로부터 그룹을 만드는 것. 대상을 특정 그룹에 포함시키는 작업은 '분류', 그룹을 만드는 것을 '군집화'라 한다.  
### &nbsp;&nbsp;&nbsp;&nbsp;2) 연관 규칙 학습 association rule learning
장바구니 학습이라고도 부르는 소위 '추천' 시스템. a 제품과 b 제품을 함께 이용하는 고객이 많다-와 같은 작업을 한다.
### &nbsp;&nbsp;&nbsp;&nbsp;3) 변환 transformation
원데이터를 쉽게 이해할 수 있도록 표현하는 것. 차원 축소 dimensionality reduction (PCA 등)이 대표적인 예시이다.
  
  
## 강화 학습
지도 학습이 배움이라면 강화 학습은 경험. 상벌 체계를 통해 더 좋은 답안을 찾는다는 것이 기본 아이디어이다.  
환경(environment)으로부터 현재의 상태(state)와 보상(reward)이 에이전트(agent)에게 전달이 되면, 
에이전트는 보상을 받기 위한 정책(policy)를 세워 행동(action)을 한다.
