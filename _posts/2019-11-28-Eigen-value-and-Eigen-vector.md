---
layout: post
categories: posts
title: "Eigen value와 Eigen vector"
tags: [math, linear-algebra]
date-string: Nobember 28, 2019
---

## Intro

 - 선형대수학에서의 eigen value와 eigen vector가 무엇인지 살펴보도록한다.

### eigen value 와 eigen vector
 - 임의의 행렬을 선형변환으로 봤을때, 선형변환에 의한 변환 결과가 자기 자신의 상수배가 되는 0이 아닌 벡터를 eigen vector(고유벡터)라 한다.
 - 여기서 상수값이 바로 eigen value(고윳값)이다.
 - 이는 선형변환이 일어난 후에도 길이는 변할 수 있지만 방향이 변하지 않는 벡터를 의미한다.
 - 그래서 선형 변환은 대개 고유벡터와 고윳값만으로 완전히 설명가능하다.
 - 참고로 고유벡터와 고윳값은 정방행렬에 대해서만 정의된다.

### 그럼 이게 왜 중요할까?
- 이것자체가 중요하다기보단 이를 활용하는 분야에서 기본적으로 사용되기 때문에 중요한 것 같다.
- 예를 들어, PCA(Principal Component Analysis)나 특이값분해(SVD, Singuler Value Decomposition)을 수행할때 사용된다.

### 식으로 표현하면?
 - $A$ : 임의의 n x n 정방행렬
 - $v$ : 길이n을 가지는 0이 아닌 임의의 열벡터
 - $\lambda$ : 상수
 - $Av = \lambda v$ 를 만족하는 열벡터 $v$를 행렬$A$의 $\lambda$에 대한 고유벡터, 상수 $\lambda$를 행렬A의 고윳값이라 정의한다.
 
### 참고
 - https://darkpgmr.tistory.com/106
 - https://en.wikipedia.org/wiki/Eigenvalues_and_eigenvectors
