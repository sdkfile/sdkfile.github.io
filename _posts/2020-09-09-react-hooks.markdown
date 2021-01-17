---
layout: post
title: '알고리즘 책 공부 시작'
subtitle: '개발자는 알고리즘부터'
categories: algorithm
tags: apss
comments: true
---

# 알고리즘 문제해결 전략

구종만님꼐서 쓰신 알고리즘 책이다. 요새 이거로 공부 하는중인데, 약간 주제넘지만 올해부터 구글 코드잼에 출전을 하면서 경험을 해볼 계획이다.

## 알고리즘 공부 하는 방법

일단은 책에 있는 문제를 코드로 (나는 XCode 기능이 좋아서 쓰는중) 적어서 읽어가면서 완전히 어떤식으로 풀이를 설계하는지 알고 나서, 프로그래머스나 백준에 있는 문제를 풀어서 풀이를 올려볼 계획이다. 아래는 코드블럭 테스트 겸

```cpp
int Code6::sum(int n){
    int ret = 0;
    for (int i = 1; i <= n; ++i){
        ret += i;
    }
    return ret;
}
```