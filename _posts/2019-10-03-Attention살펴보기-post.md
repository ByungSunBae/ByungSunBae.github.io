---
layout: post
categories: posts
title: "Attention이란?"
tags: [DeepLearning]
date-string: SETEMBER 30, 2019
---

### Intro
 - 최근 BERT 및 XLNet 등 자연어 처리를 딥러닝으로 처리하려는 모습들이 보였다.
 - 직접 구현하지 않더라도 아이디어를 얻는 차원에서 어떻게 구현됐는지 알고싶어서 이것저것 보던중 Transformer라는 걸 알아야한다는 걸 알게 됐다.
 - 그런데 Transformer를 보려고하니 알아야하는 것들이 생각보다 많아서 하나씩 살펴보려고 하는데 그중 하나가 바로 Attention이라는 것이다.
 - 여기서는 딥러닝에서 Attention이란 무엇인지 살펴보려한다.
 
### Attention은 왜 나오게 됐을까?
 - 기존 seq2seq 모델을 만들때 RNN이 주로 사용되었다.
 - 여기서 말하는 seq2seq는 Encoder를 통해 Input Vector를 받아서 Decoder를 통해 Output Vector를 출력하는 모델을 말한다.
 - 하지만 RNN의 경우 한계점이 존재했다.
     + 1) Vanishing gradient 문제
     + 2) Encoding하는 과정에서 고정된 크기의 벡터로 압축시킬때 발생하는 정보 손실문제
 - 특히, 번역 문제에서 길이가 긴 문장을 번역할 경우 성능이 떨어지는 현상으로 이어진다.
 - 그래서 이러한 문제를 해결하고자 Attention 기법이 등장했다.
 
### Attention의 아이디어
 - 기본적인 아이디어는 "다음 시퀀스를 예측할 때 Input의 어느 정보에 집중하여 더 정확하게 예측할 것인지"이다.
 - 즉, 아래와 같은 문장이 2개 있다고 해보자.
     + (1) I saw my friend that took a bus.
     + (2) 나는 버스를 탄 내 친구를 봤었다.
 - 영어 -> 한글 번역문제라고 했을 때 "친구"라는 단어는 영어문장의 어느 부분에 집중을 해야하는 것일까?
     + "bus" 보단 "friend"에 더 집중을 해야하지 않을까?
     
### Seq2seq with Attention
 - Attention은 처음에 나올 당시 단독적으로 쓰이기 보단 Seq2seq 모델에 같이 사용되었다.
 - 그래서 본 문서에서는 Seq2seq에서 어떻게 Attention이 사용됐는지 같이 살펴본다.
 - 우선 Attention은 아래와 같은 구조를 지닌다.

![](https://www.d2l.ai/_images/attention.svg)















