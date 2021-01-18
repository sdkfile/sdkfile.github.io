---
layout: post
title: '완전탐색 문제풀이 #3 : 카펫(프로그래머스), C++'
subtitle: '프로그래머스 카펫 C++'
categories: algorithm
tags: problem
comments: true
---

## 링크
<https://programmers.co.kr/learn/courses/30/lessons/42842>

## 문제 설명
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

![Image of problem](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/b1ebb809-f333-4df2-bc81-02682900dc2d/carpet.png)

Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

## 제한사항
- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

## 입출력 예

|   brown   |  yellow   |    return     |
|:---------:|:---------:|:-------------:|
|    10     |     1     |    [4, 3]     |
|     8     |     2     |    [3, 3]     |
|    24     |    24     |    [8, 6]     |

## 코드
```cpp
#include <vector>
#include <cmath>
using namespace std;

// yellow의 약수중에서 yellow의 제곱근보다 작거나 같은 쪽에 있는 약수의 목록을 구한다
vector<int> getSmallerDivisor(int n){
    vector<int> ret;
    for (int i = 1; i <= sqrt(n); ++i){
        if (n % i == 0) ret.push_back(i);
    }
    return ret;
}

// 위에서 구한 약수들을 이용해서 다음을 만족하는 x와 y를 찾아서 x + 2와 y + 2를 반환한다.
// x * y = yellow
// x + y = (brown - 4) / 2
vector<int> solution(int brown, int yellow) {
    vector<int> divisor = getSmallerDivisor(yellow);
    vector<int> answer;
    for (int i = 0; i < divisor.size(); ++i){
        int y = divisor[i];
        int x = yellow / y;
        if (x + y == (brown - 4) / 2){
            answer.push_back(x + 2);
            answer.push_back(y + 2);
            break;
        }
    }
    return answer;
}
```
