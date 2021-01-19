---
layout: post
title: '이분탐색 문제풀이 #1 : 입국심사(프로그래머스), C++'
subtitle: '프로그래머스 입국심사 C++'
categories: algorithm
tags: problem
comments: true
---
## 링크
<https://programmers.co.kr/learn/courses/30/lessons/43238>

해답은 [다음 링크](https://woongsin94.tistory.com/185) 를 참조하였습니다.

## 문제 설명
n명이 입국심사를 위해 줄을 서서 기다리고 있습니다. 각 입국심사대에 있는 심사관마다 심사하는데 걸리는 시간은 다릅니다.

처음에 모든 심사대는 비어있습니다. 한 심사대에서는 동시에 한 명만 심사를 할 수 있습니다. 가장 앞에 서 있는 사람은 비어 있는 심사대로 가서 심사를 받을 수 있습니다. 하지만 더 빨리 끝나는 심사대가 있으면 기다렸다가 그곳으로 가서 심사를 받을 수도 있습니다.

모든 사람이 심사를 받는데 걸리는 시간을 최소로 하고 싶습니다.

입국심사를 기다리는 사람 수 n, 각 심사관이 한 명을 심사하는데 걸리는 시간이 담긴 배열 times가 매개변수로 주어질 때, 모든 사람이 심사를 받는데 걸리는 시간의 최솟값을 return 하도록 solution 함수를 작성해주세요.

## 제한 조건
- 입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.
- 각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.
- 심사관은 1명 이상 100,000명 이하입니다.

## 입출력 예

|     n     |     times     |    return     |
|-----------|:-------------:|:-------------:|
|     6     |    [7, 10]    |      28       |

## 입출력 예 설명
가장 첫 두 사람은 바로 심사를 받으러 갑니다.

7분이 되었을 때, 첫 번째 심사대가 비고 3번째 사람이 심사를 받습니다.

10분이 되었을 때, 두 번째 심사대가 비고 4번째 사람이 심사를 받습니다.

14분이 되었을 때, 첫 번째 심사대가 비고 5번째 사람이 심사를 받습니다.

20분이 되었을 때, 두 번째 심사대가 비지만 6번째 사람이 그곳에서 심사를 받지 않고 1분을 더 기다린 후에 첫 번째 심사대에서 심사를 받으면 28분에 모든 사람의 심사가 끝납니다.



```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

long long solution(int n, vector<int> times) {
    sort(times.begin(), times.end());
    long long min = 1;
    long long max = (long long)(times[times.size()-1]) * n;
    long long answer = max;
    
    // 이분 탐색으로 찾을 때 까지
    while(min<=max){
        // mid 는 총 걸린 시간
        long long mid = (min + max)/2;
        long long sum = 0;
        
        // 심사위원당 맡을 수 있는 사람 수 더하기
        for(int i = 0; i < times.size(); ++i){
            sum += mid /(times[i]);
        }
        
        // 가능
        if(sum >= n){
            // 값 비교
            if(answer > mid)
                answer = mid;
            // 가능 -> 시간 줄여보기(최대 가능 경우)
            max = mid-1;
        }
        // 불가능 -> 시간을 더 많이
        else{
            min = mid+1;
        }
            
    }
    return answer;
}
```
