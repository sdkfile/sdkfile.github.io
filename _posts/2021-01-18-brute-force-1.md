---
layout: post
title: '완전탐색 문제풀이 #1'
subtitle: '프로그래머스 모의고사 C++'
categories: algorithm
tags: problem
comments: true
---
## 링크
https://programmers.co.kr/learn/courses/30/lessons/42840

## 문제 설명
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

- 1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
- 2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
- 3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

## 제한 조건
- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

## 입출력 예

| answers   |    return     |
|-----------|:-------------:|
|[1,2,3,4,5]|      [1]      |
|[1,3,2,4,2]|    [1,2,3]    |

## 입출력 예 설명
### 입출력 예 #1

- 수포자 1은 모든 문제를 맞혔습니다.
- 수포자 2는 모든 문제를 틀렸습니다.
- 수포자 3은 모든 문제를 틀렸습니다.
- 따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

### 입출력 예 #2

- 모든 사람이 2문제씩을 맞췄습니다.



```cpp
#include <string>
#include <vector>

using namespace std;
const int Slist1[5] = { 1, 2, 3, 4, 5 };
const int Slist2[8] = { 2, 1, 2, 3, 2, 4, 2, 5 };
const int Slist3[10] = { 3, 3, 1, 1, 2, 2, 4, 4, 5, 5 };

vector<int> solution(vector<int> answers) {    
    // 수포자들의 정답 배열을 초기화
    vector<int> Supos(3, 0);
    
    // 각 수포자들에 대해서 찍은 결괏값이 같으면 Supos 배열의 각 인덱스에 값 1씩 추가
    for (int i = 0; i < answers.size(); ++i){
        if (answers[i] == Slist1[i % 5]){
           ++Supos[0];
        }
        if (answers[i] == Slist2[i % 8]){
           ++Supos[1];
        }
        if (answers[i] == Slist3[i % 10]){
           ++Supos[2];
        }
    }
    // 수포자 1, 2, 3중 가장 높은 점수를 먼저 뽑는다.
    int maxvalue = max(max(Supos[0], Supos[1]), Supos[2]);
    
    // 가장 높은 점수를 얻은 수포자들을 벡터에 넣어서 반환한다.
    vector<int> answer;
    for (int i = 0; i < Supos.size(); ++i){
        if (Supos[i] == maxvalue){
            answer.push_back(i + 1);
        }
    }
    return answer;
}
```
