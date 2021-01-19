---
layout: post
title: '이분탐색 문제풀이 #2 : 징검다리(프로그래머스), C++'
subtitle: '프로그래머스 징검다리 C++'
categories: algorithm
tags: problem
comments: true
---
## 링크
<https://programmers.co.kr/learn/courses/30/lessons/43236>

해답은 [다음 링크](https://codecollector.tistory.com/669) 를 참조하였습니다.

## 문제 설명
출발지점부터 distance만큼 떨어진 곳에 도착지점이 있습니다. 그리고 그사이에는 바위들이 놓여있습니다. 바위 중 몇 개를 제거하려고 합니다.

예를 들어, 도착지점이 25만큼 떨어져 있고, 바위가 [2, 14, 11, 21, 17] 지점에 놓여있을 때 바위 2개를 제거하면 출발지점, 도착지점, 바위 간의 거리가 아래와 같습니다.

| 제거한 바위의 위치 | 각 바위 사이의 거리 | 거리의 최솟값 |
|:-----------------:|:------------------:|:------------:|
|     [21, 17]      |    [2, 9, 3, 11]   |      2       |
|      [2, 21]      |    [11, 3, 3, 8]   |      3       |
|      [2, 11]      |    [14, 3, 4, 4]   |      3       |
|     [11, 21]      |    [2, 12, 3, 8]   |      2       |
|      [2, 14]      |    [11, 6, 4, 4]   |      4       |

위에서 구한 거리의 최솟값 중에 가장 큰 값은 4입니다.

출발지점부터 도착지점까지의 거리 distance, 바위들이 있는 위치를 담은 배열 rocks, 제거할 바위의 수 n이 매개변수로 주어질 때, 바위를 n개 제거한 뒤 각 지점 사이의 거리의 최솟값 중에 가장 큰 값을 return 하도록 solution 함수를 작성해주세요.

## 제한 조건
- 도착지점까지의 거리 distance는 1 이상 1,000,000,000 이하입니다.
- 바위는 1개 이상 50,000개 이하가 있습니다.
- n 은 1 이상 바위의 개수 이하입니다.

## 입출력 예

|     distance     |         rocks         |     n    |    return     |
|:----------------:|:---------------------:|:--------:|:-------------:|
|        25        |  [2, 14, 11, 21, 17]  |     2    |       4       |

## 입출력 예 설명
문제에 나온 예와 같습니다.

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int distance, vector<int> rocks, int n) {
    int answer = 0;
    sort(rocks.begin(), rocks.end());
    //바위를 없앨 거리를 이분탐색으로 돌린다.
    int l = 0;
    int r = distance;
 
    while(l <= r){
        int mid = (l + r) / 2; //바위 사이의 거리들 중 최대값을 찾는다. (최댓값 : 대상 돌들간 거리의 중간값)
        int removeIdx = -1;
        int removeCount = 0;
        for(int i = 0 ; i<=rocks.size(); i++){
            int d;
            if(i == 0){ //돌의 처음
                d = rocks[i];
            }
            else{
                //돌의 끝.
                if(i == rocks.size())
                    d = distance - rocks[rocks.size() - 1];
                //돌의 중간
                else
                    d = rocks[i] - rocks[removeIdx];
            }
            //지울 조건에 충족 : mid보다 바위간 거리가 작을 때 지운다.
            if(d < mid)
                removeCount++;
            else
                removeIdx = i;
        }
        //너무 많이 지웠다. -> 거리를 좀 줄이자
        if(removeCount > n){
            r = mid - 1;
        }
        //너무 돌을 덜 제거했다. -> 거리를 좀 늘리자.
        else if(removeCount <= n){
            l = mid + 1;
            answer = max(answer, mid);
        }
    }
    return answer;
}
```
