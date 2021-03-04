---
layout: post
title: 생활코딩 MySQL
subtitle: 
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [TIL, Database]
comments: true
---

# Relational Data Modeling
## Cardinality
entity, attribute 간 관계를 말하며 일대일/일대다/다대다로 나뉜다. 다대다의 경우 직접 DB로 표현할 수 없기 때문에 중간에 연결 테이블(일대다)을 만들어야 한다. Entity Relationship Diagram(ERD)로 표현하면 다음과 같다.


<src img="https://user-images.githubusercontent.com/40853572/109927667-e67b1080-7d07-11eb-8324-8fd13ac2911c.png">

## Optionality
entity, attribute 간 관계가 필수적(mandatory)인지 선택적(optional)인지를 말한다. 예를 들어 모든 사용자가 글을 작성할 필요는 없지만, 모든 글에는 사용자가 있어야 한다. ERD로 표현하면 다음과 같다. 이 때 좌측 | 표기는 해당 속성(ex: 사용자)이 필수임을, 우측 O 표기는 해당 속성(ex: 글)이 선택임을 의미한다.


<src img="https://user-images.githubusercontent.com/40853572/109927926-3a85f500-7d08-11eb-8ccd-3b7e243988d3.png">
  
## Cardinality and Optionality
두 가지를 모두 고려하여 ERD를 그리면 다음과 같다.
<src img="https://user-images.githubusercontent.com/40853572/109928740-1a0a6a80-7d09-11eb-9ae8-093d211a35af.png">
